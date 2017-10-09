---
title: "aaaGet pracę z usługą Notification Hubs dla aplikacji platformy Xamarin.Android | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse push tooa powiadomień aplikacji dla systemu Xamarin Android."
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
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="9b446-103">Wprowadzenie do usługi Notification Hubs dla systemu Android na platformie Xamarin</span><span class="sxs-lookup"><span data-stu-id="9b446-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="9b446-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9b446-104">Overview</span></span>
<span data-ttu-id="9b446-105">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse push aplikacji platformy Xamarin.Android tooa powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="9b446-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="9b446-106">Utworzysz pustą aplikację platformy Xamarin.Android służącą do odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="9b446-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="9b446-107">Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="9b446-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="9b446-108">Witaj gotowy kod jest dostępny w hello [aplikacji NotificationHubs] [ GitHub] próbki.</span><span class="sxs-lookup"><span data-stu-id="9b446-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="9b446-109">W tym samouczku przedstawiono hello Prosty scenariusz wysyłania przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="9b446-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9b446-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9b446-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="9b446-111">Kod ukończyć powitalnych dla tego samouczka można znaleźć w witrynie GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="9b446-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b446-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9b446-112">Prerequisites</span></span>
<span data-ttu-id="9b446-113">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="9b446-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="9b446-114">Program Visual Studio z platformą Xamarin w systemie Windows lub program Xamarin Studio w systemie Mac OS X. Kompletne instrukcje instalacji można znaleźć w temacie [Konfigurowanie i instalowanie oprogramowania Visual Studio i Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b446-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="9b446-115">Aktywne konto Google</span><span class="sxs-lookup"><span data-stu-id="9b446-115">Active Google account</span></span>
* <span data-ttu-id="9b446-116">[Składnik Azure Messaging]</span><span class="sxs-lookup"><span data-stu-id="9b446-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="9b446-117">[Składnik Google Cloud Messaging Client]</span><span class="sxs-lookup"><span data-stu-id="9b446-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="9b446-118">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji platformy Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="9b446-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b446-119">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9b446-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9b446-120">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9b446-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9b446-121">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="9b446-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="9b446-122">Włączanie usługi Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="9b446-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="9b446-123">Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="9b446-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="9b446-124">Kliknij przycisk hello <b>Konfiguruj</b> u góry hello, wprowadź hello <b>klucz interfejsu API</b> wartość uzyskaną w poprzedniej sekcji hello, a następnie kliknij przycisk <b>zapisać</b>.</span><span class="sxs-lookup"><span data-stu-id="9b446-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="9b446-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="9b446-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="9b446-126">Centrum powiadomień jest teraz skonfigurowany toowork z usługą GCM i masz tooboth ciągów połączenia hello zarejestrować swoje powiadomienia tooreceive aplikacji i toosend powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="9b446-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="9b446-127">Łączenie aplikacji toohello Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="9b446-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="9b446-128">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="9b446-128">Create a new project</span></span>
1. <span data-ttu-id="9b446-129">W programie Xamarin Studio kliknij kolejno pozycje **New Solution** (Nowe rozwiązanie), **Android App** (Aplikacja dla systemu Android) i **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="9b446-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="9b446-130">Wprowadź nazwę aplikacji w polu **App Name** i identyfikator w polu **Identifier**.</span><span class="sxs-lookup"><span data-stu-id="9b446-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="9b446-131">Kliknij przycisk hello **Platforms docelowej** toosupport a następnie kliknij przycisk **dalej** i **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b446-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="9b446-132">Spowoduje to utworzenie nowego projektu dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9b446-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="9b446-133">Otwórz właściwości projektu hello prawym przyciskiem myszy nowy projekt w widoku Solution hello i wybierając pozycję **opcje**.</span><span class="sxs-lookup"><span data-stu-id="9b446-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="9b446-134">Wybierz hello **aplikacji systemu Android** elementu hello **kompilacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="9b446-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="9b446-135">Upewnij się, że hello pierwszą literę z **nazwy pakietu** jest pisana małymi literami.</span><span class="sxs-lookup"><span data-stu-id="9b446-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9b446-136">pierwszą literę Hello hello nazwa pakietu musi być mała.</span><span class="sxs-lookup"><span data-stu-id="9b446-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="9b446-137">W przeciwnym razie podczas rejestrowania elementów **BroadcastReceiver** i **IntentFilter** dla powiadomień wypychanych w kolejnym etapie zostaną zwrócone błędy manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b446-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="9b446-138">Opcjonalnie, zestaw hello **Minimum Android wersji** tooanother poziom interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9b446-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="9b446-139">Opcjonalnie, zestaw hello **wersji docelowej Android** toohello inna wersja interfejsu API, które mają tootarget (musi być poziom interfejsu API 8 lub nowszy).</span><span class="sxs-lookup"><span data-stu-id="9b446-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="9b446-140">Kliknij przycisk **OK** i zamknij hello opcje projektu w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="9b446-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="9b446-141">Dodaj projekt tooyour wymaganych składników hello</span><span class="sxs-lookup"><span data-stu-id="9b446-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="9b446-142">Witaj Google Cloud Messaging Client dostępny w magazynie składników Xamarin hello upraszcza proces hello obsługi powiadomień wypychanych na platformie Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="9b446-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="9b446-143">Kliknij prawym przyciskiem myszy folder Components hello w aplikacji platformy Xamarin.Android i wybierz polecenie **Uzyskaj więcej składników**.</span><span class="sxs-lookup"><span data-stu-id="9b446-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="9b446-144">Wyszukaj hello **Azure Messaging** składników i dodaj go toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="9b446-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="9b446-145">Wyszukaj hello **Google Cloud Messaging Client** składników i dodaj go toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="9b446-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="9b446-146">Konfigurowanie centrów powiadomień w projekcie</span><span class="sxs-lookup"><span data-stu-id="9b446-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="9b446-147">Zbierz następujące informacje dotyczące Twojego systemu Android aplikacji i Centrum powiadomień hello:</span><span class="sxs-lookup"><span data-stu-id="9b446-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="9b446-148">**GoogleProjectNumber**: Pobierz wartość numeru projektu z przeglądu hello aplikacji na powitania Google Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="9b446-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="9b446-149">Zanotowano wcześniej tej wartości podczas tworzenia aplikacji hello na powitania portalu.</span><span class="sxs-lookup"><span data-stu-id="9b446-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="9b446-150">**Nasłuchiwanie parametry połączenia**: na pulpicie nawigacyjnym hello w hello [klasycznego portalu Azure], kliknij przycisk **Wyświetl parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="9b446-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="9b446-151">Kopiuj hello *DefaultListenSharedAccessSignature* parametry połączenia dla tej wartości.</span><span class="sxs-lookup"><span data-stu-id="9b446-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="9b446-152">**Nazwa koncentratora**: jest to nazwa hello koncentrator z hello [klasycznego portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="9b446-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="9b446-153">Na przykład *moje_centrum_powiadomien_2*.</span><span class="sxs-lookup"><span data-stu-id="9b446-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="9b446-154">Utwórz **Constants.cs** klasy w projekcie Xamarin i zdefiniuj hello następujące wartości stałych hello klasy.</span><span class="sxs-lookup"><span data-stu-id="9b446-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="9b446-155">Zastąp symbole zastępcze hello własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="9b446-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="9b446-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="9b446-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="9b446-157">}</span><span class="sxs-lookup"><span data-stu-id="9b446-157">}</span></span>
2. <span data-ttu-id="9b446-158">Dodaj następujące hello za pomocą instrukcji**MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="9b446-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="9b446-159">Dodawanie zmiennej toohello wystąpienia `MainActivity` klasy, która będzie używana tooshow okna dialogowego alertu uruchomionej aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="9b446-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="9b446-160">Utwórz następujące metody w hello hello **MainActivity** klasy:</span><span class="sxs-lookup"><span data-stu-id="9b446-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="9b446-161">W hello `OnCreate` metody **MainActivity.cs**, zainicjować hello `instance` zmienną i dodaj wywołanie za`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="9b446-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="9b446-162">Utwórz nową klasę: **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="9b446-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9b446-163">Poniżej znajdziesz instrukcje tworzenia klasy **BroadcastReceiver** krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="9b446-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="9b446-164">Jednak toomanually alternatywnych szybkie tworzenie **MyBroadcastReceiver.cs** jest toorefer toohello **GcmService.cs** plik znajdujący się w hello przykładowym projekcie platformy Xamarin.Android dołączonym hello [Przykłady NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="9b446-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="9b446-165">Duplikowanie **GcmService.cs** i zmiana nazwy klas może być również doskonałym miejscem toostart.</span><span class="sxs-lookup"><span data-stu-id="9b446-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="9b446-166">Dodaj następujące hello za pomocą instrukcji**MyBroadcastReceiver.cs** (odwołujące się toohello składnika i zestawu dodanego wcześniej):</span><span class="sxs-lookup"><span data-stu-id="9b446-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="9b446-167">W **MyBroadcastReceiver.cs**, Dodaj następujące żądania uprawnień pomiędzy hello hello **przy użyciu** instrukcje i hello **przestrzeni nazw** deklaracji:</span><span class="sxs-lookup"><span data-stu-id="9b446-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="9b446-168">W **MyBroadcastReceiver.cs**, zmień hello **MyBroadcastReceiver** toomatch hello następujące klasy:</span><span class="sxs-lookup"><span data-stu-id="9b446-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
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
10. <span data-ttu-id="9b446-169">Dodaj w pliku **MyBroadcastReceiver.cs** kolejną klasę o nazwie **PushHandlerService** pochodzącą od klasy **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="9b446-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="9b446-170">Upewnij się, że hello tooapply **usługi** toohello klasy atrybutu:</span><span class="sxs-lookup"><span data-stu-id="9b446-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="9b446-171">Klasa **GcmServiceBase** implementuje metody **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** oraz **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="9b446-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="9b446-172">Nasze **PushHandlerService** klasa implementacji musi zastępować te metody i będą uruchamiane w odpowiedzi toointeracting hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9b446-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="9b446-173">Zastąpienie hello **OnRegistered()** metody w **PushHandlerService** przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="9b446-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
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
    > <span data-ttu-id="9b446-174">W hello **OnRegistered()** kodu powyżej, należy zwrócić uwagę hello możliwości toospecify tagi tooregister dla określonych kanałów komunikacji.</span><span class="sxs-lookup"><span data-stu-id="9b446-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="9b446-175">Zastąpienie hello **OnMessage** metody w **PushHandlerService** przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="9b446-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
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
14. <span data-ttu-id="9b446-176">Dodaj następujące hello **createNotification** i **dialogNotify** metody zbyt**PushHandlerService** powiadamiania użytkowników w przypadku otrzymania powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="9b446-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9b446-177">Projekt powiadomień w systemie Android w wersji 5.0 i nowszych znacząco różni się od tego używanego we wcześniejszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="9b446-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="9b446-178">Jeśli w przypadku testowania tej funkcji w systemie Android 5.0 lub nowszej, aplikacji hello należy toobe systemem tooreceive hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9b446-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="9b446-179">Aby uzyskać więcej informacji, zobacz [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Powiadomienia w systemie Android).</span><span class="sxs-lookup"><span data-stu-id="9b446-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
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
15. <span data-ttu-id="9b446-180">Zastąp abstrakcyjne elementy członkowskie **OnUnRegistered()**, **OnRecoverableError()** i **OnError()**, aby umożliwić skompilowanie kodu:</span><span class="sxs-lookup"><span data-stu-id="9b446-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
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

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="9b446-181">Uruchom aplikację w emulatorze hello</span><span class="sxs-lookup"><span data-stu-id="9b446-181">Run your app in hello emulator</span></span>
<span data-ttu-id="9b446-182">Po uruchomieniu tej aplikacji w emulatorze hello, upewnij się, że używasz Android Virtual Device (AVD) obsługującego interfejsy API Google.</span><span class="sxs-lookup"><span data-stu-id="9b446-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b446-183">W kolejności tooreceive powiadomienia wypychane należy skonfigurować konto Google na urządzeniu Avd.</span><span class="sxs-lookup"><span data-stu-id="9b446-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="9b446-184">(W emulatorze hello Przejdź zbyt**ustawienia** i kliknij przycisk **Dodaj konto**.) Ponadto upewnij się, że emulator tego hello jest toohello połączenia internetowego.</span><span class="sxs-lookup"><span data-stu-id="9b446-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="9b446-185">Projekt powiadomień w systemie Android w wersji 5.0 i nowszych znacząco różni się od tego używanego we wcześniejszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="9b446-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="9b446-186">Aby uzyskać więcej informacji, zobacz [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Powiadomienia w systemie Android).</span><span class="sxs-lookup"><span data-stu-id="9b446-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="9b446-187">W obszarze **Narzędzia** kliknij polecenie **Open Android Emulator Manager** (Otwórz menedżera emulatora systemu Android), zaznacz urządzenie, a następnie kliknij przycisk **Edit** (Edytuj).</span><span class="sxs-lookup"><span data-stu-id="9b446-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="9b446-188">Wybierz pozycję **Google APIs** (Interfejsy API Google) w polu **Target** (Element docelowy), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b446-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="9b446-189">Na górnym pasku narzędzi powitania kliknij **Uruchom**, a następnie wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="9b446-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="9b446-190">Uruchamia hello emulatora i działa aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="9b446-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="9b446-191">Aplikacja Hello pobiera hello *registrationId* z usługi GCM i rejestruje hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="9b446-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="9b446-192">Wysyłanie powiadomień z poziomu zaplecza</span><span class="sxs-lookup"><span data-stu-id="9b446-192">Send notifications from your backend</span></span>
<span data-ttu-id="9b446-193">Możesz przetestować odbieranie powiadomień w aplikacji, wysyłając powiadomienia w hello [klasycznego portalu Azure] za pośrednictwem hello debugowania kartę na powitania Centrum powiadomień, jak pokazano na poniższym zrzucie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="9b446-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="9b446-194">Powiadomienia wypychane są zwykle wysyłane w usłudze zaplecza, takiej jak Mobile Services czy ASP.NET, za pośrednictwem zgodnej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="9b446-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="9b446-195">Umożliwia także hello interfejsu API REST bezpośrednio toosend powiadomień wiadomości, jeśli biblioteka nie jest dostępna w danym zapleczu.</span><span class="sxs-lookup"><span data-stu-id="9b446-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="9b446-196">Poniżej przedstawiono listę kilka innych samouczków, które mogą podlegać tooreview wysyłania powiadomień:</span><span class="sxs-lookup"><span data-stu-id="9b446-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="9b446-197">ASP.NET: Zobacz [toousers powiadomienia toopush użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="9b446-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="9b446-198">Azure Java centra powiadomień SDK: zobacz [jak toouse usługi Notification Hubs za pomocą języka Java](notification-hubs-java-push-notification-tutorial.md) wysyłania powiadomień za pomocą języka Java.</span><span class="sxs-lookup"><span data-stu-id="9b446-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="9b446-199">To rozwiązanie przetestowano w programie Eclipse pod kątem tworzenia aplikacji dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="9b446-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="9b446-200">PHP: Zobacz [jak toouse usługi Notification Hubs za pomocą języka PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9b446-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="9b446-201">W hello kolejnych podsekcjach samouczka hello wysyłanie powiadomień za pomocą aplikacji konsoli .NET oraz przy użyciu usługi mobilnej za pośrednictwem skryptu węzła.</span><span class="sxs-lookup"><span data-stu-id="9b446-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="9b446-202">(Opcjonalnie) Wysyłanie powiadomień za pomocą aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="9b446-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="9b446-203">W tej sekcji wyślemy powiadomienia za pomocą aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="9b446-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="9b446-204">Utwórz nową aplikację konsoli języka Visual C#:</span><span class="sxs-lookup"><span data-stu-id="9b446-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="9b446-205">W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="9b446-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="9b446-206">Spowoduje to wyświetlenie konsoli Menedżera pakietów hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b446-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="9b446-207">W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="9b446-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="9b446-208">Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="9b446-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="9b446-209">Otwórz plik Program.cs hello i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="9b446-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="9b446-210">W Twojej `Program` klasy, Dodaj następujące metody hello.</span><span class="sxs-lookup"><span data-stu-id="9b446-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="9b446-211">Zaktualizuj tekst zastępczy hello na Twojej *DefaultFullSharedAccessSignature* nazwę Centrum i parametry połączenia z hello [klasycznego portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="9b446-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="9b446-212">Dodaj hello następujące wiersze w Twojej **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="9b446-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="9b446-213">Naciśnij klawisz hello F5 klucza toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b446-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="9b446-214">Otrzymasz powiadomienie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9b446-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="9b446-215">(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu usługi mobilnej</span><span class="sxs-lookup"><span data-stu-id="9b446-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="9b446-216">Wykonaj czynności opisane w temacie [Wprowadzenie do usług Mobile Services].</span><span class="sxs-lookup"><span data-stu-id="9b446-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="9b446-217">Zaloguj się toohello [klasycznego portalu Azure]i wybierz usługę mobilną.</span><span class="sxs-lookup"><span data-stu-id="9b446-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="9b446-218">Wybierz hello **harmonogramu** kartę w górnej części hello.</span><span class="sxs-lookup"><span data-stu-id="9b446-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="9b446-219">Utwórz nowe zadanie zaplanowane, wstaw nazwę i wybierz opcję **Na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="9b446-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="9b446-220">Po utworzeniu zadania powitania kliknij nazwę zadania hello.</span><span class="sxs-lookup"><span data-stu-id="9b446-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="9b446-221">Następnie kliknij przycisk hello **skryptu** kartę na górnym pasku hello.</span><span class="sxs-lookup"><span data-stu-id="9b446-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="9b446-222">Wstaw hello następującego skryptu w funkcji harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="9b446-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="9b446-223">Wprowadź symbole zastępcze hello tooreplace się z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultFullSharedAccessSignature* uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9b446-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="9b446-224">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9b446-224">Click **Save**.</span></span>
   
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
7. <span data-ttu-id="9b446-225">Kliknij przycisk **uruchom raz** na powitania dolnym pasku.</span><span class="sxs-lookup"><span data-stu-id="9b446-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="9b446-226">W aplikacji powinno zostać odebrane wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="9b446-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b446-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b446-227">Next steps</span></span>
<span data-ttu-id="9b446-228">W tym prostym przykładzie wysłano powiadomienia tooall urządzeń z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="9b446-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="9b446-229">W kolejności tootarget określonych użytkowników, zobacz samouczek toohello [toousers powiadomienia toopush użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="9b446-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="9b446-230">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz przeczytać [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].</span><span class="sxs-lookup"><span data-stu-id="9b446-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="9b446-231">Dowiedz się więcej na temat toouse centra powiadomień w [wskazówki dotyczące usługi Notification Hubs] w hello [toofor jak usługi Notification Hubs dla systemu Android].</span><span class="sxs-lookup"><span data-stu-id="9b446-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
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
[Wprowadzenie do usług Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[klasycznego portalu Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[toofor jak usługi Notification Hubs dla systemu Android]: http://msdn.microsoft.com/library/dn282661.aspx

[toousers powiadomienia toopush użyciu usługi Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Składnik Google Cloud Messaging Client]: http://components.xamarin.com/view/GCMClient/
[Składnik Azure Messaging]: http://components.xamarin.com/view/azure-messaging
