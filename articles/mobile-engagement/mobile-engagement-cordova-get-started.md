---
title: "Rozpoczynanie pracy z usługą Azure Mobile Engagement dla oprogramowania Cordova/Phonegap"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami wypychanymi dla aplikacji Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d7a761310782faab1dda023785f93cf90742e2ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="69f75-103">Rozpoczynanie pracy z usługą Azure Mobile Engagement dla oprogramowania Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="69f75-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="69f75-104">W tym temacie przedstawiono sposób użycia usługi Azure Mobile Engagement umożliwiający zbieranie informacji o użyciu aplikacji i wysyłanie powiadomień wypychanych do segmentowanych użytkowników aplikacji mobilnych opracowanych za pomocą oprogramowania Cordova.</span><span class="sxs-lookup"><span data-stu-id="69f75-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="69f75-105">W tym samouczku utworzymy pustą aplikację Cordova za pomocą komputera Mac, a następnie zintegrujemy zestaw Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="69f75-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="69f75-106">Rozwiązanie będzie zbierać dane analityczne i odbierać powiadomienia wypychane za pomocą systemu Apple Push Notification System (APNS) dla systemów iOS oraz usługi Google Cloud Messaging (GCM) dla systemów Android.</span><span class="sxs-lookup"><span data-stu-id="69f75-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="69f75-107">Wdrożymy aplikację na urządzeniu z systemem iOS lub Android w celu przetestowania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="69f75-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="69f75-108">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="69f75-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="69f75-109">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="69f75-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="69f75-110">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="69f75-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="69f75-111">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="69f75-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="69f75-112">Środowisko XCode, które możesz zainstalować ze sklepu Mac App Store (w przypadku wdrożenia w systemie iOS)</span><span class="sxs-lookup"><span data-stu-id="69f75-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="69f75-113">[Zestaw SDK dla systemu Android oraz emulator](http://developer.android.com/sdk/installing/index.html) (w przypadku wdrożenia w systemie Android)</span><span class="sxs-lookup"><span data-stu-id="69f75-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="69f75-114">Certyfikat powiadomień wypychanych (.p12), który można uzyskać z Centrum deweloperów firmy Apple dla rozwiązań systemu APNS</span><span class="sxs-lookup"><span data-stu-id="69f75-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="69f75-115">Numer GCM projektu, który można uzyskać z konsoli dla deweloperów Google dla usługi GCM</span><span class="sxs-lookup"><span data-stu-id="69f75-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="69f75-116">Wtyczka Mobile Engagement Cordova</span><span class="sxs-lookup"><span data-stu-id="69f75-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="69f75-117">Kod źródłowy i plik ReadMe dla wtyczki Cordova można znaleźć w serwisie [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="69f75-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="69f75-118"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji Cordova</span><span class="sxs-lookup"><span data-stu-id="69f75-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="69f75-119"><a id="connecting-app"></a>Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="69f75-119"><a id="connecting-app"></a>Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="69f75-120">Ten samouczek przedstawia „podstawową integrację”, tj. minimalny zestaw wymagany do zbierania danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="69f75-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="69f75-121">Aby zademonstrować integrację, utworzymy podstawową aplikację za pomocą systemu Cordova:</span><span class="sxs-lookup"><span data-stu-id="69f75-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="69f75-122">Tworzenie nowego projektu Cordova</span><span class="sxs-lookup"><span data-stu-id="69f75-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="69f75-123">Uruchom okno *Terminal* na komputerze Mac i wpisz następujące polecenie, które utworzy nowy projekt Cordova przy użyciu szablonu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="69f75-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="69f75-124">Upewnij się, że profil publikowania, którego możesz użyć do wdrożenia aplikacji systemu iOS, używa frazy „com.mycompany.myapp” jako identyfikatora aplikacji.</span><span class="sxs-lookup"><span data-stu-id="69f75-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="69f75-125">Wykonaj następujące czynności, aby skonfigurować projekt dla systemu **iOS** i uruchomić go w narzędziu iOS Simulator:</span><span class="sxs-lookup"><span data-stu-id="69f75-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="69f75-126">Wykonaj następujące czynności, aby skonfigurować projekt dla systemu **Android** i uruchomić go w emulatorze systemu Android.</span><span class="sxs-lookup"><span data-stu-id="69f75-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="69f75-127">Upewnij się, że ustawienia emulatora Android SDK uwzględniają cel w formie interfejsów API firmy Google (Google Inc.) z ustawieniem CPU/ABI jako menedżerem ARM interfejsów API firmy Google.</span><span class="sxs-lookup"><span data-stu-id="69f75-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="69f75-128">Dodaj wtyczkę konsoli Cordova.</span><span class="sxs-lookup"><span data-stu-id="69f75-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="69f75-129">Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="69f75-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="69f75-130">Zainstaluj wtyczkę Azure Mobile Engagement Cordova, podając wartości zmiennych w celu skonfigurowania wtyczki:</span><span class="sxs-lookup"><span data-stu-id="69f75-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="69f75-131">*Android Reach Icon* (Ikona zasięgu systemu Android): musi być nazwą zasobu bez rozszerzenia i prefiksu drawable (np. mynotificationicon), a plik ikony musi być skopiowany do projektu systemu Android (platforms/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="69f75-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="69f75-132">*iOS Reach Icon* (Ikona zasięgu systemu iOS): musi być nazwą zasobu z rozszerzeniem (np. mynotificationicon.png), a plik ikony musi być dodany do projektu systemu iOS za pomocą środowiska XCode (przy użyciu menu Dodaj pliki)</span><span class="sxs-lookup"><span data-stu-id="69f75-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <span data-ttu-id="69f75-133"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="69f75-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="69f75-134">W projekcie Cordova edytuj plik **www/js/index.js**, aby dodać wywołanie usługi Mobile Engagement i zadeklarować nowe działanie po odebraniu zdarzenia *deviceReady*.</span><span class="sxs-lookup"><span data-stu-id="69f75-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="69f75-135">Uruchom aplikację:</span><span class="sxs-lookup"><span data-stu-id="69f75-135">Run the application:</span></span>
   
   * <span data-ttu-id="69f75-136">**W przypadku systemu iOS**</span><span class="sxs-lookup"><span data-stu-id="69f75-136">**For iOS**</span></span>
     
       <span data-ttu-id="69f75-137">W oknie `Terminal` uruchom aplikację w nowym wystąpieniu narzędzia Simulator, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="69f75-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="69f75-138">**W przypadku systemu Android**</span><span class="sxs-lookup"><span data-stu-id="69f75-138">**For Android**</span></span>
     
       <span data-ttu-id="69f75-139">W oknie `Terminal` uruchom aplikację w nowym wystąpieniu emulatora, wykonując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="69f75-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="69f75-140">W dziennikach konsoli możesz zobaczyć następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="69f75-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="69f75-141"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="69f75-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="69f75-142"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="69f75-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="69f75-143">Usługa Mobile Engagement umożliwia wchodzenie w interakcję z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście kampanii.</span><span class="sxs-lookup"><span data-stu-id="69f75-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="69f75-144">Ten moduł w portalu Mobile Engagement ma nazwę REACH.</span><span class="sxs-lookup"><span data-stu-id="69f75-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="69f75-145">Poniższe sekcje umożliwią skonfigurowanie aplikacji do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="69f75-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="69f75-146">Konfigurowanie poświadczeń wypychania dla usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="69f75-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="69f75-147">Aby zezwolić usłudze Mobile Engagement na wysyłanie powiadomień wypychanych w Twoim imieniu, musisz przyznać jej dostęp do certyfikatu Apple iOS lub klucza interfejsu API serwera GCM Server.</span><span class="sxs-lookup"><span data-stu-id="69f75-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="69f75-148">Przejdź do portalu Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="69f75-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="69f75-149">Upewnij się, że jesteś w aplikacji, której używamy dla celów tego projektu, a następnie naciśnij przycisk **Engage** (Włącz) widoczny u dołu:</span><span class="sxs-lookup"><span data-stu-id="69f75-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="69f75-150">System przeniesie Cię do strony ustawień w portalu Engagement.</span><span class="sxs-lookup"><span data-stu-id="69f75-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="69f75-151">Kliknij sekcję **Native Push** (Natywne powiadomienia wypychane):</span><span class="sxs-lookup"><span data-stu-id="69f75-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="69f75-152">Skonfiguruj certyfikat systemu iOS/klucz interfejsu API serwera GCM Server</span><span class="sxs-lookup"><span data-stu-id="69f75-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="69f75-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="69f75-153">**[iOS]**</span></span>
   
    <span data-ttu-id="69f75-154">a.</span><span class="sxs-lookup"><span data-stu-id="69f75-154">a.</span></span> <span data-ttu-id="69f75-155">Wybierz element .p12, prześlij go i wpisz hasło:</span><span class="sxs-lookup"><span data-stu-id="69f75-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="69f75-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="69f75-156">**[Android]**</span></span>
   
    <span data-ttu-id="69f75-157">a.</span><span class="sxs-lookup"><span data-stu-id="69f75-157">a.</span></span> <span data-ttu-id="69f75-158">Kliknij ikonę edycji przed **kluczem interfejsu API** w sekcji Ustawienia GCM, a następnie wklej klucz serwera GCM Server w wyświetlonym oknie i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="69f75-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="69f75-159">Włączanie powiadomień wypychanych w aplikacji Cordova</span><span class="sxs-lookup"><span data-stu-id="69f75-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="69f75-160">Edytuj plik **www/js/index.js**, aby dodać wywołanie do usługi Mobile Engagement i zażądać powiadomień wypychanych oraz zadeklarować mechanizm obsługi:</span><span class="sxs-lookup"><span data-stu-id="69f75-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="69f75-161">Uruchomienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="69f75-161">Run the app</span></span>
<span data-ttu-id="69f75-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="69f75-162">**[iOS]**</span></span>

1. <span data-ttu-id="69f75-163">Użyjemy środowiska XCode do skompilowania i wdrożenia aplikacji na urządzeniu, aby przetestować powiadomienia wypychane, ponieważ system iOS umożliwia tylko wysyłanie powiadomień wypychanych do rzeczywistego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="69f75-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="69f75-164">Przejdź do lokalizacji, w której utworzono projekt Cordova, a następnie przejdź do folderu **...\platforms\ios**.</span><span class="sxs-lookup"><span data-stu-id="69f75-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="69f75-165">Otwórz plik natywny .xcodeproj w środowisku XCode.</span><span class="sxs-lookup"><span data-stu-id="69f75-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="69f75-166">Skompiluj i wdróż aplikację Cordova na urządzeniu z systemem iOS, korzystając z konta, które ma profil aprowizacji zawierający certyfikat przesłany do portalu Mobile Engagement oraz identyfikator aplikacji odpowiadający identyfikatorowi podanemu podczas tworzenia aplikacji Cordova.</span><span class="sxs-lookup"><span data-stu-id="69f75-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="69f75-167">Możesz wyewidencjonować identyfikator *Bundle identifier* w pliku **Resources\*-info.plist** w środowisku XCode, aby zapewnić zgodność identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="69f75-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="69f75-168">Zobaczysz na urządzeniu standardowe wyskakujące okno systemu iOS z informacją o tym, że aplikacja prosi o uprawnienie do wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="69f75-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="69f75-169">Przyznaj uprawnienie.</span><span class="sxs-lookup"><span data-stu-id="69f75-169">Grant the permission.</span></span> 

<span data-ttu-id="69f75-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="69f75-170">**[Android]**</span></span>

<span data-ttu-id="69f75-171">Możesz użyć emulatora do uruchomienia aplikacji systemu Android, ponieważ powiadomienia GCM są obsługiwane w emulatorze systemu Android.</span><span class="sxs-lookup"><span data-stu-id="69f75-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="69f75-172"><a id="send"></a>Wysyłanie powiadomienia do aplikacji</span><span class="sxs-lookup"><span data-stu-id="69f75-172"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="69f75-173">Teraz utworzymy prostą kampanię powiadomień wypychanych, która wyśle powiadomienie wypychane do aplikacji uruchomionej na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="69f75-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="69f75-174">Przejdź do karty **Reach** (Zasięg) w portalu Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="69f75-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="69f75-175">Kliknij przycisk **New Announcement** (Nowy anons), aby utworzyć kampanię powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="69f75-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="69f75-176">Podaj dane wejściowe, aby utworzyć kampanię dla systemu **[Android]**.</span><span class="sxs-lookup"><span data-stu-id="69f75-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="69f75-177">Podaj **nazwę** kampanii.</span><span class="sxs-lookup"><span data-stu-id="69f75-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="69f75-178">Dla ustawienia **Delivery Type** (Typ dostawy) ustaw *System notification* (Powiadomienie systemowe) *Simple* (Proste).</span><span class="sxs-lookup"><span data-stu-id="69f75-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="69f75-179">Wybierz **Delivery time** (Czas dostawy) jako *„Any Time”* (W dowolnym momencie).</span><span class="sxs-lookup"><span data-stu-id="69f75-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="69f75-180">Podaj **tytuł** powiadomienia. Będzie to pierwszy wiersz powiadomienia wypychanego.</span><span class="sxs-lookup"><span data-stu-id="69f75-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="69f75-181">Wpisz **komunikat** powiadomienia, który będzie jego główną treścią.</span><span class="sxs-lookup"><span data-stu-id="69f75-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="69f75-182">Podaj dane wejściowe, aby utworzyć kampanię dla systemu **[iOS]**.</span><span class="sxs-lookup"><span data-stu-id="69f75-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="69f75-183">Podaj **nazwę** kampanii.</span><span class="sxs-lookup"><span data-stu-id="69f75-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="69f75-184">Wybierz **Delivery time** (Czas dostawy) jako *„Out of app only”* (Tylko poza aplikacją).</span><span class="sxs-lookup"><span data-stu-id="69f75-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="69f75-185">Podaj **tytuł** powiadomienia. Będzie to pierwszy wiersz powiadomienia wypychanego.</span><span class="sxs-lookup"><span data-stu-id="69f75-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="69f75-186">Wpisz **komunikat** powiadomienia, który będzie jego główną treścią.</span><span class="sxs-lookup"><span data-stu-id="69f75-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="69f75-187">Przewiń w dół i w sekcji zawartości wybierz opcję **Notification only** (Tylko powiadomienie).</span><span class="sxs-lookup"><span data-stu-id="69f75-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="69f75-188">[Opcjonalnie] Możesz też podać adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="69f75-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="69f75-189">Upewnij się, że adres wykorzystuje schemat adresów URL podany podczas konfigurowania zmiennej **AZME\_REDIRECT\_URL** wtyczki, np. *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="69f75-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="69f75-190">Na tym kończy się konfigurowanie najbardziej podstawowej kampanii.</span><span class="sxs-lookup"><span data-stu-id="69f75-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="69f75-191">Teraz przewiń ponownie w dół i kliknij przycisk **Create** (Utwórz), aby zapisać kampanię.</span><span class="sxs-lookup"><span data-stu-id="69f75-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="69f75-192">Na koniec **aktywuj** swoją kampanię.</span><span class="sxs-lookup"><span data-stu-id="69f75-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="69f75-193">W ramach kampanii na urządzeniu lub w emulatorze powinno pojawić się powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="69f75-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="69f75-194"><a id="next-steps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="69f75-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="69f75-195">Przegląd wszystkich metod dostępnych przy użyciu zestawu Cordova Mobile Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="69f75-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

