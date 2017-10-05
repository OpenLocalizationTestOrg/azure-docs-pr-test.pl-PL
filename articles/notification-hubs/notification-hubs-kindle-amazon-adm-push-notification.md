---
title: "Rozpoczynanie pracy z usługą Azure Notification Hubs dla aplikacji dla urządzeń Kindle | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji dla urządzeń Kindle przy użyciu usługi Azure Notification Hubs."
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
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="3fe36-103">Rozpoczynanie pracy z usługą Notification Hubs dla aplikacji dla urządzeń Kindle</span><span class="sxs-lookup"><span data-stu-id="3fe36-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="3fe36-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3fe36-104">Overview</span></span>
<span data-ttu-id="3fe36-105">Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji dla urządzeń Kindle przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="3fe36-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="3fe36-106">Utworzysz pustą aplikację dla urządzeń Kindle służącą do odbierania powiadomień wypychanych przy użyciu usługi Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="3fe36-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fe36-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3fe36-107">Prerequisites</span></span>
<span data-ttu-id="3fe36-108">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3fe36-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="3fe36-109">Pobierz zestaw SDK systemu Android (założono, że używane jest środowisko Eclipse) z <a href="http://go.microsoft.com/fwlink/?LinkId=389797">witryny systemu Android</a>.</span><span class="sxs-lookup"><span data-stu-id="3fe36-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="3fe36-110">Postępuj zgodnie z instrukcjami w temacie <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> (Konfigurowanie środowiska projektowego), aby skonfigurować środowisko projektowe dla urządzeń Kindle.</span><span class="sxs-lookup"><span data-stu-id="3fe36-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="3fe36-111">Dodawanie nowej aplikacji do portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="3fe36-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="3fe36-112">Najpierw utwórz aplikację w [portalu dla deweloperów firmy Amazon].</span><span class="sxs-lookup"><span data-stu-id="3fe36-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="3fe36-113">Skopiuj wartość **Application Key** (Klucz aplikacji).</span><span class="sxs-lookup"><span data-stu-id="3fe36-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="3fe36-114">W portalu kliknij nazwę aplikacji, a następnie kliknij kartę **Device Messaging**.</span><span class="sxs-lookup"><span data-stu-id="3fe36-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="3fe36-115">Kliknij pozycję **Create a New Security Profile** (Utwórz nowy profil zabezpieczeń), a następnie utwórz nowy profil zabezpieczeń (na przykład **profil zabezpieczeń TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="3fe36-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="3fe36-116">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="3fe36-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="3fe36-117">Kliknij pozycję **Security Profiles** (Profile zabezpieczeń), aby wyświetlić utworzony profil zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="3fe36-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="3fe36-118">Skopiuj wartości **Client ID** (Identyfikator klienta) i **Client Secret** (Klucz tajny klienta) do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="3fe36-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="3fe36-119">Tworzenie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="3fe36-119">Create an API key</span></span>
1. <span data-ttu-id="3fe36-120">Otwórz wiersz polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="3fe36-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="3fe36-121">Przejdź do folderu zestawu SDK systemu Android.</span><span class="sxs-lookup"><span data-stu-id="3fe36-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="3fe36-122">Wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="3fe36-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="3fe36-123">Jako hasło **keystore** wpisz wartość **android**.</span><span class="sxs-lookup"><span data-stu-id="3fe36-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="3fe36-124">Skopiuj odcisk palca **MD5**.</span><span class="sxs-lookup"><span data-stu-id="3fe36-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="3fe36-125">W portalu dla deweloperów na karcie **Messaging** (Komunikaty) kliknij pozycję **Android/Kindle** i wpisz nazwę pakietu aplikacji (na przykład **com.sample.notificationhubtest**) oraz wartość **MD5**, a następnie kliknij pozycję **Generate API Key** (Generuj klucz API).</span><span class="sxs-lookup"><span data-stu-id="3fe36-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="3fe36-126">Dodawanie poświadczeń do centrum</span><span class="sxs-lookup"><span data-stu-id="3fe36-126">Add credentials to the hub</span></span>
<span data-ttu-id="3fe36-127">W portalu dodaj klucz tajny klienta i identyfikator klienta na karcie **Konfiguracja** w centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3fe36-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="3fe36-128">Konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="3fe36-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="3fe36-129">Podczas tworzenia aplikacji użyj co najmniej poziomu 17 interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3fe36-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="3fe36-130">Dodaj biblioteki usługi ADM do projektu Eclipse:</span><span class="sxs-lookup"><span data-stu-id="3fe36-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="3fe36-131">Aby uzyskać bibliotekę usługi ADM [pobierz zestaw SDK].</span><span class="sxs-lookup"><span data-stu-id="3fe36-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="3fe36-132">Wyodrębnij plik zip zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="3fe36-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="3fe36-133">W programie Eclipse kliknij prawym przyciskiem myszy projekt, a następnie kliknij pozycję **Properties** (Właściwości).</span><span class="sxs-lookup"><span data-stu-id="3fe36-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="3fe36-134">Wybierz **ścieżka kompilacji języka Java** po lewej stronie, a następnie wybierz ** bibliotek ** u góry.</span><span class="sxs-lookup"><span data-stu-id="3fe36-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="3fe36-135">Kliknij pozycję **Add External Jar** (Dodaj zewnętrzny plik jar) i wybierz plik `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` z katalogu, do którego wyodrębniono zestaw SDK Amazon.</span><span class="sxs-lookup"><span data-stu-id="3fe36-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="3fe36-136">Pobierz zestaw SDK usługi Notification Hubs dla systemu Android (link).</span><span class="sxs-lookup"><span data-stu-id="3fe36-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="3fe36-137">Rozpakuj pakiet, a następnie przeciągnij plik `notification-hubs-sdk.jar` do folderu `libs` w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3fe36-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="3fe36-138">Edytuj manifest aplikacji w celu zapewnienia obsługi usługi ADM:</span><span class="sxs-lookup"><span data-stu-id="3fe36-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="3fe36-139">Dodaj przestrzeń nazw Amazon do głównego elementu manifestu:</span><span class="sxs-lookup"><span data-stu-id="3fe36-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="3fe36-140">Dodaj uprawnienia jako pierwszy element w elemencie manifestu.</span><span class="sxs-lookup"><span data-stu-id="3fe36-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="3fe36-141">Zastąp wartość **[YOUR PACKAGE NAME]** nazwą pakietu użytego do utworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fe36-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="3fe36-142">Wstaw następujący element jako pierwszy element podrzędny elementu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fe36-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="3fe36-143">Pamiętaj, aby zastąpić wartość **[YOUR SERVICE NAME]** nazwą programu obsługi komunikatów ADM tworzonego w następnej sekcji (w tym pakietu) oraz wartość **[YOUR PACKAGE NAME]** nazwą pakietu, którego użyto do utworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3fe36-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
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
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="3fe36-144">Tworzenie programu obsługi usługi ADM</span><span class="sxs-lookup"><span data-stu-id="3fe36-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="3fe36-145">Utwórz nową klasę dziedziczącą z klasy `com.amazon.device.messaging.ADMMessageHandlerBase` i nadaj jej nazwę `MyADMMessageHandler`, jak przedstawiono na następującej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="3fe36-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="3fe36-146">Dodaj następujące instrukcje `import`:</span><span class="sxs-lookup"><span data-stu-id="3fe36-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="3fe36-147">Dodaj następujący kod w utworzonej klasie.</span><span class="sxs-lookup"><span data-stu-id="3fe36-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="3fe36-148">Pamiętaj, aby zastąpić nazwę centrum i parametry połączenia (nasłuchiwanie):</span><span class="sxs-lookup"><span data-stu-id="3fe36-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="3fe36-149">Dodaj następujący kod do metody `OnMessage()`:</span><span class="sxs-lookup"><span data-stu-id="3fe36-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="3fe36-150">Dodaj następujący kod do metody `OnRegistered`:</span><span class="sxs-lookup"><span data-stu-id="3fe36-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="3fe36-151">Dodaj następujący kod do metody `OnUnregistered`:</span><span class="sxs-lookup"><span data-stu-id="3fe36-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="3fe36-152">W metodzie `MainActivity` dodaj następującą instrukcję import:</span><span class="sxs-lookup"><span data-stu-id="3fe36-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="3fe36-153">Dodaj następujący kod na końcu metody `OnCreate`:</span><span class="sxs-lookup"><span data-stu-id="3fe36-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="3fe36-154">Dodawanie klucza interfejsu API do aplikacji</span><span class="sxs-lookup"><span data-stu-id="3fe36-154">Add your API key to your app</span></span>
1. <span data-ttu-id="3fe36-155">W programie Eclipse utwórz nowy plik o nazwie **api_key.txt** w katalogu zasobów projektu.</span><span class="sxs-lookup"><span data-stu-id="3fe36-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="3fe36-156">Otwórz plik i skopiuj klucz interfejsu API wygenerowany w portalu dla deweloperów firmy Amazon.</span><span class="sxs-lookup"><span data-stu-id="3fe36-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="3fe36-157">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="3fe36-157">Run the app</span></span>
1. <span data-ttu-id="3fe36-158">Uruchom emulator.</span><span class="sxs-lookup"><span data-stu-id="3fe36-158">Start the emulator.</span></span>
2. <span data-ttu-id="3fe36-159">W emulatorze szybko przesuń od góry i kliknij pozycję **Settings** (Ustawienia), a następnie kliknij pozycję **My account** (Moje konto) i zarejestruj prawidłowe konto Amazon.</span><span class="sxs-lookup"><span data-stu-id="3fe36-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="3fe36-160">Uruchom aplikację w programie Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3fe36-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="3fe36-161">W przypadku wystąpienia problemu sprawdź czas emulatora (lub urządzenia).</span><span class="sxs-lookup"><span data-stu-id="3fe36-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="3fe36-162">Wartość czasu musi być dokładna.</span><span class="sxs-lookup"><span data-stu-id="3fe36-162">The time value must be accurate.</span></span> <span data-ttu-id="3fe36-163">Aby zmienić czas emulatora urządzenia Kindle, możesz uruchomić następujące polecenie w katalogu narzędzi platformy zestawu SDK dla systemu Android:</span><span class="sxs-lookup"><span data-stu-id="3fe36-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="3fe36-164">Wysyłanie komunikatu</span><span class="sxs-lookup"><span data-stu-id="3fe36-164">Send a message</span></span>
<span data-ttu-id="3fe36-165">Aby wysłać komunikat przy użyciu programu .NET:</span><span class="sxs-lookup"><span data-stu-id="3fe36-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="3fe36-166">[portalu dla deweloperów firmy Amazon]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="3fe36-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="3fe36-167">[pobierz zestaw SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="3fe36-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
