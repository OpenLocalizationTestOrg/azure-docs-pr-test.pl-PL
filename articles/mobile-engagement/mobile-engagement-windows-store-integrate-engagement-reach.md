---
title: "aaaWindows uniwersalnych aplikacji osiągnąć integracji zestawu SDK"
description: "Jak tooIntegrate usługi Azure Mobile Engagement nawiązać połączenia z uniwersalnych aplikacji systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="89128-103">Integracja zestawu SDK osiągnąć uniwersalnych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="89128-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="89128-104">Musisz wykonać procedurę integracji hello opisanego w hello [Windows Universal integracji zestawu SDK usługi Engagement](mobile-engagement-windows-store-integrate-engagement.md) przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="89128-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="89128-105">Osadź hello Engagement Reach SDK do projektu uniwersalnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="89128-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="89128-106">Nie masz żadnych tooadd.</span><span class="sxs-lookup"><span data-stu-id="89128-106">You do not have anything tooadd.</span></span> <span data-ttu-id="89128-107">`EngagementReach`referencje i zasoby są już w projekcie.</span><span class="sxs-lookup"><span data-stu-id="89128-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="89128-108">Można dostosować obrazy znajdujące się w hello `Resources` folderu projektu, szczególnie hello brand ikona (tej domyślnej toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="89128-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="89128-109">W aplikacjach uniwersalnych można również przenosić hello `Resources` folderu na Twojej tooshare projektu udostępnionego jego zawartości między aplikacjami, ale będzie mieć tookeep hello `Resources\EngagementConfiguration.xml` pliku w domyślnej lokalizacji, ponieważ jest on zależny platformy.</span><span class="sxs-lookup"><span data-stu-id="89128-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="89128-110">Włącz hello usługi powiadomień systemu Windows</span><span class="sxs-lookup"><span data-stu-id="89128-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="89128-111">Windows 8.x i Windows Phone 8.1 tylko</span><span class="sxs-lookup"><span data-stu-id="89128-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="89128-112">W kolejności toouse hello **usługi powiadomień systemu Windows** (określanych jako WNS) w Twojej `Package.appxmanifest` plików na `Application UI` kliknij `All Image Assets` hello bot po lewej stronie pola.</span><span class="sxs-lookup"><span data-stu-id="89128-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="89128-113">Na powitania prawej strony pola hello w `Notifications`, zmień `toast capable` z `(not set)` zbyt`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="89128-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="89128-114">Wszystkie platformy</span><span class="sxs-lookup"><span data-stu-id="89128-114">All platforms</span></span>
<span data-ttu-id="89128-115">Należy toosynchronize Twojego tooyour Microsoft konta i toohello zaangażowania platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89128-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="89128-116">W tym muszą toocreate konto lub zaloguj się na [Centrum deweloperów systemu windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="89128-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="89128-117">Po którym tworzenie nowej aplikacji i znajdowanie hello identyfikator SID i klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="89128-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="89128-118">Na frontonie zaangażowania hello, przejdź na ustawienia aplikacji w `native push` i Wklej swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="89128-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="89128-119">Następnie kliknij prawym przyciskiem myszy projekt, wybierz opcję `store` i `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="89128-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="89128-120">Wystarczy, że aplikacja hello tooselect ma przed toosynchronize jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="89128-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="89128-121">Zainicjuj zestaw SDK Reach usługi Engagement hello</span><span class="sxs-lookup"><span data-stu-id="89128-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="89128-122">Modyfikowanie hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="89128-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="89128-123">Wstaw `EngagementReach.Instance.Init` tuż po `EngagementAgent.Instance.Init` w Twojej `InitEngagement` metody:</span><span class="sxs-lookup"><span data-stu-id="89128-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="89128-124">Witaj `EngagementReach.Instance.Init` działa w dedykowanym wątku.</span><span class="sxs-lookup"><span data-stu-id="89128-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="89128-125">Nie masz toodo ją samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="89128-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="89128-126">Jeśli używasz powiadomień wypychanych w innym miejscu w aplikacji, masz zbyt[udostępnianie kanału wypychania](#push-channel-sharing) z Reach usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="89128-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="89128-127">Integracja</span><span class="sxs-lookup"><span data-stu-id="89128-127">Integration</span></span>
<span data-ttu-id="89128-128">Engagement udostępnia dwa sposoby tooadd hello Reach w aplikacji transparentach i międzysegmentowe widoków w przypadku anonsów i sond w aplikacji: hello nakładki integracji i hello integracja ręczna widoki sieci web.</span><span class="sxs-lookup"><span data-stu-id="89128-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="89128-129">Nie należy łączyć oba podejścia na powitania tej samej stronie.</span><span class="sxs-lookup"><span data-stu-id="89128-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="89128-130">Hello wybór między Witaj dwie integracji można podsumować w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="89128-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="89128-131">Integracja z nakładką hello może wybrać, jeśli strony już dziedziczy hello agenta `EngagementPage`, jest wystarczy zastępowanie `EngagementPage` przez `EngagementPageOverlay` i `xmlns:engagement="using:Microsoft.Azure.Engagement"` przez `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` na swoich stronach.</span><span class="sxs-lookup"><span data-stu-id="89128-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="89128-132">Można wybrać integracji ręczne widoki sieci web hello tooprecisely miejsce hello osiągnąć interfejsu użytkownika w ramach strony lub jeśli nie chcesz tooadd innej strony poziomu tooyour dziedziczenia.</span><span class="sxs-lookup"><span data-stu-id="89128-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="89128-133">Integracja z nakładką</span><span class="sxs-lookup"><span data-stu-id="89128-133">Overlay integration</span></span>
<span data-ttu-id="89128-134">Hello zaangażowania nakładki są dodawane dynamicznie hello elementy interfejsu użytkownika używanych kampanie Zasięgowe toodisplay na stronie.</span><span class="sxs-lookup"><span data-stu-id="89128-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="89128-135">Jeśli hello nakładki nie własnych układu należy rozważyć hello widoki sieci web integracji ręczne zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="89128-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="89128-136">W przypadku zmiany pliku .xaml `EngagementPage` zbyt odwołania`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="89128-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="89128-137">Dodaj deklaracje przestrzeni nazw tooyour:</span><span class="sxs-lookup"><span data-stu-id="89128-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="89128-138">Zastąp `engagement:EngagementPage` z `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="89128-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="89128-139">**Z EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="89128-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="89128-140">**Z EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="89128-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="89128-141">Następnie w pliku .cs tag strony w `EngagementPageOverlay` zamiast `EngagementPage` i zaimportować `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="89128-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="89128-142">Zastąp `EngagementPage` z `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="89128-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="89128-143">**Z EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="89128-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="89128-144">**Z EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="89128-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="89128-145">Hello nakładki zaangażowania dodaje `Grid` element na stronie składa się z układ i hello dwa `WebView` elementy co hello banner i hello jeden z nich hello międzysegmentowe widoku.</span><span class="sxs-lookup"><span data-stu-id="89128-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="89128-146">Można dostosowywać elementy nakładki hello bezpośrednio w hello `EngagementPageOverlay.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="89128-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="89128-147">Integracja ręczna widoki sieci Web</span><span class="sxs-lookup"><span data-stu-id="89128-147">Web views manual integration</span></span>
<span data-ttu-id="89128-148">Reach będzie wyszukiwanie stron dla hello dwa `WebView` elementy odpowiada za wyświetlanie banera hello i hello międzysegmentowe widoku.</span><span class="sxs-lookup"><span data-stu-id="89128-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="89128-149">Witaj, co ma toodo jest tooadd tylko tych dwóch `WebView` elementy gdzieś na swoich stronach Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="89128-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="89128-150">W tym hello przykład `WebView` elementy są rozciągane toofit ich kontenera, który automatycznie ponownie rozmiary je w przypadku zmiany rozmiaru ekranu obrotu lub okno.</span><span class="sxs-lookup"><span data-stu-id="89128-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="89128-151">Koniecznie tookeep hello tej samej nazwy `engagement_notification_content` i `engagement_announcement_content` dla hello `WebView` elementów.</span><span class="sxs-lookup"><span data-stu-id="89128-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="89128-152">Zasięg identyfikuje je według nazwy.</span><span class="sxs-lookup"><span data-stu-id="89128-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="89128-153">Dojście datapush (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="89128-153">Handle datapush (optional)</span></span>
<span data-ttu-id="89128-154">Aby wypychania Twojej aplikacji toobe tooreceive stanie Reach danych, masz tooimplement dwa zdarzenia hello EngagementReach klasy:</span><span class="sxs-lookup"><span data-stu-id="89128-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="89128-155">W pliku App.xaml.cs w Konstruktorze App() hello należy dodać:</span><span class="sxs-lookup"><span data-stu-id="89128-155">In App.xaml.cs in hello App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="89128-156">Wywołanie zwrotne hello każdego metoda zwraca wartość logiczną jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="89128-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="89128-157">Zaangażowania wysyła opinii tooits zaplecza po wysłaniu hello wypychanie danych.</span><span class="sxs-lookup"><span data-stu-id="89128-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="89128-158">Jeśli wywołanie zwrotne hello zwraca wartość false, hello `exit` opinii będzie wysyłania.</span><span class="sxs-lookup"><span data-stu-id="89128-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="89128-159">W przeciwnym razie będzie `action`.</span><span class="sxs-lookup"><span data-stu-id="89128-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="89128-160">Jeśli bez wywołania zwrotnego ustawiono dla zdarzeń hello, hello `drop` Opinia zostanie zwrócony tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="89128-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="89128-161">Zaangażowania nie jest możliwe tooreceive wielokrotności opinie do wypychania danych.</span><span class="sxs-lookup"><span data-stu-id="89128-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="89128-162">Jeśli planujesz tooset kilka programów obsługi zdarzeń, należy pamiętać, że opinia hello będzie odpowiadać toohello ostatnią wysłane.</span><span class="sxs-lookup"><span data-stu-id="89128-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="89128-163">W takim przypadku zalecamy tooalways zwraca hello tego samego tooavoid wartość o mylące opinii na powitania frontonu.</span><span class="sxs-lookup"><span data-stu-id="89128-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="89128-164">Dostosowywanie interfejsu użytkownika (opcjonalne)</span><span class="sxs-lookup"><span data-stu-id="89128-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="89128-165">Pierwszym krokiem</span><span class="sxs-lookup"><span data-stu-id="89128-165">First step</span></span>
<span data-ttu-id="89128-166">Zezwolimy toocustomize hello reach interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89128-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="89128-167">toodo więc z toocreate podklasą hello `EngagementReachHandler` klasy.</span><span class="sxs-lookup"><span data-stu-id="89128-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="89128-168">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="89128-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="89128-169">Następnie ustaw hello zawartość hello `EngagementReach.Instance.Handler` pole z niestandardowego obiektu w Twojej `App.xaml.cs` klasa w hello `App()` — metoda.</span><span class="sxs-lookup"><span data-stu-id="89128-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="89128-170">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="89128-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="89128-171">Domyślnie program zaangażowania używa własną implementację `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="89128-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="89128-172">Nie masz toocreate własny, a jeśli tak zrobisz, nie masz toooverride każdej metody.</span><span class="sxs-lookup"><span data-stu-id="89128-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="89128-173">Witaj domyślne zachowanie to obiektu podstawowego tooselect hello zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="89128-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="89128-174">Widok sieci Web</span><span class="sxs-lookup"><span data-stu-id="89128-174">Web View</span></span>
<span data-ttu-id="89128-175">Domyślnie Reach będzie używać zasobów osadzonych hello hello DLL toodisplay hello powiadomień i strony.</span><span class="sxs-lookup"><span data-stu-id="89128-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="89128-176">tooprovide pełne możliwości dostosowywania używany tylko w widoku sieci web.</span><span class="sxs-lookup"><span data-stu-id="89128-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="89128-177">Układy toocustomize należy zastąpić bezpośrednio plików zasobów hello `EngagementAnnouncement.html` i `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="89128-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="89128-178">Engagement wymaga cały kod w `<body></body>` toorun poprawnie.</span><span class="sxs-lookup"><span data-stu-id="89128-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="89128-179">Możesz dodać tag zewnętrzne, ale `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="89128-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="89128-180">Jednak można określić toouse własnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="89128-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="89128-181">Można zastąpić `EngagementReachHandler` metody w Twojej toouse zaangażowania tootell podklasy układów, ale przyjmują mechanizmu zaangażowania hello tooembedded szczególną uwagę:</span><span class="sxs-lookup"><span data-stu-id="89128-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="89128-182">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="89128-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="89128-183">Domyślnie jest AnnouncementHTML `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="89128-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="89128-184">Reprezentuje hello plik html, który projektowania zawartości hello wiadomości wypychanych (tekst anonsu, anoucement sieci Web i anonsu sondowania).</span><span class="sxs-lookup"><span data-stu-id="89128-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="89128-185">Jest AnnouncementName `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="89128-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="89128-186">To nazwa hello hello projektu widoku sieci Web na stronie xaml.</span><span class="sxs-lookup"><span data-stu-id="89128-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="89128-187">Jest NotfificationHTML `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="89128-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="89128-188">Reprezentuje hello plik html, który projekt hello powiadomienie o wiadomości wypychanych.</span><span class="sxs-lookup"><span data-stu-id="89128-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="89128-189">Jest NotfificationName `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="89128-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="89128-190">To nazwa hello hello projektu widoku sieci Web na stronie xaml.</span><span class="sxs-lookup"><span data-stu-id="89128-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="89128-191">Dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="89128-191">Customization</span></span>
<span data-ttu-id="89128-192">Możesz dostosować powiadomień i anonsu widoku sieci web ma użytkownik w przypadku zachowania obiektu zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="89128-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="89128-193">Zajmie się obiekt widoku sieci Web jest opisano trzy razy — Witaj po raz pierwszy w Twojej xaml drugi raz w pliku .cs w metodzie "setwebview()" hello, a trzeci czas w pliku html hello.</span><span class="sxs-lookup"><span data-stu-id="89128-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="89128-194">W Twojej xaml opisywane hello bieżącego układu graficznego widoku sieci Web składnika.</span><span class="sxs-lookup"><span data-stu-id="89128-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="89128-195">W pliku .cs można zdefiniować "setwebview()", w którym można ustawić hello wymiaru webview dwóch hello (powiadomienia, anons).</span><span class="sxs-lookup"><span data-stu-id="89128-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="89128-196">Jest bardzo skuteczne, gdy aplikacja hello jest zmiana rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="89128-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="89128-197">W pliku html zaangażowania hello nasz opisano hello webview zawartości, projektowania i hello pozycji elementy między sobą.</span><span class="sxs-lookup"><span data-stu-id="89128-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="89128-198">Uruchamianie wiadomości</span><span class="sxs-lookup"><span data-stu-id="89128-198">Launch message</span></span>
<span data-ttu-id="89128-199">Gdy użytkownik kliknie powiadomienie systemowe (alert), Engagement uruchamia aplikacji hello, zawartość hello obciążenia hello push wiadomości i wyświetlenia strony hello hello odpowiedniego kampanii.</span><span class="sxs-lookup"><span data-stu-id="89128-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="89128-200">Występuje opóźnienie między uruchamiania hello hello aplikacji i hello wyświetlania strony hello (w zależności od szybkości hello sieci).</span><span class="sxs-lookup"><span data-stu-id="89128-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="89128-201">tooindicate toohello użytkownika, który wystąpił podczas ładowania, należy podać visual informacji, takich jak pasek postępu lub wskaźnik postępu.</span><span class="sxs-lookup"><span data-stu-id="89128-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="89128-202">Zaangażowania nie może obsłużyć, ale udostępnia kilka programy obsługi dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="89128-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="89128-203">Dodaj wywołanie zwrotne hello tooimplement, w pliku App.xaml.cs "Publicznego App() {}":</span><span class="sxs-lookup"><span data-stu-id="89128-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="89128-204">Wywołanie zwrotne hello można ustawić w metodzie "Publicznego App() {}" z `App.xaml.cs` plików, najlepiej przed hello `EngagementReach.Instance.Init()` wywołania.</span><span class="sxs-lookup"><span data-stu-id="89128-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="89128-205">Każdy program obsługi jest wywoływana przez hello wątku interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89128-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="89128-206">Nie masz tooworry, korzystając z MessageBox lub coś związanych z interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89128-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="89128-207"><a id="push-channel-sharing"></a>Wypychanie do udostępniania kanału</span><span class="sxs-lookup"><span data-stu-id="89128-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="89128-208">Jeśli używasz powiadomień wypychanych do innych celów w aplikacji należy kanału wypychanych hello toouse udostępniania funkcji hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="89128-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="89128-209">Jest to wypychania tooavoid pominięte.</span><span class="sxs-lookup"><span data-stu-id="89128-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="89128-210">Możesz podać własne wypychania toohello Reach usługi Engagement inicjacji kanału.</span><span class="sxs-lookup"><span data-stu-id="89128-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="89128-211">Witaj zestawu SDK będą używać go zamiast nowego żądania.</span><span class="sxs-lookup"><span data-stu-id="89128-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="89128-212">Zaktualizuj hello inicjowania Reach usługi Engagement za pomocą wypychania kanału w hello `InitEngagement` metody z hello `App.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="89128-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="89128-213">Alternatywnie wystarczy tooconsume hello push kanału po zainicjowaniu Reach hello wywołania zwrotnego można ustawić w kanale wypychania hello tooget Reach usługi Engagement po jego utworzeniu przez hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="89128-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="89128-214">Ustaw wywołanie zwrotne w dowolnym miejscu **po** hello inicjowania zasięgu:</span><span class="sxs-lookup"><span data-stu-id="89128-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="89128-215">Porada schematu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="89128-215">Custom scheme tip</span></span>
<span data-ttu-id="89128-216">Udostępniamy Użyj schematu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="89128-216">We provide custom scheme use.</span></span> <span data-ttu-id="89128-217">Możesz wysłać innego typu identyfikatora URI z toobe frontonu zaangażowania używane w aplikacji usługi engagement.</span><span class="sxs-lookup"><span data-stu-id="89128-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="89128-218">Domyślny schemat, takich jak `http, ftp, ...` są zarządzanie przez system Windows, zostanie okno wierszu są zainstalowane na urządzeniu domyślnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89128-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="89128-219">Można również utworzyć własny niestandardowy schemat dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89128-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="89128-220">Witaj prosty sposób tooset schematu niestandardowego w aplikacji jest tooopen Twojego `Package.appxmanifest` Przejdź w `Declarations` panelu.</span><span class="sxs-lookup"><span data-stu-id="89128-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="89128-221">Wybierz `Protocol` w hello Przewiń dostępne deklaracje i dodać go.</span><span class="sxs-lookup"><span data-stu-id="89128-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="89128-222">Edytuj hello `Name` pola z Twojej nowy protokół żądaną nazwę.</span><span class="sxs-lookup"><span data-stu-id="89128-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="89128-223">Teraz toouse tego protokołu, Edytuj Twojej `App.xaml.cs` z hello `OnActivated` metody i nie zapomnij zaangażowania tooinitialize tutaj również:</span><span class="sxs-lookup"><span data-stu-id="89128-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

