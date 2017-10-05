---
title: "Wprowadzenie do usługi Azure Mobile Engagement na potrzeby uniwersalnych aplikacji systemu Windows"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami wypychanymi na potrzeby uniwersalnych aplikacji systemu Windows"
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
ms.openlocfilehash: 40db7e4dd151ec391c754dc6d4145aeeb8058eca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="d1375-103">Wprowadzenie do usługi Azure Mobile Engagement na potrzeby uniwersalnych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d1375-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d1375-104">W tym temacie pokazano, jak za pomocą usługi Azure Mobile Engagement można określić sposób użycia aplikacji oraz wysyłać powiadomienia wypychane do segmentowanych użytkowników uniwersalnej aplikacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d1375-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span></span>
<span data-ttu-id="d1375-105">W tym samouczku został omówiony prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d1375-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="d1375-106">Utworzysz pustą uniwersalną aplikację systemu Windows, za pomocą której będą zbierane dane dotyczące zużycia i odbierane powiadomienia wypychane przy użyciu Usługi powiadomień systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d1375-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="d1375-107">Usługa Azure Mobile Engagement zostanie wycofana w marcu 2018 r. i jest obecnie dostępna wyłącznie dla dotychczasowych klientów.</span><span class="sxs-lookup"><span data-stu-id="d1375-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="d1375-108">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="d1375-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1375-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1375-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="d1375-110">Konfigurowanie usługi Mobile Engagement dla aplikacji uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d1375-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d1375-111"><a id="connecting-app"></a>Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d1375-111"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="d1375-112">Ten samouczek przedstawia „podstawową integrację”, tj. minimalny zestaw wymagany do zbierania danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="d1375-112">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="d1375-113">Kompletna dokumentacja integracji znajduje się w sekcji [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md) (Integracja uniwersalnego zestawu SDK systemu Windows usługi Mobile Engagement).</span><span class="sxs-lookup"><span data-stu-id="d1375-113">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="d1375-114">Aby zademonstrować integrację, utworzysz podstawową aplikację za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1375-114">You create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="d1375-115">Tworzenie projektu aplikacji uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d1375-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="d1375-116">W następujących krokach założono korzystanie z programu Visual Studio 2015, chociaż kroki są podobne także w przypadku wcześniejszych wersji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1375-116">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="d1375-117">Uruchom program Visual Studio i na ekranie **Strona główna** wybierz pozycję **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="d1375-117">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="d1375-118">W oknie podręcznym wybierz pozycję **Windows** -> **Aplikacja uniwersalna** -> **Pusta aplikacja (aplikacja uniwersalna systemu Windows)**.</span><span class="sxs-lookup"><span data-stu-id="d1375-118">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="d1375-119">Wypełnij pola **Nazwa** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1375-119">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="d1375-120">Został utworzony projekt aplikacji uniwersalnej systemu Windows, z którym następnie zintegrujesz zestaw SDK usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d1375-120">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="d1375-121">Łączenie aplikacji z zapleczem usługi Mobile Engagement </span><span class="sxs-lookup"><span data-stu-id="d1375-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="d1375-122">Zainstaluj pakiet NuGet [MicrosoftAzure.MobileEngagement] w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d1375-122">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="d1375-123">Jeśli aplikacja ma być przeznaczona zarówno dla platformy Windows, jak i Windows Phone, należy to zrobić w obu projektach.</span><span class="sxs-lookup"><span data-stu-id="d1375-123">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span></span> <span data-ttu-id="d1375-124">W przypadku systemu Windows 8.x i Windows Phone 8.1 ten sam pakiet NuGet umieszcza poprawne pliki binarne specyficzne dla platformy w każdym projekcie.</span><span class="sxs-lookup"><span data-stu-id="d1375-124">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="d1375-125">Otwórz plik **Package.appxmanifest** i upewnij się, że dodano w nim następującą funkcję:</span><span class="sxs-lookup"><span data-stu-id="d1375-125">Open **Package.appxmanifest** and make sure that the following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="d1375-126">Teraz skopiuj parametry połączenia, które wcześniej zostały skopiowane dla aplikacji usługi Mobile Engagement, a następnie wklej je do pliku `Resources\EngagementConfiguration.xml` między znaczniki `<connectionString>` i `</connectionString>`:</span><span class="sxs-lookup"><span data-stu-id="d1375-126">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="d1375-127">Jeśli aplikacja jest przeznaczona zarówno dla platformy Windows, jak i Windows Phone, nadal powinny zostać utworzone dwie aplikacje usługi Mobile Engagement — jedna dla każdej z obsługiwanych platform.</span><span class="sxs-lookup"><span data-stu-id="d1375-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="d1375-128">Dzięki dwóm aplikacjom możliwe będzie tworzenie poprawnej segmentacji odbiorców i wysyłanie odpowiednio skierowanych powiadomień dla każdej platformy.</span><span class="sxs-lookup"><span data-stu-id="d1375-128">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d1375-129">Menedżer NuGet nie kopiuje automatycznie zasobów zestawu SDK do aplikacji UWP systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d1375-129">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="d1375-130">Należy to zrobić ręcznie, postępując zgodnie z wyświetlonymi instrukcjami (plik readme.txt) podczas instalacji pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="d1375-130">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span></span>  

1. <span data-ttu-id="d1375-131">W pliku `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="d1375-131">In the `App.xaml.cs` file:</span></span>

    <span data-ttu-id="d1375-132">a.</span><span class="sxs-lookup"><span data-stu-id="d1375-132">a.</span></span> <span data-ttu-id="d1375-133">Dodaj instrukcję `using`:</span><span class="sxs-lookup"><span data-stu-id="d1375-133">Add the `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="d1375-134">b.</span><span class="sxs-lookup"><span data-stu-id="d1375-134">b.</span></span> <span data-ttu-id="d1375-135">Dodaj metodę inicjowania usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="d1375-135">Add a method that initializes the Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of the code
           }

    <span data-ttu-id="d1375-136">c.</span><span class="sxs-lookup"><span data-stu-id="d1375-136">c.</span></span> <span data-ttu-id="d1375-137">Zainicjuj zestaw SDK w metodzie **OnLaunched**:</span><span class="sxs-lookup"><span data-stu-id="d1375-137">Initialize the SDK in the **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

    <span data-ttu-id="d1375-138">d.</span><span class="sxs-lookup"><span data-stu-id="d1375-138">c.</span></span> <span data-ttu-id="d1375-139">Wstaw następujący kod w metodzie **OnActivated**, a następnie dodaj metodę, jeśli została już dodana:</span><span class="sxs-lookup"><span data-stu-id="d1375-139">Insert the following in the **OnActivated** method and add the method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

## <span data-ttu-id="d1375-140"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="d1375-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="d1375-141">Aby rozpocząć wysyłanie danych i upewnić się, że użytkownicy są aktywni, konieczne jest wysłanie co najmniej jednego ekranu (Działanie) do zaplecza usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d1375-141">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="d1375-142">W pliku **MainPage.xaml.cs** dodaj następującą instrukcję `using`:</span><span class="sxs-lookup"><span data-stu-id="d1375-142">In the **MainPage.xaml.cs**, add the following `using` statement:</span></span>

    <span data-ttu-id="d1375-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="d1375-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="d1375-144">Zmień klasę podstawową **MainPage** z **Page** na **EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="d1375-144">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="d1375-145">W pliku `MainPage.xaml`:</span><span class="sxs-lookup"><span data-stu-id="d1375-145">In the `MainPage.xaml` file:</span></span>

    <span data-ttu-id="d1375-146">a.</span><span class="sxs-lookup"><span data-stu-id="d1375-146">a.</span></span> <span data-ttu-id="d1375-147">Dodaj deklaracje przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="d1375-147">Add to your namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="d1375-148">b.</span><span class="sxs-lookup"><span data-stu-id="d1375-148">b.</span></span> <span data-ttu-id="d1375-149">Zastąp wartość **Page** w nazwie tagu XML wartością **engagement:EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="d1375-149">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1375-150">Jeśli strona zastępuje metodę `OnNavigatedTo`, nie zapomnij wywołać metody `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="d1375-150">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="d1375-151">W przeciwnym razie działanie nie zostanie zgłoszone (element `EngagementPage` wywołuje metodę `StartActivity` wewnątrz jego metody `OnNavigatedTo`).</span><span class="sxs-lookup"><span data-stu-id="d1375-151">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="d1375-152">Jest to szczególnie ważne w projekcie systemu Windows Phone, w którym szablon domyślny zawiera metodę `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="d1375-152">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="d1375-153">W **aplikacjach uniwersalnych systemu Windows 10** użyj metody zalecanej w sekcji „Recommended method: overload your Page classes” (Zalecana metoda: przeciążenie klas Page) tematu [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md) (Zaawansowane raportowanie za pomocą zestawu SDK zaangażowania aplikacji uniwersalnych systemu Windows), a nie wymienionej powyżej.</span><span class="sxs-lookup"><span data-stu-id="d1375-153">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span></span>

## <span data-ttu-id="d1375-154"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="d1375-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d1375-155"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1375-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d1375-156">Usługa Mobile Engagement umożliwia wchodzenie w interakcję z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście kampanii.</span><span class="sxs-lookup"><span data-stu-id="d1375-156">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="d1375-157">Ten moduł w portalu Mobile Engagement ma nazwę REACH.</span><span class="sxs-lookup"><span data-stu-id="d1375-157">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="d1375-158">W poniższych sekcjach aplikacja zostanie skonfigurowana do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="d1375-158">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-wns-push-notifications"></a><span data-ttu-id="d1375-159">Umożliwianie aplikacji otrzymywanie powiadomień wypychanych Usługi powiadomień systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d1375-159">Enable your app to receive WNS Push Notifications</span></span>
1. <span data-ttu-id="d1375-160">W pliku `Package.appxmanifest` na karcie **Aplikacja** w obszarze **Powiadomienia** ustaw pozycję **Możliwe do wyświetlania na pasku przewijania:** na wartość **Tak**</span><span class="sxs-lookup"><span data-stu-id="d1375-160">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span></span>

    ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="d1375-161">Inicjowanie zestawu SDK modułu REACH</span><span class="sxs-lookup"><span data-stu-id="d1375-161">Initialize the REACH SDK</span></span>
<span data-ttu-id="d1375-162">W pliku `App.xaml.cs` wywołaj metodę **EngagementReach.Instance.Init(e);** w funkcji **InitEngagement** bezpośrednio po zainicjowaniu agenta:</span><span class="sxs-lookup"><span data-stu-id="d1375-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="d1375-163">Wszystko jest gotowe do wysłania wyskakującego powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="d1375-163">You're ready to send a toast.</span></span> <span data-ttu-id="d1375-164">Następnie zweryfikujemy, czy podstawowa integracja została przeprowadzona prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="d1375-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-to-mobile-engagement-to-send-notifications"></a><span data-ttu-id="d1375-165">Udzielanie dostępu do usługi Mobile Engagement w celu wysyłania powiadomień</span><span class="sxs-lookup"><span data-stu-id="d1375-165">Grant access to Mobile Engagement to send notifications</span></span>
1. <span data-ttu-id="d1375-166">Otwórz [Centrum deweloperów Sklepu Windows] w przeglądarce internetowej, a następnie zaloguj się i utwórz konto, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d1375-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="d1375-167">Kliknij pozycję **Pulpit nawigacyjny** w prawym górnym rogu, a następnie kliknij pozycję **Utwórz nową aplikację** z menu lewego panelu.</span><span class="sxs-lookup"><span data-stu-id="d1375-167">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="d1375-168">Utwórz aplikację przez zarezerwowanie jej nazwy.</span><span class="sxs-lookup"><span data-stu-id="d1375-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="d1375-169">Po utworzeniu aplikacji przejdź do pozycji **Usługi -> Powiadomienia wypychane** z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d1375-169">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span></span>

    ![][11]
5. <span data-ttu-id="d1375-170">W sekcji Powiadomienia wypychane kliknij link **Witryna usług Live**.</span><span class="sxs-lookup"><span data-stu-id="d1375-170">In the Push notifications section, click the **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="d1375-171">Nastąpi przejście do sekcji poświadczeń wypychania.</span><span class="sxs-lookup"><span data-stu-id="d1375-171">You navigate to the Push credentials section.</span></span> <span data-ttu-id="d1375-172">Upewnij się, że jesteś w sekcji **Ustawienia aplikacji**, a następnie skopiuj swój **identyfikator SID pakietu** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="d1375-172">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="d1375-173">Przejdź do obszaru **Ustawienia** portalu Mobile Engagement, a następnie kliknij sekcję **Natywne powiadomienia wypychane** po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d1375-173">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span></span> <span data-ttu-id="d1375-174">Następnie kliknij przycisk **Edytuj**, aby wprowadzić swój **identyfikator zabezpieczeń (SID) pakietu** i **klucz tajny** w przedstawiony sposób:</span><span class="sxs-lookup"><span data-stu-id="d1375-174">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="d1375-175">Na końcu upewnij się, że aplikacja programu Visual Studio została skojarzona z tą utworzoną aplikacją w sklepie z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="d1375-175">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span></span> <span data-ttu-id="d1375-176">W programie Visual Studio kliknij pozycję **Skojarz aplikację ze sklepem**.</span><span class="sxs-lookup"><span data-stu-id="d1375-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="d1375-177"><a id="send"></a>Wysyłanie powiadomienia do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d1375-177"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="d1375-178">Jeśli aplikacja jest uruchomiona, zobaczysz powiadomienie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1375-178">If the app is running, you see an in-app notification.</span></span> <span data-ttu-id="d1375-179">W przeciwnym razie (jeśli aplikacja jest zamknięta) zobaczysz powiadomienie wyskakujące.</span><span class="sxs-lookup"><span data-stu-id="d1375-179">otherwise if the app is closed, you see a toast notification.</span></span>
<span data-ttu-id="d1375-180">Jeśli widzisz powiadomienie w aplikacji, ale nie powiadomienie wyskakujące, a aplikacja jest uruchomiona w trybie debugowania w programie Visual Studio, spróbuj użyć pozycji **Zdarzenia cyklu życia -> Wstrzymaj** na pasku narzędzi, aby upewnić się, że aplikacja została wstrzymana.</span><span class="sxs-lookup"><span data-stu-id="d1375-180">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span></span> <span data-ttu-id="d1375-181">Jeśli kliknięto przycisk Strona główna podczas debugowania aplikacji w programie Visual Studio, to aplikacja nie zawsze zostanie wstrzymana, a w związku z tym, że powiadomienie jest wyświetlane w aplikacji, to nie jest wyświetlane powiadomienie wyskakujące.</span><span class="sxs-lookup"><span data-stu-id="d1375-181">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
<span data-ttu-id="d1375-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span><span class="sxs-lookup"><span data-stu-id="d1375-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span></span>
<span data-ttu-id="d1375-183">[Centrum deweloperów Sklepu Windows]: https://dev.windows.com</span><span class="sxs-lookup"><span data-stu-id="d1375-183">[Windows Store Dev Center]: https://dev.windows.com</span></span>
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
