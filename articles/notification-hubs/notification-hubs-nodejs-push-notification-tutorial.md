---
title: "Wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs i Node.js"
description: "Dowiedz się, jak wysyłać powiadomienia wypychane z poziomu aplikacji Node.js przy użyciu usługi Notification Hubs."
keywords: powiadomienia wypychane, wypychanie notifications,node.js wypychania, wypychanych systemu ios
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: dc4987b16b2e930641c6c90eff8b65c1bf8d573c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="70242-104">Wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs i Node.js</span><span class="sxs-lookup"><span data-stu-id="70242-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="70242-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="70242-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="70242-106">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="70242-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="70242-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="70242-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="70242-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="70242-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="70242-109">W tym przewodniku opisano sposób wysyłania powiadomień wypychanych za pomocą usługi Azure Notification Hubs bezpośrednio z poziomu aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="70242-109">This guide will show you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="70242-110">Omówione scenariusze obejmują wysyłanie powiadomień wypychanych do aplikacji na następujących platformach:</span><span class="sxs-lookup"><span data-stu-id="70242-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="70242-111">Android</span><span class="sxs-lookup"><span data-stu-id="70242-111">Android</span></span>
* <span data-ttu-id="70242-112">iOS</span><span class="sxs-lookup"><span data-stu-id="70242-112">iOS</span></span>
* <span data-ttu-id="70242-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="70242-113">Windows Phone</span></span>
* <span data-ttu-id="70242-114">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="70242-114">Universal Windows Platform</span></span> 

<span data-ttu-id="70242-115">Aby uzyskać więcej informacji dotyczących usługi notification hubs, zobacz [następne kroki](#next) sekcji.</span><span class="sxs-lookup"><span data-stu-id="70242-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="70242-116">Co to jest Notification Hubs?</span><span class="sxs-lookup"><span data-stu-id="70242-116">What are Notification Hubs?</span></span>
<span data-ttu-id="70242-117">Centra powiadomień Azure zapewnia łatwy w użyciu, obejmującego wiele platform, skalowalna infrastrukturę do wysyłania powiadomień wypychanych do urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="70242-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="70242-118">Aby uzyskać szczegółowe informacje na infrastrukturę usług, zobacz [usługi Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="70242-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="70242-119">Tworzenie aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="70242-119">Create a Node.js Application</span></span>
<span data-ttu-id="70242-120">Pierwszym krokiem w tym samouczku jest utworzenie nowej aplikacji Node.js puste.</span><span class="sxs-lookup"><span data-stu-id="70242-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="70242-121">Aby uzyskać instrukcje dotyczące tworzenia aplikacji Node.js, zobacz [tworzenie i wdrażanie aplikacji Node.js do witryny sieci Web Azure][nodejswebsite], [Node.js usługi w chmurze] [ Node.js Cloud Service] przy użyciu programu Windows PowerShell lub [witryny sieci Web za pomocą programu WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="70242-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="70242-122">Skonfigurować aplikację tak, aby używać usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="70242-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="70242-123">Aby korzystać z usługi Azure Notification Hubs, konieczne pobranie i użycie Node.js [pakiet azure](https://www.npmjs.com/package/azure), która zawiera zestaw wbudowanych pomocnika bibliotek, które komunikują się z usługami REST powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="70242-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="70242-124">Umożliwia uzyskanie pakietu węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="70242-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="70242-125">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Linux) i przejdź do folderu, w którym została utworzona pusta aplikacja.</span><span class="sxs-lookup"><span data-stu-id="70242-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="70242-126">Typ **azure sb instalacji narzędzia npm** w oknie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="70242-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="70242-127">Możesz ręcznie uruchomić **ls** lub **dir** polecenie, aby sprawdzić, czy **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="70242-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="70242-128">W tym folderze, Znajdź **azure** pakiet, który zawiera biblioteki, musisz mieć dostęp do Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="70242-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="70242-129">Dowiedz się więcej na temat instalowania NPM w oficjalnym [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="70242-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="70242-130">Zaimportuj moduł</span><span class="sxs-lookup"><span data-stu-id="70242-130">Import the module</span></span>
<span data-ttu-id="70242-131">Za pomocą edytora tekstu, Dodaj następujący element do góry **server.js** pliku aplikacji:</span><span class="sxs-lookup"><span data-stu-id="70242-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="70242-132">Nawiązanie połączenia Centrum powiadomień Azure</span><span class="sxs-lookup"><span data-stu-id="70242-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="70242-133">**NotificationHubService** obiektu umożliwia pracę z usługą notification hubs.</span><span class="sxs-lookup"><span data-stu-id="70242-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="70242-134">Poniższy kod tworzy **NotificationHubService** obiektu dla koncentratora nofication o nazwie **hubname**.</span><span class="sxs-lookup"><span data-stu-id="70242-134">The following code creates a **NotificationHubService** object for the nofication hub named **hubname**.</span></span> <span data-ttu-id="70242-135">Dodaj ją w górnej części **server.js** pliku po instrukcji, aby zaimportować moduł azure:</span><span class="sxs-lookup"><span data-stu-id="70242-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="70242-136">Połączenie **connectionstring** wartość można uzyskać z [Azure Portal] , wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="70242-136">The connection **connectionstring** value can be obtained from the [Azure Portal] by performing the following steps:</span></span>

1. <span data-ttu-id="70242-137">W okienku nawigacji po lewej stronie kliknij **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="70242-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="70242-138">Wybierz **usługi Notification Hubs**, a następnie znajdź chcesz użyć przykładowej koncentratora.</span><span class="sxs-lookup"><span data-stu-id="70242-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="70242-139">Można to sprawdzić [samouczka systemu Windows wprowadzenie magazynu](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Jeśli potrzebujesz, aby uzyskać pomoc przy tworzeniu nowego centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="70242-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="70242-140">Wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="70242-140">Select **Settings**.</span></span>
4. <span data-ttu-id="70242-141">Polecenie **zasady dostępu**.</span><span class="sxs-lookup"><span data-stu-id="70242-141">Click on **Access Policies**.</span></span> <span data-ttu-id="70242-142">Zostanie wyświetlone parametry połączenia udostępnionego i pełny dostęp.</span><span class="sxs-lookup"><span data-stu-id="70242-142">You will see both shared and full access connection strings.</span></span>

![Portal Azure — centra powiadomień](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="70242-144">Można również pobrać parametry połączenia za pomocą **Get-AzureSbNamespace** udostępniane przez polecenia cmdlet [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) lub **Pokaż przestrzeni nazw azure sb** z [(Azure CLI) interfejsu wiersza polecenia azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="70242-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="70242-145">Architektura ogólna</span><span class="sxs-lookup"><span data-stu-id="70242-145">General architecture</span></span>
<span data-ttu-id="70242-146">**NotificationHubService** obiekt udostępnia następujące wystąpienia obiektu do wysyłania powiadomień wypychanych do konkretnych urządzeń i aplikacji:</span><span class="sxs-lookup"><span data-stu-id="70242-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="70242-147">**Android** -użyj **GcmService** obiektu, który jest dostępny na **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="70242-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="70242-148">**iOS** -użyj **ApnsService** obiektu, który jest dostępny pod **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="70242-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="70242-149">**Windows Phone** -użyj **MpnsService** obiektu, który jest dostępny na **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="70242-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="70242-150">**Platforma uniwersalna systemu Windows** -użyj **WnsService** obiektu, który jest dostępny na **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="70242-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="70242-151">Porady: wysyłanie powiadomień wypychanych do aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="70242-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="70242-152">**GcmService** zawiera obiekt **wysyłania** metodę, która może służyć do wysyłania powiadomień wypychanych do aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="70242-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="70242-153">**Wysyłania** metoda przyjmuje następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="70242-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="70242-154">**Tagi** — identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="70242-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="70242-155">Jeśli znacznik nie jest podany, powiadomienie zostanie wysłane do wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="70242-155">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="70242-156">**Ładunek** -JSON lub nieprzetworzony ciąg ładunek komunikatu.</span><span class="sxs-lookup"><span data-stu-id="70242-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="70242-157">**Wywołanie zwrotne** — funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="70242-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="70242-158">Aby uzyskać więcej informacji na format ładunku, zobacz **ładunku** sekcji [Implementowanie serwera GCM](http://developer.android.com/google/gcm/server.html#payload) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="70242-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="70242-159">Poniższy kod używa **GcmService** wystąpienia udostępnianych przez **NotificationHubService** do wysyłania powiadomień wypychanych do wszystkich klientów w zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="70242-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="70242-160">Porady: wysyłanie powiadomień wypychanych do aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="70242-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="70242-161">Taki sam jak z aplikacji systemu Android opisano powyżej, **ApnsService** zawiera obiekt **wysyłania** metodę, która może służyć do wysyłania powiadomień wypychanych do aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="70242-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="70242-162">**Wysyłania** metoda przyjmuje następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="70242-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="70242-163">**Tagi** — identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="70242-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="70242-164">Jeśli znacznik nie jest podany, powiadomienie zostanie wysłane do wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="70242-164">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="70242-165">**Ładunek** -ładunek JSON lub ciąg komunikatu.</span><span class="sxs-lookup"><span data-stu-id="70242-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="70242-166">**Wywołanie zwrotne** — funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="70242-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="70242-167">Aby uzyskać więcej informacji na format ładunku, zobacz **ładunek powiadomienia** sekcji [lokalnych i wypychanych Podręcznik programowania powiadomień](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="70242-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="70242-168">Poniższy kod używa **ApnsService** wystąpienia udostępnianych przez **NotificationHubService** do wysyłania alertów wiadomości do wszystkich klientów:</span><span class="sxs-lookup"><span data-stu-id="70242-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="70242-169">Porady: wysyłanie powiadomień wypychanych do aplikacji Windows Phone</span><span class="sxs-lookup"><span data-stu-id="70242-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="70242-170">**MpnsService** zawiera obiekt **wysyłania** metodę, która może służyć do wysyłania powiadomień wypychanych do aplikacji Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="70242-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="70242-171">**Wysyłania** metoda przyjmuje następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="70242-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="70242-172">**Tagi** — identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="70242-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="70242-173">Jeśli znacznik nie jest podany, powiadomienie zostanie wysłane do wszystkich klientów.</span><span class="sxs-lookup"><span data-stu-id="70242-173">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="70242-174">**Ładunek** -ładunek XML wiadomości.</span><span class="sxs-lookup"><span data-stu-id="70242-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="70242-175">**TargetName**  -  `toast` dla wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="70242-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="70242-176">`token`Kafelek powiadomień.</span><span class="sxs-lookup"><span data-stu-id="70242-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="70242-177">**NotificationClass** -priorytet powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="70242-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="70242-178">Zobacz **elementów nagłówka HTTP** sekcji [powiadomienia wypychane z serwera](http://msdn.microsoft.com/library/hh221551.aspx) dokumentu prawidłowe wartości.</span><span class="sxs-lookup"><span data-stu-id="70242-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="70242-179">**Opcje** — opcjonalne nagłówki żądań.</span><span class="sxs-lookup"><span data-stu-id="70242-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="70242-180">**Wywołanie zwrotne** — funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="70242-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="70242-181">Lista prawidłową **TargetName**, **NotificationClass** i opcje nagłówka, zapoznaj się z [powiadomienia wypychane z serwera](http://msdn.microsoft.com/library/hh221551.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="70242-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="70242-182">Poniższy przykładowy kod używa **MpnsService** wystąpienia udostępnianych przez **NotificationHubService** do wysyłania wyskakujących powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="70242-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="70242-183">Porady: wysyłanie powiadomień wypychanych do aplikacji uniwersalnych platformy systemu Windows (UWP)</span><span class="sxs-lookup"><span data-stu-id="70242-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="70242-184">**WnsService** zawiera obiekt **wysyłania** metodę, która może służyć do wysyłania powiadomień wypychanych do aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="70242-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="70242-185">**Wysyłania** metoda przyjmuje następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="70242-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="70242-186">**Tagi** — identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="70242-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="70242-187">Jeśli znacznik nie jest podany, powiadomienie zostanie wysłane do wszystkich klientów w zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="70242-187">If no tag is provided, the notification will be sent to all registered clients.</span></span>
* <span data-ttu-id="70242-188">**Ładunek** -XML ładunek komunikatu.</span><span class="sxs-lookup"><span data-stu-id="70242-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="70242-189">**Typ** — typ powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="70242-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="70242-190">**Opcje** — opcjonalne nagłówki żądań.</span><span class="sxs-lookup"><span data-stu-id="70242-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="70242-191">**Wywołanie zwrotne** — funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="70242-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="70242-192">Aby uzyskać listę prawidłowych typów i nagłówków żądań, zobacz [nagłówki żądań i odpowiedzi usługi powiadomień wypychanych](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="70242-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="70242-193">Poniższy kod używa **WnsService** wystąpienia udostępnianych przez **NotificationHubService** do wysyłania wyskakujących powiadomień wypychanych do aplikacji platformy uniwersalnej systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="70242-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="70242-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="70242-194">Next Steps</span></span>
<span data-ttu-id="70242-195">Przykładowe fragmenty kodu powyżej umożliwiają łatwe tworzenie infrastruktury usługi dostarczać powiadomienia wypychane do szerokiej gamy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="70242-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="70242-196">Teraz, kiedy znasz już podstawy przy użyciu usługi Notification Hubs za pomocą języka node.js, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat sposobu można rozszerzyć te dodatkowe możliwości.</span><span class="sxs-lookup"><span data-stu-id="70242-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="70242-197">Zobacz odwołanie MSDN [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="70242-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="70242-198">Odwiedź stronę [zestawu Azure SDK dla węzła] repozytorium w usłudze GitHub więcej przykładów i szczegóły implementacji.</span><span class="sxs-lookup"><span data-stu-id="70242-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

<span data-ttu-id="70242-199">[zestawu Azure SDK dla węzła]: https://github.com/WindowsAzure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="70242-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span></span>
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
<span data-ttu-id="70242-200">[witryny sieci Web za pomocą programu WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span><span class="sxs-lookup"><span data-stu-id="70242-200">[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span></span>
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
<span data-ttu-id="70242-201">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="70242-201">[Azure Portal]: https://portal.azure.com</span></span>
