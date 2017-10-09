---
title: "tooAndroid powiadomienia wypychane aaaSending z usługi Azure Notification Hubs i Firebase Cloud Messaging | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak toouse usługi Azure Notification Hubs i Firebase Cloud Messaging toopush powiadomienia tooAndroid urządzeń."
services: notification-hubs
documentationcenter: android
keywords: powiadomienia wypychane, powiadomienie wypychane, powiadomienia wypychane w systemie android, firebase cloud messaging
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: d2e57437ac7b0ef77abf048f991043620621e58d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="bc309-104">Wysyłanie tooAndroid powiadomień wypychanych przy użyciu usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="bc309-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="bc309-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bc309-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bc309-106">W tym temacie przedstawiono powiadomienia wypychane za pomocą usługi Google Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="bc309-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="bc309-107">Jeśli nadal używasz Google Cloud Messaging (GCM), zobacz [tooAndroid powiadomień wypychanych wysyłająca z usługi Azure Notification Hubs i GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bc309-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="bc309-108">Ten samouczek pokazuje, jak toouse usługi Azure Notification Hubs i toosend Firebase Cloud Messaging aplikacji systemu Android tooan powiadomienia push.</span><span class="sxs-lookup"><span data-stu-id="bc309-108">This tutorial shows you how toouse Azure Notification Hubs and Firebase Cloud Messaging toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="bc309-109">Utworzysz pustą aplikację dla systemu Android służącą do odbierania powiadomień wypychanych przy użyciu usługi Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="bc309-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="bc309-110">Kod ukończyć powitalnych dla tego samouczka można pobrać z witryny GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="bc309-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc309-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bc309-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bc309-112">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bc309-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="bc309-113">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="bc309-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bc309-114">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="bc309-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="bc309-115">Ponadto tooan aktywne konto platformy Azure wymienionym powyżej, ten samouczek wymaga hello najnowszą wersję [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="bc309-115">In addition tooan active Azure account mentioned above, this tutorial requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="bc309-116">System Android 2.3 lub nowszy dla usługi Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="bc309-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="bc309-117">Usługa Google Repository w wersji 27 lub nowszej jest wymagana dla usługi Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="bc309-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="bc309-118">Usługi Google Play Services 9.0.2 lub nowsze dla usługi Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="bc309-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="bc309-119">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="bc309-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="bc309-120">Tworzenie nowego projektu programu Android Studio</span><span class="sxs-lookup"><span data-stu-id="bc309-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="bc309-121">W programie Android Studio utwórz nowy projekt programu Android Studio.</span><span class="sxs-lookup"><span data-stu-id="bc309-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="bc309-122">Wybierz hello **Telefon i Tablet** współczynnik i hello **Minimum SDK** , które mają toosupport.</span><span class="sxs-lookup"><span data-stu-id="bc309-122">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="bc309-123">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="bc309-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="bc309-124">Wybierz **pusty działania** dla działania głównego hello, kliknij przycisk **dalej**, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="bc309-124">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="bc309-125">Tworzenie projektu obsługującego usługę Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="bc309-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="bc309-126">Konfigurowanie nowego centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="bc309-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="bc309-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="bc309-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="bc309-128">W hello **ustawienia** bloku Centrum powiadomień, wybierz opcję **usługi powiadomień** , a następnie **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="bc309-128">In hello **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="bc309-129">Wprowadź klucz serwera FCM hello wcześniej zostały skopiowane z hello [konsoli Firebase](https://firebase.google.com/console/) i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="bc309-129">Enter hello FCM server key you copied earlier from hello [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs — Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="bc309-131">Centrum powiadomień jest teraz skonfigurowany toowork z Firebase Messagin chmury, a masz hello tooboth ciągów połączenia zarejestrować tooreceive Twojej aplikacji oraz wysyłać powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="bc309-131">Your notification hub is now configured toowork with Firebase Cloud Messagin, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="bc309-132"><a id="connecting-app"></a>Łączenie aplikacji toohello Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="bc309-132"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="bc309-133">Dodaj projekt toohello usług Google Play</span><span class="sxs-lookup"><span data-stu-id="bc309-133">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="bc309-134">Dodawanie bibliotek usługi Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="bc309-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="bc309-135">W hello `Build.Gradle` pliku hello **aplikacji**, Dodaj następujące wiersze w hello hello **zależności** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bc309-135">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="bc309-136">Dodaj następujące repozytorium po hello hello **zależności** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bc309-136">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="bc309-137">Aktualizowanie pliku AndroidManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-137">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="bc309-138">toosupport FCM, musimy zaimplementować identyfikator wystąpienia usługi odbiornika w naszym kodzie, który jest używany zbyt[uzyskiwania tokenów rejestracji](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) przy użyciu [interfejsu API firmy Google FirebaseInstanceId](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="bc309-138">toosupport FCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="bc309-139">W tym samouczku nazwiemy klasy hello `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="bc309-139">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="bc309-140">Dodaj następujące usługi definicji toohello pliku AndroidManifest.xml wewnątrz hello hello `<application>` tagu.</span><span class="sxs-lookup"><span data-stu-id="bc309-140">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="bc309-141">Po uzyskaniu tokenu rejestracji naszych FCM z hello FirebaseInstanceId interfejsu API, użyjemy go za[Zarejestruj hello Centrum powiadomień Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="bc309-141">Once we have received our FCM registration token from hello FirebaseInstanceId API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="bc309-142">Firma Microsoft będzie obsługę rejestracji w tle hello przy użyciu `IntentService` o nazwie `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="bc309-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="bc309-143">Ta usługa będzie również odpowiadać za odświeżanie naszego tokenu rejestracji usługi FCM.</span><span class="sxs-lookup"><span data-stu-id="bc309-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="bc309-144">Dodaj następujące usługi definicji toohello pliku AndroidManifest.xml wewnątrz hello hello `<application>` tagu.</span><span class="sxs-lookup"><span data-stu-id="bc309-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="bc309-145">Zdefiniujemy również odbiornik tooreceive powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="bc309-145">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="bc309-146">Dodaj powitania po odbiornika definicji toohello pliku AndroidManifest.xml wewnątrz hello `<application>` tagu.</span><span class="sxs-lookup"><span data-stu-id="bc309-146">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="bc309-147">Zastąp hello `<your package>` symbol zastępczy hello rzeczywistą nazwą pakietu wyświetlaną u góry hello hello `AndroidManifest.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="bc309-147">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="bc309-148">Dodaj uprawnienia poniżej hello powiązane z powitania po niezbędne FCM `</application>` tagu.</span><span class="sxs-lookup"><span data-stu-id="bc309-148">Add hello following necessary FCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="bc309-149">Upewnij się, że tooreplace `<your package>` z hello nazwą pakietu wyświetlaną u góry hello hello `AndroidManifest.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="bc309-149">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="bc309-150">Aby uzyskać więcej informacji o tych uprawnieniach, zobacz [Instalatora aplikacji klienta usługi GCM dla systemu Android](https://developers.google.com/cloud-messaging/android/client#manifest) i [migracji aplikacji klienta usługi GCM dla systemu Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="bc309-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="bc309-151">Dodawanie kodu</span><span class="sxs-lookup"><span data-stu-id="bc309-151">Adding code</span></span>
1. <span data-ttu-id="bc309-152">W widoku projektu hello, rozwiń węzeł **aplikacji** > **src** > **głównego** > **java**.</span><span class="sxs-lookup"><span data-stu-id="bc309-152">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="bc309-153">Kliknij prawym przyciskiem folder pakietu w węźle **java**, kliknij pozycję **New** (Nowy), a następnie kliknij pozycję **Java Class** (Klasa Java).</span><span class="sxs-lookup"><span data-stu-id="bc309-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="bc309-154">Dodaj nową klasę o nazwie `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="bc309-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio – nowa klasa Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="bc309-156">Upewnij się, że te trzy symbole zastępcze w hello następującego kodu dla hello hello tooupdate `NotificationSettings` klasy:</span><span class="sxs-lookup"><span data-stu-id="bc309-156">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="bc309-157">**SenderId**: hello identyfikator nadawcy uzyskany wcześniej w hello **Cloud Messaging** na karcie Ustawienia projektu w hello [konsoli Firebase](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="bc309-157">**SenderId**: hello Sender Id you obtained earlier in hello **Cloud Messaging** tab of your project settings in hello [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="bc309-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** parametry połączenia Centrum.</span><span class="sxs-lookup"><span data-stu-id="bc309-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="bc309-159">Możesz skopiować te parametry połączenia, klikając **zasady dostępu** na powitania **ustawienia** bloku Centrum w hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="bc309-159">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="bc309-160">**HubName**: Użyj hello nazwy Centrum powiadomień wyświetlaną w bloku Centrum hello w hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="bc309-160">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="bc309-161">`NotificationSettings` — kod:</span><span class="sxs-lookup"><span data-stu-id="bc309-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="bc309-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="bc309-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="bc309-163">}</span><span class="sxs-lookup"><span data-stu-id="bc309-163">}</span></span>
2. <span data-ttu-id="bc309-164">Przy użyciu powyższych kroków hello, Dodaj kolejną nową klasę o nazwie `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="bc309-164">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="bc309-165">Będzie to nasza implementacja usługi odbiornika interfejsu Instance ID.</span><span class="sxs-lookup"><span data-stu-id="bc309-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="bc309-166">Witaj kod dla tej klasy będzie wywoływać naszych `IntentService` za[token FCM hello odświeżania](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) w tle hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-166">hello code for this class will call our `IntentService` too[refresh hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="bc309-167">Dodaj inny nowy projekt tooyour klasy o nazwie `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="bc309-167">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="bc309-168">Będzie to implementacja hello naszych `IntentService` która będzie obsługiwać [odświeżanie tokenu FCM hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) i [rejestrowanie w Centrum powiadomień hello](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="bc309-168">This will be hello implementation for our `IntentService` that will handle [refreshing hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="bc309-169">Witaj Użyj następującego kodu dla tej klasy.</span><span class="sxs-lookup"><span data-stu-id="bc309-169">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
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
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if hello token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete registration", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="bc309-170">W Twojej `MainActivity` klasy, Dodaj następujące hello `import` instrukcje powyżej hello deklaracji klasy.</span><span class="sxs-lookup"><span data-stu-id="bc309-170">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="bc309-171">Dodaj następujące prywatne elementy członkowskie u góry hello klasy hello hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-171">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="bc309-172">Będą one używane [Sprawdź hello dostępności usług Google Play zgodnie z zaleceniami firmy Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="bc309-172">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="bc309-173">W Twojej `MainActivity` klasy, Dodaj hello następujące metody toohello dostępności usług Google Play.</span><span class="sxs-lookup"><span data-stu-id="bc309-173">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
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
5. <span data-ttu-id="bc309-174">W Twojej `MainActivity` klasy, Dodaj hello następującego kodu, który będzie sprawdzać dostępność usług Google Play przed wywołaniem z `IntentService` tooget Twojego tokenu rejestracji FCM i rejestrowanie w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="bc309-174">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="bc309-175">W hello `OnCreate` metody hello `MainActivity` klasy, Dodaj hello następującego procesu rejestracji hello toostart kod po utworzeniu działania.</span><span class="sxs-lookup"><span data-stu-id="bc309-175">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="bc309-176">Dodaj te dodatkowe metody toohello `MainActivity` tooverify aplikacji stanu i zgłosić stan w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc309-176">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="bc309-177">Witaj `ToastNotify` metoda używa hello *"Hello World"* `TextView` kontrolować stan tooreport i powiadomień w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-177">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="bc309-178">W układzie activity_main.xml Dodaj hello następującym identyfikatorze dla tego formantu.</span><span class="sxs-lookup"><span data-stu-id="bc309-178">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="bc309-179">Następnie dodamy podklasę dla naszego odbiornika zdefiniowanego w pliku AndroidManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-179">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="bc309-180">Dodaj inny nowy projekt tooyour klasy o nazwie `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="bc309-180">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="bc309-181">Dodaj następujące instrukcje import u góry hello hello `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="bc309-181">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="bc309-182">Dodaj następującego kodu dla hello hello `MyHandler` co podklasą klasy `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="bc309-182">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="bc309-183">Ten kod zastępuje hello `OnReceive` metody, więc program hello obsługi będzie zgłaszać odbierane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="bc309-183">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="bc309-184">Program Hello obsługi wysyła również Menedżera powiadomień systemu Android toohello powiadomień wypychanych hello przy użyciu hello `sendNotification()` metody.</span><span class="sxs-lookup"><span data-stu-id="bc309-184">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="bc309-185">Witaj `sendNotification()` — metoda powinna być wykonywana w przypadku aplikacji hello nie jest uruchomiona i Otrzymano powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="bc309-185">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="bc309-186">W programie Android Studio hello paska menu, kliknij przycisk **kompilacji** > **Odbuduj projekt** toomake się upewnić, że nie istnieją wcześniejsze błędy w kodzie.</span><span class="sxs-lookup"><span data-stu-id="bc309-186">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="bc309-187">Uruchamianie aplikacji hello na urządzeniu i sprawdź, czy pomyślnie rejestruje hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="bc309-187">Run hello app on your device and verify it registers successfully with hello notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="bc309-188">Rejestracji może zakończyć się niepowodzeniem po uruchomieniu początkowej hello do hello `onTokenRefresh()` wywołanie metody wystąpienia identyfikatora usługi.</span><span class="sxs-lookup"><span data-stu-id="bc309-188">Registration may fail on hello initial launch until hello `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="bc309-189">odświeżanie Hello należy zainicjować funkcję uodparniania pomyślną rejestrację hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="bc309-189">hello refresh should intiate a successful registration with hello notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="bc309-190">Wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="bc309-190">Sending push notifications</span></span>
<span data-ttu-id="bc309-191">Możesz przetestować odbieranie powiadomień wypychanych w aplikacji, wysyłając je za pośrednictwem hello [Azure Portal] -Wyszukaj hello **Rozwiązywanie problemów** sekcji w bloku Centrum hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="bc309-191">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Azure Notification Hubs — Wysyłanie testowe](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="bc309-193">(Opcjonalnie) Wysyłanie powiadomień wypychanych bezpośrednio z aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bc309-193">(Optional) Send push notifications directly from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bc309-194">Przykładem wysyłania powiadomień z powitania klienta aplikacji jest dostępna dla tylko do celów szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="bc309-194">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="bc309-195">Ponieważ wymaga to hello `DefaultFullSharedAccessSignature` toobe na powitania klienta aplikacji, opisuje czy użytkownik może uzyskać powiadomienia toosend nieautoryzowany dostęp tooyour klientów ryzyko toohello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="bc309-195">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="bc309-196">Zwykle powiadomienia są wysyłane przy użyciu serwera zaplecza.</span><span class="sxs-lookup"><span data-stu-id="bc309-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="bc309-197">W niektórych przypadkach może być powiadomień wypychanych stanie toosend toobe bezpośrednio z powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc309-197">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="bc309-198">W tej sekcji opisano, jak hello toosend powiadomień z powitania klienta przy użyciu [interfejsu API REST Centrum powiadomień Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc309-198">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="bc309-199">W widoku projektu programu Android Studio rozwiń węzeł **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="bc309-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="bc309-200">Otwórz hello `activity_main.xml` układu plik i kliknij przycisk hello **tekst** karcie tooupdate hello zawartość tekstową pliku hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-200">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="bc309-201">Zmodyfikuj go przy użyciu hello poniższego kodu, który dodaje nowe `Button` i `EditText` Centrum powiadomień toohello komunikatów powiadomień wypychanych służy do wysyłania.</span><span class="sxs-lookup"><span data-stu-id="bc309-201">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="bc309-202">Dodaj ten kod bezpośrednio przed u dołu hello `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="bc309-202">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="bc309-203">W widoku projektu programu Android Studio rozwiń węzeł **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="bc309-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="bc309-204">Otwórz hello `strings.xml` i Dodaj wartości ciągu hello, które odwołują się nowe hello `Button` i `EditText` kontrolki.</span><span class="sxs-lookup"><span data-stu-id="bc309-204">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="bc309-205">Dodaj te u dołu hello hello pliku, bezpośrednio przed `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="bc309-205">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="bc309-206">W Twojej `NotificationSetting.java` plików, Dodaj następujące ustawienie toohello hello `NotificationSettings` klasy.</span><span class="sxs-lookup"><span data-stu-id="bc309-206">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="bc309-207">Aktualizacja `HubFullAccess` z hello **DefaultFullSharedAccessSignature** parametry połączenia Centrum.</span><span class="sxs-lookup"><span data-stu-id="bc309-207">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="bc309-208">Ten ciąg połączenia można skopiować z hello [Azure Portal] , klikając **zasady dostępu** na powitania **ustawienia** bloku dla Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="bc309-208">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="bc309-209">W Twojej `MainActivity.java` plików, Dodaj następujące hello `import` instrukcje powyżej hello `MainActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="bc309-209">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="bc309-210">W Twojej `MainActivity.java` plików, Dodaj następujące elementy członkowskie u góry hello hello hello `MainActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="bc309-210">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="bc309-211">Należy utworzyć tooauthenticate tokenu sygnatury (SaS) Centrum powiadomień tooyour wiadomości toosend POST żądania.</span><span class="sxs-lookup"><span data-stu-id="bc309-211">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="bc309-212">To zrobić, analizując hello dane klucza z parametrów połączenia hello i następnie utworzenie hello tokenu sygnatury dostępu współdzielonego, jak wspomniano w hello [wspólne pojęcia](http://msdn.microsoft.com/library/azure/dn495627.aspx) dokumentacji interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="bc309-212">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="bc309-213">powitania po kod jest przykładem implementacji.</span><span class="sxs-lookup"><span data-stu-id="bc309-213">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="bc309-214">W `MainActivity.java`, Dodaj następujące metody toohello hello `MainActivity` klasy tooparse parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="bc309-214">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
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
7. <span data-ttu-id="bc309-215">W `MainActivity.java`, Dodaj następujące metody toohello hello `MainActivity` klasy toocreate token uwierzytelniania sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="bc309-215">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
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
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
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
8. <span data-ttu-id="bc309-216">W `MainActivity.java`, Dodaj następujące metody toohello hello `MainActivity` hello toohandle klasy **Wyślij powiadomienie E-mail** kliknij przycisk i wysyłać powiadomienia wypychane hello Centrum toohello wiadomości przy użyciu hello wbudowanego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="bc309-216">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
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
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="bc309-217">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bc309-217">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="bc309-218">Powiadomienia wypychane w emulatorze hello</span><span class="sxs-lookup"><span data-stu-id="bc309-218">Push notifications in hello emulator</span></span>
<span data-ttu-id="bc309-219">Jeśli chcesz tootest powiadomienia wypychane w emulatorze, upewnij się, że obraz emulatora obsługuje poziom interfejsu API Google hello wybrany dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bc309-219">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="bc309-220">Jeśli obraz nie obsługuje natywnych interfejsów API Google, będzie na końcu hello **usługi\_nie\_dostępne** wyjątku.</span><span class="sxs-lookup"><span data-stu-id="bc309-220">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="bc309-221">Ponadto toohello powyżej, upewnij się, że dodano Twoje tooyour konto Google uruchamiania emulatora w obszarze **ustawienia** > **kont**.</span><span class="sxs-lookup"><span data-stu-id="bc309-221">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="bc309-222">W przeciwnym razie Twojej tooregister prób w usłudze GCM mogą spowodować hello **uwierzytelniania\_** wyjątku.</span><span class="sxs-lookup"><span data-stu-id="bc309-222">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="bc309-223">Uruchomienie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bc309-223">Running hello application</span></span>
1. <span data-ttu-id="bc309-224">Uruchamianie aplikacji hello i zwróć uwagę, że identyfikator rejestracji hello jest zgłaszany oznacza pomyślną rejestrację.</span><span class="sxs-lookup"><span data-stu-id="bc309-224">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="bc309-225">Wprowadź toobe komunikat powiadomienia, wysyłane tooall urządzenia Android, które zostały zarejestrowane przy użyciu koncentratora hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-225">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="bc309-226">Naciśnij przycisk **Send Notification** (Wyślij powiadomienie).</span><span class="sxs-lookup"><span data-stu-id="bc309-226">Press **Send Notification**.</span></span> <span data-ttu-id="bc309-227">Zostaną wyświetlone wszystkie urządzenia, na których jest uruchomiona aplikacja hello `AlertDialog` wystąpienia z komunikatu powiadomienia wypychane hello.</span><span class="sxs-lookup"><span data-stu-id="bc309-227">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="bc309-228">Urządzenia, które nie zostały uruchomione aplikacji hello, ale zostały wcześniej zarejestrowane dla powiadomień wypychanych, otrzymasz powiadomienie w hello Menedżera powiadomień systemu Android.</span><span class="sxs-lookup"><span data-stu-id="bc309-228">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="bc309-229">Można je wyświetlić, szybko przesuwając w dół od hello lewym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="bc309-229">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="bc309-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc309-230">Next steps</span></span>
<span data-ttu-id="bc309-231">Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka jako hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="bc309-231">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="bc309-232">Przedstawiono w nim sposób toosend powiadomień z zaplecza ASP.NET za pomocą tagów tootarget określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bc309-232">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="bc309-233">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, zapoznaj się hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka.</span><span class="sxs-lookup"><span data-stu-id="bc309-233">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="bc309-234">toolearn więcej ogólnych informacji o usłudze Notification Hubs, zobacz nasze [wskazówki dotyczące usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="bc309-234">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[wskazówki dotyczące usługi Notification Hubs]: notification-hubs-push-notification-overview.md
[toousers powiadomienia toopush użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com
