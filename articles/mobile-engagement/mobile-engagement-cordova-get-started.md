---
title: aaaGet Started with Azure Mobile Engagement dla oprogramowania Cordova/Phonegap
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji Cordova/Phonegap."
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
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="143a4-103">Rozpoczynanie pracy z usługą Azure Mobile Engagement dla oprogramowania Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="143a4-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="143a4-104">W tym temacie opisano sposób użycia i wysyłania wypychania powiadomień toosegmented użytkownikom aplikacji dla aplikacji mobilnych opracowanych za pomocą oprogramowania Cordova toounderstand usługi Azure Mobile Engagement toouse.</span><span class="sxs-lookup"><span data-stu-id="143a4-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="143a4-105">W tym samouczku utworzymy pustą aplikację Cordova za pomocą komputera Mac, a następnie zintegrujemy zestaw Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="143a4-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="143a4-106">Rozwiązanie będzie zbierać dane analityczne i odbierać powiadomienia wypychane za pomocą systemu Apple Push Notification System (APNS) dla systemów iOS oraz usługi Google Cloud Messaging (GCM) dla systemów Android.</span><span class="sxs-lookup"><span data-stu-id="143a4-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="143a4-107">Wdrożymy ten tooan z systemem iOS lub Android urządzenia do testowania.</span><span class="sxs-lookup"><span data-stu-id="143a4-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="143a4-108">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="143a4-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="143a4-109">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="143a4-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="143a4-110">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="143a4-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="143a4-111">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="143a4-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="143a4-112">Środowisko XCode, które można zainstalować ze sklepu Mac App Store (w przypadku wdrożenia tooiOS)</span><span class="sxs-lookup"><span data-stu-id="143a4-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="143a4-113">[Android SDK oraz Emulator](http://developer.android.com/sdk/installing/index.html) (w przypadku wdrożenia tooAndroid)</span><span class="sxs-lookup"><span data-stu-id="143a4-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="143a4-114">Certyfikat powiadomień wypychanych (.p12), który można uzyskać z Centrum deweloperów firmy Apple dla rozwiązań systemu APNS</span><span class="sxs-lookup"><span data-stu-id="143a4-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="143a4-115">Numer GCM projektu, który można uzyskać z konsoli dla deweloperów Google dla usługi GCM</span><span class="sxs-lookup"><span data-stu-id="143a4-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="143a4-116">Wtyczka Mobile Engagement Cordova</span><span class="sxs-lookup"><span data-stu-id="143a4-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="143a4-117">Można znaleźć kodu źródłowego hello i hello plik ReadMe dla wtyczki Cordova hello na [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="143a4-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="143a4-118"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji Cordova</span><span class="sxs-lookup"><span data-stu-id="143a4-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="143a4-119"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="143a4-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="143a4-120">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="143a4-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="143a4-121">Utworzymy podstawową aplikację z integracją hello toodemonstrate Cordova:</span><span class="sxs-lookup"><span data-stu-id="143a4-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="143a4-122">Tworzenie nowego projektu Cordova</span><span class="sxs-lookup"><span data-stu-id="143a4-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="143a4-123">Uruchom *Terminal* okno na Twojej Mac maszyny i typ powitania po, co spowoduje utworzenie nowego projektu oprogramowania Cordova z hello domyślny szablon.</span><span class="sxs-lookup"><span data-stu-id="143a4-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="143a4-124">Upewnij się, że publikowanie hello profil możesz ostatecznie toodeploy użycia aplikacji systemu iOS używa frazy "com.mycompany.myapp" jako hello identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="143a4-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="143a4-125">Wykonaj następujące tooconfigure hello projektu dla **iOS** i uruchom go w hello symulatora systemu iOS:</span><span class="sxs-lookup"><span data-stu-id="143a4-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="143a4-126">Wykonaj następujące tooconfigure hello projektu dla **Android** i uruchom go w emulatorze systemu Android hello.</span><span class="sxs-lookup"><span data-stu-id="143a4-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="143a4-127">Upewnij się, że ustawienia emulatora Android SDK uwzględniają cel w formie interfejsów API firmy Google (Google Inc.) hello procesor CPU / ABI jako menedżerem ARM interfejsów API firmy Google.</span><span class="sxs-lookup"><span data-stu-id="143a4-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="143a4-128">Dodaj wtyczkę konsoli Cordova hello.</span><span class="sxs-lookup"><span data-stu-id="143a4-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="143a4-129">Połącz zapleczu swojej aplikacji tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="143a4-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="143a4-130">Zainstaluj wtyczkę Azure Mobile Engagement Cordova hello zapewniając hello wartości zmiennych tooconfigure hello wtyczki:</span><span class="sxs-lookup"><span data-stu-id="143a4-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="143a4-131">*Android Reach ikona* : musi być nazwą hello hello zasobu bez rozszerzenia i prefiksu drawable (np: mynotificationicon), a plik ikony hello musi być skopiowany do projektu systemu android (Platform/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="143a4-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="143a4-132">*iOS Reach Icon* : musi być nazwą hello hello zasobu z rozszerzeniem (np: mynotificationicon.png), a plik ikony hello musi zostać dodany do projektu systemu iOS z XCode (przy użyciu hello Menu Dodaj pliki)</span><span class="sxs-lookup"><span data-stu-id="143a4-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="143a4-133"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="143a4-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="143a4-134">W projekcie Cordova hello — Edytuj **www/js/index.js** wywołania hello tooadd tooMobile Engagement toodeclare nowe działanie po hello *deviceReady* odebraniu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="143a4-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="143a4-135">Uruchamianie aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="143a4-135">Run hello application:</span></span>
   
   * <span data-ttu-id="143a4-136">**W przypadku systemu iOS**</span><span class="sxs-lookup"><span data-stu-id="143a4-136">**For iOS**</span></span>
     
       <span data-ttu-id="143a4-137">W `Terminal` okna Uruchom aplikację w nowym wystąpieniu narzędzia Simulator, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="143a4-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="143a4-138">**W przypadku systemu Android**</span><span class="sxs-lookup"><span data-stu-id="143a4-138">**For Android**</span></span>
     
       <span data-ttu-id="143a4-139">W `Terminal` okna Uruchom aplikację w nowym wystąpieniu emulatora, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="143a4-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="143a4-140">Można wyświetlić następujące hello w dziennikach konsoli hello:</span><span class="sxs-lookup"><span data-stu-id="143a4-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="143a4-141"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="143a4-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="143a4-142"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="143a4-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="143a4-143">Usługa Mobile Engagement umożliwia toointeract z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="143a4-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="143a4-144">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="143a4-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="143a4-145">Witaj poniższe sekcje umożliwią skonfigurowanie tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="143a4-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="143a4-146">Konfigurowanie poświadczeń wypychania dla usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="143a4-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="143a4-147">tooallow Mobile Engagement toosend powiadomień wypychanych w Twoim imieniu, należy mieć do niej dostęp tooyour Apple iOS certyfikatu lub klucza interfejsu API serwera GCM toogrant.</span><span class="sxs-lookup"><span data-stu-id="143a4-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="143a4-148">Przejdź tooyour portalu Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="143a4-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="143a4-149">Upewnij się, pracy w aplikacji hello możemy jest używany dla tego projektu, a następnie kliknij polecenie hello **Engage** u dołu hello:</span><span class="sxs-lookup"><span data-stu-id="143a4-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="143a4-150">Na stronie ustawień hello nastąpi przejście do portalu usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="143a4-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="143a4-151">Kliknij hello **natywnych powiadomień wypychanych** sekcji:</span><span class="sxs-lookup"><span data-stu-id="143a4-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="143a4-152">Skonfiguruj certyfikat systemu iOS/klucz interfejsu API serwera GCM Server</span><span class="sxs-lookup"><span data-stu-id="143a4-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="143a4-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="143a4-153">**[iOS]**</span></span>
   
    <span data-ttu-id="143a4-154">a.</span><span class="sxs-lookup"><span data-stu-id="143a4-154">a.</span></span> <span data-ttu-id="143a4-155">Wybierz element .p12, prześlij go i wpisz hasło:</span><span class="sxs-lookup"><span data-stu-id="143a4-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="143a4-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="143a4-156">**[Android]**</span></span>
   
    <span data-ttu-id="143a4-157">a.</span><span class="sxs-lookup"><span data-stu-id="143a4-157">a.</span></span> <span data-ttu-id="143a4-158">Kliknij ikonę edycji hello przed **klucz interfejsu API** w sekcji Ustawienia GCM hello i hello wyświetlonym, Wklej klucz serwera GCM Server hello i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="143a4-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="143a4-159">Włączanie powiadomień wypychanych w aplikacji Cordova hello</span><span class="sxs-lookup"><span data-stu-id="143a4-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="143a4-160">Edytuj **www/js/index.js** tooadd hello wywołania tooMobile zaangażowania toorequest powiadomień wypychanych oraz zadeklarować mechanizm obsługi:</span><span class="sxs-lookup"><span data-stu-id="143a4-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="143a4-161">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="143a4-161">Run hello app</span></span>
<span data-ttu-id="143a4-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="143a4-162">**[iOS]**</span></span>

1. <span data-ttu-id="143a4-163">Firma Microsoft będzie Użyj XCode toobuild i wdrażania aplikacji hello na powiadomienia wypychane tootest urządzenia hello, ponieważ system iOS umożliwia tylko powiadomienia wypychane tooan rzeczywistego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="143a4-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="143a4-164">Przejdź do lokalizacji toohello, w której utworzono projekt Cordova, a następnie przejdź zbyt**...\platforms\ios** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="143a4-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="143a4-165">Otwórz plik natywny .xcodeproj hello w środowisku XCode.</span><span class="sxs-lookup"><span data-stu-id="143a4-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="143a4-166">Tworzenie i wdrażanie hello Cordova aplikacji toohello iOS urządzenia przy użyciu konta hello, które ma hello zawierający certyfikatów hello przekazanym właśnie toohello portalu Mobile Engagement i hello identyfikator aplikacji, który odpowiada hello co podane podczas tworzenia profilu inicjowania obsługi administracyjnej Witaj aplikacji Cordova.</span><span class="sxs-lookup"><span data-stu-id="143a4-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="143a4-167">Można wyewidencjonować hello *identyfikator pakietu* w Twojej **zasobów\*-info.plist** plików w środowisku XCode toomatch on się.</span><span class="sxs-lookup"><span data-stu-id="143a4-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="143a4-168">Zostanie wyświetlone menu podręczne standardowe iOS hello na urządzeniu z informacją, że aplikacja hello żądania uprawnień toosend powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="143a4-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="143a4-169">Udziel uprawnienia hello.</span><span class="sxs-lookup"><span data-stu-id="143a4-169">Grant hello permission.</span></span> 

<span data-ttu-id="143a4-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="143a4-170">**[Android]**</span></span>

<span data-ttu-id="143a4-171">Ponieważ powiadomienia GCM są obsługiwane w emulatorze systemu Android hello możesz użyć aplikacji systemu Android toorun hello hello emulatora.</span><span class="sxs-lookup"><span data-stu-id="143a4-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="143a4-172"><a id="send"></a>Wyślij aplikacji tooyour powiadomień</span><span class="sxs-lookup"><span data-stu-id="143a4-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="143a4-173">Teraz utworzymy prostą kampanię powiadomień wypychanych, która będzie wysyłać aplikacji tooyour wypychania, działającej na urządzeniu hello:</span><span class="sxs-lookup"><span data-stu-id="143a4-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="143a4-174">Przejdź toohello **osiągnąć** kartę w portalu usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="143a4-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="143a4-175">Kliknij przycisk **nowy anons** toocreate kampanii wypychania</span><span class="sxs-lookup"><span data-stu-id="143a4-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="143a4-176">Podaj dane wejściowe toocreate kampanii **[Android]**</span><span class="sxs-lookup"><span data-stu-id="143a4-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="143a4-177">Podaj **nazwę** kampanii.</span><span class="sxs-lookup"><span data-stu-id="143a4-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="143a4-178">Wybierz hello **typ dostawy** jako *powiadomienie systemowe* *proste*</span><span class="sxs-lookup"><span data-stu-id="143a4-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="143a4-179">Wybierz hello **czas dostawy** jako *"Any Time"*</span><span class="sxs-lookup"><span data-stu-id="143a4-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="143a4-180">Podaj **tytuł** powiadomienia, który będzie hello pierwszy wiersz hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="143a4-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="143a4-181">Podaj **komunikat** powiadomienia, który będzie służyć jako treść wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="143a4-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="143a4-182">Podaj dane wejściowe toocreate kampanii **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="143a4-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="143a4-183">Podaj **nazwę** kampanii.</span><span class="sxs-lookup"><span data-stu-id="143a4-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="143a4-184">Wybierz hello **czas dostawy** jako *"tylko poza aplikacją"*</span><span class="sxs-lookup"><span data-stu-id="143a4-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="143a4-185">Podaj **tytuł** powiadomienia, który będzie hello pierwszy wiersz hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="143a4-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="143a4-186">Podaj **komunikat** powiadomienia, który będzie służyć jako treść wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="143a4-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="143a4-187">Przewiń w dół i w hello sekcji zawartości wybierz **tylko powiadomienie**</span><span class="sxs-lookup"><span data-stu-id="143a4-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="143a4-188">[Opcjonalnie] Możesz też podać adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="143a4-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="143a4-189">Upewnij się, że adres wykorzystuje schemat adresów URL podany podczas konfigurowania wtyczki hello **AZME\_PRZEKIEROWANIA\_adres URL** zmiennej np. *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="143a4-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="143a4-190">Ustawienie hello najprostsze kampanii możliwe jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="143a4-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="143a4-191">Teraz przewiń ponownie w dół i kliknij przycisk hello **Utwórz** przycisk toosave kampanii.</span><span class="sxs-lookup"><span data-stu-id="143a4-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="143a4-192">Na koniec **aktywuj** swoją kampanię.</span><span class="sxs-lookup"><span data-stu-id="143a4-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="143a4-193">W ramach kampanii na urządzeniu lub w emulatorze powinno pojawić się powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="143a4-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="143a4-194"><a id="next-steps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="143a4-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="143a4-195">Przegląd wszystkich metod dostępnych przy użyciu zestawu Cordova Mobile Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="143a4-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

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

