---
title: "aaaSend wypychania powiadomień tooChrome aplikacji za pomocą usługi Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosend usługi Azure Notification Hubs toouse push tooa powiadomień aplikacji dla programu Chrome."
services: notification-hubs
keywords: "powiadomienia wypychane na urządzeniach przenośnych, powiadomienia wypychane, powiadomienie wypychane, powiadomienia wypychane w przeglądarce chrome"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="80ee0-104">Wyślij powiadomienia tooChrome aplikacji za pomocą usługi Azure Notification Hubs wypychania</span><span class="sxs-lookup"><span data-stu-id="80ee0-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="80ee0-105">W tym temacie pokazano, jak toosend usługi Azure Notification Hubs toouse push tooa powiadomień aplikacji dla programu Chrome, który będzie wyświetlany w kontekście hello hello przeglądarki Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="80ee0-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="80ee0-106">W tym samouczku utworzymy aplikację dla programu Chrome, która odbiera powiadomienia wypychane za pomocą usługi [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="80ee0-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="80ee0-107">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="80ee0-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="80ee0-108">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="80ee0-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="80ee0-109">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="80ee0-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="80ee0-110">Witaj samouczek przeprowadzi Cię przez te powiadomienia wypychane tooenable podstawowe kroki:</span><span class="sxs-lookup"><span data-stu-id="80ee0-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="80ee0-111">Włączanie usługi Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="80ee0-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="80ee0-112">Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="80ee0-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="80ee0-113">Połącz toohello Centrum powiadomień aplikacji dla programu Chrome</span><span class="sxs-lookup"><span data-stu-id="80ee0-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="80ee0-114">Wyślij tooyour powiadomień wypychanych aplikacji dla programu Chrome</span><span class="sxs-lookup"><span data-stu-id="80ee0-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="80ee0-115">Dodatkowe funkcje i możliwości</span><span class="sxs-lookup"><span data-stu-id="80ee0-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="80ee0-116">Powiadomienia wypychane aplikacji dla programu Chrome nie są ogólne powiadomienia w przeglądarce — są to modelu rozszerzeń przeglądarki określonych toohello (zobacz [Chrome Apps omówienie] szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="80ee0-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="80ee0-117">Ponadto toohello przeglądarkę dla komputerów, aplikacji dla programu Chrome Uruchom na urządzeń przenośnych (Android i iOS) przy użyciu oprogramowania Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="80ee0-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="80ee0-118">Zobacz [Chrome Apps on Mobile] toolearn więcej.</span><span class="sxs-lookup"><span data-stu-id="80ee0-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="80ee0-119">Konfigurowanie usługi GCM i Azure Notification Hubs jest identyczne tooconfiguring dla systemu Android, ponieważ [Google Cloud Messaging dla programu Chrome] jest przestarzała i hello sama usługa GCM obsługuje teraz urządzenia z systemem Android i wystąpienia programu Chrome.</span><span class="sxs-lookup"><span data-stu-id="80ee0-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="80ee0-120"><a id="register"></a>Włączanie usługi Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="80ee0-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="80ee0-121">Przejdź toohello [Google Cloud Console] witryny sieci Web, zaloguj się przy użyciu poświadczeń konta Google, a następnie kliknij przycisk hello **tworzenia projektu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="80ee0-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="80ee0-122">Wprowadź odpowiednią **Nazwa projektu**, a następnie kliknij przycisk hello **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="80ee0-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="80ee0-123">Zanotuj hello **numer projektu** na powitania **projekty** strony dla hello projektu, który został właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="80ee0-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="80ee0-124">Zostanie ona użyta jako hello **identyfikator nadawcy usługi GCM** w hello tooregister aplikacji dla programu Chrome z usługą GCM.</span><span class="sxs-lookup"><span data-stu-id="80ee0-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="80ee0-125">W okienku po lewej stronie powitania kliknij **APIs & auth**, następnie przewiń w dół i kliknij przycisk tooenable Przełącz hello **Google Cloud Messaging dla systemu Android**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="80ee0-126">Nie masz tooenable **Google Cloud Messaging dla programu Chrome**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="80ee0-127">W okienku po lewej stronie powitania kliknij **poświadczenia** > **Utwórz nowy klucz** > **klucz serwera** > **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="80ee0-128">Zwróć uwagę na powitania serwera **klucz interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="80ee0-129">Spowoduje to skonfigurować w dalej powiadomień tooenable w Centrum go tooGCM powiadomień wypychanych toosend.</span><span class="sxs-lookup"><span data-stu-id="80ee0-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="80ee0-130"><a id="configure-hub"></a>Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="80ee0-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="80ee0-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="80ee0-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="80ee0-132">W hello **ustawienia** bloku, wybierz opcję **usługi powiadomień** , a następnie **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="80ee0-133">Wprowadź klucz interfejsu API hello i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="80ee0-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Azure Notification Hubs — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="80ee0-135"><a id="connect-app"></a>Połącz toohello Centrum powiadomień aplikacji dla programu Chrome</span><span class="sxs-lookup"><span data-stu-id="80ee0-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="80ee0-136">Centrum powiadomień jest teraz skonfigurowany toowork z usługą GCM i masz hello połączenie ciągów tooregister Twojego tooboth aplikacji odbierania i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="80ee0-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="80ee0-137">LK</span><span class="sxs-lookup"><span data-stu-id="80ee0-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="80ee0-138">Tworzenie nowej aplikacji dla programu Chrome</span><span class="sxs-lookup"><span data-stu-id="80ee0-138">Create a new Chrome App</span></span>
<span data-ttu-id="80ee0-139">Poniższy przykład Hello jest oparty na powitania [przykładu usługi GCM aplikacji Chrome] i używa hello zalecany sposób toocreate aplikacji dla programu Chrome.</span><span class="sxs-lookup"><span data-stu-id="80ee0-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="80ee0-140">Wyróżnione hello czynności związanych szczególnie tooAzure usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="80ee0-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="80ee0-141">Zaleca się pobrać hello źródła dla aplikacji dla programu Chrome z [przykładu Centrum powiadomień aplikacji dla programu Chrome].</span><span class="sxs-lookup"><span data-stu-id="80ee0-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="80ee0-142">Hello aplikacji dla programu Chrome została utworzona przy użyciu języka JavaScript i można użyć dowolnego edytora tekstu jej utworzenia.</span><span class="sxs-lookup"><span data-stu-id="80ee0-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="80ee0-143">Poniżej przedstawiono wygląd tworzonej aplikacji dla programu Chrome.</span><span class="sxs-lookup"><span data-stu-id="80ee0-143">Below is what this Chrome App will look like.</span></span>

![Aplikacja dla programu Google Chrome][15]

1. <span data-ttu-id="80ee0-145">Utwórz folder i nadaj mu nazwę `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="80ee0-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="80ee0-146">Oczywiście nazwa hello jest dowolnego — Jeśli nazwy inny, upewnij się, że zastępuje ścieżki hello hello wymaganych segmentach kodu.</span><span class="sxs-lookup"><span data-stu-id="80ee0-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="80ee0-147">Pobierz hello [bibliotekę crypto-js] w folderze hello utworzonego w drugim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="80ee0-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="80ee0-148">Ten folder biblioteki będzie zawierać dwa podfoldery: `components` i `rollups`.</span><span class="sxs-lookup"><span data-stu-id="80ee0-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="80ee0-149">Utwórz plik `manifest.json`.</span><span class="sxs-lookup"><span data-stu-id="80ee0-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="80ee0-150">Wszystkie aplikacje Chrome bazują na plik manifestu zawierający metadane aplikacji hello i większość co ważniejsze, wszystkie uprawnienia przyznane toohello aplikacji po jej zainstalowaniu przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="80ee0-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="80ee0-151">Powiadomienie hello `permissions` element, który określa, że aplikacji dla programu Chrome będzie możliwe tooreceive powiadomienia wypychane z usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="80ee0-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="80ee0-152">Należy także określić hello URI centra powiadomień Azure gdzie hello aplikacji dla programu Chrome będzie tooregister wywołania REST.</span><span class="sxs-lookup"><span data-stu-id="80ee0-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="80ee0-153">Nasza Przykładowa aplikacja używa również pliku ikony `gcm_128.png`, znajdziesz w źródle hello, pochodzącym z oryginalnego przykładu usługi GCM hello.</span><span class="sxs-lookup"><span data-stu-id="80ee0-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="80ee0-154">Można zastąpić go dowolnym obrazem spełniającym hello [kryteria ikony](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="80ee0-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="80ee0-155">Utwórz plik o nazwie `background.js` z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="80ee0-155">Create a file called `background.js` with hello following code:</span></span>
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="80ee0-156">To jest plik hello, który powoduje wyświetlenie okna przeglądarki Chrome aplikacji hello HTML (**register.html**), a także definiuje obsługi hello **messageReceived** toohandle hello przychodzących powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="80ee0-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="80ee0-157">Utwórz plik o nazwie `register.html` — definiuje hello UI hello aplikacji dla programu Chrome.</span><span class="sxs-lookup"><span data-stu-id="80ee0-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="80ee0-158">W tym przykładzie użyto biblioteki **CryptoJS w wersji 3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="80ee0-159">Jeśli pobrano inną wersję biblioteki hello, upewnij się, że prawidłowo zastąpiono wersję hello w hello `src` ścieżki.</span><span class="sxs-lookup"><span data-stu-id="80ee0-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="80ee0-160">Utwórz plik o nazwie `register.js` hello kod poniżej.</span><span class="sxs-lookup"><span data-stu-id="80ee0-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="80ee0-161">Ten plik zawiera skrypt hello za `register.html`.</span><span class="sxs-lookup"><span data-stu-id="80ee0-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="80ee0-162">Chrome Apps nie jest dozwolone wykonywanie śródwierszowe, więc masz toocreate oddzielny skrypt pomocniczy dla interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80ee0-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="80ee0-163">Witaj powyżej skryptu ma hello następujących parametrów klucza:</span><span class="sxs-lookup"><span data-stu-id="80ee0-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="80ee0-164">**window.onLoad** definiuje zdarzenia kliknięcia przycisków hello hello dwóch przycisków na powitania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80ee0-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="80ee0-165">Jeden służy z usługą GCM i hello innych używa hello Identyfikatora rejestracji zwróconego po rejestracji w usłudze GCM tooregister przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="80ee0-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="80ee0-166">**updateLog** to funkcja hello, która pozwala nam toohandle prostych funkcji logowania.</span><span class="sxs-lookup"><span data-stu-id="80ee0-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="80ee0-167">**registerWithGCM** jest hello pierwszy obsługi kliknięcia przycisku, dzięki czemu hello `chrome.gcm.register` wywołania tooGCM tooregister hello bieżącego aplikacji dla programu Chrome wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="80ee0-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="80ee0-168">**registerCallback** jest hello funkcja wywołania zwrotnego, która jest wywoływana po zwraca hello wywołanie rejestracji usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="80ee0-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="80ee0-169">**registerWithNH** jest hello drugi obsługi kliknięcia przycisku, który służy do rejestrowania przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="80ee0-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="80ee0-170">Pobiera `hubName` i `connectionString` (hello użytkownika, który został określony) i rzemieślniczych hello wywołania API REST rejestracji centra powiadomień.</span><span class="sxs-lookup"><span data-stu-id="80ee0-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="80ee0-171">**splitConnectionString** i **generateSaSToken** są pomocnikami reprezentującymi implementację JavaScript hello procesu tworzenia tokenu SaS, który musi być używany w wszystkie wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="80ee0-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="80ee0-172">Aby uzyskać więcej informacji, zobacz temat [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx) (Wspólne pojęcia).</span><span class="sxs-lookup"><span data-stu-id="80ee0-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="80ee0-173">**sendNHRegistrationRequest** jest wywołania funkcji hello, która sprawia, że REST protokołu HTTP tooAzure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="80ee0-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="80ee0-174">**registrationPayload** definiuje ładunek XML rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="80ee0-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="80ee0-175">Aby uzyskać więcej informacji, zobacz temat [Create Registration NH REST API] (Interfejs API REST rejestracji w usłudze Notification Hubs).</span><span class="sxs-lookup"><span data-stu-id="80ee0-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="80ee0-176">Możemy zaktualizować hello w nim identyfikator rejestracji otrzymany z usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="80ee0-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="80ee0-177">**Klient** jest wystąpieniem **XMLHttpRequest** używanym hello toomake wysłanie żądania POST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="80ee0-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="80ee0-178">Należy pamiętać, że aktualizujemy hello `Authorization` nagłówek z `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="80ee0-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="80ee0-179">Pomyślne wykonanie tego wywołania spowoduje zarejestrowanie tego wystąpienia aplikacji dla programu Chrome w usłudze Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="80ee0-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="80ee0-180">Witaj ogólna struktura folderów dla tego projektu powinna wyglądać następująco: ![aplikacji w programie Google Chrome — struktura folderów][21]</span><span class="sxs-lookup"><span data-stu-id="80ee0-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="80ee0-181">Instalowanie i testowanie aplikacji dla programu Chrome</span><span class="sxs-lookup"><span data-stu-id="80ee0-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="80ee0-182">Otwórz przeglądarkę Chrome.</span><span class="sxs-lookup"><span data-stu-id="80ee0-182">Open your Chrome browser.</span></span> <span data-ttu-id="80ee0-183">Otwórz **stronę Rozszerzenia programu Chrome** i włącz **Tryb programisty**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="80ee0-184">Kliknij przycisk **Wczytaj rozszerzenie** i przejdź do folderu toohello, w którym utworzono pliki hello.</span><span class="sxs-lookup"><span data-stu-id="80ee0-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="80ee0-185">Możesz również użyć hello **Chrome Apps & Extensions Developer Tool**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="80ee0-186">To narzędzie jest aplikacji dla programu Chrome w sobie (instalowaną ze sklepu Chrome Web Store hello) i zapewnia zaawansowane możliwości debugowania dla programowania aplikacji dla programu Chrome.</span><span class="sxs-lookup"><span data-stu-id="80ee0-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="80ee0-187">Jeśli hello aplikacji dla programu Chrome została utworzona bez żadnych błędów, zostanie wyświetlona w aplikacji dla programu Chrome widoczne.</span><span class="sxs-lookup"><span data-stu-id="80ee0-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="80ee0-188">Wprowadź hello **numer projektu** którą uzyskano wcześniej z hello **Google Cloud Console** jako identyfikator nadawcy hello, a następnie kliknij przycisk **rejestracji w usłudze GCM**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="80ee0-189">Musi zostać wyświetlony wiadomość hello **rejestracji w usłudze GCM zakończyło się pomyślnie.**</span><span class="sxs-lookup"><span data-stu-id="80ee0-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="80ee0-190">Wprowadź użytkownika **nazwę Centrum powiadomień** i hello **DefaultListenSharedAccessSignature** uzyskaną wcześniej hello portalu, a następnie kliknij przycisk **zarejestrować w usłudze Azure Notification Hubs**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="80ee0-191">Musi zostać wyświetlony wiadomość hello **pomyślnej rejestracji Centrum powiadomień!**</span><span class="sxs-lookup"><span data-stu-id="80ee0-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="80ee0-192">i identyfikator hello szczegóły hello rejestracji odpowiedzi, która zawiera hello rejestracji usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="80ee0-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="80ee0-193"><a name="send"></a>Wyślij powiadomienie tooyour aplikacji dla programu Chrome</span><span class="sxs-lookup"><span data-stu-id="80ee0-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="80ee0-194">W celach testowych wyślemy powiadomienia wypychane programu Chrome przy użyciu aplikacji konsolowej programu .NET.</span><span class="sxs-lookup"><span data-stu-id="80ee0-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="80ee0-195">Powiadomienia wypychane można wysyłać przy użyciu usługi Notification Hubs z poziomu dowolnego zaplecza za pośrednictwem naszego publicznego <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interfejsu REST</a>.</span><span class="sxs-lookup"><span data-stu-id="80ee0-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="80ee0-196">Odwiedź nasz [portal dokumentacji](https://azure.microsoft.com/documentation/services/notification-hubs/), aby uzyskać więcej przykładów dla różnych platform.</span><span class="sxs-lookup"><span data-stu-id="80ee0-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="80ee0-197">W programie Visual Studio z hello **pliku** menu, wybierz opcję **nowy** , a następnie **projektu**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="80ee0-198">W obszarze **Visual C#** kliknij pozycję **Windows**, kliknij pozycję **Aplikacja konsolowa**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="80ee0-199">Spowoduje to utworzenie nowego projektu aplikacji konsolowej.</span><span class="sxs-lookup"><span data-stu-id="80ee0-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="80ee0-200">Z hello **narzędzia** menu, kliknij przycisk **Menedżer pakietów biblioteki** , a następnie **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="80ee0-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="80ee0-201">Spowoduje to wyświetlenie konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="80ee0-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="80ee0-202">W oknie konsoli hello wykonaj następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="80ee0-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="80ee0-203">Otwórz `Program.cs` i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="80ee0-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="80ee0-204">W hello `Program` klasy, Dodaj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="80ee0-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="80ee0-205">Upewnij się, że użyto parametrów połączenia hello z **pełne** dostępu nie **nasłuchiwania** dostępu.</span><span class="sxs-lookup"><span data-stu-id="80ee0-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="80ee0-206">Witaj **nasłuchiwania** dostępu ciąg połączenia nie powoduje przyznania uprawnień toosend powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="80ee0-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="80ee0-207">Dodaj następujące hello odwołuje się hello `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="80ee0-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="80ee0-208">Upewnij się, że program Chrome jest uruchomiony, a następnie uruchom aplikację konsolową hello.</span><span class="sxs-lookup"><span data-stu-id="80ee0-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="80ee0-209">Powinny pojawić się następujące hello powiadomienia wyskakującego okienka na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="80ee0-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="80ee0-210">Możesz też sprawdzić wszystkie powiadomienia przy użyciu okna powiadomień programu Chrome hello hello zadań (w systemie Windows) gdy program Chrome jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="80ee0-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="80ee0-211">Nie trzeba toohave hello aplikacji dla programu Chrome uruchomione lub Otwórz w przeglądarce hello (chociaż hello przeglądarka Chrome musi być uruchomiona).</span><span class="sxs-lookup"><span data-stu-id="80ee0-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="80ee0-212">W oknie przeglądarki Chrome powiadomienia hello umożliwia również wyświetlenie skonsolidowanego widoku wszystkich powiadomień.</span><span class="sxs-lookup"><span data-stu-id="80ee0-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="80ee0-213"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="80ee0-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="80ee0-214">Dowiedz się więcej o usłudze Notification Hubs w temacie [Notification Hubs Overview] (Notification Hubs — omówienie).</span><span class="sxs-lookup"><span data-stu-id="80ee0-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="80ee0-215">tootarget określonych użytkowników, zobacz toohello [Azure Notification Hubs Powiadom użytkowników] samouczka.</span><span class="sxs-lookup"><span data-stu-id="80ee0-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="80ee0-216">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz wykonać hello [usługi Azure Notification Hubs fundamentalne wiadomości] samouczka.</span><span class="sxs-lookup"><span data-stu-id="80ee0-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[przykładu Centrum powiadomień aplikacji dla programu Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Overview]: notification-hubs-push-notification-overview.md (Notification Hubs — omówienie)
[Chrome Apps omówienie]: https://developer.chrome.com/apps/about_apps (Omówienie aplikacji dla programu Chrome)
[przykładu usługi GCM aplikacji Chrome]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile (Aplikacja dla programu Chrome na urządzeniach przenośnych)
[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx (Interfejs API REST tworzenia rejestracji w usłudze Notification Hubs)
[bibliotekę crypto-js]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging dla programu Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs Powiadom użytkowników]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md (Powiadamianie użytkowników przy użyciu usługi Azure Notification Hubs)
[usługi Azure Notification Hubs fundamentalne wiadomości]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md (Powiadamianie o najważniejszych wiadomościach przy użyciu usługi Azure Notification Hubs)
