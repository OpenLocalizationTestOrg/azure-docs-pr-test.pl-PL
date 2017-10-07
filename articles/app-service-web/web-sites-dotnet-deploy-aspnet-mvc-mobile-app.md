---
title: "aaaDeploy ASP.NET MVC 5 aplikacji sieci web urządzeń przenośnych w usłudze Azure App Service"
description: "Samouczek opisujący sposób funkcji toodeploy tooAzure aplikacji sieci web usługi aplikacji przy użyciu przenośnych w platformie ASP.NET MVC 5 aplikacji sieci web."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="6f75a-103">Wdrażanie aplikacji ASP.NET MVC 5 sieci web urządzeń przenośnych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6f75a-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="6f75a-104">W tym samouczku udzieli hello podstawy jak toobuild ASP.NET MVC 5 sieci web aplikacji, która jest przyjaznych dla urządzeń przenośnych i wdrożyć ją tooAzure usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="6f75a-105">W tym samouczku potrzebne [programu Visual Studio Express 2013 for Web] [ Visual Studio Express 2013] lub w wersji professional hello programu Visual Studio, jeśli masz już który.</span><span class="sxs-lookup"><span data-stu-id="6f75a-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="6f75a-106">Można użyć [programu Visual Studio 2015] , ale hello zrzuty ekranu mogą być inne, i musi być hello ASP.NET 4.x szablonów.</span><span class="sxs-lookup"><span data-stu-id="6f75a-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="6f75a-107">Jakie będzie kompilacji</span><span class="sxs-lookup"><span data-stu-id="6f75a-107">What You'll Build</span></span>
<span data-ttu-id="6f75a-108">W tym samouczku zostanie dodana Funkcje mobilne toohello proste konferencji listę aplikacji, która znajduje się w hello [projektu starter][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="6f75a-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="6f75a-109">Hello Poniższy zrzut ekranu przedstawia hello sesji programu ASP.NET w aplikacji hello ukończone, jak pokazano w emulatorze przeglądarki hello w narzędzi deweloperskich programu Internet Explorer 11 F12.</span><span class="sxs-lookup"><span data-stu-id="6f75a-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="6f75a-110">Można użyć narzędzia dla deweloperów hello F12 programu Internet Explorer 11 i hello [narzędzie Fiddler] [ Fiddler] toohelp debugowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="6f75a-111">Dowiesz się umiejętności</span><span class="sxs-lookup"><span data-stu-id="6f75a-111">Skills You'll Learn</span></span>
<span data-ttu-id="6f75a-112">Oto dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="6f75a-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="6f75a-113">Jak toopublish toouse programu Visual Studio 2013 aplikacji sieci web bezpośrednio tooa aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6f75a-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="6f75a-114">Jak szablony hello ASP.NET MVC 5 za pomocą architektury CSS Bootstrap hello zwiększające wyświetlania na urządzeniach przenośnych</span><span class="sxs-lookup"><span data-stu-id="6f75a-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="6f75a-115">Jak toocreate mobile określonych widoków tootarget określonych przeglądarki dla urządzeń przenośnych, takich jak hello iPhone i Android</span><span class="sxs-lookup"><span data-stu-id="6f75a-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="6f75a-116">Jak widoki dynamiczne toocreate (widoki, które odpowiadają toodifferent przeglądarki na urządzeniach)</span><span class="sxs-lookup"><span data-stu-id="6f75a-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="6f75a-117">Konfigurowanie środowiska deweloperskiego hello</span><span class="sxs-lookup"><span data-stu-id="6f75a-117">Set up hello development environment</span></span>
<span data-ttu-id="6f75a-118">Konfigurowanie środowiska programowania przez zainstalowanie hello Azure SDK dla platformy .NET 2.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6f75a-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="6f75a-119">Witaj tooinstall zestawu Azure SDK dla platformy .NET, kliknij poniższe łącze hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="6f75a-120">Jeśli nie masz jeszcze zainstalowany program Visual Studio 2013, zostanie zainstalowany przez łącze hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="6f75a-121">Ten samouczek wymaga programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6f75a-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="6f75a-122">[Zestaw Azure SDK dla programu Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="6f75a-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="6f75a-123">W oknie Instalatora platformy sieci Web powitania kliknij **zainstalować** i kontynuować hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="6f75a-124">Należy również emulatora przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="6f75a-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="6f75a-125">Jedną z następujących przyczyn hello będzie działać:</span><span class="sxs-lookup"><span data-stu-id="6f75a-125">Any of hello following will work:</span></span>

* <span data-ttu-id="6f75a-126">Emulator przeglądarki w [narzędzi deweloperskich programu Internet Explorer 11 F12] [ EmulatorIE11] (używane na wszystkich przeglądarkę dla telefonów zrzutach ekranu).</span><span class="sxs-lookup"><span data-stu-id="6f75a-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="6f75a-127">Ma ona predefiniowane ciąg agenta użytkownika dla systemu Windows Phone 8, Windows Phone 7 i iPad firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="6f75a-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="6f75a-128">Emulator przeglądarki w [DevTools Google Chrome][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="6f75a-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="6f75a-129">Zawiera ustawienia dla wielu urządzeń z systemem Android, a także Apple iPhone, iPad firmy Apple oraz Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="6f75a-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="6f75a-130">Emuluje on również zdarzenia touch.</span><span class="sxs-lookup"><span data-stu-id="6f75a-130">It also emulates touch events.</span></span>
* <span data-ttu-id="6f75a-131">[Opera emulatorze przenośnym][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="6f75a-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="6f75a-132">Projekty Visual Studio z C\# kod źródłowy są dostępne tooaccompany w tym temacie:</span><span class="sxs-lookup"><span data-stu-id="6f75a-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="6f75a-133">[Początkowy projektem do pobrania][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="6f75a-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="6f75a-134">[Pobranie projektu zakończone][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="6f75a-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="6f75a-135"><a name="bkmk_DeployStarterProject"></a>Wdrażanie hello starter projektu tooan aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="6f75a-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="6f75a-136">Pobierz aplikację listy konferencji hello [projektu starter][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="6f75a-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="6f75a-137">Następnie w Eksploratorze Windows, kliknij prawym przyciskiem myszy hello pobrany plik ZIP i wybierz *właściwości*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="6f75a-138">W hello **właściwości** oknie dialogowym Wybierz hello **Odblokuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="6f75a-139">(Odblokowywania uniemożliwia ostrzeżenie występujący podczas próby toouse *.zip* pliku pobranym z sieci web hello.)</span><span class="sxs-lookup"><span data-stu-id="6f75a-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="6f75a-140">Kliknij prawym przyciskiem myszy plik ZIP hello i wybierz **Wyodrębnij wszystkie** rozpakować pliku hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="6f75a-141">W programie Visual Studio Otwórz hello *C#\Mvc5Mobile.sln* pliku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="6f75a-142">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt hello, a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="6f75a-143">Na publikowanie w sieci Web, kliknij **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="6f75a-144">Jeśli jeszcze nie zostało to jeszcze zalogowania na platformie Azure, kliknij przycisk **Dodaj konto**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="6f75a-145">Wykonaj toolog monity hello na konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f75a-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="6f75a-146">Witaj w oknie dialogowym App Service powinna zostać wyświetlona zostanie jako zalogowany.</span><span class="sxs-lookup"><span data-stu-id="6f75a-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="6f75a-147">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="6f75a-148">W hello **Nazwa aplikacji sieci Web** określ prefiks nazwy aplikacji unikatowy.</span><span class="sxs-lookup"><span data-stu-id="6f75a-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="6f75a-149">Twoje Pełna nazwa aplikacji sieci web będzie  *&lt;prefiks >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="6f75a-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="6f75a-150">Ponadto wybierz lub określ nazwę nowej grupy zasobów w **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="6f75a-151">Następnie kliknij przycisk **nowy** toocreate nowy plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="6f75a-152">Skonfiguruj nowy plan usługi aplikacji hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="6f75a-153">W oknie dialogowym Tworzenie usługi App Service hello, kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="6f75a-154">Po hello Azure zasoby są tworzone, hello publikowanie w sieci Web w oknie dialogowym zostanie wypełniony hello ustawienia dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="6f75a-155">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="6f75a-156">Po zakończeniu publikowania aplikacji sieci web platformy Azure toohello projektu hello starter Visual Studio, hello pulpitu przeglądarce zostanie otwarty w aplikacji sieci web na żywo hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="6f75a-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="6f75a-157">Uruchom emulator Twojej przeglądarkę dla telefonów, skopiuj adres URL aplikacji konferencji hello hello (*<prefix>*. azurewebsites.net) w emulatorze hello, a następnie kliknij przycisk prawym górnym rogu i wybierz **Przeglądaj według znaczników**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="6f75a-158">Jeśli korzystasz z programu Internet Explorer 11 jako hello domyślnej przeglądarki, wystarczy tootype `F12`, następnie `Ctrl+8`, a następnie zmień profilu przeglądarki hello zbyt**Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="6f75a-159">Na poniższym obrazie pokazano hello *alltags —* widok w trybie portret (wybór **Przeglądaj według znaczników**).</span><span class="sxs-lookup"><span data-stu-id="6f75a-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="6f75a-160">Podczas gdy można debugować aplikacji MVC 5 z poziomu programu Visual Studio, tooAzure aplikacji sieci web można opublikować ponownie tooverify hello na żywo aplikacji sieci web bezpośrednio w przeglądarce przenośnych lub w emulatorze przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="6f75a-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="6f75a-161">Wyświetlanie Hello jest bardzo do odczytu na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="6f75a-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="6f75a-162">Można także już widoczne niektóre hello efekty wizualne zastosowane przez platformę Bootstrap CSS hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="6f75a-163">Kliknij przycisk hello **ASP.NET** łącza.</span><span class="sxs-lookup"><span data-stu-id="6f75a-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="6f75a-164">Witaj widok tagów ASP.NET jest zainstalowane powiększenia toohello ekran, który jest dla Ciebie automatycznie ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="6f75a-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="6f75a-165">Jednak może poprawić ten widok toobetter koloru hello przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="6f75a-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="6f75a-166">Na przykład Witaj **data** kolumna jest trudny do odczytania.</span><span class="sxs-lookup"><span data-stu-id="6f75a-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="6f75a-167">Później w samouczku hello zostanie zmieniona hello *alltags —* wyświetlić toomake go przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="6f75a-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="6f75a-168"><a name="bkmk_bootstrap"></a>Framework bootstrap CSS</span><span class="sxs-lookup"><span data-stu-id="6f75a-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="6f75a-169">Nowe hello MVC 5 szablon jest wbudowana obsługa ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="6f75a-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="6f75a-170">Ma już widoczny, jak od razu zwiększa hello różne widoki w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="6f75a-171">Na przykład pasek nawigacyjny hello u góry hello jest zwijany automatycznie, gdy szerokość przeglądarki hello jest mniejsza.</span><span class="sxs-lookup"><span data-stu-id="6f75a-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="6f75a-172">W przeglądarce pulpitu hello należy spróbować zmienić rozmiar okna przeglądarki hello i zobacz, jak pasek nawigacyjny hello zmienia jego wygląd i działanie.</span><span class="sxs-lookup"><span data-stu-id="6f75a-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="6f75a-173">Jest to hello web elastyczny projekt, który jest wbudowana w ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="6f75a-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="6f75a-174">toosee jak hello aplikacji sieci Web będzie wyglądać bez ładowania początkowego, otwórz *aplikacji\_Start\\BundleConfig.cs* ujmij w komentarz hello wierszy, które zawierają *bootstrap.js* i *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="6f75a-175">Witaj poniższy kod przedstawia hello ostatnich dwóch instrukcje hello `RegisterBundles` metody po zmianie hello:</span><span class="sxs-lookup"><span data-stu-id="6f75a-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="6f75a-176">Naciśnij klawisz `Ctrl+F5` toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="6f75a-177">Obserwować paska nawigacyjnego zwijanej hello jest teraz wystarczy zwykłe nieuporządkowaną listę.</span><span class="sxs-lookup"><span data-stu-id="6f75a-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="6f75a-178">Kliknij przycisk **Przeglądaj według znaczników** ponownie, następnie kliknij przycisk **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="6f75a-179">W widoku emulatorze przenośnym hello widać, nie jest już zainstalowane powiększenia toohello ekranu i musieli przewijać bok w kolejności toosee powitania po prawej stronie powitania tabeli.</span><span class="sxs-lookup"><span data-stu-id="6f75a-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="6f75a-180">Cofnij zmiany, a następnie Odśwież tooverify przeglądarkę dla telefonów hello wyświetlana przyjazna hello została przywrócona.</span><span class="sxs-lookup"><span data-stu-id="6f75a-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="6f75a-181">Ładowania początkowego nie jest określonym tooASP.NET MVC 5, a w dowolnej aplikacji sieci web mogą korzystać z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="6f75a-182">Ale teraz są wbudowane w szablon projektu programu ASP.NET MVC 5, dzięki czemu aplikacja sieci MVC 5 Web można korzystać z Bootstrap domyślnie.</span><span class="sxs-lookup"><span data-stu-id="6f75a-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="6f75a-183">Aby uzyskać więcej informacji na temat ładowania początkowego Przejdź toothe [Bootstrap] [ BootstrapSite] lokacji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="6f75a-184">W następnej sekcji hello zobaczysz jak tooprovide mobile przeglądarki konkretnych widoków.</span><span class="sxs-lookup"><span data-stu-id="6f75a-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="6f75a-185"><a name="bkmk_overrideviews"></a>Zastąpienie hello widoki, układów i widoki częściowe</span><span class="sxs-lookup"><span data-stu-id="6f75a-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="6f75a-186">Można zastąpić dowolnym widoku (w tym układy i widoki częściowe) dla przeglądarki dla urządzeń przenośnych ogólnie rzecz biorąc, poszczególne przeglądarkę dla telefonów lub dowolnej przeglądarki określone.</span><span class="sxs-lookup"><span data-stu-id="6f75a-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="6f75a-187">wyświetlanie konkretnego mobile tooprovide, możesz skopiować plik widoku i dodać *. Mobile* toohello nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="6f75a-188">Na przykład toocreate przenośnym *indeksu* widoku, możesz skopiować *widoków\\Home\\Index.cshtml* do *widoków\\Home\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="6f75a-189">W tej sekcji utworzysz plik układu specyficzne dla mobilnych.</span><span class="sxs-lookup"><span data-stu-id="6f75a-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="6f75a-190">toostart, kopiowania *widoków\\Shared\\\_Layout.cshtml* do *widoków\\Shared\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="6f75a-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="6f75a-191">Otwórz  *\_Layout.Mobile.cshtml* i Zmień tytuł hello z **aplikacji MVC5** za**MVC5 aplikacji (Mobile)**.</span><span class="sxs-lookup"><span data-stu-id="6f75a-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="6f75a-192">W każdym `Html.ActionLink` wywołać paska nawigacyjnego hello, Usuń "Przeglądaj według", w każdym odnośniku *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="6f75a-193">Witaj poniższy kod przedstawia ukończyć powitalnych `<ul class="nav navbar-nav">` tag hello przenośnych układ pliku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="6f75a-194">Hello kopiowania *widoków\\Home\\AllTags.cshtml* pliku *widoków\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="6f75a-195">Otwórz nowy plik hello i zmień `<h2>` element na podstawie "Tagi" za "tagi (M)":</span><span class="sxs-lookup"><span data-stu-id="6f75a-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="6f75a-196">Przeglądaj toohello tagi strony w przeglądarce pulpitu i przy użyciu emulatora przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="6f75a-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="6f75a-197">emulator przeglądarkę dla telefonów Hello pokazuje Witaj dwie zmiany wprowadzone (hello tytuł z  *\_Layout.Mobile.cshtml* i tytuł hello z *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="6f75a-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="6f75a-198">Z kolei hello ekranu nie został zmieniony (tytułów z  *\_Layout.cshtml* i *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="6f75a-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="6f75a-199"><a name="bkmk_browserviews"></a>Utwórz widoki specyficzne dla przeglądarki</span><span class="sxs-lookup"><span data-stu-id="6f75a-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="6f75a-200">Ponadto toomobile dotyczące pulpitu i widoki, można tworzyć widoki dla poszczególnych przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="6f75a-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="6f75a-201">Na przykład można tworzyć widoki, które są przeznaczone dla hello iPhone lub hello przeglądarki systemu Android.</span><span class="sxs-lookup"><span data-stu-id="6f75a-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="6f75a-202">W tej sekcji utworzysz układ hello iPhone przeglądarki i wersji iPhone hello *alltags —* widoku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="6f75a-203">Otwórz hello *Global.asax* plik i dodać powitania od dołu toohello kodu `Application_Start` — metoda.</span><span class="sxs-lookup"><span data-stu-id="6f75a-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="6f75a-204">Ten kod definiuje nowy tryb wyświetlania o nazwie "iPhone" pasujących względem każdego żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6f75a-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="6f75a-205">Jeśli hello żądanie przychodzące odpowiada warunku, zdefiniowane przez użytkownika (jeśli agent użytkownika hello zawiera ciąg hello "iPhone"), platformy ASP.NET MVC sprawdza widoki, których nazwa zawiera sufiksu "iPhone".</span><span class="sxs-lookup"><span data-stu-id="6f75a-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="6f75a-206">Podczas dodawania przenośnych przeglądarki specyficzne dla tryby wyświetlania, takich jak dla urządzenia iPhone i Android, można się tooset hello pierwszy argument zbyt`0` się, że w trybie specyficzne dla przeglądarki hello mają pierwszeństwo przed szablonu przenośnych hello toomake (Wstaw u góry hello hello listy) (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="6f75a-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="6f75a-207">Jeśli szablon przenośnych hello jest na początku listy hello hello, zostanie wybrana przez tryb wyświetlania zamierzone (hello pierwszego dopasowania wins i hello przenośnych szablon jest zgodny wszystkie przeglądarki dla urządzeń przenośnych).</span><span class="sxs-lookup"><span data-stu-id="6f75a-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="6f75a-208">W kodzie hello, kliknij prawym przyciskiem myszy `DefaultDisplayMode`, wybierz **rozwiązać**, a następnie wybierz pozycję `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="6f75a-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="6f75a-209">Spowoduje to dodanie toothe odwołanie `System.Web.WebPages` przestrzeni nazw, czyli gdzie `DisplayModeProvider` i `DefaultDisplayMode` typy zostały zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="6f75a-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="6f75a-210">Alternatywnie można dodawać tylko ręcznie powitania po wierszu toothe `using` sekcji hello pliku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="6f75a-211">Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-211">Save hello changes.</span></span> <span data-ttu-id="6f75a-212">Kopia *widoków\\Shared\\\_Layout.Mobile.cshtml* pliku na *widoków\\współużytkowane\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="6f75a-213">Otwórz nowy plik hello, a następnie zmień tytuł hello z `MVC5 Application (Mobile)` do `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="6f75a-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="6f75a-214">Hello kopiowania *widoków\\Home\\AllTags.Mobile.cshtml* pliku *widoków\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="6f75a-215">W hello nowy plik, zmień hello `<h2>` element z "tagi (M)" za "tagi (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="6f75a-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="6f75a-216">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-216">Run hello application.</span></span> <span data-ttu-id="6f75a-217">Uruchamianie emulatora przeglądarkę dla telefonów, upewnij się, że jego agenta użytkownika ustawiono zbyt "iPhone", a następnie przejdź toohello *alltags —* widoku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="6f75a-218">Jeśli używasz emulatora hello w narzędzi deweloperskich programu Internet Explorer 11 naciśnięcia klawisza F12, skonfiguruj emulacji toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="6f75a-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="6f75a-219">Profil przeglądarki = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="6f75a-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="6f75a-220">Ciąg agenta użytkownika = **niestandardowe**</span><span class="sxs-lookup"><span data-stu-id="6f75a-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="6f75a-221">Niestandardowy ciąg = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="6f75a-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="6f75a-222">Witaj Poniższy zrzut ekranu przedstawia hello *alltags —* widok renderowany w emulatorze w narzędzi deweloperskich programu Internet Explorer 11 F12 z hello niestandardowy ciąg agenta użytkownika (jest to ciąg agenta użytkownika iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="6f75a-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="6f75a-223">W przeglądarce przenośnych hello, wybierz hello **głośniki** łącza.</span><span class="sxs-lookup"><span data-stu-id="6f75a-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="6f75a-224">Ponieważ nie jest widokiem dla urządzeń przenośnych (*AllSpeakers.Mobile.cshtml*), wyświetlanie głośniki domyślne hello (*AllSpeakers.cshtml*) jest renderowany przy użyciu widoku układu przenośnych hello ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="6f75a-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="6f75a-225">Jak pokazano poniżej, tytuł hello **MVC5 aplikacji (Mobile)** jest zdefiniowany w  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="6f75a-226">Widok domyślny (nieprzenośnych) z renderowania w układzie przenośnych globalnie można wyłączyć, ustawiając `RequireConsistentDisplayMode` do `true` w hello *widoków\\\_ViewStart.cshtml* pliku następująco:</span><span class="sxs-lookup"><span data-stu-id="6f75a-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="6f75a-227">Gdy `RequireConsistentDisplayMode` ustawiono zbyt`true`, układ przenośnych hello (*\_Layout.Mobile.cshtml*) jest używany tylko dla widoków przenośnych (tj. gdy plik widoku ma formę hello  ***ViewName** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="6f75a-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="6f75a-228">Może być tooset `RequireConsistentDisplayMode` zbyt`true` Jeśli przenośnych układu nie działa prawidłowo w przypadku widoków przeznaczone dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="6f75a-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="6f75a-229">Witaj zrzut ekranu poniżej przedstawiono sposób hello *głośniki* renderowania strony, gdy `RequireConsistentDisplayMode` ustawiono zbyt`true` (bez ciąg hello "(wersja Mobile)" w nawigacji pasków u góry hello hello).</span><span class="sxs-lookup"><span data-stu-id="6f75a-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="6f75a-230">Spójnego trybu wyświetlania w określonym widoku można wyłączyć, ustawiając `RequireConsistentDisplayMode` zbyt`false` hello widoku pliku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="6f75a-231">Następujący kod w hello *widoków\\Home\\AllSpeakers.cshtml* plików zestawów `RequireConsistentDisplayMode` zbyt`false`:</span><span class="sxs-lookup"><span data-stu-id="6f75a-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="6f75a-232">Możemy w tej sekcji przedstawiono sposób toocreate przenośnych układy i widoki i jak układów toocreate oraz widoki dla konkretnych urządzeń, takich jak hello iPhone.</span><span class="sxs-lookup"><span data-stu-id="6f75a-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="6f75a-233">Główną zaletą framework Bootstrap CSS hello hello jest jednak elastyczny układ, co oznacza, że jednego arkusza stylów mogą być stosowane przez pulpitu, telefon i tablet przeglądarki toocreate spójny wygląd i zachowanie.</span><span class="sxs-lookup"><span data-stu-id="6f75a-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="6f75a-234">W następnej sekcji hello zobaczysz, jak tooleverage Bootstrap przyjazna toocreate widoków.</span><span class="sxs-lookup"><span data-stu-id="6f75a-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="6f75a-235"><a name="bkmk_Improvespeakerslist"></a>Poprawa hello głośniki listy</span><span class="sxs-lookup"><span data-stu-id="6f75a-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="6f75a-236">Jak został wyświetlony, hello *głośniki* widoku jest możliwy do odczytu, ale linki hello są małe i są trudne tootap na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="6f75a-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="6f75a-237">W tej sekcji należy podjąć hello *AllSpeakers* głośniki można odnaleźć widoku przyjaznych dla urządzeń przenośnych, która wyświetla dużych, łatwe wybranie łącza i zawiera tooquickly pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6f75a-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="6f75a-238">Można użyć hello Bootstrap [listy połączonej grupy] [ linked list group] stylów zwiększające hello *głośniki* widoku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="6f75a-239">W *widoków\\Home\\AllSpeakers.cshtml*, Zastąp zawartość pliku Razor hello hello hello kod poniżej.</span><span class="sxs-lookup"><span data-stu-id="6f75a-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="6f75a-240">Witaj `class="list-group"` atrybutu w hello `<div>` znacznik stosuje style Bootstrap listy i hello `class="input-group-item"` atrybut jest stosowany link tooeach stylów elementu listy ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="6f75a-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="6f75a-241">Odśwież przeglądarkę dla telefonów hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="6f75a-242">Witaj zaktualizowany widok wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="6f75a-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="6f75a-243">Witaj Bootstrap [listy połączonej grupy] [ linked list group] stylów sprawia, że hello całe okno dla każdego łącza, które są aktywne, czyli znacznie lepsze środowisko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f75a-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="6f75a-244">Przełącz widok pulpitu toothe i obserwować hello spójny wygląd i zachowanie.</span><span class="sxs-lookup"><span data-stu-id="6f75a-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="6f75a-245">Chociaż hello przeglądarkę dla telefonów widoku została ulepszona i jest trudno hello długą listę głośniki.</span><span class="sxs-lookup"><span data-stu-id="6f75a-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="6f75a-246">Ładowania początkowego nie zapewnia wyszukiwania filtr funkcji out-of box, ale można go dodać przy użyciu kilku wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="6f75a-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="6f75a-247">Należy najpierw dodać widok toohello pole wyszukiwania, a następnie podłączanie z hello kod JavaScript hello filtru funkcji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="6f75a-248">W *widoków\\Home\\AllSpeakers.cshtml*, Dodaj \<formularza\> tag zaraz po hello \<h2\> tagów, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="6f75a-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="6f75a-249">Zwróć uwagę, że hello `<form>` i `<input>` tagi zarówno ma hello toothem Bootstrap zastosowane style.</span><span class="sxs-lookup"><span data-stu-id="6f75a-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="6f75a-250">Witaj `<span>` element dodaje Bootstrap [glyphicon] [ glyphicon] toothe pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6f75a-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="6f75a-251">W hello *skryptów* folderu, Dodaj plik JavaScript o nazwie *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="6f75a-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="6f75a-252">Otwórz plik hello i Wklej hello następującego kodu do niej:</span><span class="sxs-lookup"><span data-stu-id="6f75a-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="6f75a-253">Należy również tooinclude filter.js w Twojej zarejestrowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="6f75a-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="6f75a-254">Otwórz *aplikacji\_Start\\BundleConfig.cs* i zmień hello pierwszy pakietów.</span><span class="sxs-lookup"><span data-stu-id="6f75a-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="6f75a-255">Zmień pierwsze `bundles.Add` instrukcji (dla hello **jquery** pakietu) tooinclude *skryptów\\filter.js*w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6f75a-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="6f75a-256">Witaj **jquery** pakietu jest już renderowana domyślnie hello  *\_układu* widoku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="6f75a-257">Później, możesz użyć hello JavaScript tego samego kodu tooapply widoki list tooother funkcji filtru.</span><span class="sxs-lookup"><span data-stu-id="6f75a-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="6f75a-258">Odśwież przeglądarkę dla telefonów hello i przejdź toohello *AllSpeakers* widoku.</span><span class="sxs-lookup"><span data-stu-id="6f75a-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="6f75a-259">W polu wyszukiwania wpisz "sc".</span><span class="sxs-lookup"><span data-stu-id="6f75a-259">In the search box, type "sc".</span></span> <span data-ttu-id="6f75a-260">listy głośniki Hello teraz można filtrować według tooyour ciąg wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6f75a-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="6f75a-261"><a name="bkmk_improvetags"></a>Poprawa hello listy tagów</span><span class="sxs-lookup"><span data-stu-id="6f75a-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="6f75a-262">Podobnie jak hello *głośniki* wyświetlić, hello *tagi* widoku jest możliwy do odczytu, ale linki hello są małe i trudne tootap na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="6f75a-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="6f75a-263">Można naprawić hello *tagi* widoku hello sam sposób naprawić hello *głośniki* wyświetlić, jeśli używasz zmiany kodu hello opisanego wcześniej, ale przy użyciu następujących hello `Html.ActionLink` składni metody w  *Widoki\\Home\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="6f75a-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="6f75a-264">Hello odświeżyć przeglądarkę dla komputerów wygląda w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6f75a-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="6f75a-265">I hello odświeżyć przeglądarkę dla telefonów wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="6f75a-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="6f75a-266">Jeśli zauważysz oryginalnego formatowania listy hello jest nadal istnieje w hello przeglądarkę dla telefonów i zastanawiasz się, jakie wystąpiły tooyour nieuprzywilejowany stylów Bootstrap, to artefaktu wcześniejszych akcji toocreate przenośnych określonych widoków.</span><span class="sxs-lookup"><span data-stu-id="6f75a-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="6f75a-267">Jednak teraz, gdy używasz hello Bootstrap CSS framework toocreate projektu sieci web reakcji Przejdź head i usuń te specyficzne dla mobile widoków i hello układ odpowiedni mobile.</span><span class="sxs-lookup"><span data-stu-id="6f75a-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="6f75a-268">Po wykonaniu tego hello odświeżyć przeglądarkę dla telefonów wyświetli hello stylów ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="6f75a-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="6f75a-269"><a name="bkmk_improvedates"></a>Poprawa hello listy dat</span><span class="sxs-lookup"><span data-stu-id="6f75a-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="6f75a-270">Można zwiększyć hello *dat* wyświetlania, takich jak zwiększona hello *głośniki* i *tagi* widoków, jeśli używasz hello zmiany kodu opisanego wcześniej, ale przy użyciu następującego hello `Html.ActionLink` składni metody w *widoków\\Home\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="6f75a-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="6f75a-271">Otrzymasz widoku odświeżyć przeglądarkę dla telefonów następująco:</span><span class="sxs-lookup"><span data-stu-id="6f75a-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="6f75a-272">Można jeszcze bardziej poprawić hello *dat* widoku poprzez organizowanie wartości daty i godziny hello według daty.</span><span class="sxs-lookup"><span data-stu-id="6f75a-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="6f75a-273">Można to zrobić z hello Bootstrap [panele] [ panels] style.</span><span class="sxs-lookup"><span data-stu-id="6f75a-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="6f75a-274">Zamień zawartość hello hello *widoków\\Home\\AllDates.cshtml* pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="6f75a-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="6f75a-275">Ten kod tworzy oddzielne `<div class="panel panel-primary">` tagu dla każdej różne daty listy hello i używa hello [listy połączonej grupy] [ linked list group] dla odpowiednich łączy jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="6f75a-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="6f75a-276">Oto przeglądarki przenośnych hello wygląda jak po uruchomieniu tego kodu:</span><span class="sxs-lookup"><span data-stu-id="6f75a-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="6f75a-277">Przeglądarka pulpitu toohello przełącznika.</span><span class="sxs-lookup"><span data-stu-id="6f75a-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="6f75a-278">Ponownie należy zwrócić uwagę spójny wygląd hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="6f75a-279"><a name="bkmk_improvesessionstable"></a>Poprawa hello SessionsTable widoku</span><span class="sxs-lookup"><span data-stu-id="6f75a-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="6f75a-280">W tej sekcji należy podjąć hello *SessionsTable* wyświetlić więcej przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="6f75a-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="6f75a-281">Ta zmiana jest bardziej rozległych hello wcześniejszych zmian.</span><span class="sxs-lookup"><span data-stu-id="6f75a-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="6f75a-282">W przeglądarce przenośnych hello, naciśnij przycisk hello **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6f75a-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="6f75a-283">Wybierz hello **ASP.NET** łącza.</span><span class="sxs-lookup"><span data-stu-id="6f75a-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="6f75a-284">Jak widać, wyświetlania hello jest formatowana jako tabelę, która jest obecnie zaprojektowanego toobe w przeglądarce pulpitu hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="6f75a-285">Jest jednak nieco trudne tooread na przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="6f75a-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="6f75a-286">toofix, otwórz *widoków\\Home\\SessionsTable.cshtml* , a następnie zastąpić hello zawartość pliku hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="6f75a-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="6f75a-287">Kod Hello wykonuje 3 rzeczy:</span><span class="sxs-lookup"><span data-stu-id="6f75a-287">hello code does 3 things:</span></span>

* <span data-ttu-id="6f75a-288">używa hello Bootstrap [niestandardowe listy połączonej grupy] [ custom linked list group] tooformat hello w pionie, informacji o sesji, dzięki czemu te informacje są przeznaczone do odczytu w przeglądarce przenośnych (przy użyciu klas takich jak grupy elementu tekst listy)</span><span class="sxs-lookup"><span data-stu-id="6f75a-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="6f75a-289">stosuje hello [systemu siatki] [ grid system] układu toothe tak sesji hello elementy przepływu w poziomie w przeglądarce pulpitu hello i w pionie w przeglądarce przenośnych hello (przy użyciu hello klasy col-md-4)</span><span class="sxs-lookup"><span data-stu-id="6f75a-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="6f75a-290">używa hello [reakcji narzędzia] [ responsive utilities] ukrycia znaczników sesji hello podczas wyświetlania w przeglądarce przenośnych hello (przy użyciu klasy ukryte xs hello)</span><span class="sxs-lookup"><span data-stu-id="6f75a-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="6f75a-291">Możesz także wybrać tytuł łącze toogo toohello odpowiednich sesji.</span><span class="sxs-lookup"><span data-stu-id="6f75a-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="6f75a-292">Obraz powitania poniżej odzwierciedla hello zmian w kodzie.</span><span class="sxs-lookup"><span data-stu-id="6f75a-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="6f75a-293">Witaj siatki ładowania początkowego systemu, który automatycznie zastosować rozmieszcza sesji w pionie w przeglądarce przenośnych hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="6f75a-294">Ponadto należy zauważyć, że hello tagi nie są pokazywane.</span><span class="sxs-lookup"><span data-stu-id="6f75a-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="6f75a-295">Przeglądarka pulpitu toohello przełącznika.</span><span class="sxs-lookup"><span data-stu-id="6f75a-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="6f75a-296">W przeglądarce dla komputerów hello zauważyć hello tagi są teraz wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6f75a-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="6f75a-297">Ponadto widać, że hello ładowania początkowego siatki system, który można zastosować Rozmieszcza elementy sesji hello w dwóch kolumnach.</span><span class="sxs-lookup"><span data-stu-id="6f75a-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="6f75a-298">Powiększenie przeglądarki przekonasz się, że rozmieszczenie hello zmienia toothree kolumn.</span><span class="sxs-lookup"><span data-stu-id="6f75a-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="6f75a-299"><a name="bkmk_improvesessionbycode"></a>Poprawa hello SessionByCode widoku</span><span class="sxs-lookup"><span data-stu-id="6f75a-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="6f75a-300">Na koniec będzie naprawić hello *SessionByCode* wyświetlić toomake go przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="6f75a-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="6f75a-301">W przeglądarce przenośnych hello, naciśnij przycisk hello **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6f75a-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="6f75a-302">Wybierz hello **ASP.NET** łącza.</span><span class="sxs-lookup"><span data-stu-id="6f75a-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="6f75a-303">Sesje tagu ASP.NET hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6f75a-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="6f75a-304">Wybierz hello **tworzenia aplikacji jednej strony ASP.NET i AngularJS** łącza.</span><span class="sxs-lookup"><span data-stu-id="6f75a-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="6f75a-305">widok pulpitu domyślny Hello działa poprawnie, ale może poprawić wygląd hello łatwo za pomocą niektórych składników Bootstrap graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f75a-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="6f75a-306">Otwórz *widoków\\Home\\SessionByCode.cshtml* i Zastąp zawartość hello powitania po znaczników:</span><span class="sxs-lookup"><span data-stu-id="6f75a-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="6f75a-307">Nowy kod znaczników Hello używa Bootstrap paneli Style tooimprove hello widokiem dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="6f75a-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="6f75a-308">Odśwież przeglądarkę dla telefonów hello.</span><span class="sxs-lookup"><span data-stu-id="6f75a-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="6f75a-309">Witaj poniższy obraz odzwierciedla hello zmiany kodu, które zostały wykonane:</span><span class="sxs-lookup"><span data-stu-id="6f75a-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="6f75a-310">Dobiega końca i przejrzyj</span><span class="sxs-lookup"><span data-stu-id="6f75a-310">Wrap Up and Review</span></span>
<span data-ttu-id="6f75a-311">Ten samouczek pokazuje, należy jak aplikacji sieci Web toouse ASP.NET MVC 5 toodevelop przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="6f75a-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="6f75a-312">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="6f75a-312">These include:</span></span>

* <span data-ttu-id="6f75a-313">Wdrażanie tooan aplikacji ASP.NET MVC 5 aplikacji sieci web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="6f75a-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="6f75a-314">Użyj Bootstrap toocreate układu reakcji strony sieci web w aplikacji MVC 5</span><span class="sxs-lookup"><span data-stu-id="6f75a-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="6f75a-315">Zastąpienie układu, widoków i widoki częściowe, globalnie i dla poszczególnych widoku</span><span class="sxs-lookup"><span data-stu-id="6f75a-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="6f75a-316">Układ formantu i częściowy przesłonić przy użyciu wymuszania `RequireConsistentDisplayMode` właściwości</span><span class="sxs-lookup"><span data-stu-id="6f75a-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="6f75a-317">Utwórz widoki, które odnoszą się do przeglądarki, takich jak przeglądarki iPhone hello</span><span class="sxs-lookup"><span data-stu-id="6f75a-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="6f75a-318">Zastosuj style Bootstrap w kodzie Razor</span><span class="sxs-lookup"><span data-stu-id="6f75a-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="6f75a-319">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6f75a-319">See Also</span></span>
* [<span data-ttu-id="6f75a-320">9 podstawowe zasady reakcji projektowanie witryn sieci web</span><span class="sxs-lookup"><span data-stu-id="6f75a-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="6f75a-321">[Ładowania początkowego][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="6f75a-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="6f75a-322">[Oficjalny Blog ładowania początkowego][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="6f75a-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="6f75a-323">[Twitter Bootstrap samouczek z Republika samouczka][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="6f75a-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="6f75a-324">[Witaj Plac zabaw dla ładowania początkowego][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="6f75a-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="6f75a-325">[W3C zalecenie przenośnych sieci Web aplikacji najlepsze rozwiązania][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="6f75a-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="6f75a-326">[Zalecenie Candidate W3C zapytaniami multimediów][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="6f75a-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6f75a-327">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="6f75a-327">What's changed</span></span>
* <span data-ttu-id="6f75a-328">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6f75a-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[programu Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

