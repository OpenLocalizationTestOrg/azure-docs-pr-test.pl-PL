---
title: aaaGet Started with Azure Mobile Engagement dla platformy Xamarin.Android
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Xamarin.Android."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="651d7-103">Rozpoczynanie pracy z usługą Azure Mobile Engagement na potrzeby aplikacji platformy Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="651d7-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="651d7-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji platformy Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="651d7-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="651d7-105">W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="651d7-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="651d7-106">W ramach tego samouczka zostanie utworzona pusta aplikacja platformy Xamarin.Android służąca do zbierania danych podstawowych i odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="651d7-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="651d7-107">Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów.</span><span class="sxs-lookup"><span data-stu-id="651d7-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="651d7-108">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="651d7-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="651d7-109">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="651d7-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="651d7-110">Program [Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="651d7-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="651d7-111">Można również użyć programu Visual Studio z platformą Xamarin, ale w tym samouczku używany jest program Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="651d7-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="651d7-112">Aby uzyskać instrukcje dotyczące instalowania, zobacz [Instalator i instalacja programu Visual Studio i platformy Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="651d7-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="651d7-113">Zestaw SDK platformy Xamarin usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="651d7-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="651d7-114">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="651d7-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="651d7-115">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="651d7-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="651d7-116">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="651d7-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="651d7-117"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="651d7-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="651d7-118"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="651d7-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="651d7-119">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="651d7-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="651d7-120">Utworzymy podstawową aplikację w programie Xamarin Studio toodemonstrate hello integracji.</span><span class="sxs-lookup"><span data-stu-id="651d7-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="651d7-121">Tworzenie nowego projektu platformy Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="651d7-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="651d7-122">Uruchom **Xamarin Studio** Przejdź zbyt**pliku** -> **nowy** -> **rozwiązania**</span><span class="sxs-lookup"><span data-stu-id="651d7-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="651d7-123">Wybierz **aplikacji systemu Android** upewnij się, jest język hello wybrane **C#** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="651d7-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="651d7-124">Wypełnij hello **Nazwa aplikacji** i hello **identyfikator organizacji**.</span><span class="sxs-lookup"><span data-stu-id="651d7-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="651d7-125">Upewnij się, że toocheckmark **usług Google Play** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="651d7-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="651d7-126">Aktualizacja hello **Nazwa projektu**, **Nazwa rozwiązania** i **lokalizacji** wymagane, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="651d7-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="651d7-127">Program Xamarin Studio zostanie utworzona aplikacja hello, w której zostanie zintegrowana usługa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="651d7-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="651d7-128">Połącz zapleczu swojej aplikacji tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="651d7-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="651d7-129">Kliknij prawym przyciskiem myszy hello **pakiety** folder w systemie windows rozwiązania hello i wybierz **Dodawanie pakietów...**</span><span class="sxs-lookup"><span data-stu-id="651d7-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="651d7-130">Wyszukaj hello **Microsoft Azure Mobile Engagement Xamarin SDK** i dodaj go tooyour rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="651d7-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="651d7-131">Otwórz **MainActivity.cs** i Dodaj hello następujące instrukcje using:</span><span class="sxs-lookup"><span data-stu-id="651d7-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="651d7-132">W hello `OnCreate` metody, Dodaj powitania po tooinitialize hello połączenia z zapleczem usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="651d7-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="651d7-133">Upewnij się, że tooadd Twojego **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="651d7-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="651d7-134">Dodawanie uprawnień i deklaracji usługi</span><span class="sxs-lookup"><span data-stu-id="651d7-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="651d7-135">Otwórz hello **Manifest.xml** plików w folderze właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="651d7-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="651d7-136">Wybierz kartę źródło, aby bezpośrednio zaktualizować źródło XML hello.</span><span class="sxs-lookup"><span data-stu-id="651d7-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="651d7-137">Dodaj te uprawnienia toohello Manifest.xml (można go znaleźć w obszarze hello **właściwości** folder) projektu bezpośrednio przed lub po hello `<application>` tagu:</span><span class="sxs-lookup"><span data-stu-id="651d7-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="651d7-138">Dodaj następujące hello między hello `<application>` i `</application>` znaczniki toodeclare hello agenta usługi:</span><span class="sxs-lookup"><span data-stu-id="651d7-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="651d7-139">W wklejonym właśnie kodzie hello, Zastąp `"<Your application name>"` hello etykiety.</span><span class="sxs-lookup"><span data-stu-id="651d7-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="651d7-140">Jest on wyświetlany w hello **ustawienia** menu, w którym użytkownicy mogą zobaczyć usługi uruchomione na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="651d7-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="651d7-141">Na przykład możesz dodać hello wyraz "Usługa" w tej etykiecie.</span><span class="sxs-lookup"><span data-stu-id="651d7-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="651d7-142">Wysyłanie ekranu tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="651d7-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="651d7-143">W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu.</span><span class="sxs-lookup"><span data-stu-id="651d7-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="651d7-144">Aby to zrobić — upewnij się, że hello `MainActivity` dziedziczy `EngagementActivity` zamiast `Activity`.</span><span class="sxs-lookup"><span data-stu-id="651d7-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="651d7-145">Alternatywnie jeśli nie możesz dziedziczyć z klasy `EngagementActivity`, musisz dodać metody `.StartActivity` i `.EndActivity` odpowiednio w `OnResume` i `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="651d7-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="651d7-146"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="651d7-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="651d7-147"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="651d7-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="651d7-148">Usługa Mobile Engagement umożliwia toointeract z i UŻYTKOWNIKAMI przy użyciu powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="651d7-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="651d7-149">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="651d7-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="651d7-150">następujące sekcje Hello konfiguruje tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="651d7-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
