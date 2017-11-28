---
title: aaaWindows uniwersalnych aplikacji zestawu SDK procedur uaktualniania
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
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="8c02c-103">Procedury uaktualniania uniwersalnych aplikacji systemu Windows SDK</span><span class="sxs-lookup"><span data-stu-id="8c02c-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="8c02c-104">Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="8c02c-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="8c02c-105">Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="8c02c-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="8c02c-106">Na przykład w przypadku migracji z 0.10.1 too0.11.0 masz toofirst wykonaj hello "z 0.9.0 too0.10.1" procedury, a następnie hello "z 0.10.1 too0.11.0" procedury.</span><span class="sxs-lookup"><span data-stu-id="8c02c-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="8c02c-107">Z 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="8c02c-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="8c02c-108">Dzienniki testów</span><span class="sxs-lookup"><span data-stu-id="8c02c-108">Test logs</span></span>
<span data-ttu-id="8c02c-109">Dzienniki konsoli utworzonego przez zestaw SDK hello można teraz włączone/wyłączone/odfiltrowane.</span><span class="sxs-lookup"><span data-stu-id="8c02c-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="8c02c-110">toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="8c02c-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="8c02c-111">Zasoby</span><span class="sxs-lookup"><span data-stu-id="8c02c-111">Resources</span></span>
<span data-ttu-id="8c02c-112">udoskonalono Hello Reach nakładki.</span><span class="sxs-lookup"><span data-stu-id="8c02c-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="8c02c-113">Jest ona częścią zasoby pakietu SDK NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="8c02c-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="8c02c-114">Podczas uaktualniania toohello nowej wersji zestawu SDK hello można wybrać, czy ma tookeep istniejących plików z hello nakładki folderu zasobów:</span><span class="sxs-lookup"><span data-stu-id="8c02c-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="8c02c-115">Jeśli poprzednie nakładki hello jest pracuje lub jest integrowany hello `WebView` elementy ręcznie, a następnie użytkownik może określić tookeep istniejących plików, to nadal będzie działać.</span><span class="sxs-lookup"><span data-stu-id="8c02c-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="8c02c-116">Jeśli chcesz, aby tooupdate toohello nowe nakładki, po prostu zastąpić hello całego `overlay` folder z Twoich zasobów z hello nową z pakietu SDK hello (aplikacji platformy uniwersalnej systemu Windows: po uaktualnieniu hello, możesz pobrać ze strony % USERPROFILE % hello nowy folder na nakładce\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="8c02c-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="8c02c-117">Przy użyciu nowego nakładki hello zastąpią wszelkie zmiany wprowadzone na powitania poprzedniej wersji.</span><span class="sxs-lookup"><span data-stu-id="8c02c-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="8c02c-118">Z 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="8c02c-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="8c02c-119">Zasoby</span><span class="sxs-lookup"><span data-stu-id="8c02c-119">Resources</span></span>
<span data-ttu-id="8c02c-120">Ten krok dotyczy tylko zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="8c02c-120">This step concerns customized resources only.</span></span> <span data-ttu-id="8c02c-121">Jeśli dostosowano zasobów hello udostępnianych przez hello SDK (html, obrazy, nakładki), następnie toobackup je przed uaktualnieniem, a następnie Zastosuj ponownie dostosowanie na uaktualniony zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c02c-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="8c02c-122">Z 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="8c02c-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="8c02c-123">Zasoby</span><span class="sxs-lookup"><span data-stu-id="8c02c-123">Resources</span></span>
<span data-ttu-id="8c02c-124">Ten krok dotyczy tylko zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="8c02c-124">This step concerns customized resources only.</span></span> <span data-ttu-id="8c02c-125">Jeśli dostosowano zasobów hello udostępnianych przez hello SDK (html, obrazy, nakładki), następnie toobackup je przed uaktualnieniem, a następnie Zastosuj ponownie dostosowanie na uaktualniony zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c02c-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="8c02c-126">Integracja z widoku sieci Web</span><span class="sxs-lookup"><span data-stu-id="8c02c-126">Webview integration</span></span>
<span data-ttu-id="8c02c-127">Niektóre ulepszenia toomatch innego urządzenia rozmiarach zostały wprowadzone w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="8c02c-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="8c02c-128">Upewnij się, że Twoje integracji hello webview zgodne hello następujące:</span><span class="sxs-lookup"><span data-stu-id="8c02c-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="8c02c-129">W Twojej XAML strony ():</span><span class="sxs-lookup"><span data-stu-id="8c02c-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="8c02c-130">W pliku skojarzone CS:</span><span class="sxs-lookup"><span data-stu-id="8c02c-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
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
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="8c02c-131">Z 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="8c02c-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="8c02c-132">Zasoby</span><span class="sxs-lookup"><span data-stu-id="8c02c-132">Resources</span></span>
<span data-ttu-id="8c02c-133">Ten krok dotyczy tylko zasobów niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="8c02c-133">This step concerns customized resources only.</span></span> <span data-ttu-id="8c02c-134">Jeśli dostosowano zasobów hello udostępnianych przez hello SDK (html, obrazy, nakładki), następnie toobackup je przed uaktualnieniem, a następnie Zastosuj ponownie dostosowanie na uaktualniony zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c02c-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="8c02c-135">Z 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="8c02c-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="8c02c-136">Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8c02c-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8c02c-137">Capptain i usługi Mobile Engagement nie hello tej samej usługi i procedury hello tylko podane poniżej prezentuje sposób toomigrate hello aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="8c02c-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="8c02c-138">Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów</span><span class="sxs-lookup"><span data-stu-id="8c02c-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="8c02c-139">W przypadku migracji z wcześniejszej wersji, należy najpierw zapoznaj się hello Capptain witryny sieci web toomigrate too1.1.1, zastosuj hello procedury</span><span class="sxs-lookup"><span data-stu-id="8c02c-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="8c02c-140">Pakiet Nuget</span><span class="sxs-lookup"><span data-stu-id="8c02c-140">Nuget package</span></span>
<span data-ttu-id="8c02c-141">Zastąp **Capptain.WindowsPhone** przez **MicrosoftAzure.MobileEngagement** pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="8c02c-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="8c02c-142">Stosowanie usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8c02c-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="8c02c-143">Hello SDK używany termin hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="8c02c-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="8c02c-144">Należy tooupdate toomatch Twojego projektu tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="8c02c-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="8c02c-145">Należy toouninstall bieżącego Capptain pakietu nuget.</span><span class="sxs-lookup"><span data-stu-id="8c02c-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="8c02c-146">Należy wziąć pod uwagę, że wszystkie zmiany w folderze Capptain zasoby zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="8c02c-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="8c02c-147">Jeśli tookeep tych plików, a następnie utworzyć ich kopię.</span><span class="sxs-lookup"><span data-stu-id="8c02c-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="8c02c-148">Po wykonaniu tej instalacji nowego pakietu nuget usługi Microsoft Azure Engagement hello w projekcie.</span><span class="sxs-lookup"><span data-stu-id="8c02c-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="8c02c-149">Znajdziesz ją bezpośrednio witrynie sieci Web [nuget].</span><span class="sxs-lookup"><span data-stu-id="8c02c-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="8c02c-150">lub indeks tutaj.</span><span class="sxs-lookup"><span data-stu-id="8c02c-150">or here index.</span></span> <span data-ttu-id="8c02c-151">Zastępuje tej akcji, wszystkich plików zasobów używanych przez usługi Engagement i dodaje nowe tooyour DLL zaangażowania hello projektu odwołań.</span><span class="sxs-lookup"><span data-stu-id="8c02c-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="8c02c-152">Masz tooclean odwołania projektu o usunięcie odwołania do biblioteki DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="8c02c-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="8c02c-153">Jeśli nie wprowadzisz to, wersja hello Capptain spowoduje konflikt i nastąpi błędy.</span><span class="sxs-lookup"><span data-stu-id="8c02c-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="8c02c-154">Jeśli dostosowano Capptain zasobów, skopiuj stare pliki zawartości i wklej je w nowych plików zaangażowania hello.</span><span class="sxs-lookup"><span data-stu-id="8c02c-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="8c02c-155">Należy pamiętać, że pliku xaml, jak i cs toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="8c02c-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="8c02c-156">Po wykonaniu tych kroków wystarczy tooreplace stare odwołania Capptain przez hello nowych zaangażowania odwołań.</span><span class="sxs-lookup"><span data-stu-id="8c02c-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="8c02c-157">Wszystkie przestrzenie nazw Capptain ma toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="8c02c-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="8c02c-158">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="8c02c-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="8c02c-159">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="8c02c-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="8c02c-160">Wszystkie klasy Capptain, które zawierają "Capptain" powinien zawierać "Zaangażowania".</span><span class="sxs-lookup"><span data-stu-id="8c02c-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="8c02c-161">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="8c02c-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="8c02c-162">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="8c02c-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="8c02c-163">Pliki xaml Capptain przestrzeni nazw i atrybuty także zmienić.</span><span class="sxs-lookup"><span data-stu-id="8c02c-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="8c02c-164">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="8c02c-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="8c02c-165">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="8c02c-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="8c02c-166">Nakładki strony zmiany</span><span class="sxs-lookup"><span data-stu-id="8c02c-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8c02c-167">Zmienia także nakładki.</span><span class="sxs-lookup"><span data-stu-id="8c02c-167">Overlay also changes.</span></span> <span data-ttu-id="8c02c-168">Jego nowa przestrzeń nazw to `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="8c02c-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="8c02c-169">Ma ona toobe używane w pliku xaml, jak i cs.</span><span class="sxs-lookup"><span data-stu-id="8c02c-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="8c02c-170">Ponadto `CapptainGrid` nosi nazwę toobe `EngagementGrid`, `capptain_notification_content` i `capptain_announcement_content` są nazywane `engagement_notification_content` i `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="8c02c-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="8c02c-171">Do nakładki:</span><span class="sxs-lookup"><span data-stu-id="8c02c-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="8c02c-172">Staje się:</span><span class="sxs-lookup"><span data-stu-id="8c02c-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="8c02c-173">Dla hello innych zasobów, takich jak obrazy Capptain i pliki HTML, należy pamiętać, że również zostały toouse zmieniono nazwę "Zaangażowania".</span><span class="sxs-lookup"><span data-stu-id="8c02c-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="8c02c-174">Deklaracja projektu</span><span class="sxs-lookup"><span data-stu-id="8c02c-174">Project declaration</span></span>
<span data-ttu-id="8c02c-175">Na Package.appxmanifest `File Type Associations` został zaktualizowany od:</span><span class="sxs-lookup"><span data-stu-id="8c02c-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="8c02c-176">capptain\_osiągnąć\_zawartości tooengagement\_osiągnąć\_zawartości</span><span class="sxs-lookup"><span data-stu-id="8c02c-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="8c02c-177">capptain\_dziennika\_pliku tooengagement\_dziennika\_pliku</span><span class="sxs-lookup"><span data-stu-id="8c02c-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="8c02c-178">Identyfikator aplikacji / klucz zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="8c02c-178">Application ID / SDK Key</span></span>
<span data-ttu-id="8c02c-179">Zaangażowania używa parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="8c02c-179">Engagement uses a connection string.</span></span> <span data-ttu-id="8c02c-180">Nie masz toospecify identyfikator i klucz zestawu SDK z usługi Mobile Engagement, wystarczy toospecify ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="8c02c-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="8c02c-181">Możesz można skonfigurować go na plik EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="8c02c-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="8c02c-182">Konfiguracja zaangażowania Hello może zostać ustawiona Twojej `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8c02c-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="8c02c-183">Edytuj toospecify tego pliku:</span><span class="sxs-lookup"><span data-stu-id="8c02c-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="8c02c-184">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="8c02c-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="8c02c-185">Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="8c02c-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="8c02c-186">Parametry połączenia Hello aplikacji jest wyświetlany na powitania klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c02c-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="8c02c-187">Zmiana nazwy elementów</span><span class="sxs-lookup"><span data-stu-id="8c02c-187">Items name change</span></span>
<span data-ttu-id="8c02c-188">Wszystkie elementy o nazwie *capptain* została nazwana *engagement*.</span><span class="sxs-lookup"><span data-stu-id="8c02c-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="8c02c-189">Podobnie dla *Capptain* za*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="8c02c-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="8c02c-190">Przykłady często używanych elementów Capptain:</span><span class="sxs-lookup"><span data-stu-id="8c02c-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="8c02c-191">CapptainConfiguration teraz nazwę EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="8c02c-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="8c02c-192">Teraz o nazwie EngagementAgent CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="8c02c-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="8c02c-193">Teraz o nazwie EngagementReach CapptainReach</span><span class="sxs-lookup"><span data-stu-id="8c02c-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="8c02c-194">Teraz o nazwie EngagementHttpConfig CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="8c02c-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="8c02c-195">Teraz o nazwie GetEngagementPageName GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="8c02c-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="8c02c-196">Należy pamiętać, że zmiany nazwy wpływa na przesłoniętej metody.</span><span class="sxs-lookup"><span data-stu-id="8c02c-196">Note that rename also affects overridden methods.</span></span>

