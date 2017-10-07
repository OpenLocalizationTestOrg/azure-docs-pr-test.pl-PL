---
title: "aaaAdd tooApache powiadomień wypychanych aplikacji Cordova za pomocą usługi Azure Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosend Azure Mobile Apps toouse push aplikacji oprogramowania Apache Cordova tooyour powiadomienia."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="9d8ff-103">Dodawanie aplikacji oprogramowania Apache Cordova tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="9d8ff-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="9d8ff-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9d8ff-104">Overview</span></span>
<span data-ttu-id="9d8ff-105">W tym samouczku można dodać projekt toohello [Apache Cordova szybki start] powiadomień wypychanych, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="9d8ff-106">Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="9d8ff-107">Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="9d8ff-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="9d8ff-108"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9d8ff-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="9d8ff-109">Ten samouczek obejmuje aplikacji oprogramowania Apache Cordova opracowanych za pomocą programu Visual Studio 2015 uruchamianego na powitania Emulator systemu Google Android, urządzenia z systemem Android, urządzenia z systemem Windows i urządzenia z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="9d8ff-110">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="9d8ff-111">Komputer z programem [Visual Studio Community 2015] [ 2] lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="9d8ff-112">[Visual Studio Tools for Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="9d8ff-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="9d8ff-113">[Aktywne konto platformy Azure][3].</span><span class="sxs-lookup"><span data-stu-id="9d8ff-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="9d8ff-114">Ukończono [szybki start dla oprogramowania Apache Cordova] [ 5] projektu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="9d8ff-115">(Android) A [konto Google] [ 6] z ze zweryfikowanym adresem e-mail.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="9d8ff-116">(iOS) [Członkostwo w programie dla deweloperów firmy Apple] [ 7] i urządzenia z systemem iOS (iOS Simulator nie obsługuje push).</span><span class="sxs-lookup"><span data-stu-id="9d8ff-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="9d8ff-117">(System Windows) A [konto dewelopera w Sklepie Windows] [ 8] i urządzeń z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="9d8ff-118"><a name="configure-hub"></a>Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="9d8ff-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="9d8ff-119">[Obejrzyj film wideo przedstawiający kroki opisane w tej sekcji][9]</span><span class="sxs-lookup"><span data-stu-id="9d8ff-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="9d8ff-120">Aktualizowanie powitania serwera projektu</span><span class="sxs-lookup"><span data-stu-id="9d8ff-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="9d8ff-121"><a name="add-push-to-app"></a>Modyfikowanie aplikacji platformy Cordova</span><span class="sxs-lookup"><span data-stu-id="9d8ff-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="9d8ff-122">Upewnij się, że Twój projekt aplikacji oprogramowania Apache Cordova jest gotowy toohandle powiadomienia wypychane przez Instalowanie wtyczki wypychania Cordova hello oraz wszelkich usług powiadomień wypychanych specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="9d8ff-123">Zaktualizuj wersję oprogramowania Cordova hello w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="9d8ff-124">Jeśli projekt używa oprogramowania Apache Cordova w wersji starszej niż v6.1.1, zaktualizuj powitania klienta projektu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="9d8ff-125">tooupdate hello projektu:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-125">tooupdate hello project:</span></span>

* <span data-ttu-id="9d8ff-126">Kliknij prawym przyciskiem myszy `config.xml` tooopen hello konfiguracji projektanta.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="9d8ff-127">Wybierz kartę platformy hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="9d8ff-128">Wybierz 6.1.1 hello **interfejsu Cordova CLI** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="9d8ff-129">Wybierz **kompilacji**, następnie **Kompiluj rozwiązanie** tooupdate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="9d8ff-130">Instalowanie wtyczki wypychania hello</span><span class="sxs-lookup"><span data-stu-id="9d8ff-130">Install hello push plugin</span></span>
<span data-ttu-id="9d8ff-131">Aplikacji oprogramowania Apache Cordova nie obsługują natywnie możliwości urządzenia lub sieci.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="9d8ff-132">Te możliwości są udostępniane przez wtyczek, które są publikowane, albo na [npm] [ 10] lub w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="9d8ff-133">Witaj `phonegap-plugin-push` wtyczka jest powiadomień wypychanych toohandle używane sieci.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="9d8ff-134">Można zainstalować dodatek wypychania hello w jeden z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="9d8ff-135">**Z hello wiersza polecenia:**</span><span class="sxs-lookup"><span data-stu-id="9d8ff-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="9d8ff-136">Wykonaj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="9d8ff-137">**Z poziomu programu Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="9d8ff-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="9d8ff-138">W Eksploratorze rozwiązań Otwórz hello `config.xml` kliknij plik **wtyczek** > **niestandardowy**, wybierz pozycję **Git** jako źródła instalacji, a następnie wprowadź `https://github.com/phonegap/phonegap-plugin-push`jako źródło hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="9d8ff-139">Kliknij przycisk hello strzałkę dalej źródła instalacji toohello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="9d8ff-140">W **SENDER_ID**, jeśli masz już identyfikator liczbowych projektu dla projektu konsoli dla deweloperów Google hello, możesz dodać ją tutaj.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="9d8ff-141">W przeciwnym razie wprowadź wartość symbolu zastępczego, takich jak 777777.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="9d8ff-142">Jeśli ma być przeznaczona dla systemu Android, należy zaktualizować tę wartość w pliku config.xml później.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="9d8ff-143">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-143">Click **Add**.</span></span>

<span data-ttu-id="9d8ff-144">Dodatek wypychania Hello jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="9d8ff-145">Instalowanie wtyczki urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="9d8ff-145">Install hello device plugin</span></span>
<span data-ttu-id="9d8ff-146">Wykonaj hello sama procedura stosowana tooinstall hello wypychania wtyczki.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="9d8ff-147">Dodaj wtyczkę urządzenia hello z listy wtyczek Core hello (kliknij **wtyczek** > **Core** toofind go).</span><span class="sxs-lookup"><span data-stu-id="9d8ff-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="9d8ff-148">Należy to nazwa wtyczki tooobtain hello platformy.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="9d8ff-149">Zarejestruj urządzenie przy uruchamianiu aplikacji</span><span class="sxs-lookup"><span data-stu-id="9d8ff-149">Register your device on application start-up</span></span>
<span data-ttu-id="9d8ff-150">Początkowo przeprowadzamy minimalnego kodu dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="9d8ff-151">Później należy zmodyfikować hello toorun aplikacji dla systemu iOS lub Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="9d8ff-152">Dodaj wywołanie za**registerForPushNotifications** podczas wywołania zwrotnego hello, proces logowania hello lub u dołu hello hello **onDeviceReady** metody:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="9d8ff-153">Ten przykład przedstawia wywoływanie **registerForPushNotifications** po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="9d8ff-154">Możesz wywołać `registerForPushNotifications()` tyle razy, ile jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="9d8ff-155">Dodaj nowy hello **registerForPushNotifications** metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="9d8ff-156">(Android) W hello poprzedzających kodu, Zastąp `Your_Project_ID` liczbowym hello identyfikator projektu dla aplikacji z [konsoli dla deweloperów Google][18].</span><span class="sxs-lookup"><span data-stu-id="9d8ff-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="9d8ff-157">(Opcjonalnie) Konfigurowanie i uruchamianie aplikacji hello w systemie Android</span><span class="sxs-lookup"><span data-stu-id="9d8ff-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="9d8ff-158">Ukończenie tego powiadomienia wypychane tooenable sekcji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="9d8ff-159"><a name="enable-gcm"></a>Włącz Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="9d8ff-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="9d8ff-160">Ponieważ firma Microsoft przeznaczonych hello platformy systemu Google Android początkowo, należy włączyć Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="9d8ff-161"><a name="configure-backend"></a>Konfigurowanie przy użyciu FCM hello aplikacji mobilnej zaplecza toosend wypychania żądań</span><span class="sxs-lookup"><span data-stu-id="9d8ff-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="9d8ff-162">Konfigurowanie aplikacji platformy Cordova dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="9d8ff-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="9d8ff-163">W aplikacji platformy Cordova, otwórz plik config.xml i Zastąp `Your_Project_ID` liczbowym hello identyfikator projektu dla aplikacji z hello [konsoli dla deweloperów Google][18].</span><span class="sxs-lookup"><span data-stu-id="9d8ff-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="9d8ff-164">Otwórz index.js i zaktualizuj toouse kodu hello swój identyfikator projektu liczbowych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="9d8ff-165"><a name="configure-device"></a>Konfigurowanie urządzenia z systemem Android do debugowania USB</span><span class="sxs-lookup"><span data-stu-id="9d8ff-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="9d8ff-166">Przed wdrożeniem programu tooyour aplikacji urządzenia z systemem Android należy tooenable debugowanie USB.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="9d8ff-167">Na telefonie z systemem Android, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="9d8ff-168">Przejdź za**ustawienia** > **informacje o telefonie**, naciśnij przycisk hello **numer kompilacji** dopóki (około siedem razy) jest włączony tryb dewelopera.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="9d8ff-169">W **ustawienia** > **opcje dewelopera** włączyć **debugowanie USB**, a następnie połącz programowania tooyour telefonów z systemem Android komputera za pomocą kabla USB.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="9d8ff-170">Firma Microsoft przetestowane to przy użyciu węzła Google 5 X urządzeniu z systemem Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="9d8ff-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="9d8ff-171">Jednak techniki hello są często używane przez wszystkie nowoczesne wersji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="9d8ff-172">Zainstaluj usługi Google Play</span><span class="sxs-lookup"><span data-stu-id="9d8ff-172">Install Google Play Services</span></span>
<span data-ttu-id="9d8ff-173">Dodatek wypychania Hello zależy od systemu Android usług Google Play dla powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="9d8ff-174">W programie Visual Studio, kliknij przycisk **narzędzia** > **Android** > **Android SDK Manager**, rozwiń węzeł hello **dodatki** folder i wyboru hello pole toomake się, że każdy z następujących zestawów SDK hello jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="9d8ff-175">Android 2.3 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="9d8ff-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="9d8ff-176">Poprawki repozytorium Google 27 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="9d8ff-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="9d8ff-177">Usług Google Play 9.0.2 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="9d8ff-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="9d8ff-178">Kliknij przycisk **instalowania pakietów** i poczekaj, aż hello toocomplete instalacji.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="9d8ff-179">Witaj bieżącego wymagane biblioteki są wymienione w hello [phonegap wtyczka wypychana instalacja dokumentacji][19].</span><span class="sxs-lookup"><span data-stu-id="9d8ff-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="9d8ff-180">Testowych powiadomień wypychanych w aplikacji hello w systemie Android</span><span class="sxs-lookup"><span data-stu-id="9d8ff-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="9d8ff-181">Możesz teraz hello testowych powiadomień wypychanych, uruchamiając aplikację i wstawianie elementów w tabeli TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="9d8ff-182">Można przetestować z hello tego samego urządzenia lub z drugiego urządzenia, tak długo, jak używasz hello sam wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="9d8ff-183">Testowanie aplikacji Cordova na platformie Android hello w jednym z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="9d8ff-184">**Na urządzeniu fizycznym:** dołączyć komputer programowanie tooyour urządzenia z systemem Android za pomocą kabla USB.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="9d8ff-185">Zamiast **Emulator systemu Google Android**, wybierz pozycję **urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="9d8ff-186">Visual Studio wdroży urządzenia toohello aplikacji hello, a następnie uruchomi aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="9d8ff-187">Następnie zakłócają aplikacji hello na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="9d8ff-188">Udoskonalić programowanie.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-188">Improve your development experience.</span></span>  <span data-ttu-id="9d8ff-189">Takie jak udostępnianie aplikacji ekranu [Mobizen] [ 20] mogą pomóc w tworzeniu aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="9d8ff-190">Mobizen projekcję przeglądarce sieci web tooa Android ekranu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="9d8ff-191">**Na emulatorze systemu Android:** są dodatkowe czynności konfiguracyjne wymagane podczas uruchamiania emulatora.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="9d8ff-192">Upewnij się, że wdrażasz tooa urządzenia wirtualnego, który ma ustawić jako cel hello interfejsy API Google, jak pokazano w hello Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="9d8ff-193">Jeśli chcesz toouse szybsze x86 emulatora, możesz [zainstalować sterownik HAXM hello] [ 11] i skonfigurować hello emulatora toouse go.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="9d8ff-194">Dodanie urządzenia Android toohello konto Google, klikając **aplikacje** > **ustawienia** > **Dodaj konto**, następnie postępuj zgodnie z monitami hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="9d8ff-195">Uruchamianie aplikacji todolist hello jako przed i Wstaw nowe zadanie do wykonania.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="9d8ff-196">Teraz, w obszarze powiadomień hello jest wyświetlana ikona powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="9d8ff-197">Można także otworzyć hello powiadomień szuflady tooview hello pełny tekst hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="9d8ff-198">(Opcjonalnie) Konfigurowanie i uruchamianie w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="9d8ff-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="9d8ff-199">Ta sekcja dotyczy uruchamiania projektu oprogramowania Cordova hello na urządzeniach z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="9d8ff-200">Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="9d8ff-201">Zainstaluj i uruchom hello zdalnego systemu iOS agenta kompilacji w usłudze Mac lub w chmurze</span><span class="sxs-lookup"><span data-stu-id="9d8ff-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="9d8ff-202">Przed uruchomieniem aplikacji Cordova w systemie iOS przy użyciu programu Visual Studio, wykonanie kroków hello w hello [iOS przewodnik konfiguracji] [ 12] tooinstall i hello wykonywania zdalnego agenta kompilacji.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="9d8ff-203">Upewnij się, że można tworzyć hello aplikacji dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="9d8ff-204">Witaj kroki opisane w przewodniku instalacji hello są wymagane toobuild dla systemu iOS w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="9d8ff-205">Jeśli nie masz Mac, można tworzyć dla systemu iOS w usłudze, takich jak MacInCloud przy użyciu hello zdalnego agenta kompilacji.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="9d8ff-206">Aby uzyskać więcej informacji, zobacz [uruchamianie aplikacji systemu iOS w chmurze hello][21].</span><span class="sxs-lookup"><span data-stu-id="9d8ff-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="9d8ff-207">XCode 7 lub nowszy jest wymagany toouse hello wypychania dodatku w systemie iOS.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="9d8ff-208">Znajdź hello identyfikator toouse jako Identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="9d8ff-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="9d8ff-209">Zanim zarejestrujesz aplikację dla powiadomień wypychanych, otwórz plik config.xml w aplikacji platformy Cordova, Znajdź hello `id` wartość w elemencie widget hello atrybutu i skopiować go do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="9d8ff-210">Identyfikator hello w hello po XML, jest `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="9d8ff-211">Później za pomocą tego identyfikatora po utworzeniu Identyfikatora aplikacji w portalu dla deweloperów firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="9d8ff-212">Jeśli tworzysz inny identyfikator aplikacji w portalu dla deweloperów hello, należy wykonać kilka dodatkowych czynności w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="9d8ff-213">Identyfikator Hello w elemencie widget musi odpowiadać hello identyfikator aplikacji na powitania portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="9d8ff-214">Rejestrowanie aplikacji hello powiadomień wypychanych na portalu dla deweloperów firmy Apple</span><span class="sxs-lookup"><span data-stu-id="9d8ff-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="9d8ff-215">Obejrzyj wideo przedstawiające podobne kroki</span><span class="sxs-lookup"><span data-stu-id="9d8ff-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="9d8ff-216">Konfigurowanie powiadomień wypychanych Azure toosend</span><span class="sxs-lookup"><span data-stu-id="9d8ff-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="9d8ff-217">Sprawdź, czy identyfikator aplikacji zgodna aplikacji platformy Cordova</span><span class="sxs-lookup"><span data-stu-id="9d8ff-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="9d8ff-218">Jeśli już utworzony na Twoim koncie deweloperów firmy Apple identyfikator aplikacji hello odpowiada identyfikator hello elementu widget hello w pliku config.xml, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="9d8ff-219">Witaj identyfikatory nie są zgodne, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="9d8ff-220">Usuń folder platform hello z projektu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="9d8ff-221">Usuń folder wtyczek hello z projektu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="9d8ff-222">Usuń hello node_modules folder z projektu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="9d8ff-223">Aktualizacja atrybutu id hello elementu widget hello w pliku config.xml toouse hello utworzonego w ramach Twojego konta dewelopera Apple Identyfikatora aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="9d8ff-224">Ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="9d8ff-225">Testowych powiadomień wypychanych w aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="9d8ff-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="9d8ff-226">W programie Visual Studio, upewnij się, że **iOS** został wybrany jako cel wdrożenia hello, a następnie wybierz pozycję **urządzenia** toorun na urządzeniu z systemem iOS połączonych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="9d8ff-227">Można uruchamiać na tooyour podłączone urządzenie z systemem iOS komputera za pomocą programu iTunes.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="9d8ff-228">Witaj symulatora systemu iOS nie obsługuje powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="9d8ff-229">Naciśnij klawisz hello **Uruchom** przycisk lub **F5** w Visual Studio toobuild hello projektu i rozpocząć hello aplikacji na urządzeniu z systemem iOS, a następnie kliknij **OK** tooaccept powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9d8ff-230">Aplikacja Hello zażąda potwierdzenia dla powiadomień wypychanych podczas pierwszego uruchomienia hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="9d8ff-231">W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (+) ikona.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="9d8ff-232">Sprawdź, czy powiadomienie odebraniu, a następnie kliknij przycisk OK toodismiss hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="9d8ff-233">(Opcjonalnie) Konfigurowanie i uruchamianie w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="9d8ff-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="9d8ff-234">Ta sekcja dotyczy uruchamiania projektu aplikacji oprogramowania Apache Cordova hello na urządzeniach z systemem Windows 10 (dodatek wypychania PhoneGap hello jest obsługiwana w systemie Windows 10).</span><span class="sxs-lookup"><span data-stu-id="9d8ff-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="9d8ff-235">Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="9d8ff-236">Rejestrowanie aplikacji systemu Windows dla powiadomień wypychanych z usługą WNS</span><span class="sxs-lookup"><span data-stu-id="9d8ff-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="9d8ff-237">Opcje magazynu hello toouse w programie Visual Studio, wybierz element docelowy z systemem Windows z listy platformy rozwiązania hello, tak samo, jak **Windows x64** lub **Windows x86** (uniknąć **Windows AnyCPU** Aby powiadomienia wypychane).</span><span class="sxs-lookup"><span data-stu-id="9d8ff-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="9d8ff-238">[Obejrzyj film wideo przedstawiający podobne kroki][13]</span><span class="sxs-lookup"><span data-stu-id="9d8ff-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="9d8ff-239">Konfigurowanie Centrum powiadomień hello przypadku usługi WNS</span><span class="sxs-lookup"><span data-stu-id="9d8ff-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="9d8ff-240">Konfigurowanie powiadomień wypychanych systemu Windows toosupport aplikacji Cordova</span><span class="sxs-lookup"><span data-stu-id="9d8ff-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="9d8ff-241">Hello Otwórz projektanta konfiguracji (kliknij prawym przyciskiem myszy na plik config.xml i wybierz **Widok projektanta**) wybierz pozycję hello **Windows** , a następnie wybierz **systemu Windows 10** w obszarze **Windows docelowa wersja**.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="9d8ff-242">powiadomienia wypychane toosupport w domyślnej (debugowanie) tworzy build.json otwartych plików.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="9d8ff-243">Skopiuj "wersja" Konfiguracja tooyour debugowania.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="9d8ff-244">Po zaktualizowaniu hello hello build.json powinna zawierać hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="9d8ff-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="9d8ff-245">Tworzenie aplikacji hello i sprawdź, czy użytkownik nie ma błędów.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="9d8ff-246">Twoja aplikacja kliencka powinna teraz rejestrować hello powiadomień z zaplecza aplikacji mobilnej hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="9d8ff-247">W tej sekcji należy powtórzyć dla każdego projektu systemu Windows w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="9d8ff-248">Testowych powiadomień wypychanych w aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="9d8ff-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="9d8ff-249">W programie Visual Studio, upewnij się, że platforma systemu Windows jest wybrany jako cel wdrożenia hello, takich jak **Windows x64** lub **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="9d8ff-250">Aplikacja hello toorun na komputerach z systemem Windows 10 hosting Visual Studio, wybierz **komputera lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="9d8ff-251">Naciśnij klawisz hello uruchomienia projektu hello toobuild przycisk i uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="9d8ff-252">W aplikacji hello, wpisz nazwę nowego zadania do wykonania, a następnie kliknij przycisk hello plus (+) tooadd ikonę go.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="9d8ff-253">Sprawdź, czy otrzyma powiadomienie po dodaniu elementu hello.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="9d8ff-254"><a name="next-steps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d8ff-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="9d8ff-255">Przeczytaj informacje o [usługi Notification Hubs] [ 17] toolearn o powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="9d8ff-256">Jeśli jeszcze nie Kontynuuj samouczek hello przez [Dodawanie uwierzytelniania] [ 14] tooyour aplikacji oprogramowania Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="9d8ff-257">Dowiedz się, jak toouse hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="9d8ff-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="9d8ff-258">[Zestaw Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="9d8ff-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="9d8ff-259">[Zestaw ASP.NET Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="9d8ff-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="9d8ff-260">[Zestaw node.js Server SDK][16]</span><span class="sxs-lookup"><span data-stu-id="9d8ff-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
