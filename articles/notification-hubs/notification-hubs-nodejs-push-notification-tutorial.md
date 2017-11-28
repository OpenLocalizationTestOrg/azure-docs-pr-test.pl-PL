---
title: "aaaSending powiadomień wypychanych przy użyciu usługi Azure Notification Hubs i Node.js"
description: "Dowiedz się, jak toosend usługi Notification Hubs toouse powiadomień wypychanych z poziomu aplikacji Node.js."
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
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="344aa-104">Wysyłanie powiadomień wypychanych przy użyciu usługi Azure Notification Hubs i Node.js</span><span class="sxs-lookup"><span data-stu-id="344aa-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="344aa-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="344aa-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="344aa-106">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="344aa-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="344aa-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="344aa-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="344aa-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="344aa-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="344aa-109">W tym przewodniku opisano sposób toosend powiadomienia wypychane za pomocą hello usługi Azure Notification hubs bezpośrednio z poziomu aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="344aa-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="344aa-110">omówione scenariusze Hello obejmują, wysyłanie tooapplications powiadomień wypychanych na powitania następujące platformy:</span><span class="sxs-lookup"><span data-stu-id="344aa-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="344aa-111">Android</span><span class="sxs-lookup"><span data-stu-id="344aa-111">Android</span></span>
* <span data-ttu-id="344aa-112">iOS</span><span class="sxs-lookup"><span data-stu-id="344aa-112">iOS</span></span>
* <span data-ttu-id="344aa-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="344aa-113">Windows Phone</span></span>
* <span data-ttu-id="344aa-114">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="344aa-114">Universal Windows Platform</span></span> 

<span data-ttu-id="344aa-115">Aby uzyskać więcej informacji dotyczących usługi notification hubs, zobacz hello [następne kroki](#next) sekcji.</span><span class="sxs-lookup"><span data-stu-id="344aa-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="344aa-116">Co to jest Notification Hubs?</span><span class="sxs-lookup"><span data-stu-id="344aa-116">What are Notification Hubs?</span></span>
<span data-ttu-id="344aa-117">Centra powiadomień Azure zapewnia infrastrukturę łatwy w użyciu, obejmującego wiele platform, skalowalna wysyłania urządzeń toomobile powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="344aa-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="344aa-118">Aby uzyskać szczegółowe informacje na powitania infrastrukturę usług, zobacz hello [usługi Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="344aa-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="344aa-119">Tworzenie aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="344aa-119">Create a Node.js Application</span></span>
<span data-ttu-id="344aa-120">pierwszym krokiem Hello w tym samouczku jest tworzenie nowej aplikacji Node.js puste.</span><span class="sxs-lookup"><span data-stu-id="344aa-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="344aa-121">Aby uzyskać instrukcje dotyczące tworzenia aplikacji Node.js, zobacz [tworzenie i wdrażanie tooAzure aplikacji Node.js witryny sieci Web][nodejswebsite], [Node.js usługi w chmurze] [ Node.js Cloud Service] przy użyciu programu Windows PowerShell lub [witryny sieci Web za pomocą programu WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="344aa-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="344aa-122">Konfigurowanie centrów powiadomień tooUse Twoja aplikacja</span><span class="sxs-lookup"><span data-stu-id="344aa-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="344aa-123">toouse usługi Azure Notification Hubs, należy toodownload i użyj hello Node.js [pakiet azure](https://www.npmjs.com/package/azure), który zawiera zestaw wbudowanych pomocnika bibliotek, które komunikują się z usługami REST powiadomień wypychanych hello.</span><span class="sxs-lookup"><span data-stu-id="344aa-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="344aa-124">Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="344aa-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="344aa-125">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Linux) i przejdź do folderu toohello, w którym utworzono pusta aplikacja .</span><span class="sxs-lookup"><span data-stu-id="344aa-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="344aa-126">Typ **azure sb instalacji narzędzia npm** w oknie polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="344aa-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="344aa-127">Możesz ręcznie uruchomić hello **ls** lub **dir** tooverify polecenia który **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="344aa-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="344aa-128">W tym folderze, Znajdź hello **azure** pakiet, który zawiera biblioteki hello należy tooaccess hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="344aa-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="344aa-129">Dowiedz się więcej na temat instalowania NPM na powitania oficjalne [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="344aa-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="344aa-130">Moduł hello importu</span><span class="sxs-lookup"><span data-stu-id="344aa-130">Import hello module</span></span>
<span data-ttu-id="344aa-131">Za pomocą edytora tekstu, Dodaj powitania od góry toohello hello **server.js** pliku aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="344aa-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="344aa-132">Nawiązanie połączenia Centrum powiadomień Azure</span><span class="sxs-lookup"><span data-stu-id="344aa-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="344aa-133">Witaj **NotificationHubService** obiektu umożliwia pracę z usługą notification hubs.</span><span class="sxs-lookup"><span data-stu-id="344aa-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="344aa-134">Witaj poniższy kod tworzy **NotificationHubService** obiektu o nazwie Centrum nofication hello **hubname**.</span><span class="sxs-lookup"><span data-stu-id="344aa-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="344aa-135">Dodać u góry hello hello **server.js** pliku po hello instrukcji tooimport hello azure modułu:</span><span class="sxs-lookup"><span data-stu-id="344aa-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="344aa-136">Witaj połączenia **connectionstring** wartość można uzyskać z hello [Azure Portal] , wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="344aa-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="344aa-137">W okienku nawigacji po lewej stronie powitania kliknij **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="344aa-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="344aa-138">Wybierz **usługi Notification Hubs**i następnie znajdź hello mają toouse hello próbki.</span><span class="sxs-lookup"><span data-stu-id="344aa-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="344aa-139">Może się odwoływać toohello [samouczka systemu Windows wprowadzenie magazynu](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Jeśli potrzebujesz, aby uzyskać pomoc przy tworzeniu nowego centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="344aa-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="344aa-140">Wybierz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="344aa-140">Select **Settings**.</span></span>
4. <span data-ttu-id="344aa-141">Polecenie **zasady dostępu**.</span><span class="sxs-lookup"><span data-stu-id="344aa-141">Click on **Access Policies**.</span></span> <span data-ttu-id="344aa-142">Zostanie wyświetlone parametry połączenia udostępnionego i pełny dostęp.</span><span class="sxs-lookup"><span data-stu-id="344aa-142">You will see both shared and full access connection strings.</span></span>

![Portal Azure — centra powiadomień](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="344aa-144">Można również pobrać hello ciągu połączenia za pomocą hello **Get-AzureSbNamespace** udostępniane przez polecenia cmdlet [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) lub hello **Pokaż przestrzeni nazw azure sb** z Witaj [interfejsu wiersza polecenia platformy Azure (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="344aa-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="344aa-145">Architektura ogólna</span><span class="sxs-lookup"><span data-stu-id="344aa-145">General architecture</span></span>
<span data-ttu-id="344aa-146">Witaj **NotificationHubService** obiekt udostępnia następujące wystąpienia obiektu wysyłania urządzeń toospecific powiadomień wypychanych i aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="344aa-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="344aa-147">**Android** -Użyj hello **GcmService** obiektu, który jest dostępny na **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="344aa-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="344aa-148">**iOS** -Użyj hello **ApnsService** obiektu, który jest dostępny pod **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="344aa-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="344aa-149">**Windows Phone** -Użyj hello **MpnsService** obiektu, który jest dostępny na **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="344aa-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="344aa-150">**Platforma uniwersalna systemu Windows** -Użyj hello **WnsService** obiektu, który jest dostępny na **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="344aa-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="344aa-151">Porady: wysyłanie wypychania powiadomień tooAndroid aplikacji</span><span class="sxs-lookup"><span data-stu-id="344aa-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="344aa-152">Hello **GcmService** zawiera obiekt **wysyłania** metody, które mogą być używane toosend wypychania powiadomień tooAndroid aplikacji.</span><span class="sxs-lookup"><span data-stu-id="344aa-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="344aa-153">Witaj **wysyłania** metoda przyjmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="344aa-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="344aa-154">**Tagi** — Witaj identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="344aa-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="344aa-155">Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane tooall klientów.</span><span class="sxs-lookup"><span data-stu-id="344aa-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="344aa-156">**Ładunek** — Witaj JSON lub nieprzetworzony ciąg ładunek komunikatu.</span><span class="sxs-lookup"><span data-stu-id="344aa-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="344aa-157">**Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="344aa-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="344aa-158">Aby uzyskać więcej informacji na format ładunku hello, zobacz hello **ładunku** sekcji hello [Implementowanie serwera GCM](http://developer.android.com/google/gcm/server.html#payload) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="344aa-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="344aa-159">Witaj poniższy kod używa hello **GcmService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend tooall powiadomień wypychanych zarejestrowany klientów.</span><span class="sxs-lookup"><span data-stu-id="344aa-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="344aa-160">Porady: wysyłanie wypychania powiadomień tooiOS aplikacji</span><span class="sxs-lookup"><span data-stu-id="344aa-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="344aa-161">Takie same jak w przypadku aplikacji systemu Android opisane powyżej, hello **ApnsService** zawiera obiekt **wysyłania** metody, które mogą być używane toosend wypychania powiadomień tooiOS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="344aa-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="344aa-162">Witaj **wysyłania** metoda przyjmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="344aa-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="344aa-163">**Tagi** — Witaj identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="344aa-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="344aa-164">Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane tooall klientów.</span><span class="sxs-lookup"><span data-stu-id="344aa-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="344aa-165">**Ładunek** — Witaj JSON komunikatu lub string ładunku.</span><span class="sxs-lookup"><span data-stu-id="344aa-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="344aa-166">**Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="344aa-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="344aa-167">Format ładunku hello więcej informacji, zobacz hello **ładunek powiadomienia** sekcji hello [lokalnych i wypychanych Podręcznik programowania powiadomień](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="344aa-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="344aa-168">Witaj poniższy kod używa hello **ApnsService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend alert komunikatu tooall klientów:</span><span class="sxs-lookup"><span data-stu-id="344aa-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="344aa-169">Porady: wysyłanie wypychanych aplikacji Phone tooWindows powiadomienia</span><span class="sxs-lookup"><span data-stu-id="344aa-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="344aa-170">Witaj **MpnsService** udostępnia obiekt **wysyłania** metody, które mogą być tooWindows powiadomień wypychanych toosend używanych aplikacji telefonicznej.</span><span class="sxs-lookup"><span data-stu-id="344aa-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="344aa-171">Witaj **wysyłania** metoda przyjmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="344aa-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="344aa-172">**Tagi** — Witaj identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="344aa-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="344aa-173">Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane tooall klientów.</span><span class="sxs-lookup"><span data-stu-id="344aa-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="344aa-174">**Ładunek** — Witaj ładunek XML wiadomości.</span><span class="sxs-lookup"><span data-stu-id="344aa-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="344aa-175">**TargetName**  -  `toast` dla wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="344aa-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="344aa-176">`token`Kafelek powiadomień.</span><span class="sxs-lookup"><span data-stu-id="344aa-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="344aa-177">**NotificationClass** — Witaj priorytet hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="344aa-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="344aa-178">Zobacz hello **elementów nagłówka HTTP** sekcji hello [powiadomienia wypychane z serwera](http://msdn.microsoft.com/library/hh221551.aspx) dokumentu prawidłowe wartości.</span><span class="sxs-lookup"><span data-stu-id="344aa-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="344aa-179">**Opcje** — opcjonalne nagłówki żądań.</span><span class="sxs-lookup"><span data-stu-id="344aa-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="344aa-180">**Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="344aa-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="344aa-181">Lista prawidłową **TargetName**, **NotificationClass** i opcje nagłówka wyewidencjonowania hello [powiadomienia wypychane z serwera](http://msdn.microsoft.com/library/hh221551.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="344aa-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="344aa-182">Witaj następującego przykładowego kodu używa hello **MpnsService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend wyskakujące powiadomienie wypychane:</span><span class="sxs-lookup"><span data-stu-id="344aa-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="344aa-183">Porady: wysyłanie aplikacji platformy systemu Windows (UWP) tooUniversal powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="344aa-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="344aa-184">Witaj **WnsService** zawiera obiekt **wysyłania** metody, które mogą być używane toosend wypychania powiadomień tooUniversal platformy Windows aplikacji.</span><span class="sxs-lookup"><span data-stu-id="344aa-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="344aa-185">Witaj **wysyłania** metoda przyjmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="344aa-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="344aa-186">**Tagi** — Witaj identyfikator tagu.</span><span class="sxs-lookup"><span data-stu-id="344aa-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="344aa-187">Jeśli znacznik nie jest podany, hello powiadomienie zostanie wysłane klientów tooall zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="344aa-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="344aa-188">**Ładunek** -ładunek komunikatu hello XML.</span><span class="sxs-lookup"><span data-stu-id="344aa-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="344aa-189">**Typ** — Witaj typu powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="344aa-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="344aa-190">**Opcje** — opcjonalne nagłówki żądań.</span><span class="sxs-lookup"><span data-stu-id="344aa-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="344aa-191">**Wywołanie zwrotne** — Witaj funkcja wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="344aa-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="344aa-192">Aby uzyskać listę prawidłowych typów i nagłówków żądań, zobacz [nagłówki żądań i odpowiedzi usługi powiadomień wypychanych](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="344aa-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="344aa-193">Witaj poniższy kod używa hello **WnsService** wystąpienia udostępnianych przez hello **NotificationHubService** toosend w aplikacji platformy uniwersalnej systemu Windows tooa powiadomienie wyskakujące wypychania:</span><span class="sxs-lookup"><span data-stu-id="344aa-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="344aa-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="344aa-194">Next Steps</span></span>
<span data-ttu-id="344aa-195">Zezwalaj na Hello przykładowe fragmenty kodu powyżej możesz tooeasily kompilacji usługi infrastruktury toodeliver wypychania powiadomień tooa szerokiej gamy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="344aa-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="344aa-196">Teraz, kiedy znasz już podstawy hello przy użyciu usługi Notification Hubs za pomocą języka node.js, wykonaj te toolearn łącza więcej informacji na temat sposobu można rozszerzyć te dodatkowe możliwości.</span><span class="sxs-lookup"><span data-stu-id="344aa-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="344aa-197">Zobacz odwołanie MSDN hello [usługi Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="344aa-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="344aa-198">Odwiedź hello [zestawu Azure SDK dla węzła] repozytorium w usłudze GitHub więcej przykładów i szczegóły implementacji.</span><span class="sxs-lookup"><span data-stu-id="344aa-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[zestawu Azure SDK dla węzła]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
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
[witryny sieci Web za pomocą programu WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure Portal]: https://portal.azure.com
