---
title: "aaaGet wprowadzenie do usługi Azure Notification Hubs dla aplikacji dla urządzeń Kindle | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień aplikacji dla urządzeń Kindle tooa."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="bba91-103">Rozpoczynanie pracy z usługą Notification Hubs dla aplikacji dla urządzeń Kindle</span><span class="sxs-lookup"><span data-stu-id="bba91-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="bba91-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bba91-104">Overview</span></span>
<span data-ttu-id="bba91-105">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień aplikacji dla urządzeń Kindle tooa.</span><span class="sxs-lookup"><span data-stu-id="bba91-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="bba91-106">Utworzysz pustą aplikację dla urządzeń Kindle służącą do odbierania powiadomień wypychanych przy użyciu usługi Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="bba91-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bba91-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bba91-107">Prerequisites</span></span>
<span data-ttu-id="bba91-108">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="bba91-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="bba91-109">Pobierz hello zestawu SDK systemu Android (założono, że używany jest program Eclipse) z hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">witryny systemu Android</a>.</span><span class="sxs-lookup"><span data-stu-id="bba91-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="bba91-110">Wykonaj kroki hello w <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">ustawienie Up Your Development Environment</a> tooset się środowisko rozwoju dla urządzeń Kindle.</span><span class="sxs-lookup"><span data-stu-id="bba91-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="bba91-111">Dodawanie nowego portalu deweloperów toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="bba91-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="bba91-112">Najpierw utwórz aplikację w hello [portalu dla deweloperów firmy Amazon].</span><span class="sxs-lookup"><span data-stu-id="bba91-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="bba91-113">Kopiuj hello **klucz aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="bba91-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="bba91-114">W portalu powitania kliknij nazwę hello aplikacji, a następnie kliknij hello **Device Messaging** kartę.</span><span class="sxs-lookup"><span data-stu-id="bba91-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="bba91-115">Kliknij pozycję **Create a New Security Profile** (Utwórz nowy profil zabezpieczeń), a następnie utwórz nowy profil zabezpieczeń (na przykład **profil zabezpieczeń TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="bba91-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="bba91-116">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="bba91-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="bba91-117">Kliknij przycisk **profile zabezpieczeń** tooview hello zabezpieczeń profil, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="bba91-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="bba91-118">Kopiuj hello **identyfikator klienta** i **klucz tajny klienta** do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="bba91-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="bba91-119">Tworzenie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bba91-119">Create an API key</span></span>
1. <span data-ttu-id="bba91-120">Otwórz wiersz polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="bba91-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="bba91-121">Przejdź toohello folderu zestawu SDK systemu Android.</span><span class="sxs-lookup"><span data-stu-id="bba91-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="bba91-122">Wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="bba91-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="bba91-123">Dla hello **keystore** hasła, typ **android**.</span><span class="sxs-lookup"><span data-stu-id="bba91-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="bba91-124">Kopiuj hello **MD5** linii papilarnych.</span><span class="sxs-lookup"><span data-stu-id="bba91-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="bba91-125">W portalu dla deweloperów hello, na powitania **wiadomości** , kliknij pozycję **Android/Kindle** , a następnie wprowadź nazwę hello hello pakietu aplikacji (na przykład **com.sample.notificationhubtest**) i hello **MD5** wartość, a następnie kliknij przycisk **Wygeneruj klucz interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="bba91-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="bba91-126">Dodaj Centrum toohello poświadczeń</span><span class="sxs-lookup"><span data-stu-id="bba91-126">Add credentials toohello hub</span></span>
<span data-ttu-id="bba91-127">W portalu hello dodać powitania klienta, a klucz tajny klienta identyfikator toohello **Konfiguruj** kartę Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="bba91-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="bba91-128">Konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bba91-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="bba91-129">Podczas tworzenia aplikacji użyj co najmniej poziomu 17 interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bba91-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="bba91-130">Dodaj projekcie Eclipse tooyour biblioteki usługi ADM hello:</span><span class="sxs-lookup"><span data-stu-id="bba91-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="bba91-131">biblioteki usługi ADM hello tooobtain, [Pobierz hello SDK].</span><span class="sxs-lookup"><span data-stu-id="bba91-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="bba91-132">Wyodrębnij plik zip zestawu SDK hello.</span><span class="sxs-lookup"><span data-stu-id="bba91-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="bba91-133">W programie Eclipse kliknij prawym przyciskiem myszy projekt, a następnie kliknij pozycję **Properties** (Właściwości).</span><span class="sxs-lookup"><span data-stu-id="bba91-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="bba91-134">Wybierz **ścieżka kompilacji języka Java** na powitania po lewej i wybierz opcję hello ** bibliotek ** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="bba91-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="bba91-135">Kliknij przycisk **Dodaj zewnętrzne Jar**i wybierz hello plik `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` z katalogu hello, w którym wyodrębniono hello zestaw SDK Amazon.</span><span class="sxs-lookup"><span data-stu-id="bba91-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="bba91-136">Pobierz hello NotificationHubs zestawu SDK systemu Android (link).</span><span class="sxs-lookup"><span data-stu-id="bba91-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="bba91-137">Rozpakuj pakiet hello, a następnie przeciągnij plik hello `notification-hubs-sdk.jar` do hello `libs` folderu w środowisku Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bba91-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="bba91-138">Edytowanie użytkownika toosupport manifestu aplikacji usługi ADM:</span><span class="sxs-lookup"><span data-stu-id="bba91-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="bba91-139">Dodaj przestrzeń nazw Amazon hello hello głównego elementu manifestu:</span><span class="sxs-lookup"><span data-stu-id="bba91-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="bba91-140">Dodaj uprawnienia jako pierwszy element hello w elemencie manifestu hello.</span><span class="sxs-lookup"><span data-stu-id="bba91-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="bba91-141">SUBSTITUTE **[YOUR PACKAGE NAME]** z pakietem hello używane toocreate aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bba91-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="bba91-142">Wstaw po elemencie jako hello pierwszy element podrzędny elementu aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="bba91-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="bba91-143">Należy pamiętać, toosubstitute **[YOUR SERVICE NAME]** obsługi komunikatów ADM tworzonym w następnej sekcji hello (takie jak hello pakiet), i zastąp nazwą hello **[YOUR PACKAGE NAME]** z hello Nazwa pakietu, z którego użyto do utworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bba91-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="bba91-144">Tworzenie programu obsługi usługi ADM</span><span class="sxs-lookup"><span data-stu-id="bba91-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="bba91-145">Utwórz nową klasę, która dziedziczy `com.amazon.device.messaging.ADMMessageHandlerBase` i nadaj mu nazwę `MyADMMessageHandler`, jak pokazano w hello następującej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="bba91-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="bba91-146">Dodaj następujące hello `import` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="bba91-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="bba91-147">Dodaj następujące kod w utworzonej klasie hello hello.</span><span class="sxs-lookup"><span data-stu-id="bba91-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="bba91-148">Należy pamiętać o toosubstitute hello Centrum nazwy i parametry połączenia (nasłuchiwanie):</span><span class="sxs-lookup"><span data-stu-id="bba91-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="bba91-149">Dodaj hello następującego kodu toohello `OnMessage()` metody:</span><span class="sxs-lookup"><span data-stu-id="bba91-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="bba91-150">Dodaj hello następującego kodu toohello `OnRegistered` metody:</span><span class="sxs-lookup"><span data-stu-id="bba91-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="bba91-151">Dodaj hello następującego kodu toohello `OnUnregistered` metody:</span><span class="sxs-lookup"><span data-stu-id="bba91-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="bba91-152">W hello `MainActivity` metody, Dodaj powitania po instrukcji importu:</span><span class="sxs-lookup"><span data-stu-id="bba91-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="bba91-153">Dodaj następującego kodu na końcu hello hello hello `OnCreate` metody:</span><span class="sxs-lookup"><span data-stu-id="bba91-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="bba91-154">Dodaj aplikację tooyour klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bba91-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="bba91-155">W programie Eclipse Utwórz nowy plik o nazwie **api_key.txt** w hello katalogu zasobów projektu.</span><span class="sxs-lookup"><span data-stu-id="bba91-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="bba91-156">Witaj Otwórz plik i skopiuj hello klucz interfejsu API wygenerowany w portalu dla deweloperów firmy Amazon hello.</span><span class="sxs-lookup"><span data-stu-id="bba91-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="bba91-157">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bba91-157">Run hello app</span></span>
1. <span data-ttu-id="bba91-158">Uruchom hello emulator.</span><span class="sxs-lookup"><span data-stu-id="bba91-158">Start hello emulator.</span></span>
2. <span data-ttu-id="bba91-159">W emulatorze hello, szybko przesuń od góry hello, a następnie kliknij przycisk **ustawienia**, a następnie kliknij przycisk **Moje konto** i zarejestruj prawidłowe konto Amazon.</span><span class="sxs-lookup"><span data-stu-id="bba91-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="bba91-160">W środowisku Eclipse uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bba91-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="bba91-161">Jeśli wystąpi problem, Sprawdź czas hello hello emulatora (lub urządzenia).</span><span class="sxs-lookup"><span data-stu-id="bba91-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="bba91-162">wartość czasu Hello musi być dokładna.</span><span class="sxs-lookup"><span data-stu-id="bba91-162">hello time value must be accurate.</span></span> <span data-ttu-id="bba91-163">czas hello toochange hello emulatora urządzenia Kindle, możesz uruchomić hello następujące polecenie z katalogu narzędzi platformy zestawu SDK systemu Android:</span><span class="sxs-lookup"><span data-stu-id="bba91-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="bba91-164">Wysyłanie komunikatu</span><span class="sxs-lookup"><span data-stu-id="bba91-164">Send a message</span></span>
<span data-ttu-id="bba91-165">toosend wiadomości przy użyciu programu .NET:</span><span class="sxs-lookup"><span data-stu-id="bba91-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portalu dla deweloperów firmy Amazon]: https://developer.amazon.com/home.html
[Pobierz hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
