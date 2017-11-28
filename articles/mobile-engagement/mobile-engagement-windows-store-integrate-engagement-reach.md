---
title: "Integracja zestawu SDK osiągnąć uniwersalnych aplikacji systemu Windows"
description: "Integrowanie dotarcia do usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
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
ms.openlocfilehash: 9311e998e67d8d0d56da68fc9460df32ce7ce5a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="f3fef-103">Integracja zestawu SDK osiągnąć uniwersalnych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f3fef-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="f3fef-104">Wykonaj procedury integracji opisane w sekcji [Windows Universal integracji zestawu SDK usługi Engagement](mobile-engagement-windows-store-integrate-engagement.md) przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="f3fef-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="f3fef-105">Osadzanie SDK Reach usługi Engagement w projekcie uniwersalnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f3fef-105">Embed the Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="f3fef-106">Nie ma nic do dodania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-106">You do not have anything to add.</span></span> <span data-ttu-id="f3fef-107">`EngagementReach`referencje i zasoby są już w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f3fef-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="f3fef-108">Można dostosować obrazy znajdujące się w `Resources` folderu projektu, szczególnie ikona marki (domyślnie tej ikony Engagement).</span><span class="sxs-lookup"><span data-stu-id="f3fef-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span> <span data-ttu-id="f3fef-109">W aplikacjach uniwersalnych można również przenosić `Resources` folder dla projektu udostępnionego, aby udostępnić jego zawartość między aplikacjami, ale będą musieli zachować `Resources\EngagementConfiguration.xml` pliku w domyślnej lokalizacji, ponieważ jest on zależny platformy.</span><span class="sxs-lookup"><span data-stu-id="f3fef-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-the-windows-notification-service"></a><span data-ttu-id="f3fef-110">Włącz usługę powiadomień systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f3fef-110">Enable the Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="f3fef-111">Windows 8.x i Windows Phone 8.1 tylko</span><span class="sxs-lookup"><span data-stu-id="f3fef-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="f3fef-112">Aby można było używać **usługi powiadomień systemu Windows** (określanych jako WNS) w Twojej `Package.appxmanifest` plików na `Application UI` kliknij `All Image Assets` w polu bot po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="f3fef-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span></span> <span data-ttu-id="f3fef-113">Po prawej stronie pola w `Notifications`, zmień `toast capable` z `(not set)` do `(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="f3fef-114">Wszystkie platformy</span><span class="sxs-lookup"><span data-stu-id="f3fef-114">All platforms</span></span>
<span data-ttu-id="f3fef-115">Należy zsynchronizować aplikację do swojego konta Microsoft i platformy zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span></span> <span data-ttu-id="f3fef-116">Dla tego należy utworzyć konto lub zaloguj się na [Centrum deweloperów systemu windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="f3fef-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="f3fef-117">Po wykonaniu tej Tworzenie nowej aplikacji i znajdowanie identyfikatora SID i klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="f3fef-117">After that create a new application and find the SID and secret key.</span></span> <span data-ttu-id="f3fef-118">Na frontonie zaangażowania przejdź na ustawienia aplikacji w `native push` i Wklej swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="f3fef-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="f3fef-119">Następnie kliknij prawym przyciskiem myszy projekt, wybierz opcję `store` i `Associate App with the Store...`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span></span> <span data-ttu-id="f3fef-120">Wystarczy wybrać aplikację przed ma utworzyć, aby ją zsynchronizować.</span><span class="sxs-lookup"><span data-stu-id="f3fef-120">You just need to select the application you have create before to synchronize it.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="f3fef-121">Inicjowanie Reach usługi Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="f3fef-121">Initialize the Engagement Reach SDK</span></span>
<span data-ttu-id="f3fef-122">Modyfikowanie `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="f3fef-122">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="f3fef-123">Wstaw `EngagementReach.Instance.Init` tuż po `EngagementAgent.Instance.Init` w Twojej `InitEngagement` metody:</span><span class="sxs-lookup"><span data-stu-id="f3fef-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="f3fef-124">`EngagementReach.Instance.Init` Działa w dedykowanym wątku.</span><span class="sxs-lookup"><span data-stu-id="f3fef-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="f3fef-125">Nie masz zrobić samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="f3fef-125">You do not have to do it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="f3fef-126">Jeśli używasz powiadomień wypychanych w innym miejscu w aplikacji, trzeba [udostępnianie kanału wypychania](#push-channel-sharing) z Reach usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="f3fef-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="f3fef-127">Integracja</span><span class="sxs-lookup"><span data-stu-id="f3fef-127">Integration</span></span>
<span data-ttu-id="f3fef-128">Engagement udostępnia dwa sposoby dodawania międzysegmentowe widoków w przypadku anonsów i sond i Reach transparentach w aplikacji w aplikacji: integracja z nakładką i integracja ręczne widoki sieci web.</span><span class="sxs-lookup"><span data-stu-id="f3fef-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span></span> <span data-ttu-id="f3fef-129">Nie należy łączyć oba podejścia na tej samej stronie.</span><span class="sxs-lookup"><span data-stu-id="f3fef-129">You should not combine both approach on the same page.</span></span>

<span data-ttu-id="f3fef-130">Wybór między dwoma integracji można podsumować w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="f3fef-130">The choice between the two integration could be summarized this way:</span></span>

* <span data-ttu-id="f3fef-131">Integracja z nakładką może wybrać, jeśli strony już dziedziczy od agenta `EngagementPage`, jest wystarczy zastępowanie `EngagementPage` przez `EngagementPageOverlay` i `xmlns:engagement="using:Microsoft.Azure.Engagement"` przez `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` na swoich stronach.</span><span class="sxs-lookup"><span data-stu-id="f3fef-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="f3fef-132">Możesz wybrać widoki sieci web integracji ręczne Aby precyzyjnie umieścić osiągnąć interfejsu użytkownika w ramach strony lub jeśli nie chcesz dodać kolejny poziom dziedziczenia do stron.</span><span class="sxs-lookup"><span data-stu-id="f3fef-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="f3fef-133">Integracja z nakładką</span><span class="sxs-lookup"><span data-stu-id="f3fef-133">Overlay integration</span></span>
<span data-ttu-id="f3fef-134">Nakładka zaangażowania dynamicznie dodaje elementy interfejsu użytkownika używana do wyświetlania kampanie Zasięgowe na stronie.</span><span class="sxs-lookup"><span data-stu-id="f3fef-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span></span> <span data-ttu-id="f3fef-135">Jeśli nakładki nie własnych układu należy rozważyć widoki sieci web integracji ręczne zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f3fef-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span></span>

<span data-ttu-id="f3fef-136">W przypadku zmiany pliku .xaml `EngagementPage` odwołanie do`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="f3fef-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span></span>

* <span data-ttu-id="f3fef-137">Dodaj deklaracje przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="f3fef-137">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="f3fef-138">Zastąp `engagement:EngagementPage` z `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="f3fef-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="f3fef-139">**Z EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="f3fef-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="f3fef-140">**Z EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="f3fef-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="f3fef-141">Następnie w pliku .cs tag strony w `EngagementPageOverlay` zamiast `EngagementPage` i zaimportować `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="f3fef-142">Zastąp `EngagementPage` z `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="f3fef-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="f3fef-143">**Z EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="f3fef-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="f3fef-144">**Z EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="f3fef-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="f3fef-145">Dodaje nakładki Engagement `Grid` element na stronie składa się z układu i dwa `WebView` elementy jeden na banerze i drugi dla widoku międzysegmentowe.</span><span class="sxs-lookup"><span data-stu-id="f3fef-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span></span>

<span data-ttu-id="f3fef-146">Można dostosowywać elementy nakładki bezpośrednio w `EngagementPageOverlay.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="f3fef-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="f3fef-147">Integracja ręczna widoki sieci Web</span><span class="sxs-lookup"><span data-stu-id="f3fef-147">Web views manual integration</span></span>
<span data-ttu-id="f3fef-148">Reach będzie wyszukiwanie stron dla dwóch `WebView` elementy odpowiada za wyświetlanie banera i międzysegmentowe widoku.</span><span class="sxs-lookup"><span data-stu-id="f3fef-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span></span> <span data-ttu-id="f3fef-149">Jedyną operacją, musisz wykonać jest dodanie tych dwóch `WebView` elementy gdzieś na swoich stronach Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="f3fef-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="f3fef-150">W tym przykładzie `WebView` elementy są rozciągany w celu dopasowania ich kontenera, który automatycznie ponownie rozmiary je w przypadku zmiany rozmiaru ekranu obrotu lub okno.</span><span class="sxs-lookup"><span data-stu-id="f3fef-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="f3fef-151">Ważne jest, aby zachować tego samego nazewnictwa `engagement_notification_content` i `engagement_announcement_content` dla `WebView` elementów.</span><span class="sxs-lookup"><span data-stu-id="f3fef-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span></span> <span data-ttu-id="f3fef-152">Zasięg identyfikuje je według nazwy.</span><span class="sxs-lookup"><span data-stu-id="f3fef-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="f3fef-153">Dojście datapush (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="f3fef-153">Handle datapush (optional)</span></span>
<span data-ttu-id="f3fef-154">Możliwość odbierania Reach wypychania danych aplikacji, należy zaimplementować dwa zdarzenia klasy EngagementReach:</span><span class="sxs-lookup"><span data-stu-id="f3fef-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

<span data-ttu-id="f3fef-155">W pliku App.xaml.cs w Konstruktorze App() należy dodać:</span><span class="sxs-lookup"><span data-stu-id="f3fef-155">In App.xaml.cs in the App() constructor add:</span></span>

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

<span data-ttu-id="f3fef-156">Widać, że wywołanie zwrotne każdej metody zwraca wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="f3fef-156">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="f3fef-157">Zaangażowania wysyła opinię do jego zaplecza po wysłaniu wypychanie danych.</span><span class="sxs-lookup"><span data-stu-id="f3fef-157">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="f3fef-158">Jeśli wywołanie zwrotne zwraca wartość FAŁSZ, `exit` opinii będzie wysyłania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-158">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="f3fef-159">W przeciwnym razie będzie `action`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="f3fef-160">Jeśli ustawiono bez wywołania zwrotnego dla zdarzeń, `drop` Opinia zostanie zwrócony do zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="f3fef-161">Zaangażowania nie będzie mógł odbierać opinie wielokrotności do wypychania danych.</span><span class="sxs-lookup"><span data-stu-id="f3fef-161">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="f3fef-162">Jeśli planujesz ustawić kilka programów obsługi na zdarzenie, należy pamiętać, że opinii będzie odpowiadać ostatniej jedną wysyłane.</span><span class="sxs-lookup"><span data-stu-id="f3fef-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="f3fef-163">W takim przypadku zaleca się zawsze zwraca tę samą wartość, aby uniknąć mylące opinii na frontonu.</span><span class="sxs-lookup"><span data-stu-id="f3fef-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="f3fef-164">Dostosowywanie interfejsu użytkownika (opcjonalne)</span><span class="sxs-lookup"><span data-stu-id="f3fef-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="f3fef-165">Pierwszym krokiem</span><span class="sxs-lookup"><span data-stu-id="f3fef-165">First step</span></span>
<span data-ttu-id="f3fef-166">Firma Microsoft umożliwiają dostosowanie reach interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3fef-166">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="f3fef-167">Aby to zrobić, należy utworzyć podklasy `EngagementReachHandler` klasy.</span><span class="sxs-lookup"><span data-stu-id="f3fef-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="f3fef-168">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="f3fef-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="f3fef-169">Następnie ustaw zawartość `EngagementReach.Instance.Handler` pole z niestandardowego obiektu w Twojej `App.xaml.cs` klas w ramach `App()` — metoda.</span><span class="sxs-lookup"><span data-stu-id="f3fef-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span></span>

<span data-ttu-id="f3fef-170">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="f3fef-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="f3fef-171">Domyślnie program zaangażowania używa własną implementację `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="f3fef-172">Nie trzeba tworzyć własne, a jeśli tak zrobisz, nie trzeba co metoda musi zostać zastąpiona.</span><span class="sxs-lookup"><span data-stu-id="f3fef-172">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="f3fef-173">Domyślnym zachowaniem jest wybierz obiekt podstawowy zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-173">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="f3fef-174">Widok sieci Web</span><span class="sxs-lookup"><span data-stu-id="f3fef-174">Web View</span></span>
<span data-ttu-id="f3fef-175">Domyślnie Reach zostaną użyte zasoby osadzone biblioteki dll do wyświetlania powiadomień i stron.</span><span class="sxs-lookup"><span data-stu-id="f3fef-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="f3fef-176">Aby zapewnić pełne dostosowywanie możliwości używamy są tylko widoku sieci web.</span><span class="sxs-lookup"><span data-stu-id="f3fef-176">To provide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="f3fef-177">Jeśli chcesz dostosować układów bezpośrednio zastąpienie plików zasobów `EngagementAnnouncement.html` i `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="f3fef-178">Engagement wymaga cały kod w `<body></body>` by działała poprawnie.</span><span class="sxs-lookup"><span data-stu-id="f3fef-178">Engagement needs all code in `<body></body>` to run correctly.</span></span> <span data-ttu-id="f3fef-179">Możesz dodać tag zewnętrzne, ale `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="f3fef-180">Można korzystać z własnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f3fef-180">However, you can decide to use your own resources.</span></span>

<span data-ttu-id="f3fef-181">Można zastąpić `EngagementReachHandler` metod w Twojej podklasy zaangażowania używać układów, ale należy sprawdzić osadzonych mechanizm engagement:</span><span class="sxs-lookup"><span data-stu-id="f3fef-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span></span>

<span data-ttu-id="f3fef-182">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="f3fef-182">**Sample Code :**</span></span>

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


<span data-ttu-id="f3fef-183">Domyślnie jest AnnouncementHTML `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="f3fef-184">Reprezentuje plik html, który projektowania zawartości wiadomości wypychanych (tekst anonsu, anoucement sieci Web i anonsu sondowania).</span><span class="sxs-lookup"><span data-stu-id="f3fef-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="f3fef-185">Jest AnnouncementName `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="f3fef-186">Jest to nazwa projektu widoku sieci Web ze strony xaml.</span><span class="sxs-lookup"><span data-stu-id="f3fef-186">It is the name of the webview design in your xaml page.</span></span>

<span data-ttu-id="f3fef-187">Jest NotfificationHTML `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="f3fef-188">Reprezentuje plik html, który zaprojektować powiadomienie o wiadomości wypychanych.</span><span class="sxs-lookup"><span data-stu-id="f3fef-188">It represents the html file that design the notification of a push message.</span></span> <span data-ttu-id="f3fef-189">Jest NotfificationName `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="f3fef-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="f3fef-190">Jest to nazwa projektu widoku sieci Web ze strony xaml.</span><span class="sxs-lookup"><span data-stu-id="f3fef-190">It is the name of the webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="f3fef-191">Dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="f3fef-191">Customization</span></span>
<span data-ttu-id="f3fef-192">Możesz dostosować powiadomień i anonsu widoku sieci web ma użytkownik w przypadku zachowania obiektu zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="f3fef-193">Zwróć uwagę na to, że webview obiektu opisano trzy razy — po raz pierwszy w Twojej xaml, w pliku .cs w metodzie "setwebview()" po raz drugi i trzeci czasu w pliku html.</span><span class="sxs-lookup"><span data-stu-id="f3fef-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span></span>

* <span data-ttu-id="f3fef-194">W Twojej xaml opisywane bieżącego składnika układu graficznego w widoku sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f3fef-194">In your xaml you describe the current graphical layout webview component.</span></span>
* <span data-ttu-id="f3fef-195">W pliku .cs można zdefiniować "setwebview()", w którym można ustawić wymiar dwóch widoku sieci Web (powiadomienia, anons).</span><span class="sxs-lookup"><span data-stu-id="f3fef-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span></span> <span data-ttu-id="f3fef-196">Jest bardzo skuteczne, gdy aplikacja jest zmiana rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="f3fef-196">It is very effective when the application is resizing.</span></span>
* <span data-ttu-id="f3fef-197">W pliku html zaangażowania przedstawione zawartość widoku sieci Web, projektowanie i pozycji elementów między sobą.</span><span class="sxs-lookup"><span data-stu-id="f3fef-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="f3fef-198">Uruchamianie wiadomości</span><span class="sxs-lookup"><span data-stu-id="f3fef-198">Launch message</span></span>
<span data-ttu-id="f3fef-199">Gdy użytkownik kliknie powiadomienie systemowe (alert), Engagement uruchamia aplikację, Załaduj zawartość wiadomości wypychanych i wyświetlenia strony do odpowiedniego kampanii.</span><span class="sxs-lookup"><span data-stu-id="f3fef-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="f3fef-200">Występuje opóźnienie między uruchamiania aplikacji i wyświetlania strony (w zależności od szybkości sieci).</span><span class="sxs-lookup"><span data-stu-id="f3fef-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="f3fef-201">Aby wskazać użytkownikowi coś ładowania, należy podać visual informacji, takich jak pasek postępu lub wskaźnik postępu.</span><span class="sxs-lookup"><span data-stu-id="f3fef-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="f3fef-202">Zaangażowania nie może obsłużyć, ale udostępnia kilka programy obsługi dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="f3fef-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="f3fef-203">Aby zaimplementować metodę wywołania zwrotnego, w pliku App.xaml.cs "{} App() publiczny" Dodaj:</span><span class="sxs-lookup"><span data-stu-id="f3fef-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* The application has launched and the content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* The application has finished loading the content and the page
             * is about to be displayed.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* The content has been loaded, but an error has occurred.
             * You can provide an information to the user.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="f3fef-204">Wywołania zwrotnego można ustawić w metodzie "Publicznego App() {}" z `App.xaml.cs` plików, najlepiej przed `EngagementReach.Instance.Init()` wywołania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="f3fef-205">Każdy program obsługi jest wywoływana przez wątek interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3fef-205">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="f3fef-206">Masz nie martw się, używając MessageBox lub coś związanych z interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f3fef-206">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="f3fef-207"><a id="push-channel-sharing"></a>Wypychanie do udostępniania kanału</span><span class="sxs-lookup"><span data-stu-id="f3fef-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="f3fef-208">Jeśli używane są powiadomienia wypychane do innych celów w aplikacji następnie należy użyć kanału wypychanych udostępniania funkcji zestawu SDK usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="f3fef-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span></span> <span data-ttu-id="f3fef-209">Pozwoli to uniknąć brakujących wypychania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-209">This is to avoid missed push.</span></span>

* <span data-ttu-id="f3fef-210">Możesz podać własne kanału wypychania do inicjowania Reach usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="f3fef-210">You can provide your own push channel to the Engagement Reach initialization.</span></span> <span data-ttu-id="f3fef-211">Zestaw SDK będą używać go zamiast nowego żądania.</span><span class="sxs-lookup"><span data-stu-id="f3fef-211">The SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="f3fef-212">Zaktualizuj inicjowania Reach usługi Engagement za pomocą wypychania kanału w `InitEngagement` metody z `App.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="f3fef-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="f3fef-213">Alternatywnie Jeśli chcesz, aby korzystać z kanału wypychanych po możesz inicjowania Reach można ustawiać wywołanie zwrotne Reach usługi Engagement uzyskać kanału wypychanych raz jest tworzona przez zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="f3fef-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span></span>

<span data-ttu-id="f3fef-214">Ustaw wywołanie zwrotne w dowolnym miejscu **po** inicjowania zasięgu:</span><span class="sxs-lookup"><span data-stu-id="f3fef-214">Set your callback at any place **after** the Reach initialization :</span></span>

    /* Set action on the SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* The forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="f3fef-215">Porada schematu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="f3fef-215">Custom scheme tip</span></span>
<span data-ttu-id="f3fef-216">Udostępniamy Użyj schematu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="f3fef-216">We provide custom scheme use.</span></span> <span data-ttu-id="f3fef-217">Możesz wysłać innego typu identyfikatora URI z frontonu zaangażowania do użycia w aplikacji usługi engagement.</span><span class="sxs-lookup"><span data-stu-id="f3fef-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span></span> <span data-ttu-id="f3fef-218">Domyślny schemat, takich jak `http, ftp, ...` są zarządzanie przez system Windows, zostanie okno wierszu są zainstalowane na urządzeniu domyślnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f3fef-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="f3fef-219">Można również utworzyć własny niestandardowy schemat dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f3fef-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="f3fef-220">Prosty sposób, aby ustawić schematu niestandardowego w aplikacji jest otwarcie Twojej `Package.appxmanifest` Przejdź w `Declarations` panelu.</span><span class="sxs-lookup"><span data-stu-id="f3fef-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="f3fef-221">Wybierz `Protocol` w deklaracjach dostępne przewiń okno i dodaj go.</span><span class="sxs-lookup"><span data-stu-id="f3fef-221">Select `Protocol` in the Available Declarations scroll box and add it.</span></span> <span data-ttu-id="f3fef-222">Edytuj `Name` pola z Twojej nowy protokół żądaną nazwę.</span><span class="sxs-lookup"><span data-stu-id="f3fef-222">Edit the `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="f3fef-223">Aby użyć tego protokołu, edytować Twojej `App.xaml.cs` z `OnActivated` metody i nie zapomnij inicjowania usługi engagement tutaj również:</span><span class="sxs-lookup"><span data-stu-id="f3fef-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action to do when app is launch

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

