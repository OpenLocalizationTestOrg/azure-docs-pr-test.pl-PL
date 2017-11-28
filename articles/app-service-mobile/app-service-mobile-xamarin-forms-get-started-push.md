---
title: "aplikacji platformy Xamarin.Forms tooyour powiadomień wypychanych aaaAdd | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure usług toosend obejmującego wiele platform wypychania powiadomień tooyour platformy Xamarin.Forms aplikacji."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="36ee6-103">Dodawanie aplikacji platformy Xamarin.Forms tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="36ee6-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="36ee6-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="36ee6-104">Overview</span></span>
<span data-ttu-id="36ee6-105">W tym samouczku, Dodaj wypychania powiadomień tooall hello projektów, które jest wynikiem hello [szybki start platformy Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="36ee6-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="36ee6-106">Oznacza to, że powiadomienie wypychane zostanie wysłane tooall klientów i platform, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="36ee6-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="36ee6-107">Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="36ee6-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="36ee6-108">Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="36ee6-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36ee6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="36ee6-109">Prerequisites</span></span>
<span data-ttu-id="36ee6-110">Dla systemu iOS, konieczne będzie [członkostwo w programie dla deweloperów firmy Apple](https://developer.apple.com/programs/ios/) i urządzenie fizyczne z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="36ee6-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="36ee6-111">Witaj [symulatora systemu iOS nie obsługuje powiadomień wypychanych](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="36ee6-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="36ee6-112"><a name="configure-hub"></a>Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="36ee6-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="36ee6-113">Zaktualizuj powiadomień wypychanych toosend powitania serwera projektu</span><span class="sxs-lookup"><span data-stu-id="36ee6-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="36ee6-114">Konfigurowanie i uruchamianie projektu systemu Android hello (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="36ee6-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="36ee6-115">Ukończenie tej sekcji tooenable powiadomień wypychanych dla hello Droid platformy Xamarin.Forms projektu dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="36ee6-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="36ee6-116">Włącz Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="36ee6-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="36ee6-117">Skonfiguruj hello Mobile Apps zaplecza toosend wypychania żądania przy użyciu FCM</span><span class="sxs-lookup"><span data-stu-id="36ee6-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="36ee6-118">Dodaj projekt systemu Android toohello powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="36ee6-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="36ee6-119">Witaj zaplecza skonfigurowane z FCM można dodawać składników i kody tooregister klienta toohello z FCM.</span><span class="sxs-lookup"><span data-stu-id="36ee6-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="36ee6-120">Można również zarejestrować dla powiadomień wypychanych przy użyciu usługi Azure Notification Hubs za pomocą hello Mobile Apps ponownie zakończyć i otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="36ee6-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="36ee6-121">W hello **Droid** projektu, kliknij prawym przyciskiem myszy hello **składniki** folder, a następnie kliknij przycisk **Uzyskaj więcej składników... **. Następnie wyszukaj hello **Google Cloud Messaging Client** składników i dodaj go toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="36ee6-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="36ee6-122">Ten składnik obsługuje powiadomień wypychanych dla projektu dla systemu Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="36ee6-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="36ee6-123">Otwórz plik projektu MainActivity.cs hello, a następnie dodaj powitania po instrukcji u góry pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="36ee6-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="36ee6-124">Dodaj hello następującego kodu toohello **OnCreate** za wywołanie metody po hello**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="36ee6-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="36ee6-125">Dodaj nową **CreateAndShowDialog** metody pomocnika, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="36ee6-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="36ee6-126">Dodaj hello następującego kodu toohello **MainActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="36ee6-126">Add hello following code toohello **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="36ee6-127">To przedstawia bieżący hello **MainActivity** wystąpienie, dlatego można wykonać na powitania głównego wątku interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="36ee6-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="36ee6-128">Inicjowanie hello `instance` zmiennej na początku hello hello **OnCreate** metody, w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="36ee6-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="36ee6-129">Dodaj nowy toohello pliku klasy **Droid** projektu o nazwie `GcmService.cs`i upewnij się, że następujące hello **przy użyciu** instrukcje znajdują się u góry pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="36ee6-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. <span data-ttu-id="36ee6-130">Dodaj następujące żądania uprawnień u góry pliku hello powitania po hello hello **przy użyciu** instrukcje i przed hello **przestrzeni nazw** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="36ee6-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="36ee6-131">Dodaj hello następujące przestrzeni nazw toohello definicji klasy.</span><span class="sxs-lookup"><span data-stu-id="36ee6-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="36ee6-132">Zastąp **< PROJECT_NUMBER >** wcześniej zapisany numer projektu.</span><span class="sxs-lookup"><span data-stu-id="36ee6-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="36ee6-133">Zastąp hello pusty **GcmService** klas z następującego kodu, który używa nowego odbiornika emisji hello hello:</span><span class="sxs-lookup"><span data-stu-id="36ee6-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="36ee6-134">Dodaj hello następującego kodu toohello **GcmService** klasy.</span><span class="sxs-lookup"><span data-stu-id="36ee6-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="36ee6-135">Przesłania hello **OnRegistered** obsługi zdarzeń i implementuje **zarejestrować** metody.</span><span class="sxs-lookup"><span data-stu-id="36ee6-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    <span data-ttu-id="36ee6-136">Zwróć uwagę, że ten kod używa hello `messageParam` parametru w hello szablon rejestracji.</span><span class="sxs-lookup"><span data-stu-id="36ee6-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="36ee6-137">Dodaj hello następującego kodu, który implementuje **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="36ee6-137">Add hello following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="36ee6-138">Obsługuje przychodzące powiadomienia i wysyła je toobe Menedżera powiadomień toohello wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="36ee6-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="36ee6-139">**GcmServiceBase** wymaga również tooimplement hello **OnUnRegistered** i **OnError** metody obsługi, które można wykonać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="36ee6-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="36ee6-140">Teraz są gotowe testu powiadomień wypychanych w aplikacji hello uruchomionej na urządzeniu z systemem Android lub hello emulatora.</span><span class="sxs-lookup"><span data-stu-id="36ee6-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="36ee6-141">Testowych powiadomień wypychanych w aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="36ee6-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="36ee6-142">Witaj pierwsze dwa kroki są wymagane tylko wtedy, gdy w przypadku testowania emulatora.</span><span class="sxs-lookup"><span data-stu-id="36ee6-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="36ee6-143">Upewnij się, że jest wdrażany tooor debugowania na urządzeniu wirtualnym, który ma ustawić jako cel hello interfejsy API Google, jak pokazano poniżej, w Menedżerze urządzeń wirtualnych systemu Android hello.</span><span class="sxs-lookup"><span data-stu-id="36ee6-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="36ee6-144">Dodanie urządzenia Android toohello konto Google, klikając **aplikacje** > **ustawienia** > **Dodaj konto**.</span><span class="sxs-lookup"><span data-stu-id="36ee6-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="36ee6-145">Następnie wykonaj hello monity tooadd istniejące urządzenie toohello konto Google lub toocreate nowy.</span><span class="sxs-lookup"><span data-stu-id="36ee6-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="36ee6-146">W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy hello **Droid** projekt i kliknij przycisk **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="36ee6-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="36ee6-147">Kliknij przycisk **Uruchom** toobuild hello projekt i uruchomić aplikacji hello na urządzeniu z systemem Android lub w emulatorze.</span><span class="sxs-lookup"><span data-stu-id="36ee6-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="36ee6-148">W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (**+**) ikona.</span><span class="sxs-lookup"><span data-stu-id="36ee6-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="36ee6-149">Sprawdź, czy otrzyma powiadomienie po dodaniu elementu.</span><span class="sxs-lookup"><span data-stu-id="36ee6-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="36ee6-150">Konfigurowanie i uruchamianie projektu iOS hello (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="36ee6-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="36ee6-151">Ta sekcja dotyczy uruchamiania projektu Xamarin iOS powitania dla urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="36ee6-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="36ee6-152">Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="36ee6-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="36ee6-153">Konfigurowanie Centrum powiadomień hello w przypadku usługi APNS</span><span class="sxs-lookup"><span data-stu-id="36ee6-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="36ee6-154">Następnie skonfiguruj ustawienia projektu iOS hello w programie Xamarin Studio lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36ee6-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="36ee6-155">Dodawanie aplikacji dla systemu iOS tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="36ee6-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="36ee6-156">W hello **iOS** projektu, otwórz AppDelegate.cs i Dodaj powitania po instrukcji toohello początku hello pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="36ee6-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="36ee6-157">W hello **AppDelegate** klasy, Dodaj zastąpienie hello **RegisteredForRemoteNotifications** tooregister zdarzenia dla powiadomień:</span><span class="sxs-lookup"><span data-stu-id="36ee6-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. <span data-ttu-id="36ee6-158">W **AppDelegate**, także dodać następujące zastąpienie hello hello **DidReceiveRemoteNotification** obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="36ee6-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    <span data-ttu-id="36ee6-159">Ta metoda obsługuje przychodzące powiadomienia aplikacji hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="36ee6-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="36ee6-160">W hello **AppDelegate** klasy, Dodaj hello następującego kodu toohello **FinishedLaunching** metody:</span><span class="sxs-lookup"><span data-stu-id="36ee6-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="36ee6-161">Umożliwia to obsługę zdalnego powiadomienia i żądania push rejestracji.</span><span class="sxs-lookup"><span data-stu-id="36ee6-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="36ee6-162">Aplikacja jest teraz zaktualizowane toosupport powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="36ee6-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="36ee6-163">Testowych powiadomień wypychanych w aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="36ee6-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="36ee6-164">Kliknij prawym przyciskiem myszy projekt iOS hello, a następnie kliknij przycisk **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="36ee6-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="36ee6-165">Naciśnij klawisz hello **Uruchom** przycisk lub **F5** w programie Visual Studio toobuild hello projekt i uruchomić aplikacji hello w urządzeniu z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="36ee6-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="36ee6-166">Następnie kliknij przycisk **OK** tooaccept powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="36ee6-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36ee6-167">Należy jawnie zaakceptować powiadomień wypychanych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="36ee6-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="36ee6-168">To żądanie występuje tylko hello hello aplikacja działa po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="36ee6-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="36ee6-169">W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (**+**) ikona.</span><span class="sxs-lookup"><span data-stu-id="36ee6-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="36ee6-170">Sprawdź, czy otrzyma powiadomienie, a następnie kliknij **OK** toodismiss hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="36ee6-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="36ee6-171">Konfigurowanie i uruchamianie projekty systemu Windows (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="36ee6-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="36ee6-172">Ta sekcja dotyczy uruchamiania aplikacji platformy Xamarin.Forms i WinPhone81 projektów dla urządzeń z systemem Windows hello.</span><span class="sxs-lookup"><span data-stu-id="36ee6-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="36ee6-173">Te kroki również obsługiwać projekty systemu Windows platformy Uniwersalnej.</span><span class="sxs-lookup"><span data-stu-id="36ee6-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="36ee6-174">Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="36ee6-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="36ee6-175">Rejestrowanie aplikacji systemu Windows dla powiadomień wypychanych z powiadomienia usługi WNS (Windows)</span><span class="sxs-lookup"><span data-stu-id="36ee6-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="36ee6-176">Konfigurowanie Centrum powiadomień hello przypadku usługi WNS</span><span class="sxs-lookup"><span data-stu-id="36ee6-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="36ee6-177">Dodawanie aplikacji dla systemu Windows tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="36ee6-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="36ee6-178">W programie Visual Studio Otwórz **App.xaml.cs** w systemie Windows projektu i dodaj następujące instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="36ee6-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="36ee6-179">Zastąp `<your_TodoItemManager_portable_class_namespace>` z przestrzenią nazw hello przenośne projektu zawierającego hello `TodoItemManager` klasy.</span><span class="sxs-lookup"><span data-stu-id="36ee6-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="36ee6-180">W pliku App.xaml.cs Dodaj następujące hello **InitNotificationsAsync** metody:</span><span class="sxs-lookup"><span data-stu-id="36ee6-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    <span data-ttu-id="36ee6-181">Ta metoda pobiera kanału powiadomień wypychanych hello i rejestruje powiadomienia szablonu tooreceive szablonu z Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="36ee6-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="36ee6-182">Powiadomienie szablonu, który obsługuje *messageParam* będą dostarczane toothis klienta.</span><span class="sxs-lookup"><span data-stu-id="36ee6-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="36ee6-183">W pliku App.xaml.cs aktualizacji hello **OnLaunched** definicję metody obsługi zdarzeń, dodając hello `async` modyfikator.</span><span class="sxs-lookup"><span data-stu-id="36ee6-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="36ee6-184">Następnie dodaj powitania po wiersz kodu na końcu hello metody hello:</span><span class="sxs-lookup"><span data-stu-id="36ee6-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="36ee6-185">Dzięki temu, że rejestracji powiadomień wypychanych hello jest tworzony lub odświeżyć za każdym razem, gdy aplikacja hello jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="36ee6-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="36ee6-186">Ważne jest, toodo to tooguarantee, który hello kanału wypychanych usługi WNS jest zawsze aktywna.</span><span class="sxs-lookup"><span data-stu-id="36ee6-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="36ee6-187">W Eksploratorze rozwiązań programu Visual Studio Otwórz hello **Package.appxmanifest** pliku, a następnie ustaw **wyskakujące funkcją** za**tak** w obszarze **powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="36ee6-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="36ee6-188">Tworzenie aplikacji hello i sprawdź, czy użytkownik nie ma błędów.</span><span class="sxs-lookup"><span data-stu-id="36ee6-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="36ee6-189">Twoja aplikacja kliencka powinna teraz zarejestrować hello szablonu odbieranie powiadomień z hello pewno zakończyć Mobile Apps ponownie.</span><span class="sxs-lookup"><span data-stu-id="36ee6-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="36ee6-190">W tej sekcji należy powtórzyć dla każdego projektu systemu Windows w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="36ee6-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="36ee6-191">Testowych powiadomień wypychanych w aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="36ee6-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="36ee6-192">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt dla systemu Windows, a następnie kliknij przycisk **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="36ee6-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="36ee6-193">Naciśnij klawisz hello **Uruchom** przycisk toobuild hello projekt i uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="36ee6-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="36ee6-194">W aplikacji hello, wpisz nazwę nowego zadania do wykonania, a następnie kliknij przycisk hello plus (**+**) tooadd ikonę go.</span><span class="sxs-lookup"><span data-stu-id="36ee6-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="36ee6-195">Sprawdź, czy otrzyma powiadomienie po dodaniu elementu hello.</span><span class="sxs-lookup"><span data-stu-id="36ee6-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36ee6-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36ee6-196">Next steps</span></span>
<span data-ttu-id="36ee6-197">Dodatkowe informacje na temat powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="36ee6-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="36ee6-198">Diagnozowanie problemów powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="36ee6-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="36ee6-199">Istnieją różne przyczyny, dlaczego powiadomienia mogą pobrać usunięte lub nie kończą na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="36ee6-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="36ee6-200">W tym temacie pokazano, jak tooanalyze i ustalenie potrzebnej głównego hello. Przyczyna niepowodzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="36ee6-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="36ee6-201">Można też nadal tooone hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="36ee6-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="36ee6-202">Dodaj aplikację tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="36ee6-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="36ee6-203">Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="36ee6-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="36ee6-204">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="36ee6-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="36ee6-205">Dowiedz się, jak zaplecza tooadd obsługi w trybie offline dla aplikacji przy użyciu aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="36ee6-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="36ee6-206">Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="36ee6-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
