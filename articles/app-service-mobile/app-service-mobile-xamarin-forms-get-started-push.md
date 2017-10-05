---
title: "Dodawanie powiadomień wypychanych do aplikacji platformy Xamarin.Forms | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysyłać powiadomienia wypychane obejmującego wiele platform do aplikacji platformy Xamarin.Forms przy użyciu usług Azure."
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
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="1bdc1-103">Dodawanie powiadomień wypychanych do aplikacji platformy Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="1bdc1-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="1bdc1-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1bdc1-104">Overview</span></span>
<span data-ttu-id="1bdc1-105">W tym samouczku, dodawanie powiadomień wypychanych do projektów, które powstały w wyniku [szybki start platformy Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1bdc1-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="1bdc1-106">Oznacza to, że powiadomienie wypychane zostanie wysłane do wszystkich klientów i platform, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="1bdc1-107">Jeśli nie używasz Projekt serwera pobrany szybki start, konieczne będzie pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="1bdc1-108">Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1bdc1-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bdc1-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1bdc1-109">Prerequisites</span></span>
<span data-ttu-id="1bdc1-110">Dla systemu iOS, konieczne będzie [członkostwo w programie dla deweloperów firmy Apple](https://developer.apple.com/programs/ios/) i urządzenie fizyczne z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="1bdc1-111">[Symulatora systemu iOS nie obsługuje powiadomień wypychanych](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="1bdc1-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="1bdc1-112"><a name="configure-hub"></a>Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="1bdc1-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="1bdc1-113">Aktualizowanie projektów serwera do wysyłania powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="1bdc1-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="1bdc1-114">Konfigurowanie i uruchamianie projektu systemu Android (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="1bdc1-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="1bdc1-115">Wykonaj tę sekcję, aby włączyć powiadomień wypychanych dla projektu platformy Xamarin.Forms Droid dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="1bdc1-116">Włącz Firebase Cloud Messaging (FCM)</span><span class="sxs-lookup"><span data-stu-id="1bdc1-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="1bdc1-117">Konfigurowanie zaplecza aplikacji mobilnej do wysyłania żądań wypychanych przy użyciu FCM</span><span class="sxs-lookup"><span data-stu-id="1bdc1-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="1bdc1-118">Dodawanie powiadomień wypychanych do projektu systemu Android</span><span class="sxs-lookup"><span data-stu-id="1bdc1-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="1bdc1-119">Na zapleczu skonfigurowano FCM można dodać składniki i kody klienta do rejestracji w usłudze FCM.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="1bdc1-120">Można również zarejestrować dla powiadomień wypychanych przy użyciu usługi Azure Notification Hubs przy użyciu zaplecza aplikacji mobilnych i otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="1bdc1-121">W **Droid** projektu, kliknij prawym przyciskiem myszy **składniki** folder, a następnie kliknij przycisk **Uzyskaj więcej składników...** .</span><span class="sxs-lookup"><span data-stu-id="1bdc1-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="1bdc1-122">Następnie wyszukaj **Google Cloud Messaging Client** składników i dodaj go do projektu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="1bdc1-123">Ten składnik obsługuje powiadomień wypychanych dla projektu dla systemu Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="1bdc1-124">Otwórz plik projektu MainActivity.cs i dodaj następującą instrukcję u góry pliku:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="1bdc1-125">Dodaj następujący kod do **OnCreate** metody po wywołaniu **LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="1bdc1-126">Dodaj nową **CreateAndShowDialog** metody pomocnika, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="1bdc1-127">Dodaj następujący kod do **MainActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="1bdc1-128">Udostępnia to bieżącego **MainActivity** wystąpienie, dlatego można wykonać w głównym wątku interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="1bdc1-129">Inicjowanie `instance` zmiennej na początku **OnCreate** metody, w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="1bdc1-130">Dodaj nowy plik klasy **Droid** projektu o nazwie `GcmService.cs`i upewnij się, że następujące **przy użyciu** instrukcje znajdują się w górnej części pliku:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

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
8. <span data-ttu-id="1bdc1-131">Dodaj następujące żądania uprawnień w górnej części pliku, po **przy użyciu** instrukcje i przed **przestrzeni nazw** deklaracji.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="1bdc1-132">Dodaj następującą definicję klasy do przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="1bdc1-133">Zastąp **< PROJECT_NUMBER >** wcześniej zapisany numer projektu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="1bdc1-134">Zamień wszystkie puste **GcmService** klasy z następującym kodem, który używa nowego odbiornika emisji:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="1bdc1-135">Dodaj następujący kod do **GcmService** klasy.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="1bdc1-136">Przesłania **OnRegistered** obsługi zdarzeń i implementuje **zarejestrować** metody.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="1bdc1-137">Należy pamiętać, że ten kod zawiera `messageParam` parametru w rejestracji szablonu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="1bdc1-138">Dodaj następujący kod, który implementuje **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
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

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="1bdc1-139">Obsługuje przychodzące powiadomienia i wysyła je do Menedżera powiadomień, który będzie wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="1bdc1-140">**GcmServiceBase** wymaga również implementować **OnUnRegistered** i **OnError** metody obsługi, które można wykonać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="1bdc1-141">Teraz wszystko jest gotowe testowych powiadomień wypychanych w aplikacji uruchomionych na urządzeniu z systemem Android lub emulator.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="1bdc1-142">Testowych powiadomień wypychanych w aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="1bdc1-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="1bdc1-143">Pierwsze dwa kroki są wymagane tylko wtedy, gdy w przypadku testowania emulatora.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="1bdc1-144">Upewnij się, że wdrażania lub debugowanie na urządzeniu wirtualnym, który ma ustawioną jako docelową, interfejsy API Google, jak pokazano poniżej, w Menedżerze urządzeń wirtualnych systemu Android.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="1bdc1-145">Dodaj konto Google na urządzeniu z systemem Android, klikając **aplikacje** > **ustawienia** > **Dodaj konto**.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="1bdc1-146">Następnie postępuj zgodnie z monitami dodanie istniejącego konta Google na urządzeniu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="1bdc1-147">W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy **Droid** projekt i kliknij przycisk **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="1bdc1-148">Kliknij przycisk **Uruchom** Aby skompilować projekt i uruchomić aplikację na urządzeniu z systemem Android lub w emulatorze.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="1bdc1-149">W aplikacji wpisz zadania, a następnie kliknij przycisk plus (**+**) ikona.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="1bdc1-150">Sprawdź, czy otrzyma powiadomienie po dodaniu elementu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="1bdc1-151">Konfigurowanie i uruchamianie projektu iOS (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="1bdc1-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="1bdc1-152">Ta sekcja dotyczy uruchamiania projektu Xamarin iOS dla urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="1bdc1-153">Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="1bdc1-154">Konfigurowanie Centrum powiadomień dla usługi APNS</span><span class="sxs-lookup"><span data-stu-id="1bdc1-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="1bdc1-155">Następnie skonfiguruj ustawienia projektu dla systemu iOS w programie Xamarin Studio lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="1bdc1-156">Dodawanie powiadomień wypychanych do aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="1bdc1-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="1bdc1-157">W **iOS** projektu, otwórz AppDelegate.cs i dodaj następującą instrukcję na początku pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="1bdc1-158">W **AppDelegate** klasy, Dodaj zastąpienie **RegisteredForRemoteNotifications** zdarzenia do zarejestrowania dla powiadomień:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

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
3. <span data-ttu-id="1bdc1-159">W **AppDelegate**, także dodać następujące zastąpienie dla **DidReceiveRemoteNotification** obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="1bdc1-160">Ta metoda obsługuje przychodzące powiadomienia, gdy aplikacja jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="1bdc1-161">W **AppDelegate** klasy, Dodaj następujący kod, aby **FinishedLaunching** metody:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="1bdc1-162">Umożliwia to obsługę zdalnego powiadomienia i żądania push rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="1bdc1-163">Aplikacja jest teraz zaktualizowana do obsługi powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="1bdc1-164">Testowych powiadomień wypychanych w aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="1bdc1-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="1bdc1-165">Kliknij prawym przyciskiem myszy projekt iOS, a następnie kliknij przycisk **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="1bdc1-166">Naciśnij klawisz **Uruchom** przycisk lub **F5** w Visual Studio, aby skompilować projekt i uruchomić aplikację w urządzeniu z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="1bdc1-167">Następnie kliknij przycisk **OK** do akceptowania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1bdc1-168">Należy jawnie zaakceptować powiadomień wypychanych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="1bdc1-169">To żądanie występuje tylko aplikacja jest uruchamiana po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="1bdc1-170">W aplikacji wpisz zadania, a następnie kliknij przycisk plus (**+**) ikona.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="1bdc1-171">Sprawdź, czy otrzyma powiadomienie, a następnie kliknij **OK** na odrzucenie powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="1bdc1-172">Konfigurowanie i uruchamianie projekty systemu Windows (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="1bdc1-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="1bdc1-173">Ta sekcja dotyczy uruchamiania aplikacji platformy Xamarin.Forms i WinPhone81 projektów dla urządzeń z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="1bdc1-174">Te kroki również obsługiwać projekty systemu Windows platformy Uniwersalnej.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="1bdc1-175">Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="1bdc1-176">Rejestrowanie aplikacji systemu Windows dla powiadomień wypychanych z powiadomienia usługi WNS (Windows)</span><span class="sxs-lookup"><span data-stu-id="1bdc1-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="1bdc1-177">Konfigurowanie Centrum powiadomień w przypadku usługi WNS</span><span class="sxs-lookup"><span data-stu-id="1bdc1-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="1bdc1-178">Dodawanie powiadomień wypychanych do aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1bdc1-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="1bdc1-179">W programie Visual Studio Otwórz **App.xaml.cs** w systemie Windows projektu i dodaj następujące instrukcje.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="1bdc1-180">Zastąp `<your_TodoItemManager_portable_class_namespace>` z przestrzenią nazw przenośne projektu zawierającego `TodoItemManager` klasy.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="1bdc1-181">W pliku App.xaml.cs Dodaj następujące **InitNotificationsAsync** metody:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="1bdc1-182">Ta metoda pobiera kanału powiadomień wypychanych i rejestruje szablonu, aby otrzymywać powiadomienia szablonu z Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="1bdc1-183">Powiadomienie szablonu, który obsługuje *messageParam* będą dostarczane do tego klienta.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="1bdc1-184">W pliku App.xaml.cs aktualizacji **OnLaunched** definicję metody obsługi zdarzeń, dodając `async` modyfikator.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="1bdc1-185">Następnie dodaj następujący wiersz kodu na końcu metody:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="1bdc1-186">Dzięki temu, że rejestracji powiadomień wypychanych jest tworzony lub odświeżyć za każdym razem, gdy aplikacja jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="1bdc1-187">Należy to zrobić, aby zagwarantować kanału wypychanych usługi WNS jest zawsze aktywna.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="1bdc1-188">Otwórz w Eksploratorze rozwiązań programu Visual Studio, **Package.appxmanifest** pliku, a następnie ustaw **wyskakujące funkcją** do **tak** w obszarze **powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="1bdc1-189">Tworzenie aplikacji i sprawdź, czy użytkownik nie ma błędów.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="1bdc1-190">Twoja aplikacja kliencka powinna teraz rejestrować się dla szablonu powiadomień z zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="1bdc1-191">W tej sekcji należy powtórzyć dla każdego projektu systemu Windows w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="1bdc1-192">Testowych powiadomień wypychanych w aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1bdc1-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="1bdc1-193">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt dla systemu Windows, a następnie kliknij przycisk **Ustaw jako projekt startowy**.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="1bdc1-194">Kliknij przycisk **Uruchom**, aby skompilować projekt i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="1bdc1-195">W aplikacji wpisz nazwę nowego zadania do wykonania, a następnie kliknij przycisk plus (**+**) ikonę, aby dodać go.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="1bdc1-196">Sprawdź, czy otrzyma powiadomienie po dodaniu elementu.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bdc1-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1bdc1-197">Next steps</span></span>
<span data-ttu-id="1bdc1-198">Dodatkowe informacje na temat powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="1bdc1-199">Diagnozowanie problemów powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="1bdc1-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="1bdc1-200">Istnieją różne przyczyny, dlaczego powiadomienia mogą pobrać usunięte lub nie kończą na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="1bdc1-201">W tym temacie przedstawiono sposób analizowania i ustalić główną przyczynę niepowodzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="1bdc1-202">Możesz również na jedno z następujących samouczków:</span><span class="sxs-lookup"><span data-stu-id="1bdc1-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="1bdc1-203">Dodawanie uwierzytelniania do aplikacji</span><span class="sxs-lookup"><span data-stu-id="1bdc1-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="1bdc1-204">Dowiedz się, jak uwierzytelniać użytkowników aplikacji przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="1bdc1-205">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="1bdc1-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="1bdc1-206">Dowiedz się, jak dodać obsługę aplikacji w trybie offline przy użyciu zaplecza funkcji Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="1bdc1-207">Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="1bdc1-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
