---
title: "aaaGet pracy z aplikacjami usługi Azure Mobile Engagement dla Windows Phone Silverlight"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji Windows Phone Silverlight."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="3255e-103">Wprowadzenie do usługi Azure Mobile Engagement na potrzeby aplikacji platformy Silverlight systemu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3255e-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="3255e-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse Twoje użycie aplikacji i wysyłania powiadomień użytkowników toosegmented aplikacji Windows Phone Silverlight push.</span><span class="sxs-lookup"><span data-stu-id="3255e-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="3255e-105">W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3255e-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="3255e-106">W ramach tego samouczka utworzona zostanie pusta aplikacja platformy Silverlight systemu Windows Phone, za pomocą której będą zbierane podstawowe dane i odbierane powiadomienia wypychane przy użyciu Usługi powiadomień systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3255e-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="3255e-107">Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów.</span><span class="sxs-lookup"><span data-stu-id="3255e-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="3255e-108">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="3255e-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="3255e-109">Projekty systemu Windows Phone 8.1 i wcześniejszych nie są obsługiwane w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3255e-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="3255e-110">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="3255e-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="3255e-111">Jeśli ma być przeznaczona dla Windows Phone 8.1 (z systemem innym niż platformy Silverlight), zapoznaj się z pomocą techniczną firmy toohello [samouczek aplikacji uniwersalnych systemu Windows](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3255e-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="3255e-112">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="3255e-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="3255e-113">Program Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3255e-113">Visual Studio 2013</span></span>
* <span data-ttu-id="3255e-114">Pakiet NuGet [MicrosoftAzure.MobileEngagement]</span><span class="sxs-lookup"><span data-stu-id="3255e-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="3255e-115">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3255e-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3255e-116">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="3255e-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3255e-117">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="3255e-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="3255e-118"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3255e-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="3255e-119"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="3255e-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="3255e-120">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="3255e-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="3255e-121">Witaj kompletna dokumentacja integracji znajduje się w hello [integracji zestawu SDK usługi Mobile Engagement Windows Phone](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3255e-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="3255e-122">Utworzymy podstawową aplikację z integracją hello toodemonstrate programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3255e-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="3255e-123">Tworzenie nowego projektu platformy Silverlight systemu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3255e-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="3255e-124">Hello następujących krokach założono użycie hello programu Visual Studio 2015 chociaż hello kroki są podobne we wcześniejszych wersjach programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3255e-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="3255e-125">Uruchom program Visual Studio w hello **Home** ekranu wybierz **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="3255e-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="3255e-126">W oknie podręcznym hello wybierz **systemu Windows 8** -> **Windows Phone** -> **pusta aplikacja (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="3255e-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="3255e-127">Wypełnij aplikacji hello **nazwa** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3255e-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="3255e-128">Można wybrać tootarget albo **Windows Phone 8.0** lub **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="3255e-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="3255e-129">Teraz utworzono nową aplikację systemu Windows Phone Silverlight, w którym zostanie zintegrowany zestaw SDK usługi Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="3255e-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="3255e-130">Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="3255e-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="3255e-131">Zainstaluj hello [MicrosoftAzure.MobileEngagement] pakietu nuget w projekcie.</span><span class="sxs-lookup"><span data-stu-id="3255e-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="3255e-132">Otwórz `WMAppManifest.xml` (znajduje się w folderze właściwości hello) i upewnij się, że zadeklarowany następujący hello (dodać je, gdy nie są one) w hello `<Capabilities />` tagu:</span><span class="sxs-lookup"><span data-stu-id="3255e-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="3255e-133">Teraz Wklej parametry połączenia hello, które wcześniej zostały skopiowane dla aplikacji usługi Mobile Engagement i wklej go w hello `Resources\EngagementConfiguration.xml` plików między hello `<connectionString>` i `</connectionString>` tagów:</span><span class="sxs-lookup"><span data-stu-id="3255e-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="3255e-134">W hello `App.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="3255e-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="3255e-135">a.</span><span class="sxs-lookup"><span data-stu-id="3255e-135">a.</span></span> <span data-ttu-id="3255e-136">Dodaj hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="3255e-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="3255e-137">b.</span><span class="sxs-lookup"><span data-stu-id="3255e-137">b.</span></span> <span data-ttu-id="3255e-138">Inicjowanie hello zestawu SDK w hello `Application_Launching` metody:</span><span class="sxs-lookup"><span data-stu-id="3255e-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="3255e-139">c.</span><span class="sxs-lookup"><span data-stu-id="3255e-139">c.</span></span> <span data-ttu-id="3255e-140">Wstaw następujące hello w hello `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="3255e-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="3255e-141"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="3255e-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="3255e-142">W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).</span><span class="sxs-lookup"><span data-stu-id="3255e-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="3255e-143">W hello MainPage.xaml.cs Dodaj hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="3255e-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="3255e-144">Zastąp klasę podstawową hello **MainPage**, czyli przed **PhoneApplicationPage**, z **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="3255e-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="3255e-145">W pliku `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="3255e-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="3255e-146">a.</span><span class="sxs-lookup"><span data-stu-id="3255e-146">a.</span></span> <span data-ttu-id="3255e-147">Dodaj deklaracje przestrzeni nazw tooyour:</span><span class="sxs-lookup"><span data-stu-id="3255e-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="3255e-148">b.</span><span class="sxs-lookup"><span data-stu-id="3255e-148">b.</span></span> <span data-ttu-id="3255e-149">Zastąp `phone:PhoneApplicationPage` w nazwie tagu XML hello z `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="3255e-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="3255e-150"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="3255e-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="3255e-151"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="3255e-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="3255e-152">Usługa Mobile Engagement umożliwia toointeract i użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście hello kampanii.</span><span class="sxs-lookup"><span data-stu-id="3255e-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="3255e-153">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="3255e-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="3255e-154">Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="3255e-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="3255e-155">Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi MPNS</span><span class="sxs-lookup"><span data-stu-id="3255e-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="3255e-156">Dodaj nowe możliwości tooyour `WMAppManifest.xml` pliku:</span><span class="sxs-lookup"><span data-stu-id="3255e-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="3255e-157">Inicjowanie hello OSIĄGNĄĆ zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="3255e-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="3255e-158">W `App.xaml.cs`, wywołaj `EngagementReach.Instance.Init();` w hello **Application_Launching** bezpośrednio po zainicjowaniu agenta hello:</span><span class="sxs-lookup"><span data-stu-id="3255e-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="3255e-159">W `App.xaml.cs`, wywołaj `EngagementReach.Instance.OnActivated(e);` w hello **Application_Activated** bezpośrednio po zainicjowaniu agenta hello:</span><span class="sxs-lookup"><span data-stu-id="3255e-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="3255e-160">Wszystko jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="3255e-160">You're all set.</span></span> <span data-ttu-id="3255e-161">Teraz zostanie zweryfikowane, czy podstawowa integracja została przeprowadzona prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="3255e-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="3255e-162"><a id="send"></a>Wyślij aplikacji tooyour powiadomień</span><span class="sxs-lookup"><span data-stu-id="3255e-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="3255e-163">Powinien zostać wyświetlony powiadomienia na urządzeniu, które będzie widoczne jako powiadomienie w aplikacji, jeśli aplikacja hello jest otwarty jako powiadomienie wyskakujące, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3255e-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
