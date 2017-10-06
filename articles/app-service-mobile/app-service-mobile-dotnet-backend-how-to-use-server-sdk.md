---
title: "toowork aaaHow z serwera wewnętrznej bazy danych hello .NET SDK for Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toowork z serwera wewnętrznej bazy danych .NET SDK usługi Azure App Service Mobile Apps."
keywords: "usługi aplikacji, usługa aplikacji azure, aplikacji mobilnej, usługi mobilnej, wdrażanie aplikacji wdrożenia usługi azure app skali, skalowalna,"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="31527-104">Praca z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="31527-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="31527-105">W tym temacie pokazano, jak toouse hello serwera wewnętrznej bazy danych .NET SDK w różnych kluczowych scenariuszy Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="31527-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="31527-106">zestaw SDK usługi Azure Mobile Apps Hello pomaga w pracy z klientów mobilnych, z poziomu aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="31527-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="31527-107">Witaj [serwer .NET SDK usługi Azure Mobile Apps] [ 2] jest typu open source w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="31527-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="31527-108">Witaj repozytorium zawiera wszystkie kodu źródłowego, w tym zestaw testów jednostkowych hello całego serwera zestawu SDK i kilka przykładowych projektach.</span><span class="sxs-lookup"><span data-stu-id="31527-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="31527-109">Dokumentacja referencyjna</span><span class="sxs-lookup"><span data-stu-id="31527-109">Reference documentation</span></span>
<span data-ttu-id="31527-110">Hello dokumentacji powitania serwera zestawu SDK jest zlokalizowana tutaj: [Azure Mobile Apps .NET Reference][1].</span><span class="sxs-lookup"><span data-stu-id="31527-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="31527-111"><a name="create-app"></a>Porady: tworzenie zaplecza aplikacji mobilnej platformy .NET</span><span class="sxs-lookup"><span data-stu-id="31527-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="31527-112">Jeśli uruchamiasz nowego projektu można utworzyć aplikację usługi aplikacji przy użyciu albo hello [portalu Azure] lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31527-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="31527-113">Można uruchomić lokalnie hello aplikacji usługi App Service lub opublikować hello projektu tooyour oparte na chmurze usługi aplikacji — warstwa aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="31527-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="31527-114">W przypadku dodawania funkcji mobilnych tooan istniejącego projektu, zobacz hello [pobierania i zainicjuj hello SDK](#install-sdk) sekcji.</span><span class="sxs-lookup"><span data-stu-id="31527-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="31527-115">Tworzenie zaplecza .NET przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="31527-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="31527-116">toocreate zaplecza aplikacji mobilnych usługi aplikacji, albo wykonaj hello [samouczek Szybki Start] [ 3] lub wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31527-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="31527-117">Po powrocie do hello *wprowadzenie* bloku, w obszarze **Utwórz tabelę interfejsu API**, wybierz **C#** jako z **język wewnętrznej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="31527-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="31527-118">Kliknij przycisk **Pobierz**, Wyodrębnij komputera lokalnego tooyour pliki skompresowane projektu i otwórz rozwiązanie hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31527-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="31527-119">Tworzenie zaplecza .NET przy użyciu programu Visual Studio 2013 i Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="31527-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="31527-120">Zainstaluj hello [zestawu Azure SDK dla platformy .NET] [ 4] (wersja 2.9.0 lub nowszym) toocreate Azure Mobile Apps projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31527-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="31527-121">Po zainstalowaniu hello zestawu SDK, tworzenie aplikacji ASP.NET przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31527-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="31527-122">Otwórz hello **nowy projekt** okna dialogowego (z *pliku* > **nowy** > **projektu...** ).</span><span class="sxs-lookup"><span data-stu-id="31527-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="31527-123">Rozwiń węzeł **szablony** > **Visual C#**i wybierz **Web**.</span><span class="sxs-lookup"><span data-stu-id="31527-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="31527-124">Wybierz **aplikacji sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="31527-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="31527-125">Wprowadź nazwę projektu hello.</span><span class="sxs-lookup"><span data-stu-id="31527-125">Fill in hello project name.</span></span> <span data-ttu-id="31527-126">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="31527-126">Then click **OK**.</span></span>
5. <span data-ttu-id="31527-127">W obszarze *ASP.NET 4.5.2 szablony*, wybierz pozycję **aplikacji mobilnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="31527-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="31527-128">Sprawdź **Host w chmurze hello** toocreate zaplecza aplikacji mobilnych w hello chmury toowhich można opublikować tego projektu.</span><span class="sxs-lookup"><span data-stu-id="31527-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="31527-129">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="31527-129">Click **OK**.</span></span>

## <span data-ttu-id="31527-130"><a name="install-sdk"></a>Porady: pobieranie i zainicjuj hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="31527-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="31527-131">Witaj zestaw SDK jest dostępny na [NuGet.org]. Ten pakiet zawiera tooget podstawowe funkcje wymagane hello uruchomiony przy użyciu hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="31527-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="31527-132">tooinitialize hello zestawu SDK, należy tooperform akcje na powitania **HttpConfiguration** obiektu.</span><span class="sxs-lookup"><span data-stu-id="31527-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="31527-133">Zainstaluj hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="31527-133">Install hello SDK</span></span>
<span data-ttu-id="31527-134">Witaj tooinstall zestawu SDK, kliknij prawym przyciskiem myszy na powitania serwera projektu programu Visual Studio, wybierz **Zarządzaj pakietami NuGet**, wyszukaj hello [Microsoft.Azure.Mobile.Server] pakietu, a następnie kliknij przycisk  **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="31527-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="31527-135"><a name="server-project-setup"></a>Inicjowanie hello na serwerze project Server</span><span class="sxs-lookup"><span data-stu-id="31527-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="31527-136">Projekt serwera zaplecza .NET jest zainicjowane podobne tooother projekty programu ASP.NET, umieszczając w niej klasę początkową OWIN.</span><span class="sxs-lookup"><span data-stu-id="31527-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="31527-137">Upewnij się, że ma odwołanie do pakietu NuGet hello `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="31527-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="31527-138">tooadd tej klasy w Visual Studio, kliknij prawym przyciskiem myszy projekt serwera i wybierz **Dodaj** >
**nowy element**, następnie **Web**  >  ** Ogólne** > **klasy początkowej OWIN**.</span><span class="sxs-lookup"><span data-stu-id="31527-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="31527-139">Klasa jest generowana za pomocą hello następującego atrybutu:</span><span class="sxs-lookup"><span data-stu-id="31527-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="31527-140">W hello `Configuration()` metoda z klasy początkowej OWIN, użyj **HttpConfiguration** środowisko usługi Azure Mobile Apps hello tooconfigure obiektu.</span><span class="sxs-lookup"><span data-stu-id="31527-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="31527-141">Poniższy przykład Hello inicjuje Projekt serwera hello z nie dodatkowe funkcje:</span><span class="sxs-lookup"><span data-stu-id="31527-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="31527-142">tooenable poszczególne funkcje, należy wywołać metody rozszerzenia na powitania **MobileAppConfiguration** obiekt przed wywołaniem **metody ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="31527-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="31527-143">Dodaje na przykład hello następującego kodu domyślnego hello kieruje kontrolerów tooall interfejsu API, które mają atrybut hello `[MobileAppController]` podczas inicjowania:</span><span class="sxs-lookup"><span data-stu-id="31527-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="31527-144">Szybki Start serwera na powitania z hello Azure wywołania portalu **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="31527-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="31527-145">To odpowiednik toohello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="31527-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="31527-146">metody rozszerzenia Hello używane są:</span><span class="sxs-lookup"><span data-stu-id="31527-146">hello extension methods used are:</span></span>

* <span data-ttu-id="31527-147">`AddMobileAppHomeController()`udostępnia hello domyślną stronę główną usługi Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="31527-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="31527-148">`MapApiControllers()`udostępnia niestandardowego interfejsu API funkcji WebAPI kontrolerów ozdobione hello `[MobileAppController]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="31527-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="31527-149">`AddTables()`udostępnia mapowanie hello `/tables` kontrolerów tootable punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="31527-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="31527-150">`AddTablesWithEntityFramework()`jest skrótowym dla mapowania hello `/tables` kontrolerów na podstawie punktów końcowych przy użyciu programu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="31527-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="31527-151">`AddPushNotifications()`zapewnia prostą metodę rejestrowania urządzeń do usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="31527-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="31527-152">`MapLegacyCrossDomainController()`zawiera standardowe nagłówki CORS dla rozwoju lokalnych.</span><span class="sxs-lookup"><span data-stu-id="31527-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="31527-153">Rozszerzenia zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="31527-153">SDK extensions</span></span>
<span data-ttu-id="31527-154">następujące pakiety NuGet, na podstawie rozszerzenia Hello zapewniają różne funkcje mobilne, które mogą być używane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="31527-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="31527-155">Włącz rozszerzenia podczas inicjowania przy użyciu hello **MobileAppConfiguration** obiektu.</span><span class="sxs-lookup"><span data-stu-id="31527-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="31527-156">[Microsoft.Azure.Mobile.Server.Quickstart] obsługuje hello podstawowa konfiguracja aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="31527-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="31527-157">Konfiguracja toohello dodanych przez wywołanie hello **UseDefaultConfiguration** — metoda rozszerzenia podczas inicjowania.</span><span class="sxs-lookup"><span data-stu-id="31527-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="31527-158">To rozszerzenie zawiera następujące rozszerzenia: powiadomienia, uwierzytelnianie, jednostki, tabel, między domenami i pakiety głównej.</span><span class="sxs-lookup"><span data-stu-id="31527-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="31527-159">Ten pakiet jest używany przez hello Mobile Apps Szybki Start dostępny na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="31527-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="31527-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementuje domyślny hello *tej aplikacji mobilnej jest uruchomiona strona* dla katalogu głównego witryny sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="31527-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="31527-161">Dodaj konfigurację toohello przez wywołanie metody **AddMobileAppHomeController** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="31527-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) zawiera klasy do pracy z potoku danych hello danych i ustawia w górę.</span><span class="sxs-lookup"><span data-stu-id="31527-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="31527-163">Dodaj konfigurację toohello przez wywołanie hello **AddTables** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="31527-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) umożliwia hello Entity Framework tooaccess danych w hello bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="31527-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="31527-165">Dodaj konfigurację toohello przez wywołanie hello **AddTablesWithEntityFramework** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="31527-166">[Microsoft.Azure.Mobile.Server.Authentication] umożliwia uwierzytelnianie i zestawy w górę hello OWIN oprogramowanie pośredniczące używane toovalidate tokenów.</span><span class="sxs-lookup"><span data-stu-id="31527-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="31527-167">Dodaj konfigurację toohello przez wywołanie hello **AddAppServiceAuthentication** i **IAppBuilder**. **UseAppServiceAuthentication** metody rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="31527-168">[Microsoft.Azure.Mobile.Server.Notifications] umożliwia wypychanie powiadomień i definiuje punktu końcowego rejestracji wypychania.</span><span class="sxs-lookup"><span data-stu-id="31527-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="31527-169">Dodaj konfigurację toohello przez wywołanie hello **AddPushNotifications** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="31527-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) tworzy kontroler, który służy toolegacy danych przeglądarki sieci web z aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="31527-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="31527-171">Dodaj konfigurację toohello przez wywołanie metody **MapLegacyCrossDomainController** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="31527-172">[Microsoft.Azure.Mobile.Server.Login] zapewnia hello AppServiceLoginHandler.CreateToken() metodę, która jest metodą statyczną, używane podczas uwierzytelniania niestandardowego scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="31527-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="31527-173"><a name="publish-server-project"></a>Porady: publikowanie projektu serwera hello</span><span class="sxs-lookup"><span data-stu-id="31527-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="31527-174">W tej sekcji przedstawiono, jak toopublish zaplecza .NET projektu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31527-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="31527-175">Można także wdrożyć projektu zaplecza przy użyciu narzędzia Git lub hello żadnego z innych metod opisanych w hello [dokumentacja wdrażania usługi aplikacji Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="31527-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="31527-176">W programie Visual Studio Skompiluj ponownie pakietów NuGet toorestore projektu hello.</span><span class="sxs-lookup"><span data-stu-id="31527-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="31527-177">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello projektu, kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="31527-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="31527-178">Witaj publikowania, po raz pierwszy należy toodefine profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="31527-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="31527-179">Jeśli istnieje już profil zdefiniowane, możesz wybrać go i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="31527-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="31527-180">Pytania tooselect, lokalizacja docelowa publikowania, kliknij przycisk **Microsoft Azure App Service** > **dalej**, a następnie (w razie potrzeby) logowania przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="31527-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="31527-181">Program Visual Studio pobierze i bezpiecznie przechowywane są Twoje ustawienia publikowania bezpośrednio z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="31527-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="31527-182">Wybierz użytkownika **subskrypcji**, wybierz pozycję **typu zasobu** z **widoku**, rozwiń węzeł **aplikacji mobilnej**i kliknij przycisk zaplecza aplikacji mobilnej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="31527-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="31527-183">Sprawdź hello publikowania informacji o profilu i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="31527-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="31527-184">Po zaplecza aplikacji mobilnej został pomyślnie opublikowany, pojawi się Strona początkowa, informujący o powodzeniu.</span><span class="sxs-lookup"><span data-stu-id="31527-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="31527-185"><a name="define-table-controller"></a>Porady: Definiowanie kontrolera tabeli</span><span class="sxs-lookup"><span data-stu-id="31527-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="31527-186">Zdefiniuj tooexpose kontrolera tabeli klientom toomobile tabeli SQL.</span><span class="sxs-lookup"><span data-stu-id="31527-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="31527-187">Konfigurowanie kontrolera tabeli wymaga trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="31527-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="31527-188">Utwórz klasę obiektu transferu danych (DTO).</span><span class="sxs-lookup"><span data-stu-id="31527-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="31527-189">Skonfiguruj odwołania do tabeli w hello klasy Mobile DbContext.</span><span class="sxs-lookup"><span data-stu-id="31527-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="31527-190">Tworzenie kontrolera tabeli.</span><span class="sxs-lookup"><span data-stu-id="31527-190">Create a table controller.</span></span>

<span data-ttu-id="31527-191">Skanowania danych Transfer obiektu (DTO) jest to zwykły C# obiekt dziedziczący z `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="31527-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="31527-192">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="31527-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="31527-193">Witaj DTO jest używane toodefine hello tabeli w bazie danych SQL hello.</span><span class="sxs-lookup"><span data-stu-id="31527-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="31527-194">Witaj toocreate bazy danych wpisu, Dodaj `DbSet<>` właściwości na powitania DbContext używasz.</span><span class="sxs-lookup"><span data-stu-id="31527-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="31527-195">Witaj domyślny szablon projektu usługi Azure Mobile Apps, hello DbContext nosi nazwę `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="31527-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="31527-196">Jeśli masz hello zainstalowania zestawu Azure SDK, można teraz utworzyć kontrolera tabeli szablonu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="31527-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="31527-197">Kliknij prawym przyciskiem myszy folder kontrolery hello i wybierz **Dodaj** > **kontrolera...** .</span><span class="sxs-lookup"><span data-stu-id="31527-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="31527-198">Wybierz hello **Azure Mobile Apps tabeli kontrolera** opcji, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="31527-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="31527-199">W hello **Dodaj kontroler** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="31527-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="31527-200">W hello **klasa modelu** listy rozwijanej wybierz Twoje nowe DTO.</span><span class="sxs-lookup"><span data-stu-id="31527-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="31527-201">W hello **DbContext** listy rozwijanej wybierz hello klasy DbContext usługi mobilnej.</span><span class="sxs-lookup"><span data-stu-id="31527-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="31527-202">Nazwa kontrolera Hello jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="31527-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="31527-203">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="31527-203">Click **Add**.</span></span>

<span data-ttu-id="31527-204">Projekt serwera szybkiego startu Hello zawiera przykład prostą **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="31527-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="31527-205"><a name="adjust-pagesize"></a>Porady: dopasowywanie hello tabeli stronicowania</span><span class="sxs-lookup"><span data-stu-id="31527-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="31527-206">Domyślnie program Azure Mobile Apps zwraca 50 rekordów na żądanie.</span><span class="sxs-lookup"><span data-stu-id="31527-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="31527-207">Stronicowanie gwarantuje, że powitania klienta nie blokuje ich UI wątku ani powitania serwera zbyt długo, zapewniając uzyskać komfortowe środowisko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31527-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="31527-208">Witaj toochange tabeli stronicowania, po stronie serwera na powitania wzrost "dozwolony rozmiar kwerendy" i hello po stronie klienta rozmiar powitania po stronie serwera "dozwolony rozmiar zapytania" jest dostosowana przy użyciu hello `EnableQuery` atrybutu:</span><span class="sxs-lookup"><span data-stu-id="31527-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="31527-209">Upewnij się, że hello PageSize jest hello sam lub większy niż rozmiar hello zażądał powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="31527-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="31527-210">Zapoznaj się z dokumentacją Porada określonego klienta toohello szczegółowe informacje na temat zmieniania rozmiaru strony powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="31527-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="31527-211">Porady: Definiowanie niestandardowego kontrolera interfejsu API</span><span class="sxs-lookup"><span data-stu-id="31527-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="31527-212">kontrolera niestandardowego interfejsu API Hello zapewnia zaplecza aplikacji mobilnej tooyour najbardziej podstawowa funkcjonalność hello przez udostępnianie punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="31527-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="31527-213">Można zarejestrować kontrolera interfejsu API specyficzne dla mobilnych za pomocą atrybutu hello [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="31527-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="31527-214">Witaj `MobileAppController` atrybut rejestruje trasę hello, konfiguruje serializator JSON aplikacji mobilnej hello i włącza [Sprawdzanie wersji klienta](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="31527-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="31527-215">W programie Visual Studio, kliknij prawym przyciskiem myszy folder kontrolery hello, następnie kliknij przycisk **Dodaj** > **kontrolera**, wybierz pozycję **kontroler 2 interfejsu API sieci Web&mdash;pusty** i Kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="31527-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="31527-216">Podaj **nazwy kontrolera**, takich jak `CustomController`i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="31527-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="31527-217">Hello nowy plik klasy kontrolera, Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="31527-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="31527-218">Zastosuj hello **[MobileAppController]** atrybutu definicji klasy kontrolera toohello interfejsu API, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="31527-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="31527-219">W pliku App_Start/Startup.MobileApp.cs Dodaj toohello wywołania **MapApiControllers** — metoda rozszerzenia, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="31527-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="31527-220">Można również użyć hello `UseDefaultConfiguration()` — metoda rozszerzenia zamiast `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="31527-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="31527-221">Każdego kontrolera, który nie ma **MobileAppControllerAttribute** stosowane nadal mogą być używane przez klientów, ale go może nie być poprawnie używane przez klientów przy użyciu dowolnego klienta aplikacji mobilnej zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="31527-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="31527-222">Porady: Praca z uwierzytelnianiem</span><span class="sxs-lookup"><span data-stu-id="31527-222">How to: Work with authentication</span></span>
<span data-ttu-id="31527-223">Aplikacje mobilne platformy Azure korzysta z aplikacji usługi uwierzytelniania / autoryzacji toosecure z zaplecza aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="31527-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="31527-224">W tej sekcji opisano sposób hello tooperform następujące zadania związane z uwierzytelnianiem w projekcie serwera zaplecza .NET:</span><span class="sxs-lookup"><span data-stu-id="31527-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="31527-225">Porady: Dodawanie uwierzytelniania tooa serwera projektu</span><span class="sxs-lookup"><span data-stu-id="31527-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="31527-226">Porady: użycie uwierzytelniania niestandardowego dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="31527-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="31527-227">Porady: pobieranie uwierzytelniony informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="31527-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="31527-228">Porady: ograniczanie autoryzowanym użytkownikom dostęp do danych</span><span class="sxs-lookup"><span data-stu-id="31527-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="31527-229"><a name="add-auth"></a>Porady: Dodawanie uwierzytelniania tooa serwera projektu</span><span class="sxs-lookup"><span data-stu-id="31527-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="31527-230">Można dodać projekt serwera tooyour uwierzytelniania, rozszerzając hello **MobileAppConfiguration** obiektu i konfigurowanie oprogramowania pośredniczącego OWIN.</span><span class="sxs-lookup"><span data-stu-id="31527-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="31527-231">Po zainstalowaniu hello [Microsoft.Azure.Mobile.Server.Quickstart] hello pakietu i wywołanie **UseDefaultConfiguration** — metoda rozszerzenia, możesz pominąć toostep 3.</span><span class="sxs-lookup"><span data-stu-id="31527-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="31527-232">W programie Visual Studio należy zainstalować hello [Microsoft.Azure.Mobile.Server.Authentication] pakietu.</span><span class="sxs-lookup"><span data-stu-id="31527-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="31527-233">W pliku projektu Startup.cs hello, Dodaj następujące wiersz kodu na początku hello hello hello **konfiguracji** metody:</span><span class="sxs-lookup"><span data-stu-id="31527-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="31527-234">Ten składnik oprogramowania pośredniczącego OWIN weryfikuje tokeny wystawione przez bramę usługi aplikacji hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="31527-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="31527-235">Dodaj hello `[Authorize]` atrybutu tooany kontrolera lub metody, która wymaga uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="31527-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="31527-236">toolearn temat tooauthenticate klientów tooyour zaplecza Mobile Apps, zobacz [aplikacji tooyour authentication Dodaj](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="31527-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="31527-237"><a name="custom-auth"></a>Porady: użycie uwierzytelniania niestandardowego dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="31527-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="31527-238">Jeśli nie chcesz, aby toouse jednego z dostawców uwierzytelniania/autoryzacji dla aplikacji usługi hello, można zaimplementować systemu logowania.</span><span class="sxs-lookup"><span data-stu-id="31527-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="31527-239">Zainstaluj hello [Microsoft.Azure.Mobile.Server.Login] pakietu tooassist generacji tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="31527-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="31527-240">Sprawdzanie poprawności poświadczeń użytkownika Podaj własny kod.</span><span class="sxs-lookup"><span data-stu-id="31527-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="31527-241">Na przykład sprawdzić przed solone i skrótu hasła w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="31527-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="31527-242">W poniższym przykładzie hello, hello `isValidAssertion()` — metoda (zdefiniowany w innym miejscu) jest odpowiedzialny za kontrole.</span><span class="sxs-lookup"><span data-stu-id="31527-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="31527-243">niestandardowe uwierzytelnianie Hello jest udostępniany przez tworzenie klasy ApiController i udostępnianie `register` i `login` akcje.</span><span class="sxs-lookup"><span data-stu-id="31527-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="31527-244">powitania klienta należy używać niestandardowych informacji hello toocollect interfejsu użytkownika na powitania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31527-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="31527-245">informacje Hello są następnie wywołaj przesłanych toohello interfejsu API z standardowe HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="31527-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="31527-246">Gdy serwer hello sprawdza potwierdzenia hello, token jest wystawiane przy użyciu hello `AppServiceLoginHandler.CreateToken()` metody.</span><span class="sxs-lookup"><span data-stu-id="31527-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="31527-247">Witaj klasy ApiController **nie powinien** Użyj hello `[MobileAppController]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="31527-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="31527-248">Przykład `login` akcji:</span><span class="sxs-lookup"><span data-stu-id="31527-248">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="31527-249">W hello poprzedzających przykładzie LoginResult i LoginResultUser są obiekty możliwe do serializacji udostępnianie wymagane właściwości.</span><span class="sxs-lookup"><span data-stu-id="31527-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="31527-250">powitania klienta oczekuje logowania odpowiedzi toobe zwracane w postaci obiektów JSON hello formularza:</span><span class="sxs-lookup"><span data-stu-id="31527-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="31527-251">Witaj `AppServiceLoginHandler.CreateToken()` metoda zawiera *odbiorców* i *wystawcy* parametru.</span><span class="sxs-lookup"><span data-stu-id="31527-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="31527-252">Oba te parametry są ustawiane toohello adres URL katalogu aplikacji przy użyciu hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31527-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="31527-253">Podobnie należy ustawić *secretKey* klucza podpisywania wartość hello toobe aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31527-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="31527-254">Nie rozpowszechniaj hello klucza w kliencie podpisywania, który może być kluczy używanych toomint i personifikować użytkowników.</span><span class="sxs-lookup"><span data-stu-id="31527-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="31527-255">Możesz uzyskać hello klucza podczas hostowanych w usłudze App Service za pomocą odwołań do hello podpisywania *witryny sieci Web\_uwierzytelniania\_podpisywanie\_klucza* zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="31527-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="31527-256">W razie potrzeby w kontekście lokalnego debugowania, wykonaj instrukcje hello hello [debugowania lokalnego z uwierzytelnianiem](#local-debug) sekcji tooretrieve hello klucz i zapisz go jako ustawienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31527-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="31527-257">Witaj wystawiony token mogą również obejmować inne oświadczenia oraz datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="31527-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="31527-258">Minimalny, hello wystawiony token musi zawierać temat (**sub**) oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="31527-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="31527-259">Może obsługiwać powitania klienta standardowe `loginAsync()` metoda przeciążenia hello uwierzytelniania trasy.</span><span class="sxs-lookup"><span data-stu-id="31527-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="31527-260">Jeśli klient hello wywołuje `client.loginAsync('custom');` toolog w, Twoje trasy nie może być `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="31527-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="31527-261">Można ustawić hello trasę dla przy użyciu kontrolera niestandardowego uwierzytelniania hello `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="31527-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="31527-262">Przy użyciu hello `loginAsync()` podejście zapewnia token uwierzytelniania hello jest dołączony tooevery kolejne wywołanie toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="31527-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="31527-263"><a name="user-info"></a>Porady: pobieranie uwierzytelniony informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="31527-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="31527-264">Gdy użytkownik jest uwierzytelniany przez usługę App Service, można uzyskać dostępu do hello przypisany identyfikator użytkownika i inne informacje w kodzie zaplecza .NET.</span><span class="sxs-lookup"><span data-stu-id="31527-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="31527-265">informacje o użytkowniku Hello może służyć do podejmowania decyzji dotyczących autoryzacji w hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="31527-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="31527-266">Witaj następujący kod uzyskuje hello identyfikator użytkownika skojarzony z żądaniem:</span><span class="sxs-lookup"><span data-stu-id="31527-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="31527-267">Hello identyfikator SID jest określana na podstawie Identyfikatora użytkownika specyficznych dla dostawcy hello i jest statyczny dla danego użytkownika i dostawcy logowania.</span><span class="sxs-lookup"><span data-stu-id="31527-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="31527-268">Witaj identyfikator SID ma wartość null dla nieprawidłowego uwierzytelniania tokenów.</span><span class="sxs-lookup"><span data-stu-id="31527-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="31527-269">Usługa App Service umożliwia również żądania określonych oświadczeń od dostawcy logowania.</span><span class="sxs-lookup"><span data-stu-id="31527-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="31527-270">Każdy dostawca tożsamości Aby uzyskać więcej informacji, przy użyciu dostawcy tożsamości zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="31527-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="31527-271">Na przykład można użyć hello interfejsu Graph API usługi Facebook informacji znajomych.</span><span class="sxs-lookup"><span data-stu-id="31527-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="31527-272">W bloku dostawcy hello w hello portalu Azure, można określić oświadczenia, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="31527-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="31527-273">Niektóre oświadczenia wymagają dodatkowej konfiguracji z hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="31527-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="31527-274">Witaj poniższy kod hello wywołania **GetAppServiceIdentityAsync** rozszerzenia metody tooget hello poświadczenia logowania, które obejmują żądania tokenu toomake wymagane dostępu hello przed hello interfejsu Graph API usługi Facebook:</span><span class="sxs-lookup"><span data-stu-id="31527-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="31527-275">Dodaj using instrukcji dla `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="31527-276"><a name="authorize"></a>Porady: ograniczanie autoryzowanym użytkownikom dostęp do danych</span><span class="sxs-lookup"><span data-stu-id="31527-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="31527-277">W poprzedniej sekcji hello możemy pokazano, jak tooretrieve hello identyfikator użytkownika uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31527-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="31527-278">Można ograniczyć toodata dostępu i innych zasobów na podstawie tej wartości.</span><span class="sxs-lookup"><span data-stu-id="31527-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="31527-279">Na przykład dodawanie tootables kolumny userId i filtrowanie wyników zapytania hello przy użyciu Identyfikatora użytkownika hello jest toolimit prosty sposób zwracane tylko użytkownicy tooauthorized danych.</span><span class="sxs-lookup"><span data-stu-id="31527-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="31527-280">Witaj następujący kod zwraca wiersze danych tylko wtedy, gdy hello identyfikator SID jest zgodna z wartością w kolumnie Identyfikator UserId hello w tabeli TodoItem hello:</span><span class="sxs-lookup"><span data-stu-id="31527-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="31527-281">Witaj `Query()` metoda zwraca `IQueryable` który można manipulować filtrowania toohandle LINQ.</span><span class="sxs-lookup"><span data-stu-id="31527-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="31527-282">Porady: Dodawanie Projekt serwera tooa powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="31527-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="31527-283">Dodaj projekt serwera tooyour powiadomienia wypychane przez rozszerzenie hello **MobileAppConfiguration** obiektu i Tworzenie klienta usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="31527-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="31527-284">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj `Microsoft.Azure.Mobile.Server.Notifications`, następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="31527-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="31527-285">Powtórz ten krok hello tooinstall `Microsoft.Azure.NotificationHubs` pakiet, który zawiera hello biblioteki klienta usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="31527-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="31527-286">W App_Start/Startup.MobileApp.cs i Dodaj toohello wywołania **AddPushNotifications()** — metoda rozszerzenia podczas inicjowania:</span><span class="sxs-lookup"><span data-stu-id="31527-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="31527-287">Dodaj następującego kodu tworzącego klienta usługi Notification Hubs hello:</span><span class="sxs-lookup"><span data-stu-id="31527-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="31527-288">Teraz można używać urządzeń tooregistered powiadomień wypychanych toosend hello centra powiadomień klienta.</span><span class="sxs-lookup"><span data-stu-id="31527-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="31527-289">Aby uzyskać więcej informacji, zobacz [aplikacji tooyour powiadomień wypychanych Dodaj](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="31527-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="31527-290">toolearn więcej informacji na temat usługi Notification Hubs, zobacz [omówienie centra powiadomień](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31527-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="31527-291"><a name="tags"></a>Porady: Włączanie docelowe wypychanych przy użyciu tagów</span><span class="sxs-lookup"><span data-stu-id="31527-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="31527-292">Usługi Notification Hubs umożliwia wysyłanie powiadomień docelowe toospecific rejestracji przy użyciu tagów.</span><span class="sxs-lookup"><span data-stu-id="31527-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="31527-293">Kilka tagi są tworzone automatycznie:</span><span class="sxs-lookup"><span data-stu-id="31527-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="31527-294">Witaj identyfikator instalacji identyfikuje określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="31527-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="31527-295">Witaj identyfikator użytkownika na podstawie hello uwierzytelniony identyfikator SID identyfikuje określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="31527-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="31527-296">Witaj instalacji identyfikator jest możliwy z hello **installationId** właściwość hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="31527-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="31527-297">Hello poniższy przykład przedstawia użycie tooadd identyfikator instalacji instalacji określonych tooa tag w centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="31527-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="31527-298">Dowolne tagi dostarczonych przez klienta na powitania podczas rejestracji powiadomień wypychanych są ignorowane przez hello wewnętrznej bazy danych, tworząc hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="31527-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="31527-299">tooenable tooadd klienta znaczniki toohello instalacji, należy utworzyć niestandardowego interfejsu API, który dodaje znaczniki przy użyciu hello poprzedzających wzorca.</span><span class="sxs-lookup"><span data-stu-id="31527-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="31527-300">Zobacz [tagi powiadomień wypychanych dodać klienta] [ 5] w przykładowym ukończone szybkiego startu App Service Mobile Apps hello przykład.</span><span class="sxs-lookup"><span data-stu-id="31527-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="31527-301"><a name="push-user"></a>Porady: tooan powiadomień wypychanych wysyłania uwierzytelniony użytkownik</span><span class="sxs-lookup"><span data-stu-id="31527-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="31527-302">Uwierzytelniony użytkownik rejestruje dla powiadomień wypychanych, tag identyfikator użytkownika jest automatycznie dodawany toohello rejestracji.</span><span class="sxs-lookup"><span data-stu-id="31527-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="31527-303">Za pomocą tego tagu, możesz wysłać powiadomienia tooall urządzeń zarejestrowanych przez tę osobę wypychania.</span><span class="sxs-lookup"><span data-stu-id="31527-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="31527-304">Hello poniższy kod pobiera identyfikator SID użytkownika w żądaniu skierowanym hello i wysyła rejestracji urządzenia tooevery powiadomień wypychanych szablonu dla tej osoby:</span><span class="sxs-lookup"><span data-stu-id="31527-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="31527-305">Podczas rejestrowania dla powiadomień wypychanych z uwierzytelnionego klienta, upewnij się, że przed podjęciem próby wykonania rejestracji zakończeniem uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="31527-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="31527-306">Aby uzyskać więcej informacji, zobacz [Push toousers] [ 6] hello App Service Mobile Apps ukończone szybkiego startu próbki dla zaplecza .NET.</span><span class="sxs-lookup"><span data-stu-id="31527-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="31527-307">Porady: debugowania i rozwiązywania problemów z hello .NET Server SDK</span><span class="sxs-lookup"><span data-stu-id="31527-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="31527-308">Usługa aplikacji Azure zapewnia kilka debugowania i rozwiązywanie problemów z techniki dla aplikacji ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="31527-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="31527-309">Monitorowanie usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="31527-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="31527-310">Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="31527-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="31527-311">Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31527-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="31527-312">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="31527-312">Logging</span></span>
<span data-ttu-id="31527-313">Dzienniki diagnostyczne usługi tooApp można pisać przy użyciu hello standardowe zapisu śledzenia ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="31527-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="31527-314">Aby można było tworzyć toohello dzienników, należy włączyć diagnostyki w zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="31527-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="31527-315">tooenable diagnostyki i zapisu dzienniki toohello:</span><span class="sxs-lookup"><span data-stu-id="31527-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="31527-316">Wykonaj kroki hello w [jak diagnostyki tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="31527-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="31527-317">Dodaj następujące hello przy użyciu instrukcji w pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="31527-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="31527-318">Utwórz toowrite moduł zapisujący śledzenia z hello .NET backend toohello dzienników diagnostycznych, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="31527-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="31527-319">Ponownie opublikować projekt serwera, a hello aplikacji mobilnej zaplecza tooexecute hello kodu ścieżki z rejestrowaniem hello dostępu.</span><span class="sxs-lookup"><span data-stu-id="31527-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="31527-320">Pobierz i ocenić hello dzienniki, zgodnie z opisem w [porady: pobieranie dzienników](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="31527-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="31527-321"><a name="local-debug"></a>Debugowanie za pomocą uwierzytelniania lokalnego</span><span class="sxs-lookup"><span data-stu-id="31527-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="31527-322">Aplikację można uruchomić lokalnie tootest zmiany przed ich opublikowaniem toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="31527-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="31527-323">Dla większości zapleczy Azure Mobile Apps, naciśnij klawisz *F5* while w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31527-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="31527-324">Istnieją pewne dodatkowe kwestie przy użyciu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="31527-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="31527-325">Musi być oparta na chmurze aplikacji mobilnej z aplikacji usługi uwierzytelniania/autoryzacji skonfigurowany, a klient musi mieć punktu końcowego w chmurze hello określony jako hello alternatywnego hosta.</span><span class="sxs-lookup"><span data-stu-id="31527-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="31527-326">Zapoznaj się dokumentacją powitania dla danej platformy klienta, aby poznać konkretne kroki hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="31527-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="31527-327">Upewnij się, że Twoje zaplecze aplikacji mobilnej ma [Microsoft.Azure.Mobile.Server.Authentication] zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="31527-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="31527-328">Następnie, w aplikacji klasy początkowej OWIN, Dodaj następujące hello po `MobileAppConfiguration` został zastosowany tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="31527-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="31527-329">W hello poprzedzających przykład, należy skonfigurować hello *authAudience* i *authIssuer* ustawienia aplikacji w pliku Web.config pliku tooeach być adresem URL katalogu aplikacji przy użyciu hello HTTPS schemat.</span><span class="sxs-lookup"><span data-stu-id="31527-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="31527-330">Podobnie należy ustawić *authSigningKey* klucza podpisywania wartość hello toobe aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31527-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="31527-331">tooobtain hello klucza podpisywania:</span><span class="sxs-lookup"><span data-stu-id="31527-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="31527-332">Przejdź tooyour aplikacji w ramach hello [portalu Azure]</span><span class="sxs-lookup"><span data-stu-id="31527-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="31527-333">Kliknij przycisk **narzędzia**, **Kudu**, **Przejdź**.</span><span class="sxs-lookup"><span data-stu-id="31527-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="31527-334">W witrynie zarządzania Kudu hello, kliknij przycisk **środowiska**.</span><span class="sxs-lookup"><span data-stu-id="31527-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="31527-335">Znajdź wartość hello *witryny sieci Web\_uwierzytelniania\_podpisywanie\_klucza*.</span><span class="sxs-lookup"><span data-stu-id="31527-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="31527-336">Witaj użycia klucza dla hello podpisywania *authSigningKey* parametru w pliku config aplikacji lokalnej.  Twoje zaplecze aplikacji mobilnej jest teraz tokeny wyposażone toovalidate podczas uruchamiania lokalnego powitania klienta uzyskuje hello tokenu z punktu końcowego hello oparte na chmurze.</span><span class="sxs-lookup"><span data-stu-id="31527-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portalu Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
