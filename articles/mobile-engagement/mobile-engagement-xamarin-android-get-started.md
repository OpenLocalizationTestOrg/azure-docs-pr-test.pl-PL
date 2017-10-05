---
title: "Wprowadzenie do usługi Azure Mobile Engagement na potrzeby platformy Xamarin.Android"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami wypychanymi na potrzeby aplikacji platformy Xamarin.Android."
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
ms.openlocfilehash: 7b3d01b32c2d5a40448fc22861cd45f612238f2f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="d0196-103">Rozpoczynanie pracy z usługą Azure Mobile Engagement na potrzeby aplikacji platformy Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="d0196-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d0196-104">W tym temacie pokazano, jak za pomocą usługi Azure Mobile Engagement można określić sposób użycia aplikacji oraz wysyłać powiadomienia wypychane do segmentowanych użytkowników aplikacji platformy Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="d0196-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="d0196-105">W tym samouczku został omówiony prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d0196-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="d0196-106">W ramach tego samouczka zostanie utworzona pusta aplikacja platformy Xamarin.Android służąca do zbierania danych podstawowych i odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="d0196-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="d0196-107">Usługa Azure Mobile Engagement zostanie wycofana w marcu 2018 r. i jest obecnie dostępna wyłącznie dla dotychczasowych klientów.</span><span class="sxs-lookup"><span data-stu-id="d0196-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="d0196-108">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="d0196-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="d0196-109">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d0196-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="d0196-110">Program [Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="d0196-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="d0196-111">Można również użyć programu Visual Studio z platformą Xamarin, ale w tym samouczku używany jest program Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="d0196-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="d0196-112">Aby uzyskać instrukcje dotyczące instalowania, zobacz [Instalator i instalacja programu Visual Studio i platformy Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0196-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="d0196-113">Zestaw SDK platformy Xamarin usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0196-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="d0196-114">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d0196-114">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d0196-115">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d0196-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d0196-116">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="d0196-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="d0196-117"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="d0196-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d0196-118"><a id="connecting-app"></a>Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0196-118"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="d0196-119">Ten samouczek przedstawia „podstawową integrację”, tj. minimalny zestaw wymagany do zbierania danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="d0196-119">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="d0196-120">Aby zademonstrować integrację, utworzona zostanie podstawowa aplikacja za pomocą programu Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="d0196-120">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="d0196-121">Tworzenie nowego projektu platformy Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="d0196-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="d0196-122">Uruchom program **Xamarin Studio**. Wybierz pozycję **File** (Plik) -> **New** (Nowy) -> **Solution** (Rozwiązanie).</span><span class="sxs-lookup"><span data-stu-id="d0196-122">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="d0196-123">Wybierz pozycję **Android App** (Aplikacja systemu Android), upewnij się, że wybrany język to **C#**, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="d0196-123">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="d0196-124">Wypełnij pole **App Name** (Nazwa aplikacji) i **Organization Identifier** (Identyfikator organizacji).</span><span class="sxs-lookup"><span data-stu-id="d0196-124">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="d0196-125">Upewnij się, że zaznaczono pole wyboru **Google Play Services** (Usługi Google Play), a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="d0196-125">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="d0196-126">Jeśli to będzie konieczne, zaktualizuj pola **Project Name** (Nazwa projektu), **Solution Name** (Nazwa rozwiązania) i **Location** (Lokalizacja), a następnie kliknij pozycję **Create** (Utwórz).</span><span class="sxs-lookup"><span data-stu-id="d0196-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="d0196-127">Za pomocą platformy Xamarin Studio zostanie utworzona aplikacja, w której zostanie zintegrowana usługa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d0196-127">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="d0196-128">Łączenie aplikacji z zapleczem usługi Mobile Engagement </span><span class="sxs-lookup"><span data-stu-id="d0196-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="d0196-129">Kliknij prawym przyciskiem myszy folder **Packages** w oknie Solution (Rozwiązanie), a następnie wybierz pozycję **Add Packages** (Dodaj pakiety).</span><span class="sxs-lookup"><span data-stu-id="d0196-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="d0196-130">Wyszukaj zestaw **Microsoft Azure Mobile Engagement Xamarin SDK** i dodaj go do swojego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d0196-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="d0196-131">Otwórz plik **MainActivity.cs** i dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="d0196-131">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="d0196-132">W metodzie `OnCreate` dodaj następujący kod, aby zainicjować połączenia z zapleczem usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d0196-132">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="d0196-133">Upewnij się, że został dodany element **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="d0196-133">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="d0196-134">Dodawanie uprawnień i deklaracji usługi</span><span class="sxs-lookup"><span data-stu-id="d0196-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="d0196-135">Otwórz plik **Manifest.xml** w folderze właściwości.</span><span class="sxs-lookup"><span data-stu-id="d0196-135">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="d0196-136">Wybierz kartę Source (Źródło), aby bezpośrednio zaktualizować źródło XML.</span><span class="sxs-lookup"><span data-stu-id="d0196-136">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="d0196-137">Te uprawnienia są dodawane do pliku Manifest.xml (można go znaleźć w folderze **Properties**) projektu bezpośrednio przed lub po znaczniku `<application>`:</span><span class="sxs-lookup"><span data-stu-id="d0196-137">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="d0196-138">Dodaj następujący kod między tagami `<application>` i `</application>`, aby zadeklarować usługę agenta:</span><span class="sxs-lookup"><span data-stu-id="d0196-138">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="d0196-139">We wklejonym właśnie kodzie zamień element `"<Your application name>"` w etykiecie.</span><span class="sxs-lookup"><span data-stu-id="d0196-139">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="d0196-140">Ta wartość jest wyświetlana w menu **Ustawienia**, w którym użytkownicy mogą zobaczyć usługi uruchomione na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="d0196-140">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="d0196-141">Możesz na przykład dodać wyraz „Usługa” w tej etykiecie.</span><span class="sxs-lookup"><span data-stu-id="d0196-141">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="d0196-142">Wysyłanie ekranu do usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0196-142">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="d0196-143">Aby rozpocząć wysyłanie danych i sprawdzić, czy użytkownicy są aktywni, konieczne jest wysłanie co najmniej jednego ekranu do zaplecza usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d0196-143">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="d0196-144">Aby to zrobić, upewnij się, że klasa `MainActivity` dziedziczy z klasy `EngagementActivity`, a nie z klasy `Activity`.</span><span class="sxs-lookup"><span data-stu-id="d0196-144">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="d0196-145">Alternatywnie jeśli nie możesz dziedziczyć z klasy `EngagementActivity`, musisz dodać metody `.StartActivity` i `.EndActivity` odpowiednio w `OnResume` i `OnPause`.</span><span class="sxs-lookup"><span data-stu-id="d0196-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

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

## <span data-ttu-id="d0196-146"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="d0196-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d0196-147"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="d0196-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d0196-148">Usługa Mobile Engagement umożliwia interakcję z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście kampanii.</span><span class="sxs-lookup"><span data-stu-id="d0196-148">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="d0196-149">Ten moduł w portalu Mobile Engagement ma nazwę REACH.</span><span class="sxs-lookup"><span data-stu-id="d0196-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="d0196-150">W poniższych sekcjach aplikacja zostanie skonfigurowana do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="d0196-150">The following sections sets up your app to receive them.</span></span>

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
