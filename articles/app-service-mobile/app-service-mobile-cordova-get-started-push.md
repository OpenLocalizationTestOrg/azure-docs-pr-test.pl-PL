---
title: "Dodawanie powiadomień wypychanych do aplikacji platformy Apache Cordova z usługi Azure Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi Azure Mobile Apps do wysyłania powiadomień wypychanych do aplikacji platformy Apache Cordova."
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
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="81391-103">Dodawanie powiadomień wypychanych do aplikacji platformy Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="81391-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="81391-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="81391-104">Overview</span></span>
<span data-ttu-id="81391-105">W tym samouczku można Dodawanie powiadomień wypychanych do projektu [Apache Cordova szybki start] tak, aby powiadomienia wypychane są wysyłane do urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="81391-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="81391-106">Szybki start pobrany Projekt serwera nie jest używany, należy najpierw pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="81391-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="81391-107">Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="81391-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="81391-108"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="81391-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="81391-109">Ten samouczek obejmuje aplikacji oprogramowania Apache Cordova opracowanych za pomocą programu Visual Studio 2015 uruchamianego na Emulator systemu Google Android, urządzenia z systemem Android, urządzenia z systemem Windows i urządzenia z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="81391-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="81391-110">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="81391-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="81391-111">Komputer z programem [Visual Studio Community 2015] [ 2] lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="81391-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="81391-112">[Visual Studio Tools for Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="81391-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="81391-113">[Aktywne konto platformy Azure][3].</span><span class="sxs-lookup"><span data-stu-id="81391-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="81391-114">Ukończono [szybki start dla oprogramowania Apache Cordova] [ 5] projektu.</span><span class="sxs-lookup"><span data-stu-id="81391-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="81391-115">(Android) A [konto Google] [ 6] z ze zweryfikowanym adresem e-mail.</span><span class="sxs-lookup"><span data-stu-id="81391-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="81391-116">(iOS) [Członkostwo w programie dla deweloperów firmy Apple] [ 7] i urządzenia z systemem iOS (iOS Simulator nie obsługuje push).</span><span class="sxs-lookup"><span data-stu-id="81391-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="81391-117">(System Windows) A [konto dewelopera w Sklepie Windows] [ 8] i urządzeń z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="81391-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="81391-118"><a name="configure-hub"></a>Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="81391-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="81391-119">[Obejrzyj film wideo przedstawiający kroki opisane w tej sekcji][9]</span><span class="sxs-lookup"><span data-stu-id="81391-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="81391-120">Aktualizowanie projektu serwera</span><span class="sxs-lookup"><span data-stu-id="81391-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="81391-121"><a name="add-push-to-app"></a>Modyfikowanie aplikacji platformy Cordova</span><span class="sxs-lookup"><span data-stu-id="81391-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="81391-122">Upewnij się, że Twój projekt aplikacji oprogramowania Apache Cordova jest gotowy do obsługi powiadomień wypychanych, instalując wtyczki Cordova wypychania plus żadnych usług powiadomień wypychanych specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="81391-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="81391-123">Zaktualizuj wersję oprogramowania Cordova w projekcie.</span><span class="sxs-lookup"><span data-stu-id="81391-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="81391-124">Jeśli projekt używa oprogramowania Apache Cordova w wersji starszej niż v6.1.1, zaktualizuj projekt klienta.</span><span class="sxs-lookup"><span data-stu-id="81391-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="81391-125">Aby zaktualizować projektu:</span><span class="sxs-lookup"><span data-stu-id="81391-125">To update the project:</span></span>

* <span data-ttu-id="81391-126">Kliknij prawym przyciskiem myszy `config.xml` otworzyć projektanta konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="81391-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="81391-127">Wybierz kartę platformy.</span><span class="sxs-lookup"><span data-stu-id="81391-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="81391-128">Wybierz 6.1.1 w **interfejsu Cordova CLI** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="81391-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="81391-129">Wybierz **kompilacji**, następnie **Kompiluj rozwiązanie** można zaktualizować projektu.</span><span class="sxs-lookup"><span data-stu-id="81391-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="81391-130">Instalowanie wtyczki wypychania</span><span class="sxs-lookup"><span data-stu-id="81391-130">Install the push plugin</span></span>
<span data-ttu-id="81391-131">Aplikacji oprogramowania Apache Cordova nie obsługują natywnie możliwości urządzenia lub sieci.</span><span class="sxs-lookup"><span data-stu-id="81391-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="81391-132">Te możliwości są udostępniane przez wtyczek, które są publikowane, albo na [npm] [ 10] lub w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="81391-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="81391-133">`phonegap-plugin-push` Wtyczki służy do obsługi powiadomień wypychanych w sieci.</span><span class="sxs-lookup"><span data-stu-id="81391-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="81391-134">Można zainstalować dodatek wypychania w jeden z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="81391-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="81391-135">**W wierszu polecenia:**</span><span class="sxs-lookup"><span data-stu-id="81391-135">**From the command-prompt:**</span></span>

<span data-ttu-id="81391-136">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="81391-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="81391-137">**Z poziomu programu Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="81391-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="81391-138">W Eksploratorze rozwiązań Otwórz `config.xml` kliknij plik **wtyczek** > **niestandardowy**, wybierz pozycję **Git** jako źródła instalacji, wprowadź `https://github.com/phonegap/phonegap-plugin-push` jako źródło.</span><span class="sxs-lookup"><span data-stu-id="81391-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="81391-139">Kliknij strzałkę obok źródła instalacji.</span><span class="sxs-lookup"><span data-stu-id="81391-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="81391-140">W **SENDER_ID**, jeśli masz już identyfikator liczbowych projektu dla projektu konsoli dla deweloperów Google, możesz dodać ją tutaj.</span><span class="sxs-lookup"><span data-stu-id="81391-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="81391-141">W przeciwnym razie wprowadź wartość symbolu zastępczego, takich jak 777777.</span><span class="sxs-lookup"><span data-stu-id="81391-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="81391-142">Jeśli ma być przeznaczona dla systemu Android, należy zaktualizować tę wartość w pliku config.xml później.</span><span class="sxs-lookup"><span data-stu-id="81391-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="81391-143">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="81391-143">Click **Add**.</span></span>

<span data-ttu-id="81391-144">Dodatek wypychania jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="81391-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="81391-145">Instalowanie wtyczki urządzenia</span><span class="sxs-lookup"><span data-stu-id="81391-145">Install the device plugin</span></span>
<span data-ttu-id="81391-146">Postępuj zgodnie z tą samą procedurą, którego użyto Instalowanie wtyczki wypychania.</span><span class="sxs-lookup"><span data-stu-id="81391-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="81391-147">Dodaj wtyczkę urządzenie z listy wtyczek Core (kliknij **wtyczek** > **Core** go znaleźć).</span><span class="sxs-lookup"><span data-stu-id="81391-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="81391-148">Należy to dodatek plug-in, aby uzyskać nazwę platformy.</span><span class="sxs-lookup"><span data-stu-id="81391-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="81391-149">Zarejestruj urządzenie przy uruchamianiu aplikacji</span><span class="sxs-lookup"><span data-stu-id="81391-149">Register your device on application start-up</span></span>
<span data-ttu-id="81391-150">Początkowo przeprowadzamy minimalnego kodu dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="81391-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="81391-151">Później należy zmodyfikować aplikację do uruchamiania w systemie iOS lub Windows 10.</span><span class="sxs-lookup"><span data-stu-id="81391-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="81391-152">Dodaj wywołanie do **registerForPushNotifications** podczas wywołania zwrotnego dla procesu logowania lub u dołu **onDeviceReady** metody:</span><span class="sxs-lookup"><span data-stu-id="81391-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="81391-153">Ten przykład przedstawia wywoływanie **registerForPushNotifications** po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="81391-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="81391-154">Możesz wywołać `registerForPushNotifications()` tyle razy, ile jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="81391-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="81391-155">Dodaj nowe **registerForPushNotifications** metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="81391-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
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
3. <span data-ttu-id="81391-156">(Android) W powyższym kodzie Zamień `Your_Project_ID` liczbowym identyfikator projektu dla aplikacji z [konsoli dla deweloperów Google][18].</span><span class="sxs-lookup"><span data-stu-id="81391-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="81391-157">(Opcjonalnie) Konfigurowanie i uruchamianie aplikacji w systemie Android</span><span class="sxs-lookup"><span data-stu-id="81391-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="81391-158">Wykonaj tę sekcję, aby włączyć powiadomień wypychanych dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="81391-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="81391-159"><a name="enable-gcm"></a>Włącz Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="81391-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="81391-160">Ponieważ firma Microsoft są początkowo korzystających z platformy systemu Google Android, należy włączyć Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="81391-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="81391-161"><a name="configure-backend"></a>Konfigurowanie zaplecza aplikacji mobilnej do wysyłania żądań wypychanych przy użyciu FCM</span><span class="sxs-lookup"><span data-stu-id="81391-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="81391-162">Konfigurowanie aplikacji platformy Cordova dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="81391-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="81391-163">W aplikacji platformy Cordova, otwórz plik config.xml i Zastąp `Your_Project_ID` liczbowym identyfikator projektu dla aplikacji z [konsoli dla deweloperów Google][18].</span><span class="sxs-lookup"><span data-stu-id="81391-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="81391-164">Otwórz index.js i zaktualizuj kod, aby używać swojego identyfikatora liczbowego projektu.</span><span class="sxs-lookup"><span data-stu-id="81391-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="81391-165"><a name="configure-device"></a>Konfigurowanie urządzenia z systemem Android do debugowania USB</span><span class="sxs-lookup"><span data-stu-id="81391-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="81391-166">Zanim będzie można wdrożyć aplikację na urządzeniu z systemem Android, musisz włączyć debugowanie USB.</span><span class="sxs-lookup"><span data-stu-id="81391-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="81391-167">Na telefonie z systemem Android, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="81391-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="81391-168">Przejdź do **ustawienia** > **informacje o telefonie**, naciśnij przycisk **numer kompilacji** dopóki (około siedem razy) jest włączony tryb dewelopera.</span><span class="sxs-lookup"><span data-stu-id="81391-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="81391-169">W **ustawienia** > **opcje dewelopera** włączyć **debugowanie USB**, następnie podłącz telefon z systemem Android na komputerze za pomocą kabla USB.</span><span class="sxs-lookup"><span data-stu-id="81391-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="81391-170">Firma Microsoft przetestowane to przy użyciu węzła Google 5 X urządzeniu z systemem Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="81391-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="81391-171">Jednak te techniki są często używane przez wszystkie nowoczesne wersji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="81391-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="81391-172">Zainstaluj usługi Google Play</span><span class="sxs-lookup"><span data-stu-id="81391-172">Install Google Play Services</span></span>
<span data-ttu-id="81391-173">Dodatek wypychania zależy od systemu Android usług Google Play dla powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="81391-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="81391-174">W programie Visual Studio, kliknij przycisk **narzędzia** > **Android** > **Android SDK Manager**, rozwiń węzeł **dodatki** folder i zaznacz opcję, aby upewnić się, każdy z następujących zestawów SDK jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="81391-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="81391-175">Android 2.3 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="81391-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="81391-176">Poprawki repozytorium Google 27 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="81391-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="81391-177">Usług Google Play 9.0.2 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="81391-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="81391-178">Kliknij przycisk **instalowania pakietów** i poczekaj, aż do ukończenia instalacji.</span><span class="sxs-lookup"><span data-stu-id="81391-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="81391-179">Bieżący wymaganych bibliotek są wyświetlane w [phonegap wtyczka wypychana instalacja dokumentacji][19].</span><span class="sxs-lookup"><span data-stu-id="81391-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="81391-180">Testowych powiadomień wypychanych w aplikacji w systemie Android</span><span class="sxs-lookup"><span data-stu-id="81391-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="81391-181">Możesz teraz testowych powiadomień wypychanych przez aplikację i wstawianie elementów w tabeli TodoItem.</span><span class="sxs-lookup"><span data-stu-id="81391-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="81391-182">Można przetestować z tego samego urządzenia lub drugiego urządzenia, tak długo, jak w przypadku korzystania z tej samej wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="81391-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="81391-183">Testowanie aplikacji Cordova na platformie Android w jednym z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="81391-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="81391-184">**Na urządzeniu fizycznym:** Dołączanie urządzenia z systemem Android do komputera programowanie za pomocą kabla USB.</span><span class="sxs-lookup"><span data-stu-id="81391-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="81391-185">Zamiast **Emulator systemu Google Android**, wybierz pozycję **urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="81391-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="81391-186">Visual Studio wdraża aplikację na urządzeniu, a następnie uruchomi aplikację.</span><span class="sxs-lookup"><span data-stu-id="81391-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="81391-187">Następnie zakłócają aplikacji na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="81391-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="81391-188">Udoskonalić programowanie.</span><span class="sxs-lookup"><span data-stu-id="81391-188">Improve your development experience.</span></span>  <span data-ttu-id="81391-189">Takie jak udostępnianie aplikacji ekranu [Mobizen] [ 20] mogą pomóc w tworzeniu aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="81391-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="81391-190">Mobizen projektów dla systemu Android ekranu w przeglądarce sieci web na komputerze.</span><span class="sxs-lookup"><span data-stu-id="81391-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="81391-191">**Na emulatorze systemu Android:** są dodatkowe czynności konfiguracyjne wymagane podczas uruchamiania emulatora.</span><span class="sxs-lookup"><span data-stu-id="81391-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="81391-192">Upewnij się, że jest wdrażany z urządzenia wirtualnego, który ma ustawioną jako docelową, interfejsy API Google, jak pokazano w programie Android Virtual Device (AVD) manager.</span><span class="sxs-lookup"><span data-stu-id="81391-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="81391-193">Jeśli chcesz użyć szybsze x86 emulatora, możesz [zainstalować sterownik HAXM] [ 11] i skonfigurować emulator, aby go użyć.</span><span class="sxs-lookup"><span data-stu-id="81391-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="81391-194">Dodaj konto Google na urządzeniu z systemem Android, klikając **aplikacje** > **ustawienia** > **Dodaj konto**, postępuj zgodnie z monitami.</span><span class="sxs-lookup"><span data-stu-id="81391-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="81391-195">Uruchamianie aplikacji todolist jako przed i Wstaw nowe zadanie do wykonania.</span><span class="sxs-lookup"><span data-stu-id="81391-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="81391-196">Teraz, w obszarze powiadomień jest wyświetlana ikona powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="81391-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="81391-197">Można także otworzyć menu powiadomień, aby wyświetlić pełny tekst powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="81391-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="81391-198">(Opcjonalnie) Konfigurowanie i uruchamianie w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="81391-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="81391-199">Ta sekcja dotyczy uruchamiania projektu Cordova na urządzeniach z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="81391-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="81391-200">Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="81391-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="81391-201">Zainstaluj i uruchom agenta kompilacji zdalnej systemu iOS w usłudze Mac lub w chmurze</span><span class="sxs-lookup"><span data-stu-id="81391-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="81391-202">Przed uruchomieniem aplikacji Cordova w systemie iOS przy użyciu programu Visual Studio, przejdź do kroków [iOS przewodnik konfiguracji] [ 12] do zainstalowania i uruchomienia agenta kompilacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="81391-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="81391-203">Upewnij się, że można tworzyć aplikacji dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="81391-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="81391-204">Kroki opisane w przewodniku po instalacji są wymagane do utworzenia dla systemu iOS w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81391-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="81391-205">Jeśli nie masz Mac, można tworzyć dla systemu iOS w usłudze, takich jak MacInCloud przy użyciu agenta kompilacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="81391-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="81391-206">Aby uzyskać więcej informacji, zobacz [uruchamianie aplikacji systemu iOS w chmurze][21].</span><span class="sxs-lookup"><span data-stu-id="81391-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="81391-207">XCode 7 lub nowszy jest wymagany do użycia wtyczki wypychania w systemie iOS.</span><span class="sxs-lookup"><span data-stu-id="81391-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="81391-208">Znajdź identyfikator, który ma być używana jako Identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="81391-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="81391-209">Przed rejestrowania aplikacji w taki sposób, aby powiadomienia wypychane, otwórz plik config.xml w aplikacji platformy Cordova `id` wartość w elemencie widget atrybutu i skopiować go do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="81391-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="81391-210">W poniższych XML identyfikator jest `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="81391-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="81391-211">Później za pomocą tego identyfikatora po utworzeniu Identyfikatora aplikacji w portalu dla deweloperów firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="81391-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="81391-212">Jeśli tworzysz inny identyfikator aplikacji w portalu dla deweloperów, należy wykonać kilka dodatkowych czynności w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="81391-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="81391-213">Identyfikator w elemencie widget muszą być zgodne, identyfikator aplikacji w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="81391-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="81391-214">Rejestrowanie aplikacji dla powiadomień wypychanych w portalu dla deweloperów firmy Apple</span><span class="sxs-lookup"><span data-stu-id="81391-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="81391-215">Obejrzyj wideo przedstawiające podobne kroki</span><span class="sxs-lookup"><span data-stu-id="81391-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="81391-216">Konfigurowanie usługi Azure do wysyłania powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="81391-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="81391-217">Sprawdź, czy identyfikator aplikacji zgodna aplikacji platformy Cordova</span><span class="sxs-lookup"><span data-stu-id="81391-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="81391-218">Jeśli już utworzony na Twoim koncie deweloperów firmy Apple identyfikator aplikacji jest zgodny z Identyfikatorem elementu widget w pliku config.xml, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="81391-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="81391-219">Jednak jeśli identyfikatory nie są zgodne, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="81391-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="81391-220">Usuń folder platform z projektu.</span><span class="sxs-lookup"><span data-stu-id="81391-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="81391-221">Usuń folder wtyczki z projektu.</span><span class="sxs-lookup"><span data-stu-id="81391-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="81391-222">Usuń node_modules folder z projektu.</span><span class="sxs-lookup"><span data-stu-id="81391-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="81391-223">Aktualizacja atrybutu id elementu widget w pliku config.xml, aby użyć utworzonego w ramach Twojego konta dewelopera Apple Identyfikatora aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81391-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="81391-224">Ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="81391-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="81391-225">Testowych powiadomień wypychanych w aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="81391-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="81391-226">W programie Visual Studio, upewnij się, że **iOS** został wybrany jako cel wdrożenia, a następnie wybierz pozycję **urządzenia** do uruchomienia na urządzeniu z systemem iOS połączonych.</span><span class="sxs-lookup"><span data-stu-id="81391-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="81391-227">Można uruchomić na urządzeniu z systemem iOS podłączona do komputera za pomocą programu iTunes.</span><span class="sxs-lookup"><span data-stu-id="81391-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="81391-228">Symulatora systemu iOS nie obsługuje powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="81391-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="81391-229">Naciśnij klawisz **Uruchom** przycisk lub **F5** w Visual Studio, aby skompilować projekt i uruchomić aplikację w urządzeniu z systemem iOS, następnie kliknij przycisk **OK** do akceptowania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="81391-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="81391-230">Aplikacja prosi o potwierdzenie dla powiadomień wypychanych przy pierwszym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="81391-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="81391-231">W aplikacji wpisz zadania, a następnie kliknij przycisk plus (+) ikona.</span><span class="sxs-lookup"><span data-stu-id="81391-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="81391-232">Sprawdź, czy powiadomienie o odebraniu, a następnie kliknięcie przycisku OK spowoduje odrzucenie powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="81391-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="81391-233">(Opcjonalnie) Konfigurowanie i uruchamianie w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="81391-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="81391-234">Ta sekcja dotyczy uruchamiania projektu aplikacji oprogramowania Apache Cordova na urządzeniach z systemem Windows 10 (PhoneGap wtyczki wypychania jest obsługiwany w systemie Windows 10).</span><span class="sxs-lookup"><span data-stu-id="81391-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="81391-235">Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="81391-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="81391-236">Rejestrowanie aplikacji systemu Windows dla powiadomień wypychanych z usługą WNS</span><span class="sxs-lookup"><span data-stu-id="81391-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="81391-237">Aby użyć opcji magazynu w programie Visual Studio, wybierz element docelowy z systemem Windows z listy platformy rozwiązania tak samo, jak **Windows x64** lub **Windows x86** (uniknąć **Windows AnyCPU** dla powiadomień wypychanych).</span><span class="sxs-lookup"><span data-stu-id="81391-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="81391-238">[Obejrzyj film wideo przedstawiający podobne kroki][13]</span><span class="sxs-lookup"><span data-stu-id="81391-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="81391-239">Konfigurowanie Centrum powiadomień w przypadku usługi WNS</span><span class="sxs-lookup"><span data-stu-id="81391-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="81391-240">Konfigurowanie aplikacji platformy Cordova do obsługi powiadomień wypychanych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="81391-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="81391-241">Otwórz projektanta konfiguracji (kliknij prawym przyciskiem myszy na plik config.xml i wybierz **Widok projektanta**), wybierz pozycję **Windows** , a następnie wybierz **systemu Windows 10** w obszarze **Windows docelową wersję**.</span><span class="sxs-lookup"><span data-stu-id="81391-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="81391-242">Do obsługi wypychania powiadomień w domyślnej (debugowanie) kompilacjach build.json otwartych plików.</span><span class="sxs-lookup"><span data-stu-id="81391-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="81391-243">Kopiowanie konfiguracji "wersja" konfiguracji debugowania.</span><span class="sxs-lookup"><span data-stu-id="81391-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="81391-244">Po aktualizacji build.json powinien zawierać następujący kod:</span><span class="sxs-lookup"><span data-stu-id="81391-244">After the update, the build.json should contain the following code:</span></span>

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

<span data-ttu-id="81391-245">Tworzenie aplikacji i sprawdź, czy użytkownik nie ma błędów.</span><span class="sxs-lookup"><span data-stu-id="81391-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="81391-246">Twoja aplikacja kliencka teraz należy zarejestrować odbieranie powiadomień z zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="81391-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="81391-247">W tej sekcji należy powtórzyć dla każdego projektu systemu Windows w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="81391-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="81391-248">Testowych powiadomień wypychanych w aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="81391-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="81391-249">W programie Visual Studio, upewnij się, że platformy systemu Windows jest wybrany jako cel wdrożenia, takich jak **Windows x64** lub **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="81391-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="81391-250">Aby uruchomić aplikację na komputerach z systemem Windows 10 hosting Visual Studio, wybierz **komputera lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="81391-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="81391-251">Naciśnij przycisk Uruchom, aby skompilować projekt i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="81391-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="81391-252">W aplikacji wpisz nazwę nowego zadania do wykonania, a następnie kliknij przycisk plus (+) ikonę, aby dodać go.</span><span class="sxs-lookup"><span data-stu-id="81391-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="81391-253">Sprawdź, czy otrzyma powiadomienie po dodaniu elementu.</span><span class="sxs-lookup"><span data-stu-id="81391-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="81391-254"><a name="next-steps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="81391-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="81391-255">Przeczytaj informacje o [usługi Notification Hubs] [ 17] Aby dowiedzieć się więcej na temat powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="81391-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="81391-256">Jeśli jeszcze nie Kontynuuj samouczek przez [Dodawanie uwierzytelniania] [ 14] do swojej aplikacji Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="81391-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="81391-257">Dowiedz się, jak korzystać z zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="81391-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="81391-258">[Zestaw Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="81391-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="81391-259">[Zestaw ASP.NET Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="81391-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="81391-260">[Zestaw node.js Server SDK][16]</span><span class="sxs-lookup"><span data-stu-id="81391-260">[Node.js Server SDK][16]</span></span>

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
