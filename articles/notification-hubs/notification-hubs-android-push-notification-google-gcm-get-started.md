---
title: "Wysyłanie powiadomień wypychanych do urządzeń z systemem Android przy użyciu usługi Azure Notification Hubs | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak za pomocą usługi Azure Notification Hubs wysyłać powiadomienia wypychane do urządzeń z systemem Android."
services: notification-hubs
documentationcenter: android
keywords: powiadomienia wypychane, powiadomienie wypychane, powiadomienia wypychane w systemie android
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 808fc10ef1ebb3288facbdf2e9e817b27d4fc6bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="be48c-104">Wysyłanie powiadomień wypychanych do urządzeń z systemem Android przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="be48c-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="be48c-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="be48c-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="be48c-106">W tym temacie przedstawiono powiadomienia wypychane za pomocą usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="be48c-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="be48c-107">Jeśli używasz usługi Google Firebase Cloud Messaging (FCM), zobacz [Wysyłanie powiadomień wypychanych do urządzeń z systemem Android przy użyciu usług Azure Notification Hubs i FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="be48c-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="be48c-108">Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji dla systemu Android przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="be48c-108">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an Android application.</span></span>
<span data-ttu-id="be48c-109">Utworzysz pustą aplikację dla systemu Android służącą do odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="be48c-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="be48c-110">Kompletny kod dla tego samouczka można pobrać z witryny GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="be48c-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be48c-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be48c-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="be48c-112">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="be48c-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="be48c-113">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="be48c-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="be48c-114">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="be48c-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="be48c-115">Oprócz aktywnego konta platformy Azure wspomnianego powyżej w tym samouczku wymagana jest jedynie najnowsza wersja programu [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="be48c-115">In addition to an active Azure account mentioned above, this tutorial only requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="be48c-116">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="be48c-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="be48c-117">Tworzenie projektu obsługującego usługę Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="be48c-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="be48c-118">Konfigurowanie nowego centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="be48c-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="be48c-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="be48c-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="be48c-120">W bloku **Ustawienia** wybierz pozycję **Usługi powiadomień**, a następnie wybierz pozycję **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="be48c-120">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="be48c-121">Wprowadź klucz interfejsu API i kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="be48c-121">Enter the API key and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="be48c-123">Twoje centrum powiadomień jest teraz skonfigurowane do pracy z usługą GCM i uzyskano parametry połączenia do rejestrowania aplikacji w celu odbierania i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="be48c-123">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="be48c-124"><a id="connecting-app"></a>Łączenie aplikacji z centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="be48c-124"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="be48c-125">Tworzenie nowego projektu dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="be48c-125">Create a new Android project</span></span>
1. <span data-ttu-id="be48c-126">W programie Android Studio utwórz nowy projekt programu Android Studio.</span><span class="sxs-lookup"><span data-stu-id="be48c-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio — nowy projekt][13]
2. <span data-ttu-id="be48c-128">Wybierz kształt **Phone and Tablet** (Telefon i tablet) oraz odpowiednią wersję z listy **Minimum SDK** (Minimalna wersja zestawu SDK), która ma być obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="be48c-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="be48c-129">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="be48c-129">Then click **Next**.</span></span>
   
   ![Android Studio — przepływ pracy tworzenia projektu][14]
3. <span data-ttu-id="be48c-131">Wybierz pozycję **Empty Activity** (Puste działanie) dla głównego działania i kliknij przycisk **Next** (Dalej), a następnie kliknij przycisk **Finish** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="be48c-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="be48c-132">Dodawanie usług Google Play do projektu</span><span class="sxs-lookup"><span data-stu-id="be48c-132">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="be48c-133">Dodawanie bibliotek usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="be48c-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="be48c-134">W pliku `Build.Gradle` dla **aplikacji** dodaj następujące wiersze w sekcji **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="be48c-134">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="be48c-135">Dodaj następujące repozytorium po sekcji **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="be48c-135">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="be48c-136">Aktualizowanie pliku AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="be48c-136">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="be48c-137">W celu zapewnienia obsługi usługi GCM musimy zaimplementować w naszym kodzie wystąpienie usługi odbiornika interfejsu Instance ID, który służy do [uzyskiwania tokenów rejestracji](https://developers.google.com/cloud-messaging/android/client#sample-register) przy użyciu [interfejsu API Instance ID firmy Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="be48c-137">To support GCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="be48c-138">W tym samouczku nazwiemy tę klasę `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="be48c-138">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="be48c-139">Dodaj następującą definicję usługi do pliku AndroidManifest.xml wewnątrz tagu `<application>`.</span><span class="sxs-lookup"><span data-stu-id="be48c-139">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="be48c-140">Zastąp symbol zastępczy `<your package>` rzeczywistą nazwą pakietu wyświetlaną u góry pliku `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="be48c-140">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="be48c-141">Po uzyskaniu tokenu rejestracji usługi GCM z interfejsu API Instance ID użyjemy go do [rejestracji w usłudze Azure Notification Hubs](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="be48c-141">Once we have received our GCM registration token from the Instance ID API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="be48c-142">Zapewnimy obsługę rejestracji w tle przy użyciu klasy `IntentService` o nazwie `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="be48c-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="be48c-143">Ta usługa będzie również odpowiadać za [odświeżanie naszego tokenu rejestracji usługi GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="be48c-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="be48c-144">Dodaj następującą definicję usługi do pliku AndroidManifest.xml wewnątrz tagu `<application>`.</span><span class="sxs-lookup"><span data-stu-id="be48c-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="be48c-145">Zastąp symbol zastępczy `<your package>` rzeczywistą nazwą pakietu wyświetlaną u góry pliku `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="be48c-145">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="be48c-146">Zdefiniujemy również odbiornik, aby otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="be48c-146">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="be48c-147">Dodaj następującą definicję odbiornika do pliku AndroidManifest.xml wewnątrz tagu `<application>`.</span><span class="sxs-lookup"><span data-stu-id="be48c-147">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="be48c-148">Zastąp symbol zastępczy `<your package>` rzeczywistą nazwą pakietu wyświetlaną u góry pliku `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="be48c-148">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="be48c-149">Dodaj następujące wymagane uprawnienia powiązane z usługą GCM poniżej tagu `</application>`.</span><span class="sxs-lookup"><span data-stu-id="be48c-149">Add the following necessary GCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="be48c-150">Zastąp wartość `<your package>` nazwą pakietu wyświetlaną u góry pliku `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="be48c-150">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="be48c-151">Aby uzyskać więcej informacji o tych uprawnieniach, zobacz [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) (Konfigurowanie aplikacji klienta usługi GCM dla systemu Android).</span><span class="sxs-lookup"><span data-stu-id="be48c-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="be48c-152">Dodawanie kodu</span><span class="sxs-lookup"><span data-stu-id="be48c-152">Adding code</span></span>
1. <span data-ttu-id="be48c-153">W widoku projektu rozwiń węzeł **app** > **src** > **main** > **java**.</span><span class="sxs-lookup"><span data-stu-id="be48c-153">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="be48c-154">Kliknij prawym przyciskiem folder pakietu w węźle **java**, kliknij pozycję **New** (Nowy), a następnie kliknij pozycję **Java Class** (Klasa Java).</span><span class="sxs-lookup"><span data-stu-id="be48c-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="be48c-155">Dodaj nową klasę o nazwie `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="be48c-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio – nowa klasa Java][6]
   
    <span data-ttu-id="be48c-157">Zaktualizuj te trzy symbole zastępcze w poniższym kodzie dla klasy `NotificationSettings`:</span><span class="sxs-lookup"><span data-stu-id="be48c-157">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="be48c-158">**SenderId**: numer projektu uzyskany wcześniej w konsoli [Google Cloud Console](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="be48c-158">**SenderId**: The project number you obtained earlier in the [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="be48c-159">**HubListenConnectionString**: domyślne parametry połączenia **DefaultListenAccessSignature** dla centrum.</span><span class="sxs-lookup"><span data-stu-id="be48c-159">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="be48c-160">Możesz skopiować te parametry połączenia, klikając pozycję **Zasady dostępu** w bloku **Ustawienia** centrum w witrynie [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="be48c-160">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="be48c-161">**HubName**: użyj nazwy centrum powiadomień wyświetlanej w bloku centrum w witrynie [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="be48c-161">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="be48c-162">`NotificationSettings` — kod:</span><span class="sxs-lookup"><span data-stu-id="be48c-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="be48c-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="be48c-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="be48c-164">}</span><span class="sxs-lookup"><span data-stu-id="be48c-164">}</span></span>
2. <span data-ttu-id="be48c-165">Przy użyciu powyższych kroków dodaj nową klasę o nazwie `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="be48c-165">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="be48c-166">Będzie to nasza implementacja usługi odbiornika interfejsu Instance ID.</span><span class="sxs-lookup"><span data-stu-id="be48c-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="be48c-167">Kod dla tej klasy będzie wywoływać naszą klasę `IntentService` w celu [odświeżenia tokenu usługi GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) w tle.</span><span class="sxs-lookup"><span data-stu-id="be48c-167">The code for this class will call our `IntentService` to [refresh the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="be48c-168">Dodaj kolejną nową klasę o nazwie `RegistrationIntentService` do projektu.</span><span class="sxs-lookup"><span data-stu-id="be48c-168">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="be48c-169">Będzie to implementacja naszej klasy `IntentService`, która będzie obsługiwać [odświeżanie tokenu usługi GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) i [rejestrowanie w centrum powiadomień](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="be48c-169">This will be the implementation for our `IntentService` that will handle [refreshing the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="be48c-170">Użyj następującego kodu dla tej klasy.</span><span class="sxs-lookup"><span data-stu-id="be48c-170">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting to register with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete token refresh", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="be48c-171">W klasie `MainActivity` dodaj następujące instrukcje `import` nad deklaracją klasy.</span><span class="sxs-lookup"><span data-stu-id="be48c-171">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="be48c-172">Dodaj następujące prywatne elementy członkowskie u góry klasy.</span><span class="sxs-lookup"><span data-stu-id="be48c-172">Add the following private members at the top of the class.</span></span> <span data-ttu-id="be48c-173">Będą one używane do [sprawdzania dostępności usług Google Play zgodnie z zaleceniami firmy Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="be48c-173">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="be48c-174">W klasie `MainActivity` dodaj następującą metodę do sprawdzania dostępności usług Google Play.</span><span class="sxs-lookup"><span data-stu-id="be48c-174">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="be48c-175">W klasie `MainActivity` dodaj następujący kod, który będzie sprawdzać dostępność usług Google Play przed wywołaniem klasy `IntentService` w celu pobrania tokenu rejestracji GCM i rejestracji w centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="be48c-175">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService to register this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="be48c-176">W metodzie `OnCreate` klasy `MainActivity` dodaj następujący kod w celu uruchomienia procesu rejestracji po utworzeniu działania.</span><span class="sxs-lookup"><span data-stu-id="be48c-176">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="be48c-177">Dodaj te dodatkowe metody do klasy `MainActivity`, aby zweryfikować stan aplikacji i zgłosić stan w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be48c-177">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="be48c-178">Metoda `ToastNotify` używa kontrolki *"Hello World"* `TextView` do trwałego zgłaszania stanu i powiadomień w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be48c-178">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="be48c-179">W układzie activity_main.xml dodaj następujący identyfikator dla tej kontrolki.</span><span class="sxs-lookup"><span data-stu-id="be48c-179">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="be48c-180">Następnie dodamy podklasę dla naszego odbiornika zdefiniowanego w pliku AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="be48c-180">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="be48c-181">Dodaj kolejną nową klasę o nazwie `MyHandler` do projektu.</span><span class="sxs-lookup"><span data-stu-id="be48c-181">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="be48c-182">Dodaj następujące instrukcje import u góry pliku `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="be48c-182">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="be48c-183">Dodaj następujący kod do klasy `MyHandler`, aby stała się podklasą klasy `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="be48c-183">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="be48c-184">Ten kod zastępuje metodę `OnReceive`, dlatego program obsługi będzie zgłaszać odbierane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="be48c-184">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="be48c-185">Program obsługi wysyła również powiadomienie wypychane do menedżera powiadomień systemu Android za pomocą metody `sendNotification()`.</span><span class="sxs-lookup"><span data-stu-id="be48c-185">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="be48c-186">Metoda `sendNotification()` powinna być wykonywana, gdy aplikacja nie jest uruchomiona i otrzymano powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="be48c-186">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="be48c-187">W programie Android Studio na pasku menu kliknij pozycję **Build** > **Rebuild Project** (Kompiluj — Kompiluj ponownie projekt), aby upewnić się, że w kodzie nie występują żadne błędy.</span><span class="sxs-lookup"><span data-stu-id="be48c-187">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="be48c-188">Wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="be48c-188">Sending push notifications</span></span>
<span data-ttu-id="be48c-189">Odbieranie powiadomień wypychanych w aplikacji możesz przetestować, wysyłając je z poziomu witryny [Azure Portal] za pośrednictwem sekcji **Rozwiązywanie problemów** w bloku centrum, jak przedstawiono poniżej.</span><span class="sxs-lookup"><span data-stu-id="be48c-189">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure Notification Hubs — Wysyłanie testowe](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="be48c-191">(Opcjonalnie) Wysyłanie powiadomień wypychanych bezpośrednio z poziomu aplikacji</span><span class="sxs-lookup"><span data-stu-id="be48c-191">(Optional) Send push notifications directly from the app</span></span>
<span data-ttu-id="be48c-192">Zwykle powiadomienia są wysyłane przy użyciu serwera zaplecza.</span><span class="sxs-lookup"><span data-stu-id="be48c-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="be48c-193">W niektórych przypadkach warto wysyłać powiadomienia bezpośrednio z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="be48c-193">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="be48c-194">W tej sekcji wyjaśniono sposób wysyłania powiadomień z klienta przy użyciu [interfejsu API REST usługi Azure Notification Hubs](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="be48c-194">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="be48c-195">W widoku projektu programu Android Studio rozwiń węzeł **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="be48c-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="be48c-196">Otwórz plik układu `activity_main.xml` i kliknij kartę **Text** (Tekst), aby zaktualizować zawartość tekstową pliku.</span><span class="sxs-lookup"><span data-stu-id="be48c-196">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="be48c-197">Zaktualizuj go przy użyciu poniższego kodu, który dodaje nowe kontrolki `Button` i `EditText` służące do wysyłania komunikatów powiadomień wypychanych do centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="be48c-197">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="be48c-198">Dodaj ten kod w dolnej części bezpośrednio przed elementem `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="be48c-198">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="be48c-199">W widoku projektu programu Android Studio rozwiń węzeł **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="be48c-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="be48c-200">Otwórz plik `strings.xml` i dodaj wartości ciągu, do których odwołują się nowe kontrolki `Button` i `EditText`.</span><span class="sxs-lookup"><span data-stu-id="be48c-200">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="be48c-201">Dodaj je w dolnej części pliku, bezpośrednio przed elementem `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="be48c-201">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="be48c-202">W pliku `NotificationSetting.java` dodaj następujące ustawienie do klasy `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="be48c-202">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="be48c-203">Zaktualizuj element `HubFullAccess` przy użyciu parametrów połączenia **DefaultFullSharedAccessSignature** dla swojego centrum.</span><span class="sxs-lookup"><span data-stu-id="be48c-203">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="be48c-204">Parametry połączenia można skopiować z witryny [Azure Portal], klikając pozycję **Zasady dostępu** w bloku **Ustawienia** centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="be48c-204">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="be48c-205">W pliku `MainActivity.java` dodaj następujące instrukcje `import` nad klasą `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="be48c-205">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="be48c-206">W pliku `MainActivity.java` dodaj następujące elementy członkowskie u góry klasy `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="be48c-206">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="be48c-207">Należy utworzyć token sygnatury dostępu współdzielonego w celu uwierzytelnienia żądania POST do wysyłania komunikatów do centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="be48c-207">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="be48c-208">W tym celu należy przeanalizować dane klucza z parametrów połączenia, a następnie utworzyć token sygnatury dostępu współdzielonego, jak określono w dokumentacji interfejsu API REST [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) (Wspólne pojęcia).</span><span class="sxs-lookup"><span data-stu-id="be48c-208">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="be48c-209">Poniższy kod jest przykładem implementacji.</span><span class="sxs-lookup"><span data-stu-id="be48c-209">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="be48c-210">W pliku `MainActivity.java` dodaj następującą metodę do klasy `MainActivity`, aby przeanalizować parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="be48c-210">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="be48c-211">W pliku `MainActivity.java` dodaj następującą metodę do klasy `MainActivity`, aby utworzyć token uwierzytelniania sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="be48c-211">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="be48c-212">W pliku `MainActivity.java` dodaj następującą metodę do klasy `MainActivity` w celu obsługi kliknięcia przycisku **Send Notification** (Wyślij powiadomienie) i wysłania komunikatu do centrum przy użyciu wbudowanego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="be48c-212">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="be48c-213">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="be48c-213">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="be48c-214">Powiadomienia wypychane w emulatorze</span><span class="sxs-lookup"><span data-stu-id="be48c-214">Push notifications in the emulator</span></span>
<span data-ttu-id="be48c-215">Aby przetestować powiadomienia wypychane w emulatorze, upewnij się, że obraz emulatora obsługuje poziom interfejsu API Google wybrany dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be48c-215">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="be48c-216">Jeśli obraz nie obsługuje natywnych interfejsów API Google, wystąpi wyjątek **SERVICE\_NOT\_AVAILABLE** (usługa niedostępna).</span><span class="sxs-lookup"><span data-stu-id="be48c-216">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="be48c-217">Oprócz powyższego, upewnij się, że dodano konto Google do uruchomionego emulatora w obszarze **Settings** > **Accounts** (Ustawienia — Konta).</span><span class="sxs-lookup"><span data-stu-id="be48c-217">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="be48c-218">W przeciwnym razie próby rejestracji w usłudze GCM mogą spowodować wystąpienie wyjątku **AUTHENTICATION\_FAILED** (uwierzytelnianie nie powiodło się).</span><span class="sxs-lookup"><span data-stu-id="be48c-218">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="be48c-219">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="be48c-219">Running the application</span></span>
1. <span data-ttu-id="be48c-220">Uruchom aplikację i zwróć uwagę, czy identyfikator rejestracji jest zgłaszany, co oznacza pomyślną rejestrację.</span><span class="sxs-lookup"><span data-stu-id="be48c-220">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
      ![Testowanie w systemie Android — rejestracja kanału][18]
2. <span data-ttu-id="be48c-222">Wprowadź komunikat powiadomienia, który ma zostać wysłany do wszystkich urządzeń z systemem Android zarejestrowanych w centrum.</span><span class="sxs-lookup"><span data-stu-id="be48c-222">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
      ![Testowanie w systemie Android — wysyłanie komunikatu][19]

3. <span data-ttu-id="be48c-224">Naciśnij przycisk **Send Notification** (Wyślij powiadomienie).</span><span class="sxs-lookup"><span data-stu-id="be48c-224">Press **Send Notification**.</span></span> <span data-ttu-id="be48c-225">Na wszystkich urządzeniach, na których jest uruchomiona aplikacja, zostanie wyświetlone wystąpienie kontrolki `AlertDialog` z komunikatem powiadomienia wypychanego.</span><span class="sxs-lookup"><span data-stu-id="be48c-225">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="be48c-226">Urządzenia, na których aplikacja nie jest uruchomiona, ale zostały wcześniej zarejestrowane do otrzymywania powiadomień wypychanych otrzymają powiadomienie w menedżerze powiadomień systemu Android.</span><span class="sxs-lookup"><span data-stu-id="be48c-226">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="be48c-227">Można je wyświetlić, szybko przesuwając w dół od lewego górnego rogu.</span><span class="sxs-lookup"><span data-stu-id="be48c-227">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
      ![Testowanie w systemie Android — powiadomienia][21]

## <a name="next-steps"></a><span data-ttu-id="be48c-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be48c-229">Next steps</span></span>
<span data-ttu-id="be48c-230">Zalecanym następnym krokiem jest zapoznanie się z samouczkiem [Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="be48c-230">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="be48c-231">Przedstawiono w nim sposób wysyłania powiadomień z zaplecza programu ASP.NET przy użyciu tagów służących do adresowania powiadomień do określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="be48c-231">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="be48c-232">Jeśli chcesz podzielić użytkowników na grupy zainteresowań, zobacz samouczek [Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="be48c-232">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="be48c-233">Więcej ogólnych informacji o usłudze Notification Hubs zawiera temat [Wskazówki dotyczące usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="be48c-233">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="be48c-234">[Wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="be48c-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="be48c-235">[Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="be48c-235">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="be48c-236">[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="be48c-236">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="be48c-237">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="be48c-237">[Azure Portal]: https://portal.azure.com</span></span>
