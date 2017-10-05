---
title: "Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu Android"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami wypychanymi na potrzeby aplikacji systemu Android."
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
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="a741f-103">Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="a741f-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a741f-104">W tym temacie pokazano, jak za pomocą usługi Azure Mobile Engagement można określić sposób użycia aplikacji oraz wysyłać powiadomienia wypychane do określonych segmentów użytkowników aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="a741f-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="a741f-105">W tym samouczku został omówiony prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a741f-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="a741f-106">W tym samouczku zostanie utworzona pusta aplikacja systemu Android służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="a741f-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a741f-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a741f-107">Prerequisites</span></span>
<span data-ttu-id="a741f-108">Wykonanie kroków tego samouczka wymaga [narzędzi dla deweloperów systemu Android](https://developer.android.com/sdk/index.html), które obejmują zintegrowane środowisko projektowe Android Studio, oraz najnowszej platformy Android.</span><span class="sxs-lookup"><span data-stu-id="a741f-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="a741f-109">Wymagany jest również [zestaw Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="a741f-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a741f-110">Do wykonania kroków tego samouczka jest potrzebne aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a741f-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="a741f-111">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a741f-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a741f-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="a741f-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="a741f-113">Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="a741f-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="a741f-114">Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a741f-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="a741f-115">Ten samouczek przedstawia „podstawową integrację”, tj. minimalny zestaw wymagany do zbierania danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="a741f-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="a741f-116">Aby zademonstrować integrację, utworzysz podstawową aplikację za pomocą programu Android Studio.</span><span class="sxs-lookup"><span data-stu-id="a741f-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="a741f-117">Kompletna dokumentacja integracji znajduje się w sekcji [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md) (Integracja z zestawem Mobile Engagement Android SDK).</span><span class="sxs-lookup"><span data-stu-id="a741f-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="a741f-118">Tworzenie projektu systemu Android</span><span class="sxs-lookup"><span data-stu-id="a741f-118">Create an Android project</span></span>
1. <span data-ttu-id="a741f-119">Uruchom program **Android Studio** i w oknie podręcznym wybierz pozycję **Start a new Android Studio project** (Utwórz nowy projekt programu Android Studio).</span><span class="sxs-lookup"><span data-stu-id="a741f-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="a741f-120">Podaj nazwę aplikacji i domenę firmy.</span><span class="sxs-lookup"><span data-stu-id="a741f-120">Provide an app name and company domain.</span></span> <span data-ttu-id="a741f-121">Zanotuj te informacje, ponieważ będą one potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="a741f-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="a741f-122">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a741f-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="a741f-123">Wybierz docelowy typ urządzeń i poziom interfejsu API, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="a741f-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a741f-124">Usługa Mobile Engagement wymaga co najmniej interfejsu API na poziomie 10 (Android 2.3.3).</span><span class="sxs-lookup"><span data-stu-id="a741f-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="a741f-125">Wybierz tutaj pozycję **Blank Activity** (Puste działanie), które jest jedynym ekranem dla tej aplikacji, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="a741f-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="a741f-126">Pozostaw wartości domyślne, a następnie kliknij pozycję **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="a741f-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="a741f-127">W programie Android Studio zostanie utworzona aplikacja demonstracyjna, z którą będzie zintegrowana usługa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a741f-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="a741f-128">Dołączanie biblioteki SDK do projektu</span><span class="sxs-lookup"><span data-stu-id="a741f-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="a741f-129">Pobierz zestaw [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span><span class="sxs-lookup"><span data-stu-id="a741f-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="a741f-130">Wypakuj plik archiwum do folderu na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="a741f-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="a741f-131">Ustal bibliotekę jar dla bieżącej wersji tego zestawu SDK, a następnie skopiuj ją do Schowka.</span><span class="sxs-lookup"><span data-stu-id="a741f-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="a741f-132">Przejdź do sekcji **Project** (Projekt) (1) i wklej plik jar w folderze libs (2).</span><span class="sxs-lookup"><span data-stu-id="a741f-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="a741f-133">Aby załadować bibliotekę, zsynchronizuj projekt.</span><span class="sxs-lookup"><span data-stu-id="a741f-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="a741f-134">Łączenie aplikacji z zapleczem usługi Mobile Engagement za pomocą parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="a741f-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="a741f-135">Skopiuj następujące wiersze kodu do lokalizacji tworzenia działania (należy to zrobić tylko w jednym miejscu aplikacji, zwykle w głównym działaniu).</span><span class="sxs-lookup"><span data-stu-id="a741f-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="a741f-136">Dla tej aplikacji przykładowej otwórz plik MainActivity w folderze src -> main -> java i dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="a741f-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="a741f-137">Rozpoznaj odwołania, naciskając klawisze Alt + Enter lub dodając następujące instrukcje importu:</span><span class="sxs-lookup"><span data-stu-id="a741f-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="a741f-138">Wróć do klasycznego portalu Azure i na stronie **Informacje o połączeniu** aplikacji skopiuj wartość **Parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="a741f-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="a741f-139">Wklej ją do parametru `setConnectionString`, zastępując cały ciąg pokazany w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="a741f-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="a741f-140">Dodawanie uprawnień i deklaracji usługi</span><span class="sxs-lookup"><span data-stu-id="a741f-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="a741f-141">Dodaj te uprawnienia do pliku Manifest.xml projektu bezpośrednio przed tagiem `<application>` lub po nim:</span><span class="sxs-lookup"><span data-stu-id="a741f-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="a741f-142">Aby zadeklarować usługę agenta, dodaj ten kod między tagami `<application>` i `</application>`:</span><span class="sxs-lookup"><span data-stu-id="a741f-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="a741f-143">We wklejonym kodzie zastąp tag `"<Your application name>"` w etykiecie wyświetlanej w menu **Ustawienia**, w którym można zobaczyć usługi uruchomione na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="a741f-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="a741f-144">Możesz na przykład dodać wyraz „Usługa” w tej etykiecie.</span><span class="sxs-lookup"><span data-stu-id="a741f-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="a741f-145">Wysyłanie ekranu do usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a741f-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="a741f-146">Aby rozpocząć wysyłanie danych i upewnić się, że użytkownicy są aktywni, konieczne jest wysłanie co najmniej jednego ekranu (Działanie) do zaplecza usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a741f-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="a741f-147">Przejdź do pliku **MainActivity.java** i dodaj następujący kod, aby zastąpić klasę podstawową klasy **MainActivity** klasą **EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="a741f-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="a741f-148">Jeśli klasą podstawową nie jest *Activity*, zapoznaj się z artykułem [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) (Zaawansowane raportowanie w systemie Android), aby poznać sposób dziedziczenia z różnych klas.</span><span class="sxs-lookup"><span data-stu-id="a741f-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="a741f-149">Oznacz jako komentarz następujący wiersz w tym prostym scenariuszu przykładowym:</span><span class="sxs-lookup"><span data-stu-id="a741f-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="a741f-150">Jeśli chcesz zachować `ActionBar` w aplikacji, zobacz [Zaawansowane raportowanie w systemie Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="a741f-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="a741f-151">Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="a741f-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="a741f-152">Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="a741f-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="a741f-153">W czasie kampanii usługa Mobile Engagement umożliwia interakcję z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a741f-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="a741f-154">Ten moduł w portalu Mobile Engagement ma nazwę REACH.</span><span class="sxs-lookup"><span data-stu-id="a741f-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="a741f-155">W poniższej sekcji aplikacja zostanie skonfigurowana do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="a741f-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="a741f-156">Kopiowanie zasobów zestawu SDK w projekcie</span><span class="sxs-lookup"><span data-stu-id="a741f-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="a741f-157">Przejdź wstecz do zawartości pobierania zestawu SDK i skopiuj folder **res**.</span><span class="sxs-lookup"><span data-stu-id="a741f-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="a741f-158">Wróć do programu Android Studio, wybierz katalog **main** plików projektu, a następnie wklej go, aby dodać zasoby do projektu.</span><span class="sxs-lookup"><span data-stu-id="a741f-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="a741f-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a741f-159">Next steps</span></span>
<span data-ttu-id="a741f-160">Przejdź do sekcji [Android SDK](mobile-engagement-android-sdk-overview.md) (Zestaw Android SDK), aby uzyskać szczegółową wiedzę na temat integracji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="a741f-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

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
