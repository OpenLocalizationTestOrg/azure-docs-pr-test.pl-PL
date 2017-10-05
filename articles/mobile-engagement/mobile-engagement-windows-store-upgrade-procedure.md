---
title: Procedury uaktualniania uniwersalnych aplikacji systemu Windows SDK
description: "Procedury uaktualniania systemu Windows Universal SDK aplikacji dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="55d95-103">Procedury uaktualniania uniwersalnych aplikacji systemu Windows SDK</span><span class="sxs-lookup"><span data-stu-id="55d95-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="55d95-104">Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy wziąć pod uwagę następujące kwestie, podczas uaktualniania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="55d95-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="55d95-105">Należy wykonać kilka procedur, jeśli pominięte kilka wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="55d95-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="55d95-106">Na przykład w przypadku migrowania z 0.10.1 do 0.11.0, należy najpierw wykonać procedurę "od 0.9.0 do 0.10.1" następnie procedury "od 0.10.1 do 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="55d95-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="55d95-107">Z 3.3.0 do 3.4.0</span><span class="sxs-lookup"><span data-stu-id="55d95-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="55d95-108">Dzienniki testów</span><span class="sxs-lookup"><span data-stu-id="55d95-108">Test logs</span></span>
<span data-ttu-id="55d95-109">Dzienniki konsoli utworzonego przez zestaw SDK można teraz włączone/wyłączone/odfiltrowane.</span><span class="sxs-lookup"><span data-stu-id="55d95-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="55d95-110">Aby dostosować to, zaktualizuj właściwość `EngagementAgent.Instance.TestLogEnabled` do jednej z dostępnych wartości `EngagementTestLogLevel` wyliczenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="55d95-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="55d95-111">Zasoby</span><span class="sxs-lookup"><span data-stu-id="55d95-111">Resources</span></span>
<span data-ttu-id="55d95-112">Udoskonalono nakładki Reach.</span><span class="sxs-lookup"><span data-stu-id="55d95-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="55d95-113">Jest ona częścią zasoby pakietu NuGet zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="55d95-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="55d95-114">Podczas uaktualniania do nowej wersji zestawu SDK można wybrać, czy chcesz zachować istniejące pliki z folderu nakładki zasobów lub nie:</span><span class="sxs-lookup"><span data-stu-id="55d95-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="55d95-115">Jeśli poprzednie nakładki działa dla Ciebie lub jest integrowany `WebView` elementy ręcznie następnie chcesz zachować istniejących plików, to nadal będzie działać.</span><span class="sxs-lookup"><span data-stu-id="55d95-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="55d95-116">Jeśli chcesz zaktualizować nowe nakładce, po prostu zastąpić całego `overlay` folder z Twoich zasobów nową z pakietu SDK (aplikacji platformy uniwersalnej systemu Windows: po uaktualnieniu, możesz pobrać ze strony % USERPROFILE % nowy folder nakładki\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="55d95-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="55d95-117">Przy użyciu nowego nakładki zastąpią wszelkie dostosowania z poprzedniej wersji.</span><span class="sxs-lookup"><span data-stu-id="55d95-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="55d95-118">Z 3.2.0 do 3.3.0</span><span class="sxs-lookup"><span data-stu-id="55d95-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="55d95-119">Zasoby</span><span class="sxs-lookup"><span data-stu-id="55d95-119">Resources</span></span>
<span data-ttu-id="55d95-120">Ten krok dotyczy tylko zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="55d95-120">This step concerns customized resources only.</span></span> <span data-ttu-id="55d95-121">Jeśli dostosowano zasobów udostępnianych przez zestaw SDK (html, obrazy, nakładki) następnie trzeba kopii zapasowej je przed uaktualnieniem i ponownie zastosuj dostosowanie uaktualnionego zasobów.</span><span class="sxs-lookup"><span data-stu-id="55d95-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="55d95-122">Z 3.1.0 do 3.2.0</span><span class="sxs-lookup"><span data-stu-id="55d95-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="55d95-123">Zasoby</span><span class="sxs-lookup"><span data-stu-id="55d95-123">Resources</span></span>
<span data-ttu-id="55d95-124">Ten krok dotyczy tylko zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="55d95-124">This step concerns customized resources only.</span></span> <span data-ttu-id="55d95-125">Jeśli dostosowano zasobów udostępnianych przez zestaw SDK (html, obrazy, nakładki) następnie trzeba kopii zapasowej je przed uaktualnieniem i ponownie zastosuj dostosowanie uaktualnionego zasobów.</span><span class="sxs-lookup"><span data-stu-id="55d95-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="55d95-126">Integracja z widoku sieci Web</span><span class="sxs-lookup"><span data-stu-id="55d95-126">Webview integration</span></span>
<span data-ttu-id="55d95-127">Niektóre ulepszenia zgodne urządzenie różnych rozmiarach zostały wprowadzone w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="55d95-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="55d95-128">Upewnij się, że integracją z widoku sieci Web zgodne z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="55d95-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="55d95-129">W Twojej XAML strony ():</span><span class="sxs-lookup"><span data-stu-id="55d95-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="55d95-130">W pliku skojarzone CS:</span><span class="sxs-lookup"><span data-stu-id="55d95-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="55d95-131">Z 2.0.0 do 3.0.0</span><span class="sxs-lookup"><span data-stu-id="55d95-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="55d95-132">Zasoby</span><span class="sxs-lookup"><span data-stu-id="55d95-132">Resources</span></span>
<span data-ttu-id="55d95-133">Ten krok dotyczy tylko zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="55d95-133">This step concerns customized resources only.</span></span> <span data-ttu-id="55d95-134">Jeśli dostosowano zasobów udostępnianych przez zestaw SDK (html, obrazy, nakładki) następnie trzeba kopii zapasowej je przed uaktualnieniem i ponownie zastosuj dostosowanie uaktualnionego zasobów.</span><span class="sxs-lookup"><span data-stu-id="55d95-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="55d95-135">Z 1.1.1 do 2.0.0</span><span class="sxs-lookup"><span data-stu-id="55d95-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="55d95-136">Poniżej opisano sposób migracji integracji zestawu SDK usługi Capptain oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="55d95-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="55d95-137">Capptain i usługi Mobile Engagement nie są takie same usługi i procedury przedstawionej poniżej tylko prezentuje sposób migracji aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="55d95-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="55d95-138">Migrowanie zestawu SDK w aplikacji wiadomości nie będzie migrację danych z serwerów Capptain do serwerów usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="55d95-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="55d95-139">W przypadku migracji z wcześniejszej wersji, przejrzyj witrynę sieci web Capptain do pierwszej kolejności przeprowadzenie migracji 1.1.1, zastosuj następującą procedurę</span><span class="sxs-lookup"><span data-stu-id="55d95-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="55d95-140">Pakiet Nuget</span><span class="sxs-lookup"><span data-stu-id="55d95-140">Nuget package</span></span>
<span data-ttu-id="55d95-141">Zastąp **Capptain.WindowsPhone** przez **MicrosoftAzure.MobileEngagement** pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="55d95-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="55d95-142">Stosowanie usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="55d95-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="55d95-143">Zestaw SDK używany jest termin `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="55d95-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="55d95-144">Musisz zaktualizować projektu do dopasowania tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="55d95-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="55d95-145">Konieczne jest odinstalowanie bieżącego Capptain pakietu nuget.</span><span class="sxs-lookup"><span data-stu-id="55d95-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="55d95-146">Należy wziąć pod uwagę, że wszystkie zmiany w folderze Capptain zasoby zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="55d95-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="55d95-147">Jeśli chcesz zachować te pliki, a następnie utworzyć ich kopię.</span><span class="sxs-lookup"><span data-stu-id="55d95-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="55d95-148">Po tym należy zainstalować pakiet nuget usługi Microsoft Azure Engagement w projekcie.</span><span class="sxs-lookup"><span data-stu-id="55d95-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="55d95-149">Znajdziesz ją bezpośrednio witrynie sieci Web [nuget].</span><span class="sxs-lookup"><span data-stu-id="55d95-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="55d95-150">lub indeks tutaj.</span><span class="sxs-lookup"><span data-stu-id="55d95-150">or here index.</span></span> <span data-ttu-id="55d95-151">Ta akcja zastępuje wszystkie pliki zasoby używane przez usługi Engagement i dodaje nowe DLL zaangażowania do odwołania projektu.</span><span class="sxs-lookup"><span data-stu-id="55d95-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="55d95-152">Należy wyczyścić przez usunięcie odwołania do biblioteki DLL Capptain odwołania projektu.</span><span class="sxs-lookup"><span data-stu-id="55d95-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="55d95-153">Jeśli nie wprowadzisz to, wersja Capptain spowoduje konflikt i nastąpi błędy.</span><span class="sxs-lookup"><span data-stu-id="55d95-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="55d95-154">Jeśli dostosowano Capptain zasobów, skopiuj stare pliki zawartości i wklej je w nowych plików zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="55d95-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="55d95-155">Należy pamiętać, że można zaktualizować pliku xaml, jak i cs.</span><span class="sxs-lookup"><span data-stu-id="55d95-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="55d95-156">Po wykonaniu tych kroków należy tylko zastąpić starego odwołania Capptain przez nowego odwołania zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="55d95-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="55d95-157">Wszystkie przestrzenie nazw Capptain wymagają aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="55d95-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="55d95-158">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="55d95-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="55d95-159">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="55d95-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="55d95-160">Wszystkie klasy Capptain, które zawierają "Capptain" powinien zawierać "Zaangażowania".</span><span class="sxs-lookup"><span data-stu-id="55d95-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="55d95-161">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="55d95-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="55d95-162">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="55d95-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="55d95-163">Pliki xaml Capptain przestrzeni nazw i atrybuty także zmienić.</span><span class="sxs-lookup"><span data-stu-id="55d95-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="55d95-164">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="55d95-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="55d95-165">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="55d95-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="55d95-166">Nakładki strony zmiany</span><span class="sxs-lookup"><span data-stu-id="55d95-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="55d95-167">Zmienia także nakładki.</span><span class="sxs-lookup"><span data-stu-id="55d95-167">Overlay also changes.</span></span> <span data-ttu-id="55d95-168">Jego nowa przestrzeń nazw to `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="55d95-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="55d95-169">Składa się z stosowaną w pliku xaml, jak i cs.</span><span class="sxs-lookup"><span data-stu-id="55d95-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="55d95-170">Ponadto `CapptainGrid` ma być nazwane `EngagementGrid`, `capptain_notification_content` i `capptain_announcement_content` są nazywane `engagement_notification_content` i `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="55d95-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="55d95-171">Do nakładki:</span><span class="sxs-lookup"><span data-stu-id="55d95-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="55d95-172">Staje się:</span><span class="sxs-lookup"><span data-stu-id="55d95-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="55d95-173">Dla innych zasobów takich jak obrazy Capptain i pliki HTML należy pamiętać, że one również zmieniono za pomocą "Engagement".</span><span class="sxs-lookup"><span data-stu-id="55d95-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="55d95-174">Deklaracja projektu</span><span class="sxs-lookup"><span data-stu-id="55d95-174">Project declaration</span></span>
<span data-ttu-id="55d95-175">Na Package.appxmanifest `File Type Associations` został zaktualizowany od:</span><span class="sxs-lookup"><span data-stu-id="55d95-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="55d95-176">capptain\_osiągnąć\_zawartości do usługi engagement\_osiągnąć\_zawartości</span><span class="sxs-lookup"><span data-stu-id="55d95-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="55d95-177">capptain\_dziennika\_pliku do usługi engagement\_dziennika\_pliku</span><span class="sxs-lookup"><span data-stu-id="55d95-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="55d95-178">Identyfikator aplikacji / klucz zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="55d95-178">Application ID / SDK Key</span></span>
<span data-ttu-id="55d95-179">Zaangażowania używa parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="55d95-179">Engagement uses a connection string.</span></span> <span data-ttu-id="55d95-180">Nie trzeba określić identyfikator i klucz zestawu SDK usługi Mobile Engagement, wystarczy tylko określić parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="55d95-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="55d95-181">Możesz można skonfigurować go na plik EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="55d95-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="55d95-182">Konfiguracja usługi Engagement może zostać ustawiona Twojej `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="55d95-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="55d95-183">Edytuj ten plik, aby określić:</span><span class="sxs-lookup"><span data-stu-id="55d95-183">Edit this file to specify:</span></span>

* <span data-ttu-id="55d95-184">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="55d95-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="55d95-185">Jeśli chcesz określić je w czasie wykonywania, należy wywołać metodę następujące przed zainicjowaniem agenta usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="55d95-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="55d95-186">Ciąg połączenia dla aplikacji jest wyświetlany w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="55d95-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="55d95-187">Zmiana nazwy elementów</span><span class="sxs-lookup"><span data-stu-id="55d95-187">Items name change</span></span>
<span data-ttu-id="55d95-188">Wszystkie elementy o nazwie *capptain* została nazwana *engagement*.</span><span class="sxs-lookup"><span data-stu-id="55d95-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="55d95-189">Podobnie dla *Capptain* do *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="55d95-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="55d95-190">Przykłady często używanych elementów Capptain:</span><span class="sxs-lookup"><span data-stu-id="55d95-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="55d95-191">CapptainConfiguration teraz nazwę EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="55d95-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="55d95-192">Teraz o nazwie EngagementAgent CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="55d95-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="55d95-193">Teraz o nazwie EngagementReach CapptainReach</span><span class="sxs-lookup"><span data-stu-id="55d95-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="55d95-194">Teraz o nazwie EngagementHttpConfig CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="55d95-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="55d95-195">Teraz o nazwie GetEngagementPageName GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="55d95-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="55d95-196">Należy pamiętać, że zmiany nazwy wpływa na przesłoniętej metody.</span><span class="sxs-lookup"><span data-stu-id="55d95-196">Note that rename also affects overridden methods.</span></span>

