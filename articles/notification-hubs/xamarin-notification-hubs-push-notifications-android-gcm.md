---
title: "Wprowadzenie do usługi Notification Hubs dla aplikacji platformy Xamarin.Android | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji platformy Xamarin Android przy użyciu usługi Azure Notification Hubs."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e0ef1b006a2b202c08a71caaff4ef4d763d50d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="1070b-103">Wprowadzenie do usługi Notification Hubs dla systemu Android na platformie Xamarin</span><span class="sxs-lookup"><span data-stu-id="1070b-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1070b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1070b-104">Overview</span></span>
<span data-ttu-id="1070b-105">Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji platformy Xamarin.Android przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1070b-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span>
<span data-ttu-id="1070b-106">Utworzysz pustą aplikację platformy Xamarin.Android służącą do odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="1070b-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="1070b-107">Po zakończeniu będzie można za pomocą centrum powiadomień wysyłać powiadomienia wypychane do wszystkich urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="1070b-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="1070b-108">Gotowy kod jest dostępny w przykładowej aplikacji [NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="1070b-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="1070b-109">W tym samouczku został omówiony prosty scenariusz wysyłania przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1070b-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1070b-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1070b-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="1070b-111">Kompletny kod dla tego samouczka można znaleźć w witrynie GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="1070b-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1070b-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1070b-112">Prerequisites</span></span>
<span data-ttu-id="1070b-113">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1070b-113">This tutorial requires the following:</span></span>

* <span data-ttu-id="1070b-114">Program Visual Studio z platformą Xamarin w systemie Windows lub program Xamarin Studio w systemie Mac OS X. Kompletne instrukcje instalacji można znaleźć w temacie [Konfigurowanie i instalowanie oprogramowania Visual Studio i Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="1070b-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="1070b-115">Aktywne konto Google</span><span class="sxs-lookup"><span data-stu-id="1070b-115">Active Google account</span></span>
* <span data-ttu-id="1070b-116">[Składnik Azure Messaging]</span><span class="sxs-lookup"><span data-stu-id="1070b-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="1070b-117">[Składnik Google Cloud Messaging Client]</span><span class="sxs-lookup"><span data-stu-id="1070b-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="1070b-118">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji platformy Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="1070b-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1070b-119">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1070b-119">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1070b-120">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1070b-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1070b-121">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="1070b-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="1070b-122">Włączanie usługi Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="1070b-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="1070b-123">Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="1070b-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="1070b-124">Kliknij kartę <b>Konfiguracja</b> w górnej części ekranu, wprowadź wartość <b>Klucz interfejsu API</b> uzyskaną w poprzedniej sekcji, a następnie kliknij pozycję <b>Zapisz</b>.</span><span class="sxs-lookup"><span data-stu-id="1070b-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="1070b-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="1070b-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="1070b-126">Centrum powiadomień jest teraz skonfigurowane do pracy z usługą GCM i uzyskano parametry połączenia do rejestrowania aplikacji zarówno w celu odbierania, jak i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1070b-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="1070b-127">Łączenie aplikacji z centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="1070b-127">Connect your app to the notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="1070b-128">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="1070b-128">Create a new project</span></span>
1. <span data-ttu-id="1070b-129">W programie Xamarin Studio kliknij kolejno pozycje **New Solution** (Nowe rozwiązanie), **Android App** (Aplikacja dla systemu Android) i **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="1070b-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="1070b-130">Wprowadź nazwę aplikacji w polu **App Name** i identyfikator w polu **Identifier**.</span><span class="sxs-lookup"><span data-stu-id="1070b-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="1070b-131">W obszarze **Target Platforms** (Platformy docelowe) kliknij platformy, które mają być obsługiwane, a następnie kliknij kolejno pozycje **Next** (Dalej) i **Create** (Utwórz).</span><span class="sxs-lookup"><span data-stu-id="1070b-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="1070b-132">Spowoduje to utworzenie nowego projektu dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="1070b-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="1070b-133">Otwórz właściwości projektu, klikając utworzony projekt prawym przyciskiem myszy w widoku Solution (Rozwiązanie) i wybierając pozycję **Options** (Opcje).</span><span class="sxs-lookup"><span data-stu-id="1070b-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span></span> <span data-ttu-id="1070b-134">Wybierz pozycję **Android Application** (Aplikacja dla systemu Android) w sekcji **Build** (Kompilacja).</span><span class="sxs-lookup"><span data-stu-id="1070b-134">Select the **Android Application** item in the **Build** section.</span></span>
   
    <span data-ttu-id="1070b-135">Upewnij się, że pierwsza litera w polu **Package name** (Nazwa pakietu) jest mała.</span><span class="sxs-lookup"><span data-stu-id="1070b-135">Ensure that the first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="1070b-136">Nazwa pakietu musi zaczynać się od małej litery.</span><span class="sxs-lookup"><span data-stu-id="1070b-136">The first letter of the package name must be lowercase.</span></span> <span data-ttu-id="1070b-137">W przeciwnym razie podczas rejestrowania elementów **BroadcastReceiver** i **IntentFilter** dla powiadomień wypychanych w kolejnym etapie zostaną zwrócone błędy manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1070b-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="1070b-138">Opcjonalnie możesz ustawić wartość w polu **Minimum Android version** (Minimalna wersja systemu Android) na inny poziom interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1070b-138">Optionally, set the **Minimum Android version** to another API Level.</span></span>
3. <span data-ttu-id="1070b-139">Opcjonalnie możesz ustawić wartość w polu **Target Android version** (Docelowa wersja systemu Android) na inną docelową wersję interfejsu API (wymagany poziom 8 lub wyższy).</span><span class="sxs-lookup"><span data-stu-id="1070b-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span></span>

<span data-ttu-id="1070b-140">Kliknij przycisk **OK** i zamknij okno dialogowe Project Options (Opcje projektu).</span><span class="sxs-lookup"><span data-stu-id="1070b-140">Click **OK** and close the Project Options dialog.</span></span>

### <a name="add-the-required-components-to-your-project"></a><span data-ttu-id="1070b-141">Dodawanie wymaganych składników do projektu</span><span class="sxs-lookup"><span data-stu-id="1070b-141">Add the required components to your project</span></span>
<span data-ttu-id="1070b-142">Składnik Google Cloud Messaging Client dostępny w magazynie składników Xamarin Component Store upraszcza proces obsługi powiadomień wypychanych na platformie Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="1070b-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="1070b-143">Kliknij prawym przyciskiem myszy folder Components (Składniki) w aplikacji platformy Xamarin.Android i wybierz polecenie **Get More Components** (Uzyskaj więcej składników).</span><span class="sxs-lookup"><span data-stu-id="1070b-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="1070b-144">Wyszukaj składnik **Azure Messaging** i dodaj go do projektu.</span><span class="sxs-lookup"><span data-stu-id="1070b-144">Search for the **Azure Messaging** component and add it to the project.</span></span>
3. <span data-ttu-id="1070b-145">Wyszukaj składnik **Google Cloud Messaging Client** i dodaj go do projektu.</span><span class="sxs-lookup"><span data-stu-id="1070b-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="1070b-146">Konfigurowanie centrów powiadomień w projekcie</span><span class="sxs-lookup"><span data-stu-id="1070b-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="1070b-147">Zbierz następujące informacje dotyczące aplikacji dla systemu Android i centrum powiadomień:</span><span class="sxs-lookup"><span data-stu-id="1070b-147">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="1070b-148">**GoogleProjectNumber**: wartość numeru projektu, którą znajdziesz na stronie przeglądu swojej aplikacji w portalu Google Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="1070b-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span></span> <span data-ttu-id="1070b-149">Tę wartość zanotowano wcześniej — po utworzeniu aplikacji w portalu.</span><span class="sxs-lookup"><span data-stu-id="1070b-149">You made a note of this value earlier when you created the app on the portal.</span></span>
   * <span data-ttu-id="1070b-150">**Listen connection string**: na pulpicie nawigacyjnym w [klasyczny portal Azure] kliknij pozycję **Wyświetl parametry połączeń**.</span><span class="sxs-lookup"><span data-stu-id="1070b-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="1070b-151">Skopiuj parametr połączenia *DefaultListenSharedAccessSignature* dla tej wartości.</span><span class="sxs-lookup"><span data-stu-id="1070b-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="1070b-152">**Hub name**: nazwa centrum wprowadzona w [klasyczny portal Azure].</span><span class="sxs-lookup"><span data-stu-id="1070b-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span></span> <span data-ttu-id="1070b-153">Na przykład *moje_centrum_powiadomien_2*.</span><span class="sxs-lookup"><span data-stu-id="1070b-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="1070b-154">Utwórz klasę **Constants.cs** w projekcie Xamarin i zdefiniuj w tej klasie następujące wartości stałych.</span><span class="sxs-lookup"><span data-stu-id="1070b-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="1070b-155">Zastąp tekst zastępczy własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="1070b-155">Replace the placeholders with your values.</span></span>
     
       <span data-ttu-id="1070b-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="1070b-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="1070b-157">}</span><span class="sxs-lookup"><span data-stu-id="1070b-157">}</span></span>
2. <span data-ttu-id="1070b-158">W pliku **MainActivity.cs** dodaj następujące instrukcje using:</span><span class="sxs-lookup"><span data-stu-id="1070b-158">Add the following using statements to **MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="1070b-159">Dodaj do klasy `MainActivity` zmienną instance w celu wyświetlania okna dialogowego alertu podczas działania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="1070b-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="1070b-160">Utwórz następującą metodę w klasie **MainActivity**:</span><span class="sxs-lookup"><span data-stu-id="1070b-160">Create the following method in the **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="1070b-161">W ramach metody `OnCreate` w pliku **MainActivity.cs** zainicjuj zmienną `instance` i dodaj wywołanie `RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="1070b-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from the "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="1070b-162">Utwórz nową klasę: **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="1070b-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1070b-163">Poniżej znajdziesz instrukcje tworzenia klasy **BroadcastReceiver** krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="1070b-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="1070b-164">Szybszą alternatywą dla ręcznego tworzenia pliku **MyBroadcastReceiver.cs** jest skorzystanie z pliku **GcmService.cs**, który można znaleźć w przykładowym projekcie platformy Xamarin.Android dołączonym do [przykładów aplikacji NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="1070b-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="1070b-165">Dobrym sposobem na rozpoczęcie może być też zduplikowanie pliku **GcmService.cs** i zmiana nazw klas.</span><span class="sxs-lookup"><span data-stu-id="1070b-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span></span>
   > 
   > 
7. <span data-ttu-id="1070b-166">Dodaj następujące instrukcje using do pliku **MyBroadcastReceiver.cs** (odwołujące się do dodanego wcześniej składnika i zestawu):</span><span class="sxs-lookup"><span data-stu-id="1070b-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="1070b-167">W pliku **MyBroadcastReceiver.cs** dodaj następujące żądania uprawnień pomiędzy instrukcjami **using** a deklaracją **namespace**:</span><span class="sxs-lookup"><span data-stu-id="1070b-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="1070b-168">W pliku **MyBroadcastReceiver.cs** zmień klasę **MyBroadcastReceiver** zgodnie z poniższym kodem:</span><span class="sxs-lookup"><span data-stu-id="1070b-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="1070b-169">Dodaj w pliku **MyBroadcastReceiver.cs** kolejną klasę o nazwie **PushHandlerService** pochodzącą od klasy **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="1070b-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="1070b-170">Pamiętaj o zastosowaniu do klasy atrybutu **Service**:</span><span class="sxs-lookup"><span data-stu-id="1070b-170">Make sure to apply the **Service** attribute to the class:</span></span>
    
         [Service] // Must use the service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="1070b-171">Klasa **GcmServiceBase** implementuje metody **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** oraz **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="1070b-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="1070b-172">Klasa implementacji **PushHandlerService** musi zastępować te metody, które będą uruchamiane w odpowiedzi na interakcję z centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1070b-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span></span>
12. <span data-ttu-id="1070b-173">Zastąp metodę **OnRegistered()** w klasie **PushHandlerService**, używając następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="1070b-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "The device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="1070b-174">W ramach powyższego kodu metody **OnRegistered()** zwróć uwagę na możliwość określenia tagów do rejestracji dla określonych kanałów komunikacji.</span><span class="sxs-lookup"><span data-stu-id="1070b-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="1070b-175">Zastąp metodę **OnMessage** w klasie **PushHandlerService**, używając następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="1070b-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="1070b-176">Dodaj następujące metody **createNotification** i **dialogNotify** do klasy **PushHandlerService** w celu powiadomienia użytkowników w przypadku otrzymania powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="1070b-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="1070b-177">Projekt powiadomień w systemie Android w wersji 5.0 i nowszych znacząco różni się od tego używanego we wcześniejszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="1070b-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="1070b-178">W przypadku testowania tej funkcji w systemie Android 5.0 lub nowszym otrzymanie powiadomienia będzie wymagało uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1070b-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span></span> <span data-ttu-id="1070b-179">Aby uzyskać więcej informacji, zobacz [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Powiadomienia w systemie Android).</span><span class="sxs-lookup"><span data-stu-id="1070b-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent to show UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create the notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove the notification once the user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set the notification info
            //we use the pending intent, passing our ui intent over, which will get called
            //when the notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show the notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="1070b-180">Zastąp abstrakcyjne elementy członkowskie **OnUnRegistered()**, **OnRecoverableError()** i **OnError()**, aby umożliwić skompilowanie kodu:</span><span class="sxs-lookup"><span data-stu-id="1070b-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "The device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-the-emulator"></a><span data-ttu-id="1070b-181">Uruchamianie aplikacji w emulatorze</span><span class="sxs-lookup"><span data-stu-id="1070b-181">Run your app in the emulator</span></span>
<span data-ttu-id="1070b-182">W przypadku uruchamiania aplikacji w emulatorze upewnij się, że korzystasz z urządzenia wirtualnego systemu Android (Android Virtual Device, AVD) obsługującego interfejsy API Google.</span><span class="sxs-lookup"><span data-stu-id="1070b-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1070b-183">Aby otrzymywać powiadomienia wypychane, należy skonfigurować konto Google na urządzeniu AVD.</span><span class="sxs-lookup"><span data-stu-id="1070b-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="1070b-184">W tym celu w emulatorze przejdź do pozycji **Settings** (Ustawienia) i kliknij polecenie **Add Account** (Dodaj konto). Upewnij się też, że emulator ma połączenie z Internetem.</span><span class="sxs-lookup"><span data-stu-id="1070b-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="1070b-185">Projekt powiadomień w systemie Android w wersji 5.0 i nowszych znacząco różni się od tego używanego we wcześniejszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="1070b-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="1070b-186">Aby uzyskać więcej informacji, zobacz [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Powiadomienia w systemie Android).</span><span class="sxs-lookup"><span data-stu-id="1070b-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="1070b-187">W obszarze **Narzędzia** kliknij polecenie **Open Android Emulator Manager** (Otwórz menedżera emulatora systemu Android), zaznacz urządzenie, a następnie kliknij przycisk **Edit** (Edytuj).</span><span class="sxs-lookup"><span data-stu-id="1070b-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="1070b-188">Wybierz pozycję **Google APIs** (Interfejsy API Google) w polu **Target** (Element docelowy), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1070b-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="1070b-189">Na górnym pasku narzędzi kliknij pozycję **Run** (Uruchom), a następnie wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="1070b-189">On the top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="1070b-190">Spowoduje to uruchomienie emulatora i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1070b-190">This starts the emulator and runs the app.</span></span>
   
   <span data-ttu-id="1070b-191">Aplikacja pobiera wartość *registrationId* z usługi GCM i rejestruje się w centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="1070b-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="1070b-192">Wysyłanie powiadomień z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="1070b-192">Send notifications from your backend</span></span>
<span data-ttu-id="1070b-193">Odbieranie powiadomień w aplikacji możesz przetestować, wysyłając powiadomienia w [klasyczny portal Azure] za pomocą karty Debugowanie w centrum powiadomień, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="1070b-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span></span>

![][30]

<span data-ttu-id="1070b-194">Powiadomienia wypychane są zwykle wysyłane w usłudze zaplecza, takiej jak Mobile Services czy ASP.NET, za pośrednictwem zgodnej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="1070b-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="1070b-195">Można również wysyłać powiadomienia bezpośrednio za pomocą interfejsu API REST, jeśli biblioteka nie jest dostępna w danym zapleczu.</span><span class="sxs-lookup"><span data-stu-id="1070b-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="1070b-196">Poniższa lista zawiera kilka innych samouczków, z którymi warto się zapoznać, planując wysyłanie powiadomień:</span><span class="sxs-lookup"><span data-stu-id="1070b-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span></span>

* <span data-ttu-id="1070b-197">ASP.NET: zobacz [Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1070b-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span></span>
* <span data-ttu-id="1070b-198">Zestaw SDK Java usługi Azure Notification Hubs: zobacz [Jak używać usługi Notification Hubs za pomocą języka Java](notification-hubs-java-push-notification-tutorial.md), aby zapoznać się ze sposobem wysyłania powiadomień za pomocą języka Java.</span><span class="sxs-lookup"><span data-stu-id="1070b-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="1070b-199">To rozwiązanie przetestowano w programie Eclipse do tworzenia aplikacji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="1070b-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="1070b-200">PHP: zobacz [Jak używać usługi Notification Hubs za pomocą języka PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1070b-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="1070b-201">W kolejnych podsekcjach samouczka wyślesz powiadomienia przy użyciu aplikacji konsoli .NET oraz przy użyciu usługi mobilnej za pośrednictwem skryptu węzła.</span><span class="sxs-lookup"><span data-stu-id="1070b-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="1070b-202">(Opcjonalnie) Wysyłanie powiadomień za pomocą aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="1070b-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="1070b-203">W tej sekcji wyślemy powiadomienia za pomocą aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="1070b-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="1070b-204">Utwórz nową aplikację konsoli języka Visual C#:</span><span class="sxs-lookup"><span data-stu-id="1070b-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="1070b-205">W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="1070b-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="1070b-206">Spowoduje to wyświetlenie Konsoli menedżera pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1070b-206">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="1070b-207">W oknie Konsola menedżera pakietów ustaw nowy projekt aplikacji konsoli jako **Projekt domyślny**, a następnie w oknie konsoli uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1070b-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="1070b-208">Spowoduje to dodanie odwołania do zestawu SDK usługi Azure Notification Hubs z użyciem <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="1070b-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="1070b-209">Otwórz plik Program.cs i dodaj następującą instrukcję `using`:</span><span class="sxs-lookup"><span data-stu-id="1070b-209">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="1070b-210">Dodaj następującą metodę w klasie `Program`.</span><span class="sxs-lookup"><span data-stu-id="1070b-210">In your `Program` class, add the following method.</span></span> <span data-ttu-id="1070b-211">Zmień tekst zastępczy na parametry połączenia *DefaultFullSharedAccessSignature* i nazwę centrum z [klasyczny portal Azure].</span><span class="sxs-lookup"><span data-stu-id="1070b-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="1070b-212">Dodaj następujące wiersze do metody **Main**:</span><span class="sxs-lookup"><span data-stu-id="1070b-212">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="1070b-213">Naciśnij klawisz F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1070b-213">Press the F5 key to run the app.</span></span> <span data-ttu-id="1070b-214">W aplikacji powinno zostać odebrane powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="1070b-214">You should receive a notification in the app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="1070b-215">(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu usługi mobilnej</span><span class="sxs-lookup"><span data-stu-id="1070b-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="1070b-216">Wykonaj czynności opisane w temacie [Wprowadzenie do usług Mobile Services].</span><span class="sxs-lookup"><span data-stu-id="1070b-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="1070b-217">Zaloguj się do [klasyczny portal Azure] i wybierz usługę mobilną.</span><span class="sxs-lookup"><span data-stu-id="1070b-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="1070b-218">Wybierz kartę **Harmonogram** na górnym pasku.</span><span class="sxs-lookup"><span data-stu-id="1070b-218">Select the **Scheduler** tab on the top.</span></span>
   
      ![][22]
4. <span data-ttu-id="1070b-219">Utwórz nowe zadanie zaplanowane, wstaw nazwę i wybierz opcję **Na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="1070b-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="1070b-220">Po utworzeniu zadania kliknij jego nazwę.</span><span class="sxs-lookup"><span data-stu-id="1070b-220">When the job is created, click the job name.</span></span> <span data-ttu-id="1070b-221">Następnie kliknij kartę **Skrypt** na górnym pasku.</span><span class="sxs-lookup"><span data-stu-id="1070b-221">Then click the **Script** tab on the top bar.</span></span>
6. <span data-ttu-id="1070b-222">Wstaw następujący skrypt w funkcji harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="1070b-222">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="1070b-223">Pamiętaj o zastąpieniu tekstu zastępczego uzyskanymi wcześniej wartościami: nazwą centrum powiadomień i parametrami połączenia *DefaultFullSharedAccessSignature*.</span><span class="sxs-lookup"><span data-stu-id="1070b-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="1070b-224">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1070b-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="1070b-225">Kliknij pozycję **Uruchom raz** na dolnym pasku.</span><span class="sxs-lookup"><span data-stu-id="1070b-225">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="1070b-226">W aplikacji powinno zostać odebrane wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="1070b-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1070b-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1070b-227">Next steps</span></span>
<span data-ttu-id="1070b-228">W tym prostym przykładzie wysłano powiadomienia do wszystkich urządzeń z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="1070b-228">In this simple example, you broadcasted notifications to all your Android devices.</span></span> <span data-ttu-id="1070b-229">Aby skierować je do określonych użytkowników, zapoznaj się z samouczkiem [Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1070b-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="1070b-230">Jeśli chcesz podzielić użytkowników na grupy zainteresowań, zobacz [Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1070b-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="1070b-231">Aby uzyskać więcej informacji na temat korzystania z usługi Notification Hubs, zobacz [Wskazówki dotyczące usługi Notification Hubs] oraz [Poradnik dotyczący usługi Notification Hubs dla systemu Android].</span><span class="sxs-lookup"><span data-stu-id="1070b-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="1070b-232">[Wprowadzenie do usług Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span><span class="sxs-lookup"><span data-stu-id="1070b-232">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span></span>
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

<span data-ttu-id="1070b-233">[klasyczny portal Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="1070b-233">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
<span data-ttu-id="1070b-234">[Wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="1070b-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="1070b-235">[Poradnik dotyczący usługi Notification Hubs dla systemu Android]: http://msdn.microsoft.com/library/dn282661.aspx</span><span class="sxs-lookup"><span data-stu-id="1070b-235">[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx</span></span>

<span data-ttu-id="1070b-236">[Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="1070b-236">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="1070b-237">[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="1070b-237">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="1070b-238">[Składnik Google Cloud Messaging Client]: http://components.xamarin.com/view/GCMClient/</span><span class="sxs-lookup"><span data-stu-id="1070b-238">[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/</span></span>
<span data-ttu-id="1070b-239">[Składnik Azure Messaging]: http://components.xamarin.com/view/azure-messaging</span><span class="sxs-lookup"><span data-stu-id="1070b-239">[Azure Messaging Component]: http://components.xamarin.com/view/azure-messaging</span></span>
