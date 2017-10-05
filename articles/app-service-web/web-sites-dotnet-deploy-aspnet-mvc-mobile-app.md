---
title: "Wdrażanie aplikacji ASP.NET MVC 5 sieci web urządzeń przenośnych w usłudze Azure App Service"
description: "Samouczek, który jest przedstawienie sposobu wdrażania aplikacji sieci web w usłudze Azure App Service przy użyciu funkcji mobilnych w aplikacji sieci web platformy ASP.NET MVC 5."
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
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="226d9-103">Wdrażanie aplikacji ASP.NET MVC 5 sieci web urządzeń przenośnych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="226d9-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="226d9-104">Ten samouczek pokazuje podstawy do tworzenia aplikacji sieci web platformy ASP.NET MVC 5 jest przyjaznych dla urządzeń przenośnych i wdrożyć ją w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="226d9-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="226d9-105">W tym samouczku potrzebne [programu Visual Studio Express 2013 for Web] [ Visual Studio Express 2013] lub programu Visual Studio, jeśli masz już który wersji professional.</span><span class="sxs-lookup"><span data-stu-id="226d9-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="226d9-106">Można użyć [programu Visual Studio 2015] , ale zrzuty ekranu będzie różna i należy użyć szablonów ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="226d9-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="226d9-107">Jakie będzie kompilacji</span><span class="sxs-lookup"><span data-stu-id="226d9-107">What You'll Build</span></span>
<span data-ttu-id="226d9-108">W tym samouczku, warto Funkcje mobilne prostą aplikację konferencji listę, która znajduje się w [projektu starter][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="226d9-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="226d9-109">Poniższy zrzut ekranu przedstawia sesji platformy ASP.NET w ukończona aplikacja, jak pokazano w emulatorze przeglądarki w narzędziach developer F12 programu Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="226d9-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="226d9-110">Korzystając z narzędzi deweloperskich programu Internet Explorer 11 F12 i [narzędzie Fiddler] [ Fiddler] do debugowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="226d9-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="226d9-111">Dowiesz się umiejętności</span><span class="sxs-lookup"><span data-stu-id="226d9-111">Skills You'll Learn</span></span>
<span data-ttu-id="226d9-112">Oto dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="226d9-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="226d9-113">Jak opublikować aplikację sieci web bezpośrednio do aplikacji sieci web w usłudze Azure App Service przy użyciu programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="226d9-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="226d9-114">Jak szablony ASP.NET MVC 5 za pomocą architektury CSS Bootstrap zwiększające wyświetlania na urządzeniach przenośnych</span><span class="sxs-lookup"><span data-stu-id="226d9-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="226d9-115">Jak tworzyć widoki specyficzne dla mobile pod kątem określonych przeglądarki dla urządzeń przenośnych, takich jak urządzenia iPhone i Android</span><span class="sxs-lookup"><span data-stu-id="226d9-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="226d9-116">Jak tworzyć widoki dynamiczne (widoki, które odpowiadają na różnych przeglądarkach różnych urządzeń)</span><span class="sxs-lookup"><span data-stu-id="226d9-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="226d9-117">Konfigurowanie środowiska deweloperskiego</span><span class="sxs-lookup"><span data-stu-id="226d9-117">Set up the development environment</span></span>
<span data-ttu-id="226d9-118">Konfigurowanie środowiska programowania przez zainstalowanie zestawu Azure SDK dla platformy .NET 2.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="226d9-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="226d9-119">Aby zainstalować zestaw Azure SDK dla platformy .NET, kliknij poniższe łącze.</span><span class="sxs-lookup"><span data-stu-id="226d9-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="226d9-120">Jeśli nie masz jeszcze zainstalowany program Visual Studio 2013, zostanie zainstalowany przez to łącze.</span><span class="sxs-lookup"><span data-stu-id="226d9-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="226d9-121">Ten samouczek wymaga programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="226d9-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="226d9-122">[Zestaw Azure SDK dla programu Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="226d9-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="226d9-123">W oknie Instalatora platformy sieci Web kliknij **zainstalować** i kontynuować instalację.</span><span class="sxs-lookup"><span data-stu-id="226d9-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="226d9-124">Należy również emulatora przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="226d9-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="226d9-125">Działa jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="226d9-125">Any of the following will work:</span></span>

* <span data-ttu-id="226d9-126">Emulator przeglądarki w [narzędzi deweloperskich programu Internet Explorer 11 F12] [ EmulatorIE11] (używane na wszystkich przeglądarkę dla telefonów zrzutach ekranu).</span><span class="sxs-lookup"><span data-stu-id="226d9-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="226d9-127">Ma ona predefiniowane ciąg agenta użytkownika dla systemu Windows Phone 8, Windows Phone 7 i iPad firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="226d9-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="226d9-128">Emulator przeglądarki w [DevTools Google Chrome][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="226d9-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="226d9-129">Zawiera ustawienia dla wielu urządzeń z systemem Android, a także Apple iPhone, iPad firmy Apple oraz Amazon Kindle Fire.</span><span class="sxs-lookup"><span data-stu-id="226d9-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="226d9-130">Emuluje on również zdarzenia touch.</span><span class="sxs-lookup"><span data-stu-id="226d9-130">It also emulates touch events.</span></span>
* <span data-ttu-id="226d9-131">[Opera emulatorze przenośnym][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="226d9-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="226d9-132">Projekty Visual Studio z C\# kodu źródłowego są dostępne powiązany z tym tematem:</span><span class="sxs-lookup"><span data-stu-id="226d9-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="226d9-133">[Początkowy projektem do pobrania][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="226d9-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="226d9-134">[Pobranie projektu zakończone][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="226d9-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="226d9-135"><a name="bkmk_DeployStarterProject"></a>Wdrażanie projektu początkową aplikację sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="226d9-135"><a name="bkmk_DeployStarterProject"></a>Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="226d9-136">Pobierz aplikację listy konferencji [projektu starter][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="226d9-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="226d9-137">Następnie w Eksploratorze Windows, kliknij prawym przyciskiem myszy pobrany plik ZIP i wybierz *właściwości*.</span><span class="sxs-lookup"><span data-stu-id="226d9-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="226d9-138">W **właściwości** oknie dialogowym wybierz **Odblokuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="226d9-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="226d9-139">(Odblokowywania uniemożliwia ostrzeżenie występuje, gdy użytkownik próbuje użyć *.zip* pliku pobranym z sieci web.)</span><span class="sxs-lookup"><span data-stu-id="226d9-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="226d9-140">Kliknij prawym przyciskiem myszy plik ZIP, a następnie wybierz **Wyodrębnij wszystkie** aby rozpakować plik.</span><span class="sxs-lookup"><span data-stu-id="226d9-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="226d9-141">W programie Visual Studio Otwórz *C#\Mvc5Mobile.sln* pliku.</span><span class="sxs-lookup"><span data-stu-id="226d9-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="226d9-142">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="226d9-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="226d9-143">Na publikowanie w sieci Web, kliknij **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="226d9-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="226d9-144">Jeśli jeszcze nie zostało to jeszcze zalogowania na platformie Azure, kliknij przycisk **Dodaj konto**.</span><span class="sxs-lookup"><span data-stu-id="226d9-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="226d9-145">Postępuj zgodnie z monitami, aby zalogować się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="226d9-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="226d9-146">Usługi aplikacji — okno dialogowe powinna zostać wyświetlona zostanie jako zalogowany.</span><span class="sxs-lookup"><span data-stu-id="226d9-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="226d9-147">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="226d9-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="226d9-148">W **Nazwa aplikacji sieci Web** określ prefiks nazwy aplikacji unikatowy.</span><span class="sxs-lookup"><span data-stu-id="226d9-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="226d9-149">Twoje Pełna nazwa aplikacji sieci web będzie  *&lt;prefiks >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="226d9-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="226d9-150">Ponadto wybierz lub określ nazwę nowej grupy zasobów w **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="226d9-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="226d9-151">Następnie kliknij przycisk **nowy** Aby utworzyć nowy plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="226d9-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="226d9-152">Skonfiguruj nowy plan usługi aplikacji, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="226d9-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="226d9-153">W oknie dialogowym Tworzenie usługi App Service kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="226d9-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="226d9-154">Po Azure zasoby są tworzone, publikowanie w sieci Web okna dialogowego zostaną wypełnione przy użyciu ustawień dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="226d9-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="226d9-155">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="226d9-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="226d9-156">Gdy program Visual Studio zakończy publikowanie projektu starter do aplikacji sieci web platformy Azure, pulpitu przeglądarce zostanie otwarty do wyświetlenia aplikacji sieci web na żywo.</span><span class="sxs-lookup"><span data-stu-id="226d9-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="226d9-157">Uruchom z emulatora przeglądarkę dla telefonów, skopiuj adres URL dla aplikacji konferencji (*<prefix>*. azurewebsites.net) w emulatorze, a następnie kliknij przycisk prawym górnym rogu i wybierz **Przeglądaj według znaczników**.</span><span class="sxs-lookup"><span data-stu-id="226d9-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="226d9-158">Jeśli korzystasz z programu Internet Explorer 11 jako domyślnej przeglądarki, wystarczy wpisać `F12`, następnie `Ctrl+8`, a następnie zmień profilu przeglądarki, aby **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="226d9-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="226d9-159">Obraz poniżej przedstawia *alltags —* widok w trybie portret (wybór **Przeglądaj według znaczników**).</span><span class="sxs-lookup"><span data-stu-id="226d9-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="226d9-160">Podczas można debugować aplikacji MVC 5 z poziomu programu Visual Studio, możesz opublikować aplikację sieci web Azure ponownie, aby zweryfikować aplikacji sieci web bezpośrednio w przeglądarce przenośnych lub w emulatorze przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="226d9-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="226d9-161">Ekran jest bardzo do odczytu na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="226d9-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="226d9-162">Można także już widoczne niektóre efekty wizualne zastosowane przez platformę Bootstrap CSS.</span><span class="sxs-lookup"><span data-stu-id="226d9-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="226d9-163">Kliknij przycisk **ASP.NET** łącza.</span><span class="sxs-lookup"><span data-stu-id="226d9-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="226d9-164">Widok znaczników ASP.NET jest zainstalowane powiększenia do ekranu, która obsługuje można automatycznie ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="226d9-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="226d9-165">Jednak może poprawić ten widok, aby lepiej dopasować przenośnych przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="226d9-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="226d9-166">Na przykład **data** kolumna jest trudny do odczytania.</span><span class="sxs-lookup"><span data-stu-id="226d9-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="226d9-167">W dalszej części tego samouczka zostanie zmieniona *alltags —* widok, aby była przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <span data-ttu-id="226d9-168"><a name="bkmk_bootstrap"></a>Framework bootstrap CSS</span><span class="sxs-lookup"><span data-stu-id="226d9-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="226d9-169">Nowe MVC 5 szablon jest wbudowana obsługa ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="226d9-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="226d9-170">Ma już widoczny, jak od razu zwiększa różne widoki w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="226d9-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="226d9-171">Na przykład pasek nawigacyjny u góry jest zwijany automatycznie, gdy szerokość przeglądarki jest mniejsza.</span><span class="sxs-lookup"><span data-stu-id="226d9-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="226d9-172">W przeglądarce pulpitu należy spróbować zmienić rozmiar okna przeglądarki i zobacz, jak na pasku nawigacyjnym zmienia jego wygląd i działanie.</span><span class="sxs-lookup"><span data-stu-id="226d9-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="226d9-173">Jest to projekt dynamiczne sieci web, który jest wbudowany w ładowania początkowego.</span><span class="sxs-lookup"><span data-stu-id="226d9-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="226d9-174">Aby zobaczyć, jak będzie wyglądać aplikacji sieci Web bez ładowania początkowego, otwórz *aplikacji\_Start\\BundleConfig.cs* ujmij w komentarz wierszy, które zawierają *bootstrap.js* i  *bootstrap.CSS*.</span><span class="sxs-lookup"><span data-stu-id="226d9-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="226d9-175">Poniższy kod przedstawia dwa ostatnie instrukcje `RegisterBundles` metody po zmianie:</span><span class="sxs-lookup"><span data-stu-id="226d9-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="226d9-176">Naciśnij klawisz `Ctrl+F5` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="226d9-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="226d9-177">Sprawdź na pasku nawigacyjnym zwijanej jest teraz wystarczy zwykłe nieuporządkowaną listę.</span><span class="sxs-lookup"><span data-stu-id="226d9-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="226d9-178">Kliknij przycisk **Przeglądaj według znaczników** ponownie, następnie kliknij przycisk **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="226d9-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="226d9-179">W widoku emulatorze przenośnym widać, nie jest już zainstalowane powiększenia do ekranu i musieli przewijać bok aby zobaczyć prawej tabeli.</span><span class="sxs-lookup"><span data-stu-id="226d9-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="226d9-180">Cofnij zmiany i odświeżyć przeglądarkę przenośnych, aby sprawdzić, czy wyświetlana przyjazna została przywrócona.</span><span class="sxs-lookup"><span data-stu-id="226d9-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="226d9-181">Ładowania początkowego nie jest specyficzne dla platformy ASP.NET MVC 5, a w dowolnej aplikacji sieci web mogą korzystać z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="226d9-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="226d9-182">Ale teraz są wbudowane w szablon projektu programu ASP.NET MVC 5, dzięki czemu aplikacja sieci MVC 5 Web można korzystać z Bootstrap domyślnie.</span><span class="sxs-lookup"><span data-stu-id="226d9-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="226d9-183">Aby uzyskać więcej informacji na temat ładowania początkowego, przejdź do [Bootstrap] [ BootstrapSite] lokacji.</span><span class="sxs-lookup"><span data-stu-id="226d9-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="226d9-184">W następnej sekcji pojawi się, jak zapewnić konkretnych widoków mobile przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="226d9-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <span data-ttu-id="226d9-185"><a name="bkmk_overrideviews"></a>Zastąpienie widoki, układów i widoki częściowe</span><span class="sxs-lookup"><span data-stu-id="226d9-185"><a name="bkmk_overrideviews"></a> Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="226d9-186">Można zastąpić dowolnym widoku (w tym układy i widoki częściowe) dla przeglądarki dla urządzeń przenośnych ogólnie rzecz biorąc, poszczególne przeglądarkę dla telefonów lub dowolnej przeglądarki określone.</span><span class="sxs-lookup"><span data-stu-id="226d9-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="226d9-187">W celu zapewnienia przeglądu specyficzne dla mobilnych, skopiuj plik widoku i Dodaj *. Mobile* do nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="226d9-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="226d9-188">Na przykład, aby utworzyć przenośnym *indeksu* widoku, możesz skopiować *widoków\\Home\\Index.cshtml* do *widoków\\Home\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="226d9-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="226d9-189">W tej sekcji utworzysz plik układu specyficzne dla mobilnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="226d9-190">Aby rozpocząć, skopiuj *widoków\\Shared\\\_Layout.cshtml* do *widoków\\Shared\\\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="226d9-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="226d9-191">Otwórz  *\_Layout.Mobile.cshtml* i Zmień tytuł z **aplikacji MVC5** do **MVC5 aplikacji (Mobile)**.</span><span class="sxs-lookup"><span data-stu-id="226d9-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="226d9-192">W każdym `Html.ActionLink` wymagać pasku nawigacyjnym, Usuń "Przeglądaj według", w każdym odnośniku *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="226d9-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="226d9-193">Poniższy kod przedstawia ukończonej `<ul class="nav navbar-nav">` tag pliku przenośnych układu.</span><span class="sxs-lookup"><span data-stu-id="226d9-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="226d9-194">Kopiuj *widoków\\Home\\AllTags.cshtml* pliku na *widoków\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="226d9-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="226d9-195">Otwórz nowy plik i zmień `<h2>` element na podstawie "Tagi" do "tagi (M)":</span><span class="sxs-lookup"><span data-stu-id="226d9-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="226d9-196">Przejdź do strony tagów za pomocą przeglądarki pulpitu i przy użyciu emulatora przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="226d9-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="226d9-197">Emulator przeglądarkę dla telefonów zawiera dwie zmiany (tytuł z  *\_Layout.Mobile.cshtml* i tytuł z *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="226d9-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="226d9-198">Z kolei Monitor nie zmienił się (tytułów z  *\_Layout.cshtml* i *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="226d9-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="226d9-199"><a name="bkmk_browserviews"></a>Utwórz widoki specyficzne dla przeglądarki</span><span class="sxs-lookup"><span data-stu-id="226d9-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="226d9-200">Oprócz mobile dotyczące pulpitu i widoki można tworzyć widoki dla poszczególnych przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="226d9-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="226d9-201">Na przykład można tworzyć widoki, które są przeznaczone dla telefonów iPhone lub przeglądarki systemu Android.</span><span class="sxs-lookup"><span data-stu-id="226d9-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="226d9-202">W tej sekcji utworzysz układu dla przeglądarki iPhone i wersji iPhone *alltags —* widoku.</span><span class="sxs-lookup"><span data-stu-id="226d9-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="226d9-203">Otwórz *Global.asax* pliku i Dodaj następujący kod do dołu `Application_Start` metody.</span><span class="sxs-lookup"><span data-stu-id="226d9-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="226d9-204">Ten kod definiuje nowy tryb wyświetlania o nazwie "iPhone" pasujących względem każdego żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="226d9-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="226d9-205">Jeśli żądanie przychodzące odpowiada warunku, zdefiniowane przez użytkownika (jeśli agent użytkownika zawiera ciąg "iPhone"), platformy ASP.NET MVC sprawdza widoki, których nazwa zawiera sufiksu "iPhone".</span><span class="sxs-lookup"><span data-stu-id="226d9-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="226d9-206">Podczas dodawania trybów wyświetlania przeglądarki dotyczące przenośnych, takie jak w przypadku telefonów iPhone i Android, upewnij się ustawić pierwszy argument `0` (Wstaw na początku listy) aby upewnić się, tryb specyficzne dla przeglądarki ma pierwszeństwo przed przenośnych szablonu (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="226d9-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="226d9-207">Jeśli szablon przenośnych jest na początku listy, zostanie wybrany na tryb wyświetlania zamierzone (pierwszy wins dopasowania i przenośnych szablonu dopasowuje wszystkie przeglądarki dla urządzeń przenośnych).</span><span class="sxs-lookup"><span data-stu-id="226d9-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="226d9-208">W kodzie, kliknij prawym przyciskiem myszy `DefaultDisplayMode`, wybierz **rozwiązać**, a następnie wybierz pozycję `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="226d9-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="226d9-209">Spowoduje to dodanie odwołania do `System.Web.WebPages` przestrzeni nazw, czyli gdzie `DisplayModeProvider` i `DefaultDisplayMode` typy zostały zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="226d9-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="226d9-210">Alternatywnie można po prostu ręcznie dodaj następujący wiersz do `using` sekcji pliku.</span><span class="sxs-lookup"><span data-stu-id="226d9-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="226d9-211">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="226d9-211">Save the changes.</span></span> <span data-ttu-id="226d9-212">Kopia *widoków\\Shared\\\_Layout.Mobile.cshtml* pliku na *widoków\\współużytkowane\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="226d9-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="226d9-213">Otwórz nowy plik, a następnie zmień tytuł z `MVC5 Application (Mobile)` do `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="226d9-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="226d9-214">Kopiuj *widoków\\Home\\AllTags.Mobile.cshtml* pliku na *widoków\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="226d9-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="226d9-215">W nowym pliku zmienić `<h2>` element z "tagi (M)" do "Tagów (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="226d9-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="226d9-216">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="226d9-216">Run the application.</span></span> <span data-ttu-id="226d9-217">Uruchamianie emulatora przeglądarkę dla telefonów, upewnij się, że jego agenta użytkownika ma ustawioną wartość "iPhone" i przejdź do *alltags —* widoku.</span><span class="sxs-lookup"><span data-stu-id="226d9-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="226d9-218">Jeśli używasz emulatora w narzędzi deweloperskich programu Internet Explorer 11 naciśnięcia klawisza F12, Konfiguracja funkcji emulacji do następującego:</span><span class="sxs-lookup"><span data-stu-id="226d9-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="226d9-219">Profil przeglądarki = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="226d9-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="226d9-220">Ciąg agenta użytkownika = **niestandardowe**</span><span class="sxs-lookup"><span data-stu-id="226d9-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="226d9-221">Niestandardowy ciąg = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="226d9-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="226d9-222">Poniższy zrzut ekranu przedstawia *alltags —* widok renderowany w emulatorze w narzędzi deweloperskich programu Internet Explorer 11 F12 z niestandardowy ciąg agenta użytkownika (jest to ciąg agenta użytkownika iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="226d9-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="226d9-223">W przeglądarce przenośnym, wybierz **głośniki** łącza.</span><span class="sxs-lookup"><span data-stu-id="226d9-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="226d9-224">Ponieważ nie jest widokiem dla urządzeń przenośnych (*AllSpeakers.Mobile.cshtml*), wyświetlanie głośniki domyślne (*AllSpeakers.cshtml*) jest renderowany przy użyciu widoku układu przenośnych ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="226d9-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="226d9-225">Jak pokazano poniżej, tytuł **MVC5 aplikacji (Mobile)** jest zdefiniowany w  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="226d9-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="226d9-226">Widok domyślny (nieprzenośnych) z renderowania w układzie przenośnych globalnie można wyłączyć, ustawiając `RequireConsistentDisplayMode` do `true` w *widoków\\\_ViewStart.cshtml* pliku następująco:</span><span class="sxs-lookup"><span data-stu-id="226d9-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="226d9-227">Gdy `RequireConsistentDisplayMode` ma ustawioną wartość `true`, przenośnych układu (*\_Layout.Mobile.cshtml*) jest używany tylko dla widoków przenośnych (tj. gdy plik widok jest w formie  ***ViewName**. Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="226d9-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="226d9-228">Należy ustawić `RequireConsistentDisplayMode` do `true` Jeśli przenośnych układu nie działa prawidłowo w przypadku widoków przeznaczone dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="226d9-229">Zrzut ekranu poniżej przedstawiono sposób *głośniki* renderowania strony, gdy `RequireConsistentDisplayMode` ma ustawioną wartość `true` (bez ciąg "(wersja Mobile)" na pasku nawigacji u góry).</span><span class="sxs-lookup"><span data-stu-id="226d9-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="226d9-230">Spójnego trybu wyświetlania w określonym widoku można wyłączyć, ustawiając `RequireConsistentDisplayMode` do `false` w pliku widoku.</span><span class="sxs-lookup"><span data-stu-id="226d9-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="226d9-231">Następujący kod w *widoków\\Home\\AllSpeakers.cshtml* plików zestawów `RequireConsistentDisplayMode` do `false`:</span><span class="sxs-lookup"><span data-stu-id="226d9-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="226d9-232">W tej sekcji możemy przedstawiono sposób tworzenia widoków i układy przenośnych oraz sposobu tworzenia widoków dla konkretnych urządzeń, takich jak telefonów iPhone i układów.</span><span class="sxs-lookup"><span data-stu-id="226d9-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="226d9-233">Główną zaletą framework CSS ładowania początkowego jest jednak elastyczny układ, co oznacza, że jednego arkusza stylów mogą być stosowane przez pulpitu, telefon i tablet przeglądarki do utworzenia spójny wygląd i zachowanie.</span><span class="sxs-lookup"><span data-stu-id="226d9-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="226d9-234">W następnej sekcji pojawi się, jak wykorzystać ładowania początkowego tworzenia widoków przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <span data-ttu-id="226d9-235"><a name="bkmk_Improvespeakerslist"></a>Poprawa listy głośniki</span><span class="sxs-lookup"><span data-stu-id="226d9-235"><a name="bkmk_Improvespeakerslist"></a> Improve the Speakers List</span></span>
<span data-ttu-id="226d9-236">Jak został wyświetlony, *głośniki* widoku jest możliwy do odczytu, ale łącza są małe i są trudne do naciśnij na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="226d9-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="226d9-237">W tej sekcji należy podjąć *AllSpeakers* wyświetlić przyjaznych dla urządzeń przenośnych, który wyświetla dużych, łatwe wybranie łącza i zawiera pole wyszukiwania, aby szybko znaleźć głośniki.</span><span class="sxs-lookup"><span data-stu-id="226d9-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="226d9-238">Można użyć ładowania początkowego programu [listy połączonej grupy] [ linked list group] stylów zwiększające *głośniki* widoku.</span><span class="sxs-lookup"><span data-stu-id="226d9-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="226d9-239">W *widoków\\Home\\AllSpeakers.cshtml*, Zastąp zawartość pliku Razor przy użyciu poniższego kodu.</span><span class="sxs-lookup"><span data-stu-id="226d9-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

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

<span data-ttu-id="226d9-240">`class="list-group"` Atrybutu w `<div>` znacznik stosuje style Bootstrap listy i `class="input-group-item"` atrybut dotyczy stylów elementu listy Bootstrap każdego łącza.</span><span class="sxs-lookup"><span data-stu-id="226d9-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="226d9-241">Odśwież przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="226d9-241">Refresh the mobile browser.</span></span> <span data-ttu-id="226d9-242">Widok zaktualizowanej wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="226d9-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="226d9-243">Ładowania początkowego programu [listy połączonej grupy] [ linked list group] stylów sprawia, że całe okno dla każdego łącza, które są aktywne, czyli znacznie lepsze środowisko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="226d9-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="226d9-244">Przełącz do widoku pulpitu i obserwować spójny wygląd i zachowanie.</span><span class="sxs-lookup"><span data-stu-id="226d9-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="226d9-245">Chociaż widoku przeglądarkę dla telefonów została ulepszona i jest trudno długą listę głośniki.</span><span class="sxs-lookup"><span data-stu-id="226d9-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="226d9-246">Ładowania początkowego nie zapewnia wyszukiwania filtr funkcji out-of box, ale można go dodać przy użyciu kilku wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="226d9-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="226d9-247">Należy najpierw dodać pole wyszukiwania do widoku, a następnie podłączanie z kodu JavaScript dla funkcji filtru.</span><span class="sxs-lookup"><span data-stu-id="226d9-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="226d9-248">W *widoków\\Home\\AllSpeakers.cshtml*, Dodaj \<formularza\> tuż po tagu \<h2\> tagów, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="226d9-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

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

<span data-ttu-id="226d9-249">Zwróć uwagę, że `<form>` i `<input>` tagi zarówno ma ładowania początkowego stylów zastosowanych do nich.</span><span class="sxs-lookup"><span data-stu-id="226d9-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="226d9-250">`<span>` Element dodaje Bootstrap [glyphicon] [ glyphicon] do pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="226d9-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="226d9-251">W *skryptów* folderu, Dodaj plik JavaScript o nazwie *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="226d9-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="226d9-252">Otwórz plik i Wklej do niego następujący kod:</span><span class="sxs-lookup"><span data-stu-id="226d9-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
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

<span data-ttu-id="226d9-253">Należy również uwzględnić filter.js w Twojej zarejestrowanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="226d9-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="226d9-254">Otwórz *aplikacji\_Start\\BundleConfig.cs* i Zmień pierwszy pakietów.</span><span class="sxs-lookup"><span data-stu-id="226d9-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="226d9-255">Zmień pierwsze `bundles.Add` instrukcji (dla **jquery** pakietu) do uwzględnienia *skryptów\\filter.js*w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="226d9-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="226d9-256">**Jquery** pakietu jest już renderowana przez domyślny  *\_układu* widoku.</span><span class="sxs-lookup"><span data-stu-id="226d9-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="226d9-257">Później możesz użyć tego samego kodu JavaScript do zastosowania funkcji filtrowania z innymi widokami listy.</span><span class="sxs-lookup"><span data-stu-id="226d9-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="226d9-258">Odśwież przeglądarkę dla telefonów i przejdź do *AllSpeakers* widoku.</span><span class="sxs-lookup"><span data-stu-id="226d9-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="226d9-259">W polu wyszukiwania wpisz "sc".</span><span class="sxs-lookup"><span data-stu-id="226d9-259">In the search box, type "sc".</span></span> <span data-ttu-id="226d9-260">Na liście głośniki teraz powinny być filtrowane według ciąg wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="226d9-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="226d9-261"><a name="bkmk_improvetags"></a>Poprawa listy tagów</span><span class="sxs-lookup"><span data-stu-id="226d9-261"><a name="bkmk_improvetags"></a> Improve the Tags List</span></span>
<span data-ttu-id="226d9-262">Podobnie jak *głośniki* widoku *tagi* widoku jest możliwy do odczytu, ale łącza są małe i trudne do naciśnij na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="226d9-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="226d9-263">Problem można rozwiązać *tagi* wyświetlać ten sam sposób, w rozwiązaniu *głośniki* wyświetlić, korzystając z opisanych wcześniej, ale z następującymi zmian w kodzie `Html.ActionLink` składni metody w *widoków\\ Strona główna\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="226d9-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="226d9-264">Odświeżyć przeglądarkę dla komputerów wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="226d9-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="226d9-265">I odświeżyć przeglądarkę dla telefonów wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="226d9-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="226d9-266">Jeśli zauważysz, że oryginalne formatowanie listy nadal znajduje się w przeglądarce przenośnych i zastanawiasz się, co się stało z nieuprzywilejowany Bootstrap związanych ze stylami, to artefaktu użytkownika wcześniejszą akcję w celu utworzenia przenośnych konkretnych widoków.</span><span class="sxs-lookup"><span data-stu-id="226d9-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="226d9-267">Jednak teraz, aby utworzyć projekt sieci web reakcji przy użyciu framework Bootstrap CSS Przejdź head i usuń te widoki specyficzne dla mobilnych i widoki specyficzne dla mobile układu.</span><span class="sxs-lookup"><span data-stu-id="226d9-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="226d9-268">Po wykonaniu czynności odświeżyć przeglądarkę dla telefonów wyświetli Bootstrap style.</span><span class="sxs-lookup"><span data-stu-id="226d9-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="226d9-269"><a name="bkmk_improvedates"></a>Poprawa listy dat</span><span class="sxs-lookup"><span data-stu-id="226d9-269"><a name="bkmk_improvedates"></a> Improve the Dates List</span></span>
<span data-ttu-id="226d9-270">Można zwiększyć *dat* wyświetlania, takich jak zwiększona możesz *głośniki* i *tagi* widoków, jeśli używasz zmiany kodu opisanego wcześniej, ale z następującymi `Html.ActionLink` Składnia metody w *widoków\\Home\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="226d9-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="226d9-271">Otrzymasz widoku odświeżyć przeglądarkę dla telefonów następująco:</span><span class="sxs-lookup"><span data-stu-id="226d9-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="226d9-272">Można jeszcze bardziej poprawić *dat* widoku poprzez organizowanie wartości daty i godziny według daty.</span><span class="sxs-lookup"><span data-stu-id="226d9-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="226d9-273">Można to zrobić z ładowania początkowego programu [panele] [ panels] style.</span><span class="sxs-lookup"><span data-stu-id="226d9-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="226d9-274">Zastąp zawartość *widoków\\Home\\AllDates.cshtml* pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="226d9-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="226d9-275">Ten kod tworzy oddzielne `<div class="panel panel-primary">` tagu dla każdej różne daty na liście i używa [listy połączonej grupy] [ linked list group] dla odpowiednich łączy jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="226d9-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="226d9-276">Oto przeglądarkę dla telefonów wygląd po uruchomieniu tego kodu:</span><span class="sxs-lookup"><span data-stu-id="226d9-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="226d9-277">Przełącz się do pulpitów przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="226d9-277">Switch to the desktop browser.</span></span> <span data-ttu-id="226d9-278">Ponownie należy zwrócić uwagę spójny wygląd.</span><span class="sxs-lookup"><span data-stu-id="226d9-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="226d9-279"><a name="bkmk_improvesessionstable"></a>Poprawa widoku SessionsTable</span><span class="sxs-lookup"><span data-stu-id="226d9-279"><a name="bkmk_improvesessionstable"></a> Improve the SessionsTable View</span></span>
<span data-ttu-id="226d9-280">W tej sekcji należy podjąć *SessionsTable* wyświetlić więcej przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="226d9-281">Ta zmiana jest bardziej rozległych wcześniejszych zmian.</span><span class="sxs-lookup"><span data-stu-id="226d9-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="226d9-282">W przeglądarce przenośnym, wybierz **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="226d9-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="226d9-283">Wybierz **ASP.NET** łącza.</span><span class="sxs-lookup"><span data-stu-id="226d9-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="226d9-284">Jak widać, ekran jest w formacie tabeli, która obecnie jest przeznaczony do wyświetlania w przeglądarce pulpitu.</span><span class="sxs-lookup"><span data-stu-id="226d9-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="226d9-285">Jednak nieco trudno jest do odczytu w przeglądarce przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="226d9-286">Aby rozwiązać ten problem, otwórz *widoków\\Home\\SessionsTable.cshtml* i Zastąp zawartość pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="226d9-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

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

<span data-ttu-id="226d9-287">Kod wykonuje 3 rzeczy:</span><span class="sxs-lookup"><span data-stu-id="226d9-287">The code does 3 things:</span></span>

* <span data-ttu-id="226d9-288">używa ładowania początkowego programu [niestandardowe listy połączonej grupy] [ custom linked list group] sformatować informacji o sesji w pionie, tak aby te informacje są przeznaczone do odczytu w przeglądarce przenośnych (przy użyciu klas, takie jak listy grupy elementu tekst)</span><span class="sxs-lookup"><span data-stu-id="226d9-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="226d9-289">stosuje [systemu siatki] [ grid system] do układu, tak aby elementy sesji poziomie przepływu w przeglądarce dla komputerów i w pionie w przeglądarce przenośnych (przy użyciu klasy col-md-4)</span><span class="sxs-lookup"><span data-stu-id="226d9-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="226d9-290">używa [reakcji narzędzia] [ responsive utilities] ukrycia znaczników sesji podczas wyświetlania w przeglądarce przenośnych (przy użyciu klasy xs ukryte)</span><span class="sxs-lookup"><span data-stu-id="226d9-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="226d9-291">Można również wybrać link tytuł można przejść do odpowiedniej sesji.</span><span class="sxs-lookup"><span data-stu-id="226d9-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="226d9-292">Na poniższym obrazie odzwierciedla zmiany kodu.</span><span class="sxs-lookup"><span data-stu-id="226d9-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="226d9-293">System ładowania początkowego siatki, który automatycznie zastosować rozmieszcza sesji w pionie w przeglądarce przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="226d9-294">Zauważ również, że tagi nie są pokazywane.</span><span class="sxs-lookup"><span data-stu-id="226d9-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="226d9-295">Przełącz się do pulpitów przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="226d9-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="226d9-296">W przeglądarce pulpitu Zwróć uwagę, znaczniki są teraz wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="226d9-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="226d9-297">Ponadto widać, że system ładowania początkowego siatki zastosowane Rozmieszcza elementy sesji w dwóch kolumnach.</span><span class="sxs-lookup"><span data-stu-id="226d9-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="226d9-298">Powiększenie przeglądarki, zobaczysz, że rozmieszczenia zmienia się na trzy kolumny.</span><span class="sxs-lookup"><span data-stu-id="226d9-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <span data-ttu-id="226d9-299"><a name="bkmk_improvesessionbycode"></a>Poprawa widoku SessionByCode</span><span class="sxs-lookup"><span data-stu-id="226d9-299"><a name="bkmk_improvesessionbycode"></a> Improve the SessionByCode View</span></span>
<span data-ttu-id="226d9-300">Na koniec będzie naprawić *SessionByCode* widok, aby była przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="226d9-301">W przeglądarce przenośnym, wybierz **Tag** przycisk, a następnie wprowadź `asp` w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="226d9-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="226d9-302">Wybierz **ASP.NET** łącza.</span><span class="sxs-lookup"><span data-stu-id="226d9-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="226d9-303">Sesje dla tagu ASP.NET są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="226d9-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="226d9-304">Wybierz **tworzenia aplikacji jednej strony ASP.NET i AngularJS** łącza.</span><span class="sxs-lookup"><span data-stu-id="226d9-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="226d9-305">Domyślny widok pulpitu działa poprawnie, ale może poprawić wygląd łatwo za pomocą niektórych składników Bootstrap graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="226d9-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="226d9-306">Otwórz *widoków\\Home\\SessionByCode.cshtml* i Zastąp zawartość następujący kod:</span><span class="sxs-lookup"><span data-stu-id="226d9-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

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

<span data-ttu-id="226d9-307">Znaczników nowej używa Bootstrap paneli Style zwiększające widokiem dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="226d9-308">Odśwież przeglądarkę dla telefonów.</span><span class="sxs-lookup"><span data-stu-id="226d9-308">Refresh the mobile browser.</span></span> <span data-ttu-id="226d9-309">Poniższa ilustracja odzwierciedla zmiany kodu, które zostały wykonane:</span><span class="sxs-lookup"><span data-stu-id="226d9-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="226d9-310">Dobiega końca i przejrzyj</span><span class="sxs-lookup"><span data-stu-id="226d9-310">Wrap Up and Review</span></span>
<span data-ttu-id="226d9-311">W tym samouczku ma pokazano, jak używać programu ASP.NET MVC 5 do tworzenia aplikacji sieci Web przyjaznych dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="226d9-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="226d9-312">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="226d9-312">These include:</span></span>

* <span data-ttu-id="226d9-313">Wdrażanie aplikacji ASP.NET MVC 5 do aplikacji sieci web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="226d9-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="226d9-314">Użyj Bootstrap, aby utworzyć układ dynamiczne sieci web w aplikacji MVC 5</span><span class="sxs-lookup"><span data-stu-id="226d9-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="226d9-315">Zastąpienie układu, widoków i widoki częściowe, globalnie i dla poszczególnych widoku</span><span class="sxs-lookup"><span data-stu-id="226d9-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="226d9-316">Układ formantu i częściowy przesłonić przy użyciu wymuszania `RequireConsistentDisplayMode` właściwości</span><span class="sxs-lookup"><span data-stu-id="226d9-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="226d9-317">Utwórz widoki, które odnoszą się do przeglądarki, takich jak przeglądarki iPhone</span><span class="sxs-lookup"><span data-stu-id="226d9-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="226d9-318">Zastosuj style Bootstrap w kodzie Razor</span><span class="sxs-lookup"><span data-stu-id="226d9-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="226d9-319">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="226d9-319">See Also</span></span>
* [<span data-ttu-id="226d9-320">9 podstawowe zasady reakcji projektowanie witryn sieci web</span><span class="sxs-lookup"><span data-stu-id="226d9-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="226d9-321">[Ładowania początkowego][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="226d9-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="226d9-322">[Oficjalny Blog ładowania początkowego][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="226d9-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="226d9-323">[Twitter Bootstrap samouczek z Republika samouczka][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="226d9-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="226d9-324">[Bootstrap Plac zabaw dla][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="226d9-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="226d9-325">[W3C zalecenie przenośnych sieci Web aplikacji najlepsze rozwiązania][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="226d9-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="226d9-326">[Zalecenie Candidate W3C zapytaniami multimediów][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="226d9-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="226d9-327">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="226d9-327">What's changed</span></span>
* <span data-ttu-id="226d9-328">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="226d9-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

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
[The Bootstrap Playground]: http://www.bootply.com/
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

