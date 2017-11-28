---
title: "wprowadzenie do systemu Windows Universal aplikacji usługi Azure Mobile Engagement aaaGet"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji uniwersalnych systemu Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="1345c-103">Wprowadzenie do usługi Azure Mobile Engagement na potrzeby uniwersalnych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1345c-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="1345c-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji, a wysłać wypychanie powiadomień użytkowników toosegmented aplikacji uniwersalnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1345c-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="1345c-105">W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1345c-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="1345c-106">Utworzysz pustą uniwersalną aplikację systemu Windows, za pomocą której będą zbierane dane dotyczące zużycia i odbierane powiadomienia wypychane przy użyciu Usługi powiadomień systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1345c-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="1345c-107">Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów.</span><span class="sxs-lookup"><span data-stu-id="1345c-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="1345c-108">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="1345c-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1345c-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1345c-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="1345c-110">Konfigurowanie usługi Mobile Engagement dla aplikacji uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1345c-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="1345c-111"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="1345c-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="1345c-112">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1345c-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="1345c-113">Witaj kompletna dokumentacja integracji znajduje się w hello [integracja zestawu Mobile Engagement Windows Universal SDK](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1345c-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="1345c-114">Utworzeniu Podstawowa aplikacja za pomocą programu Visual Studio toodemonstrate hello integracji.</span><span class="sxs-lookup"><span data-stu-id="1345c-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="1345c-115">Tworzenie projektu aplikacji uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1345c-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="1345c-116">Hello następujących krokach założono użycie hello programu Visual Studio 2015 chociaż hello kroki są podobne we wcześniejszych wersjach programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1345c-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="1345c-117">Uruchom program Visual Studio w hello **Home** ekranu wybierz **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="1345c-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="1345c-118">W oknie podręcznym hello wybierz **Windows** -> **uniwersalnych** -> **pusta aplikacja (uniwersalna systemu Windows)**.</span><span class="sxs-lookup"><span data-stu-id="1345c-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="1345c-119">Wypełnij aplikacji hello **nazwa** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1345c-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="1345c-120">Został utworzony projekt aplikacji uniwersalnej systemu Windows, do którego obok integracji hello zestaw SDK usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1345c-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="1345c-121">Połącz zapleczu swojej aplikacji tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="1345c-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="1345c-122">Zainstaluj hello [MicrosoftAzure.MobileEngagement] pakietu Nuget w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1345c-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="1345c-123">Jeśli ma być przeznaczona dla platform systemów Windows i Windows Phone, musisz toodo to dla obu tych projektów.</span><span class="sxs-lookup"><span data-stu-id="1345c-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="1345c-124">Dla systemu Windows 8.x i Windows Phone 8.1, hello tego samego Nuget pakietu miejsca hello poprawne specyficzne dla platformy pliki binarne w każdym projekcie.</span><span class="sxs-lookup"><span data-stu-id="1345c-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="1345c-125">Otwórz **Package.appxmanifest** i upewnij się, że dodano tego hello następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="1345c-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="1345c-126">Teraz skopiuj parametry połączenia hello, które wcześniej zostały skopiowane dla aplikacji usługi Mobile Engagement i wklej go w hello `Resources\EngagementConfiguration.xml` plików między hello `<connectionString>` i `</connectionString>` tagów:</span><span class="sxs-lookup"><span data-stu-id="1345c-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="1345c-127">Jeśli aplikacja jest przeznaczona zarówno dla platformy Windows, jak i Windows Phone, nadal powinny zostać utworzone dwie aplikacje usługi Mobile Engagement — jedna dla każdej z obsługiwanych platform.</span><span class="sxs-lookup"><span data-stu-id="1345c-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="1345c-128">Mając dwie aplikacje gwarantuje, że można utworzyć poprawnej segmentacji odbiorców hello i można wysyłanie odpowiednio skierowanych powiadomień dla każdej platformy.</span><span class="sxs-lookup"><span data-stu-id="1345c-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1345c-129">NuGet nie kopiuje automatycznie hello zasobów zestawu SDK w aplikacji platformy uniwersalnej systemu Windows do systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1345c-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="1345c-130">Masz toodo go ręcznie następujące kroki hello, które widać (readme.txt) jest zainstalowany pakiet Nuget hello.</span><span class="sxs-lookup"><span data-stu-id="1345c-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="1345c-131">W hello `App.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="1345c-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="1345c-132">a.</span><span class="sxs-lookup"><span data-stu-id="1345c-132">a.</span></span> <span data-ttu-id="1345c-133">Dodaj hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1345c-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="1345c-134">b.</span><span class="sxs-lookup"><span data-stu-id="1345c-134">b.</span></span> <span data-ttu-id="1345c-135">Dodaj metodę, która inicjuje hello Engagement:</span><span class="sxs-lookup"><span data-stu-id="1345c-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="1345c-136">c.</span><span class="sxs-lookup"><span data-stu-id="1345c-136">c.</span></span> <span data-ttu-id="1345c-137">Inicjowanie hello zestawu SDK w hello **OnLaunched** metody:</span><span class="sxs-lookup"><span data-stu-id="1345c-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="1345c-138">c.</span><span class="sxs-lookup"><span data-stu-id="1345c-138">c.</span></span> <span data-ttu-id="1345c-139">Wstaw następujące hello w hello **OnActivated** — metoda i Dodawanie metody hello, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="1345c-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="1345c-140"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1345c-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="1345c-141">toostart wysyłanie danych i zapewnienia, że hello użytkownicy są aktywni, konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).</span><span class="sxs-lookup"><span data-stu-id="1345c-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="1345c-142">W hello **MainPage.xaml.cs**, Dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1345c-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="1345c-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="1345c-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="1345c-144">Zmień klasę podstawową hello **MainPage** z **strony** za**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="1345c-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="1345c-145">W hello `MainPage.xaml` pliku:</span><span class="sxs-lookup"><span data-stu-id="1345c-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="1345c-146">a.</span><span class="sxs-lookup"><span data-stu-id="1345c-146">a.</span></span> <span data-ttu-id="1345c-147">Dodaj deklaracje przestrzeni nazw tooyour:</span><span class="sxs-lookup"><span data-stu-id="1345c-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="1345c-148">b.</span><span class="sxs-lookup"><span data-stu-id="1345c-148">b.</span></span> <span data-ttu-id="1345c-149">Zastąp hello **strony** w nazwie tagu XML hello z **engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="1345c-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1345c-150">Jeśli strona zastępuje hello `OnNavigatedTo` metody, należy się toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="1345c-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="1345c-151">W przeciwnym razie hello działania nie został zgłoszony `EngagementPage` wywołania `StartActivity` wewnątrz jego `OnNavigatedTo` metody).</span><span class="sxs-lookup"><span data-stu-id="1345c-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="1345c-152">Jest to szczególnie ważne w projekcie Windows Phone, gdzie ma hello domyślny szablon `OnNavigatedTo` metody.</span><span class="sxs-lookup"><span data-stu-id="1345c-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="1345c-153">Dla **aplikacji uniwersalnych systemu Windows 10**, należy użyć metody hello zalecane w hello "zalecana metoda: przeciążenia klas strony" sekcji [zaawansowane raporty dzięki hello Windows Universal SDK zaangażowania aplikacji](mobile-engagement-windows-store-advanced-reporting.md) , zamiast hello jedną wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="1345c-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="1345c-154"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1345c-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="1345c-155"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="1345c-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="1345c-156">Usługa Mobile Engagement umożliwia toointeract i użytkownikami przy użyciu powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1345c-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="1345c-157">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="1345c-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="1345c-158">Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="1345c-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="1345c-159">Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi WNS</span><span class="sxs-lookup"><span data-stu-id="1345c-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="1345c-160">W hello `Package.appxmanifest` pliku w hello **aplikacji** , w obszarze **powiadomienia**ustaw **wyskakujące funkcją:** zbyt**tak**</span><span class="sxs-lookup"><span data-stu-id="1345c-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="1345c-161">Inicjowanie hello OSIĄGNĄĆ zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="1345c-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="1345c-162">W `App.xaml.cs`, wywołaj **EngagementReach.Instance.Init(e);** w hello **InitEngagement** bezpośrednio po zainicjowaniu agenta hello:</span><span class="sxs-lookup"><span data-stu-id="1345c-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="1345c-163">Wszystko jest gotowe toosend wyskakującego powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="1345c-163">You're ready toosend a toast.</span></span> <span data-ttu-id="1345c-164">Następnie zweryfikujemy, czy podstawowa integracja została przeprowadzona prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="1345c-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="1345c-165">Udziel dostępu tooMobile zaangażowania toosend powiadomienia</span><span class="sxs-lookup"><span data-stu-id="1345c-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="1345c-166">Otwórz [Centrum deweloperów Sklepu Windows] w przeglądarce internetowej, a następnie zaloguj się i utwórz konto, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1345c-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="1345c-167">Kliknij przycisk **pulpitu nawigacyjnego** na powitania prawym górnym rogu, a następnie kliknij przycisk **Utwórz nową aplikację** z menu lewego panelu hello.</span><span class="sxs-lookup"><span data-stu-id="1345c-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="1345c-168">Utwórz aplikację przez zarezerwowanie jej nazwy.</span><span class="sxs-lookup"><span data-stu-id="1345c-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="1345c-169">Po utworzeniu aplikacji hello Przejdź zbyt**usługi -> powiadomienia wypychane** z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="1345c-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="1345c-170">W hello Push sekcji powiadomień, kliknij przycisk hello **witryna usług Live** łącza.</span><span class="sxs-lookup"><span data-stu-id="1345c-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="1345c-171">Możesz przejść sekcji poświadczeń wypychania toohello.</span><span class="sxs-lookup"><span data-stu-id="1345c-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="1345c-172">Upewnij się, że jesteś w hello **ustawień aplikacji** sekcji, a następnie skopiuj z **identyfikatora SID pakietu** i **klucz tajny klienta**</span><span class="sxs-lookup"><span data-stu-id="1345c-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="1345c-173">Przejdź toohello **ustawienia** z portalu usługi Mobile Engagement i kliknij przycisk hello **natywnych powiadomień wypychanych** sekcji powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1345c-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="1345c-174">Kliknięcie hello **Edytuj** tooenter przycisk z **identyfikator zabezpieczeń (SID) pakietu** i **klucz tajny** pokazany:</span><span class="sxs-lookup"><span data-stu-id="1345c-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="1345c-175">Na koniec upewnij się, że aplikacja programu Visual Studio został skojarzony z tą utworzoną aplikacją w sklepie z aplikacjami hello.</span><span class="sxs-lookup"><span data-stu-id="1345c-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="1345c-176">W programie Visual Studio kliknij pozycję **Skojarz aplikację ze sklepem**.</span><span class="sxs-lookup"><span data-stu-id="1345c-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="1345c-177"><a id="send"></a>Wyślij aplikacji tooyour powiadomień</span><span class="sxs-lookup"><span data-stu-id="1345c-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="1345c-178">Jeśli aplikacja hello jest uruchomiona, zobaczysz powiadomienie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1345c-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="1345c-179">Jeśli aplikacja hello są zamknięte, w przeciwnym razie Zobacz wyskakujące powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="1345c-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="1345c-180">Jeśli zobaczysz powiadomienie w aplikacji, ale nie powiadomienie wyskakujące, a aplikacja hello są uruchomione w trybie debugowania w programie Visual Studio, spróbuj **zdarzenia cyklu życia -> Wstrzymaj** w tooensure narzędzi hello jest wstrzymana, aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="1345c-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="1345c-181">Jeśli kliknięto przycisk Strona główna hello podczas debugowania aplikacji hello w programie Visual Studio, następnie go nie zawsze zostanie wstrzymana, a gdy zostanie wyświetlone powiadomienie hello w aplikacji, nie wyświetla jako powiadomienie wyskakujące.</span><span class="sxs-lookup"><span data-stu-id="1345c-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Centrum deweloperów Sklepu Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
