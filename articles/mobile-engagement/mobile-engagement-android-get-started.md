---
title: "aaaGet pracy z systemem Android aplikacje usługi Azure Mobile Engagement"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji systemu Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="88a94-103">Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="88a94-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="88a94-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="88a94-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="88a94-105">W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="88a94-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="88a94-106">W tym samouczku zostanie utworzona pusta aplikacja systemu Android służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="88a94-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88a94-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="88a94-107">Prerequisites</span></span>
<span data-ttu-id="88a94-108">Wykonanie kroków tego samouczka wymaga hello [Android Developer Tools](https://developer.android.com/sdk/index.html), w tym hello Android Studio zintegrowane środowisko programistyczne oraz najnowszej platformy Android hello.</span><span class="sxs-lookup"><span data-stu-id="88a94-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="88a94-109">Wymagany jest również hello [zestaw Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="88a94-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88a94-110">toocomplete tego samouczka potrzebne aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="88a94-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="88a94-111">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="88a94-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="88a94-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="88a94-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="88a94-113">Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="88a94-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="88a94-114">Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="88a94-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="88a94-115">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="88a94-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="88a94-116">Utworzeniu Podstawowa aplikacja za pomocą integracji hello toodemonstrate Android Studio.</span><span class="sxs-lookup"><span data-stu-id="88a94-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="88a94-117">Witaj kompletna dokumentacja integracji znajduje się w hello [zestaw Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88a94-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="88a94-118">Tworzenie projektu systemu Android</span><span class="sxs-lookup"><span data-stu-id="88a94-118">Create an Android project</span></span>
1. <span data-ttu-id="88a94-119">Uruchom **Android Studio**i wybierz w oknie podręcznym hello **Utwórz nowy projekt Android Studio**.</span><span class="sxs-lookup"><span data-stu-id="88a94-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="88a94-120">Podaj nazwę aplikacji i domenę firmy.</span><span class="sxs-lookup"><span data-stu-id="88a94-120">Provide an app name and company domain.</span></span> <span data-ttu-id="88a94-121">Zanotuj te informacje, ponieważ będą one potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="88a94-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="88a94-122">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="88a94-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="88a94-123">Wybierz hello docelowy typ urządzeń i poziom interfejsu API, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="88a94-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="88a94-124">Usługa Mobile Engagement wymaga co najmniej interfejsu API na poziomie 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="88a94-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="88a94-125">Wybierz **puste działanie** miejsca, czyli hello jedynym ekranem dla tej aplikacji i kliknij pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="88a94-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="88a94-126">Na koniec, pozostaw domyślne hello jest, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="88a94-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="88a94-127">Android Studio zostanie utworzona aplikacja demonstracyjna hello, w której zostanie zintegrowana usługa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="88a94-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="88a94-128">Uwzględnione hello Biblioteka zestawu SDK w projekcie</span><span class="sxs-lookup"><span data-stu-id="88a94-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="88a94-129">Pobierz hello [zestaw Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="88a94-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="88a94-130">Wyodrębnij hello archiwum pliku tooa folderu na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="88a94-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="88a94-131">Identyfikowanie hello bibliotekę JAR dla bieżącej wersji hello tego zestawu SDK i skopiuj go toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="88a94-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="88a94-132">Przejdź toohello **projektu** sekcji (1) i Wklej hello JAR w folderze libs hello (2).</span><span class="sxs-lookup"><span data-stu-id="88a94-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="88a94-133">tooload hello biblioteki projektu hello synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="88a94-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="88a94-134">Uzyskuj zapleczu swojej aplikacji tooMobile zaangażowania hello parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="88a94-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="88a94-135">Skopiuj następujące wiersze kodu do tworzenia działania hello (należy to zrobić tylko w jednym miejscu aplikacji, zwykle hello głównym działaniu) hello.</span><span class="sxs-lookup"><span data-stu-id="88a94-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="88a94-136">Dla tej aplikacji przykładowej Otwórz zapasowej hello MainActivity w folderze src -> main -> java i dodaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="88a94-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="88a94-137">Rozpoznać odwołań hello, naciskając klawisze Alt + Enter lub dodając następujące instrukcje importu hello:</span><span class="sxs-lookup"><span data-stu-id="88a94-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="88a94-138">Przejdź wstecz toohello klasycznego portalu Azure w Twojej aplikacji **informacje o połączeniu** hello strony i skopiuj **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="88a94-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="88a94-139">Wklej go do hello `setConnectionString` parametru, zastępując cały ciąg hello pokazano hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="88a94-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="88a94-140">Dodawanie uprawnień i deklaracji usługi</span><span class="sxs-lookup"><span data-stu-id="88a94-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="88a94-141">Dodaj te uprawnienia toohello Manifest.xml projektu bezpośrednio przed lub po hello `<application>` tagu:</span><span class="sxs-lookup"><span data-stu-id="88a94-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="88a94-142">toodeclare hello Usługa agenta, Dodaj ten kod między hello `<application>` i `</application>` tagów:</span><span class="sxs-lookup"><span data-stu-id="88a94-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="88a94-143">W kodzie hello wklejonych, Zastąp `"<Your application name>"` hello etykiety, który jest wyświetlany w hello **ustawienia** menu, w którym można zobaczyć usługi uruchomione na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="88a94-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="88a94-144">Na przykład możesz dodać hello wyraz "Usługa" w tej etykiecie.</span><span class="sxs-lookup"><span data-stu-id="88a94-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="88a94-145">Wysyłanie ekranu tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="88a94-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="88a94-146">toostart wysyłanie danych i upewnij się, że hello użytkownicy są aktywni, konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).</span><span class="sxs-lookup"><span data-stu-id="88a94-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="88a94-147">Przejdź za**MainActivity.java** i Dodaj powitania po tooreplace hello klasa podstawowa **MainActivity** za**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="88a94-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="88a94-148">Jeśli nie jest klasą podstawową *działania*, zapoznaj się [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) jak tooinherit z różnych klas.</span><span class="sxs-lookup"><span data-stu-id="88a94-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="88a94-149">Komentarz powitania po wierszu dla tym prostym scenariuszu przykładowym:</span><span class="sxs-lookup"><span data-stu-id="88a94-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="88a94-150">Jeśli chcesz, aby tookeep hello `ActionBar` w aplikacji, zobacz [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="88a94-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="88a94-151">Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="88a94-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="88a94-152">Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="88a94-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="88a94-153">W czasie kampanii usługa Mobile Engagement umożliwia interakcję z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88a94-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="88a94-154">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="88a94-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="88a94-155">powitania po sekcji konfiguruje tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="88a94-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="88a94-156">Kopiowanie zasobów zestawu SDK w projekcie</span><span class="sxs-lookup"><span data-stu-id="88a94-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="88a94-157">Przejdź wstecz tooyour SDK pobierania zawartości i skopiuj hello **res** folderu.</span><span class="sxs-lookup"><span data-stu-id="88a94-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="88a94-158">Przejdź wstecz tooAndroid Studio, wybierz hello **głównego** katalogu plików projektu, a następnie wklej go tooadd hello zasobów tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="88a94-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="88a94-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88a94-159">Next steps</span></span>
<span data-ttu-id="88a94-160">Przejdź za[zestawu SDK systemu Android](mobile-engagement-android-sdk-overview.md) tooget szczegółowych informacji o hello integracji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="88a94-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
