---
title: "Jak pracować z serwera wewnętrznej bazy danych .NET SDK dla aplikacji mobilnych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure App Service Mobile Apps."
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
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="2849a-104">Praca z zestawem SDK serwera zaplecza platformy .NET na potrzeby usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="2849a-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="2849a-105">W tym temacie przedstawiono sposób użycia serwera wewnętrznej bazy danych .NET SDK w różnych kluczowych scenariuszy Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="2849a-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="2849a-106">Zestaw SDK usługi Azure Mobile Apps pomaga w pracy z klientów mobilnych, z poziomu aplikacji ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2849a-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="2849a-107">[Serwer .NET SDK usługi Azure Mobile Apps] [ 2] jest typu open source w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="2849a-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="2849a-108">Repozytorium zawiera wszystkie kodu źródłowego, w tym zestaw testów jednostkowych SDK całego serwera i kilka przykładowych projektach.</span><span class="sxs-lookup"><span data-stu-id="2849a-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="2849a-109">Dokumentacja referencyjna</span><span class="sxs-lookup"><span data-stu-id="2849a-109">Reference documentation</span></span>
<span data-ttu-id="2849a-110">Dokumentacja referencyjna dla serwera zestawu SDK znajduje się tutaj: [Azure Mobile Apps .NET Reference][1].</span><span class="sxs-lookup"><span data-stu-id="2849a-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="2849a-111"><a name="create-app"></a>Porady: tworzenie zaplecza aplikacji mobilnej platformy .NET</span><span class="sxs-lookup"><span data-stu-id="2849a-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="2849a-112">Jeśli uruchamiasz nowego projektu można utworzyć aplikację usługi aplikacji za pomocą [portalu Azure] lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2849a-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="2849a-113">Można uruchomić aplikację usługi aplikacji — lokalnie lub publikowania projektu na chmurze aplikacji mobilnej usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2849a-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="2849a-114">Jeśli dodajesz funkcji mobilnych do istniejącego projektu, zobacz [pobrać i zainicjuj zestaw SDK](#install-sdk) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2849a-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="2849a-115">Tworzenie zaplecza .NET przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2849a-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="2849a-116">Aby utworzyć zaplecze aplikacji mobilnej usługi aplikacji, albo wykonaj [samouczek Szybki Start] [ 3] lub wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2849a-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="2849a-117">W *wprowadzenie* bloku, w obszarze **Utwórz tabelę interfejsu API**, wybierz **C#** jako sieci **język wewnętrznej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="2849a-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="2849a-118">Kliknij przycisk **Pobierz**, a następnie Wyodrębnij skompresowane pliki projektu na komputerze lokalnym i otwórz rozwiązanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2849a-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="2849a-119">Tworzenie zaplecza .NET przy użyciu programu Visual Studio 2013 i Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="2849a-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="2849a-120">Zainstaluj [zestawu Azure SDK dla platformy .NET] [ 4] (wersja 2.9.0 lub nowszym) do tworzenia projektu usługi Azure Mobile Apps w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2849a-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="2849a-121">Po zainstalowaniu zestawu SDK, należy utworzyć aplikację ASP.NET, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2849a-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="2849a-122">Otwórz **nowy projekt** okna dialogowego (z *pliku* > **nowy** > **projektu...** ).</span><span class="sxs-lookup"><span data-stu-id="2849a-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="2849a-123">Rozwiń węzeł **szablony** > **Visual C#**i wybierz **Web**.</span><span class="sxs-lookup"><span data-stu-id="2849a-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="2849a-124">Wybierz **aplikacji sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="2849a-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="2849a-125">Wprowadź nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="2849a-125">Fill in the project name.</span></span> <span data-ttu-id="2849a-126">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2849a-126">Then click **OK**.</span></span>
5. <span data-ttu-id="2849a-127">W obszarze *ASP.NET 4.5.2 szablony*, wybierz pozycję **aplikacji mobilnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="2849a-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="2849a-128">Sprawdź **Hostuj w chmurze** utworzyć przenośnych wewnętrznej bazy danych w chmurze, do którego można opublikować tego projektu.</span><span class="sxs-lookup"><span data-stu-id="2849a-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="2849a-129">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2849a-129">Click **OK**.</span></span>

## <span data-ttu-id="2849a-130"><a name="install-sdk"></a>Porady: pobieranie i zainicjuj zestaw SDK</span><span class="sxs-lookup"><span data-stu-id="2849a-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="2849a-131">Zestaw SDK jest dostępny na [NuGet.org].</span><span class="sxs-lookup"><span data-stu-id="2849a-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="2849a-132">Ten pakiet zawiera podstawowe funkcje wymagane, aby rozpocząć korzystanie z zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2849a-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="2849a-133">Aby zainicjować zestawu SDK, należy wykonywać działania na **HttpConfiguration** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2849a-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="2849a-134">Instalacja zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="2849a-134">Install the SDK</span></span>
<span data-ttu-id="2849a-135">Aby zainstalować zestaw SDK, kliknij prawym przyciskiem myszy projekt serwera w programie Visual Studio, wybierz **Zarządzaj pakietami NuGet**, wyszukaj [Microsoft.Azure.Mobile.Server] pakietu, a następnie kliknij przycisk **zainstalować** .</span><span class="sxs-lookup"><span data-stu-id="2849a-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="2849a-136"><a name="server-project-setup"></a>Inicjowanie projektu serwera</span><span class="sxs-lookup"><span data-stu-id="2849a-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="2849a-137">Projekt serwera zaplecza .NET zainicjowano podobne do innych projektów programu ASP.NET, umieszczając klasę początkową OWIN.</span><span class="sxs-lookup"><span data-stu-id="2849a-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="2849a-138">Upewnij się, że ma odwołanie do pakietu NuGet `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="2849a-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="2849a-139">Aby dodać do tej klasy w Visual Studio, kliknij prawym przyciskiem myszy projekt serwera, a następnie wybierz **Dodaj** >
**nowy element**, następnie **Web**  >  ** Ogólne** > **klasy początkowej OWIN**.</span><span class="sxs-lookup"><span data-stu-id="2849a-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="2849a-140">Klasa jest generowana za pomocą następującego atrybutu:</span><span class="sxs-lookup"><span data-stu-id="2849a-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="2849a-141">W `Configuration()` metoda z klasy początkowej OWIN, użyj **HttpConfiguration** obiekt, aby skonfigurować środowisko usługi Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="2849a-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="2849a-142">W poniższym przykładzie inicjowane Projekt serwera z nie dodatkowe funkcje:</span><span class="sxs-lookup"><span data-stu-id="2849a-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="2849a-143">Aby włączyć poszczególne funkcje, należy wywołać metody rozszerzenia na **MobileAppConfiguration** obiekt przed wywołaniem **metody ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="2849a-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="2849a-144">Na przykład następujący kod dodaje tras domyślnych do wszystkich kontrolerów interfejsu API, które mają atrybut `[MobileAppController]` podczas inicjowania:</span><span class="sxs-lookup"><span data-stu-id="2849a-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="2849a-145">Szybki Start serwera z portalu Azure wywołań **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="2849a-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="2849a-146">To odpowiednik następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="2849a-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="2849a-147">Metody rozszerzenia używane są:</span><span class="sxs-lookup"><span data-stu-id="2849a-147">The extension methods used are:</span></span>

* <span data-ttu-id="2849a-148">`AddMobileAppHomeController()`udostępnia domyślną stronę główną usługi Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="2849a-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="2849a-149">`MapApiControllers()`zapewnia niestandardowego interfejsu API funkcji WebAPI kontrolerów ozdobione `[MobileAppController]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2849a-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="2849a-150">`AddTables()`zapewnia mapowanie `/tables` punktów końcowych do tabeli kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="2849a-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="2849a-151">`AddTablesWithEntityFramework()`jest skrótowym mapowania `/tables` kontrolerów na podstawie punktów końcowych przy użyciu programu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="2849a-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="2849a-152">`AddPushNotifications()`zapewnia prostą metodę rejestrowania urządzeń do usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="2849a-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="2849a-153">`MapLegacyCrossDomainController()`zawiera standardowe nagłówki CORS dla rozwoju lokalnych.</span><span class="sxs-lookup"><span data-stu-id="2849a-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="2849a-154">Rozszerzenia zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="2849a-154">SDK extensions</span></span>
<span data-ttu-id="2849a-155">Następujące pakiety NuGet, na podstawie rozszerzenia zawierają różne funkcje mobilne, które mogą być używane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="2849a-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="2849a-156">Włącz rozszerzenia podczas inicjowania przy użyciu **MobileAppConfiguration** obiektu.</span><span class="sxs-lookup"><span data-stu-id="2849a-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="2849a-157">[Microsoft.Azure.Mobile.Server.Quickstart] obsługuje podstawowa konfiguracja aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="2849a-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="2849a-158">Dodany do konfiguracji przez wywołanie metody **UseDefaultConfiguration** — metoda rozszerzenia podczas inicjowania.</span><span class="sxs-lookup"><span data-stu-id="2849a-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="2849a-159">To rozszerzenie zawiera następujące rozszerzenia: powiadomienia, uwierzytelnianie, jednostki, tabel, między domenami i pakiety głównej.</span><span class="sxs-lookup"><span data-stu-id="2849a-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="2849a-160">Ten pakiet jest używany przez Szybki Start aplikacji mobilnej, które są dostępne w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2849a-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="2849a-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementuje domyślny *tej aplikacji mobilnej jest uruchomiona strona* dla katalogu głównego witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="2849a-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="2849a-162">Dodaj do konfiguracji przez wywołanie metody **AddMobileAppHomeController** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="2849a-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) zawiera klasy do pracy z danymi i zestawy danych potoku w górę.</span><span class="sxs-lookup"><span data-stu-id="2849a-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="2849a-164">Dodaj do konfiguracji przez wywołanie metody **AddTables** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="2849a-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) umożliwia programu Entity Framework w celu dostępu do danych w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="2849a-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="2849a-166">Dodaj do konfiguracji przez wywołanie metody **AddTablesWithEntityFramework** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="2849a-167">[Microsoft.Azure.Mobile.Server.Authentication] umożliwia uwierzytelnianie i zestawy oprogramowanie pośredniczące OWIN służący do weryfikowania tokenów w górę.</span><span class="sxs-lookup"><span data-stu-id="2849a-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="2849a-168">Dodaj do konfiguracji przez wywołanie metody **AddAppServiceAuthentication** i **IAppBuilder**. **UseAppServiceAuthentication** metody rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="2849a-169">[Microsoft.Azure.Mobile.Server.Notifications] umożliwia wypychanie powiadomień i definiuje punktu końcowego rejestracji wypychania.</span><span class="sxs-lookup"><span data-stu-id="2849a-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="2849a-170">Dodaj do konfiguracji przez wywołanie metody **AddPushNotifications** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="2849a-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) tworzy kontroler, który służy danych do starszej wersji przeglądarki z aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="2849a-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="2849a-172">Dodaj do konfiguracji przez wywołanie metody **MapLegacyCrossDomainController** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="2849a-173">[Microsoft.Azure.Mobile.Server.Login] udostępnia metody AppServiceLoginHandler.CreateToken(), która jest metodą statyczną, używane podczas uwierzytelniania niestandardowego scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="2849a-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="2849a-174"><a name="publish-server-project"></a>Porady: publikowanie projektu serwera</span><span class="sxs-lookup"><span data-stu-id="2849a-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="2849a-175">W tej sekcji przedstawiono sposób publikowania projektu zaplecza .NET z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2849a-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="2849a-176">Można także wdrożyć projektu zaplecza przy użyciu narzędzia Git lub innych metod opisanych w [dokumentacja wdrażania usługi aplikacji Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2849a-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="2849a-177">W programie Visual Studio Skompiluj ponownie projekt pod kątem przywracania pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="2849a-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="2849a-178">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="2849a-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="2849a-179">Przy pierwszym uruchomieniu publikowania, musisz zdefiniować profil publikowania.</span><span class="sxs-lookup"><span data-stu-id="2849a-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="2849a-180">Jeśli istnieje już profil zdefiniowane, możesz wybrać go i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="2849a-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="2849a-181">Jeśli prośba o wybierz cel, publikowania, kliknij przycisk **Microsoft Azure App Service** > **dalej**, a następnie (w razie potrzeby) logowania przy użyciu poświadczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2849a-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="2849a-182">Program Visual Studio pobierze i bezpiecznie przechowywane są Twoje ustawienia publikowania bezpośrednio z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2849a-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="2849a-183">Wybierz użytkownika **subskrypcji**, wybierz pozycję **typu zasobu** z **widoku**, rozwiń węzeł **aplikacji mobilnej**i kliknij przycisk zaplecza aplikacji mobilnej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2849a-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="2849a-184">Sprawdź informacje o profilu publikowania i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="2849a-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="2849a-185">Po zaplecza aplikacji mobilnej został pomyślnie opublikowany, pojawi się Strona początkowa, informujący o powodzeniu.</span><span class="sxs-lookup"><span data-stu-id="2849a-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="2849a-186"><a name="define-table-controller"></a>Porady: Definiowanie kontrolera tabeli</span><span class="sxs-lookup"><span data-stu-id="2849a-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="2849a-187">Zdefiniuj kontrolera tabeli do udostępnienia tabeli SQL do klientów mobilnych.</span><span class="sxs-lookup"><span data-stu-id="2849a-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="2849a-188">Konfigurowanie kontrolera tabeli wymaga trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="2849a-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="2849a-189">Utwórz klasę obiektu transferu danych (DTO).</span><span class="sxs-lookup"><span data-stu-id="2849a-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="2849a-190">Skonfiguruj odwołania do tabeli w klasy Mobile DbContext.</span><span class="sxs-lookup"><span data-stu-id="2849a-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="2849a-191">Tworzenie kontrolera tabeli.</span><span class="sxs-lookup"><span data-stu-id="2849a-191">Create a table controller.</span></span>

<span data-ttu-id="2849a-192">Skanowania danych Transfer obiektu (DTO) jest to zwykły C# obiekt dziedziczący z `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="2849a-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="2849a-193">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2849a-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="2849a-194">DTO służy do definiowania tabeli w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="2849a-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="2849a-195">Aby utworzyć wpis w bazie danych, należy dodać `DbSet<>` właściwości DbContext używasz.</span><span class="sxs-lookup"><span data-stu-id="2849a-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="2849a-196">W domyślnym szablonie projektu usługi Azure Mobile Apps, nosi nazwę kontekstu DbContext `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="2849a-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="2849a-197">Jeśli masz zainstalowany zestaw SDK platformy Azure, można teraz utworzyć kontroler tabeli szablonu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2849a-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="2849a-198">Kliknij prawym przyciskiem myszy folder kontrolery, a następnie wybierz **Dodaj** > **kontrolera...** .</span><span class="sxs-lookup"><span data-stu-id="2849a-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="2849a-199">Wybierz **Azure Mobile Apps tabeli kontrolera** opcji, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2849a-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="2849a-200">W **Dodaj kontroler** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="2849a-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="2849a-201">W **klasa modelu** listy rozwijanej wybierz Twoje nowe DTO.</span><span class="sxs-lookup"><span data-stu-id="2849a-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="2849a-202">W **DbContext** listy rozwijanej wybierz klasę DbContext usługi mobilnej.</span><span class="sxs-lookup"><span data-stu-id="2849a-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="2849a-203">Nazwa kontrolera jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="2849a-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="2849a-204">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2849a-204">Click **Add**.</span></span>

<span data-ttu-id="2849a-205">Projekt serwera szybkiego startu zawiera przykład prostą **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="2849a-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="2849a-206"><a name="adjust-pagesize"></a>Porady: dopasowywanie rozmiaru stronicowania tabeli</span><span class="sxs-lookup"><span data-stu-id="2849a-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="2849a-207">Domyślnie program Azure Mobile Apps zwraca 50 rekordów na żądanie.</span><span class="sxs-lookup"><span data-stu-id="2849a-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="2849a-208">Stronicowanie gwarantuje, że klient nie blokuje ich wątku interfejsu użytkownika ani server zbyt długo, zapewniając uzyskać komfortowe środowisko użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2849a-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="2849a-209">Aby zmienić rozmiar tabeli stronicowania, Zwiększ "dozwolony rozmiar zapytania" po stronie serwera i po stronie serwera rozmiaru strony po stronie klienta "dozwolony rozmiar zapytania" jest dostosowywana przy użyciu `EnableQuery` atrybutu:</span><span class="sxs-lookup"><span data-stu-id="2849a-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="2849a-210">Upewnij się, wartość właściwości PageSize jest taki sam lub większy niż rozmiar żądanej przez klienta.</span><span class="sxs-lookup"><span data-stu-id="2849a-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="2849a-211">Odnoszą się do określonego klienta Porada dokumentacji, aby uzyskać więcej informacji na temat zmieniania rozmiaru strony klienta.</span><span class="sxs-lookup"><span data-stu-id="2849a-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="2849a-212">Porady: Definiowanie niestandardowego kontrolera interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2849a-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="2849a-213">Kontrolera niestandardowego interfejsu API zapewnia najbardziej podstawowe funkcje do zaplecza aplikacji mobilnej w przypadku wystawianego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="2849a-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="2849a-214">Można zarejestrować kontrolera interfejsu API specyficzne dla mobilnych za pomocą atrybutu [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="2849a-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="2849a-215">`MobileAppController` Atrybut rejestruje trasę, konfiguruje serializator JSON aplikacji mobilnych i włącza [Sprawdzanie wersji klienta](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="2849a-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="2849a-216">W programie Visual Studio, kliknij prawym przyciskiem myszy folder kontrolery, a następnie kliknij przycisk **Dodaj** > **kontrolera**, wybierz pozycję **kontroler 2 interfejsu API sieci Web&mdash;pusty** i Kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2849a-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="2849a-217">Podaj **nazwy kontrolera**, takich jak `CustomController`i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2849a-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="2849a-218">W nowym pliku klasy kontroler, dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="2849a-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="2849a-219">Zastosuj **[MobileAppController]** atrybutu w definicji klasy kontrolera interfejsu API, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="2849a-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="2849a-220">W pliku App_Start/Startup.MobileApp.cs, dodaj wywołanie do **MapApiControllers** — metoda rozszerzenia, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="2849a-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="2849a-221">Można również użyć `UseDefaultConfiguration()` — metoda rozszerzenia zamiast `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="2849a-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="2849a-222">Każdego kontrolera, który nie ma **MobileAppControllerAttribute** stosowane nadal mogą być używane przez klientów, ale go może nie być poprawnie używane przez klientów przy użyciu dowolnego klienta aplikacji mobilnej zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2849a-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="2849a-223">Porady: Praca z uwierzytelnianiem</span><span class="sxs-lookup"><span data-stu-id="2849a-223">How to: Work with authentication</span></span>
<span data-ttu-id="2849a-224">Aplikacje mobilne platformy Azure korzysta z aplikacji usługi uwierzytelniania / autoryzacji do zabezpieczania sieci zaplecza aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="2849a-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="2849a-225">W tej sekcji pokazano, jak wykonywać następujące zadania związane z uwierzytelnianiem w projekcie serwera zaplecza .NET:</span><span class="sxs-lookup"><span data-stu-id="2849a-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="2849a-226">Porady: Dodawanie uwierzytelniania do server project</span><span class="sxs-lookup"><span data-stu-id="2849a-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="2849a-227">Porady: użycie uwierzytelniania niestandardowego dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="2849a-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="2849a-228">Porady: pobieranie uwierzytelniony informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="2849a-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="2849a-229">Porady: ograniczanie autoryzowanym użytkownikom dostęp do danych</span><span class="sxs-lookup"><span data-stu-id="2849a-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="2849a-230"><a name="add-auth"></a>Porady: Dodawanie uwierzytelniania do server project</span><span class="sxs-lookup"><span data-stu-id="2849a-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="2849a-231">Uwierzytelnianie można dodać do projektu serwera, rozszerzając **MobileAppConfiguration** obiektu i konfigurowanie oprogramowania pośredniczącego OWIN.</span><span class="sxs-lookup"><span data-stu-id="2849a-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="2849a-232">Po zainstalowaniu [Microsoft.Azure.Mobile.Server.Quickstart] pakietu i wywołanie **UseDefaultConfiguration** — metoda rozszerzenia, możesz przejść do kroku 3.</span><span class="sxs-lookup"><span data-stu-id="2849a-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="2849a-233">W programie Visual Studio należy zainstalować [Microsoft.Azure.Mobile.Server.Authentication] pakietu.</span><span class="sxs-lookup"><span data-stu-id="2849a-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="2849a-234">W pliku Startup.cs projekt, Dodaj następujący wiersz kodu na początku **konfiguracji** metody:</span><span class="sxs-lookup"><span data-stu-id="2849a-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="2849a-235">Ten składnik oprogramowania pośredniczącego OWIN weryfikuje tokeny wystawione przez skojarzone bramy usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2849a-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="2849a-236">Dodaj `[Authorize]` atrybutu kontrolera lub metody, która wymaga uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="2849a-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="2849a-237">Aby uzyskać informacje dotyczące sposobu uwierzytelniania klientów z wewnętrzną bazą danych Mobile Apps, zobacz [Dodawanie uwierzytelniania do aplikacji](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="2849a-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="2849a-238"><a name="custom-auth"></a>Porady: użycie uwierzytelniania niestandardowego dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="2849a-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="2849a-239">Jeśli nie chcesz używać jednego z dostawców uwierzytelniania/autoryzacji dla aplikacji usługi, można zaimplementować systemu logowania.</span><span class="sxs-lookup"><span data-stu-id="2849a-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="2849a-240">Zainstaluj [Microsoft.Azure.Mobile.Server.Login] pakietu z generowania tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2849a-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="2849a-241">Sprawdzanie poprawności poświadczeń użytkownika Podaj własny kod.</span><span class="sxs-lookup"><span data-stu-id="2849a-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="2849a-242">Na przykład sprawdzić przed solone i skrótu hasła w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2849a-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="2849a-243">W poniższym przykładzie `isValidAssertion()` — metoda (zdefiniowany w innym miejscu) jest odpowiedzialny za kontrole.</span><span class="sxs-lookup"><span data-stu-id="2849a-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="2849a-244">Niestandardowe uwierzytelnianie jest udostępniany przez tworzenie klasy ApiController i udostępnianie `register` i `login` akcje.</span><span class="sxs-lookup"><span data-stu-id="2849a-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="2849a-245">Niestandardowy interfejs użytkownika powinien używać klient do zbiera informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="2849a-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="2849a-246">Informacje jest następnie przesłane do interfejsu API przy użyciu standardowych wywołania metody POST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="2849a-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="2849a-247">Gdy serwer sprawdza to potwierdzenie, token jest wystawiane przy użyciu `AppServiceLoginHandler.CreateToken()` metody.</span><span class="sxs-lookup"><span data-stu-id="2849a-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="2849a-248">Klasy ApiController **nie powinien** użyj `[MobileAppController]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2849a-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="2849a-249">Przykład `login` akcji:</span><span class="sxs-lookup"><span data-stu-id="2849a-249">An example `login` action:</span></span>

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

<span data-ttu-id="2849a-250">W powyższym przykładzie LoginResult i LoginResultUser są obiekty możliwe do serializacji udostępnianie wymagane właściwości.</span><span class="sxs-lookup"><span data-stu-id="2849a-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="2849a-251">Klient oczekuje odpowiedzi logowania, które są zwracane w postaci obiektów JSON w postaci:</span><span class="sxs-lookup"><span data-stu-id="2849a-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="2849a-252">`AppServiceLoginHandler.CreateToken()` Metoda zawiera *odbiorców* i *wystawcy* parametru.</span><span class="sxs-lookup"><span data-stu-id="2849a-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="2849a-253">Oba te parametry są ustawione na adres URL katalogu aplikacji za pomocą schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2849a-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="2849a-254">Podobnie należy ustawić *secretKey* jako klucza do podpisywania wartości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2849a-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="2849a-255">Nie rozpowszechniaj klucza podpisywania w kliencie jako mogą być używane do trudniej zdobyć kluczy i personifikować użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2849a-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="2849a-256">Można uzyskać klucza podpisywania, podczas gdy hostowanych w usłudze App Service za pomocą odwołań do *witryny sieci Web\_uwierzytelniania\_podpisywanie\_klucza* zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="2849a-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="2849a-257">W razie potrzeby w kontekście lokalnego debugowania, postępuj zgodnie z instrukcjami [debugowania lokalnego z uwierzytelnianiem](#local-debug) sekcji, aby pobrać klucz i zapisz go jako ustawienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2849a-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="2849a-258">Wystawiony token mogą również obejmować inne oświadczenia oraz datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="2849a-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="2849a-259">Minimalny, wystawionego tokenu musi zawierać temat (**sub**) oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2849a-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="2849a-260">Standardowa klienta może obsługiwać `loginAsync()` metoda przeciążenia trasy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2849a-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="2849a-261">Jeśli klient wywołuje `client.loginAsync('custom');` się zalogować, Twoje trasy nie może być `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="2849a-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="2849a-262">Można ustawić trasy dla kontrolera niestandardowego uwierzytelniania za pomocą `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="2849a-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="2849a-263">Przy użyciu `loginAsync()` podejście zapewnia, że token uwierzytelniania jest dołączona do każdego kolejne wywołania do usługi.</span><span class="sxs-lookup"><span data-stu-id="2849a-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="2849a-264"><a name="user-info"></a>Porady: pobieranie uwierzytelniony informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="2849a-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="2849a-265">Gdy użytkownik jest uwierzytelniany przez usługę App Service, są dostępne identyfikator użytkownika przypisany i inne informacje w kodzie zaplecza .NET.</span><span class="sxs-lookup"><span data-stu-id="2849a-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="2849a-266">Informacje o użytkowniku może służyć do podejmowania decyzji dotyczących autoryzacji w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2849a-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="2849a-267">Poniższy kod pobiera identyfikator użytkownika skojarzony z żądaniem:</span><span class="sxs-lookup"><span data-stu-id="2849a-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="2849a-268">Identyfikator SID jest określana na podstawie Identyfikatora użytkownika specyficznych dla dostawcy i jest statyczny dla danego użytkownika i dostawcy logowania.</span><span class="sxs-lookup"><span data-stu-id="2849a-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="2849a-269">Identyfikator SID ma wartość null dla nieprawidłowego uwierzytelniania tokenów.</span><span class="sxs-lookup"><span data-stu-id="2849a-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="2849a-270">Usługa App Service umożliwia również żądania określonych oświadczeń od dostawcy logowania.</span><span class="sxs-lookup"><span data-stu-id="2849a-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="2849a-271">Każdy dostawca tożsamości Aby uzyskać więcej informacji, przy użyciu dostawcy tożsamości zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2849a-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="2849a-272">Na przykład można użyć interfejsu API programu Graph usługi Facebook informacji znajomych.</span><span class="sxs-lookup"><span data-stu-id="2849a-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="2849a-273">W bloku dostawcy w portalu Azure, można określić oświadczenia, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="2849a-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="2849a-274">Niektóre oświadczenia wymagają dodatkowej konfiguracji z dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="2849a-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="2849a-275">Poniższy kod wywołania **GetAppServiceIdentityAsync** — metoda rozszerzenia można pobrać tokenu poświadczenia logowania, które obejmują dostęp potrzebne do podejmowania żądania kierowane do interfejsu Graph API usługi Facebook:</span><span class="sxs-lookup"><span data-stu-id="2849a-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="2849a-276">Dodaj using instrukcji dla `System.Security.Principal` zapewnienie **GetAppServiceIdentityAsync** — metoda rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="2849a-277"><a name="authorize"></a>Porady: ograniczanie autoryzowanym użytkownikom dostęp do danych</span><span class="sxs-lookup"><span data-stu-id="2849a-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="2849a-278">W poprzedniej sekcji możemy pokazano, jak uzyskać identyfikator użytkownika uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2849a-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="2849a-279">Można ograniczyć dostęp do danych i innych zasobów na podstawie tej wartości.</span><span class="sxs-lookup"><span data-stu-id="2849a-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="2849a-280">Na przykład dodać kolumnę userId do tabel i filtrowanie wyników zapytania za pomocą Identyfikatora użytkownika jest prosty sposób, aby ograniczyć liczbę zwracanych danych tylko do autoryzowanych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2849a-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="2849a-281">Poniższy kod zwraca wiersze danych tylko wtedy, gdy identyfikator SID jest zgodna z wartością w kolumnie identyfikator użytkownika w tabeli TodoItem:</span><span class="sxs-lookup"><span data-stu-id="2849a-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="2849a-282">`Query()` Metoda zwraca `IQueryable` który można manipulować LINQ do obsługi filtrowania.</span><span class="sxs-lookup"><span data-stu-id="2849a-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="2849a-283">Porady: Dodawanie wypychania powiadomień do projektu serwera</span><span class="sxs-lookup"><span data-stu-id="2849a-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="2849a-284">Dodawanie powiadomień wypychanych do projektu serwera przez rozszerzenie **MobileAppConfiguration** obiektu i Tworzenie klienta usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="2849a-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="2849a-285">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj `Microsoft.Azure.Mobile.Server.Notifications`, następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="2849a-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="2849a-286">Powtórz ten krok, aby zainstalować `Microsoft.Azure.NotificationHubs` pakiet, który zawiera Biblioteka klienta usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="2849a-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="2849a-287">W App_Start/Startup.MobileApp.cs i dodaj wywołanie do **AddPushNotifications()** — metoda rozszerzenia podczas inicjowania:</span><span class="sxs-lookup"><span data-stu-id="2849a-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="2849a-288">Dodaj następujący kod, który tworzy centra powiadomień klienta:</span><span class="sxs-lookup"><span data-stu-id="2849a-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="2849a-289">Klienta usługi Notification Hubs można teraz używać do wysyłania powiadomień wypychanych do zarejestrowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="2849a-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="2849a-290">Aby uzyskać więcej informacji, zobacz [Dodawanie powiadomień wypychanych do aplikacji](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="2849a-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="2849a-291">Aby dowiedzieć się więcej o usłudze Notification Hubs, zobacz [omówienie centra powiadomień](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2849a-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="2849a-292"><a name="tags"></a>Porady: Włączanie docelowe wypychanych przy użyciu tagów</span><span class="sxs-lookup"><span data-stu-id="2849a-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="2849a-293">Usługi Notification Hubs umożliwia wysyłanie powiadomień docelowe do określonych rejestracji przy użyciu tagów.</span><span class="sxs-lookup"><span data-stu-id="2849a-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="2849a-294">Kilka tagi są tworzone automatycznie:</span><span class="sxs-lookup"><span data-stu-id="2849a-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="2849a-295">Identyfikator instalacji identyfikuje określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2849a-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="2849a-296">Nazwa użytkownika, oparte na uwierzytelniony identyfikator SID identyfikuje określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2849a-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="2849a-297">Identyfikator jest możliwy z instalacji **installationId** właściwość **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="2849a-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="2849a-298">Poniższy przykład pokazuje, jak dodać tag do instalacji określonych w usłudze Notification Hubs za pomocą Identyfikatora instalacji:</span><span class="sxs-lookup"><span data-stu-id="2849a-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="2849a-299">Wszystkie znaczniki dostarczany przez klienta podczas rejestracji powiadomień wypychanych są ignorowane przez zaplecze, podczas tworzenia instalacji.</span><span class="sxs-lookup"><span data-stu-id="2849a-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="2849a-300">Aby włączyć klienta dodać tagi do instalacji, należy utworzyć niestandardowego interfejsu API, który dodaje znaczniki przy użyciu poprzedniego wzorca.</span><span class="sxs-lookup"><span data-stu-id="2849a-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="2849a-301">Zobacz [tagi powiadomień wypychanych dodać klienta] [ 5] w przykładowym ukończone szybkiego startu App Service Mobile Apps przykład.</span><span class="sxs-lookup"><span data-stu-id="2849a-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="2849a-302"><a name="push-user"></a>Porady: wysyłanie powiadomień wypychanych do uwierzytelnionego użytkownika</span><span class="sxs-lookup"><span data-stu-id="2849a-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="2849a-303">Uwierzytelniony użytkownik rejestrujący dla powiadomień wypychanych, tag identyfikator użytkownika jest automatycznie dodawany do rejestracji.</span><span class="sxs-lookup"><span data-stu-id="2849a-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="2849a-304">Za pomocą tego tagu, można wysyłać powiadomienia wypychane do wszystkich urządzeń zarejestrowanych przez tę osobę.</span><span class="sxs-lookup"><span data-stu-id="2849a-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="2849a-305">Poniższy kod pobiera identyfikator SID użytkownika wysyłającego żądanie i wyśle powiadomienie wypychane szablonu do rejestracji urządzeń dla tej osoby:</span><span class="sxs-lookup"><span data-stu-id="2849a-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="2849a-306">Podczas rejestrowania dla powiadomień wypychanych z uwierzytelnionego klienta, upewnij się, że przed podjęciem próby wykonania rejestracji zakończeniem uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2849a-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="2849a-307">Aby uzyskać więcej informacji, zobacz [Push użytkownikom] [ 6] w próbce App Service Mobile Apps ukończone szybkiego startu dla zaplecza .NET.</span><span class="sxs-lookup"><span data-stu-id="2849a-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="2849a-308">Porady: debugowanie i rozwiązywanie problemów z serwerem zestawu SDK .NET</span><span class="sxs-lookup"><span data-stu-id="2849a-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="2849a-309">Usługa aplikacji Azure zapewnia kilka debugowania i rozwiązywanie problemów z techniki dla aplikacji ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="2849a-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="2849a-310">Monitorowanie usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="2849a-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="2849a-311">Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="2849a-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="2849a-312">Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2849a-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="2849a-313">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="2849a-313">Logging</span></span>
<span data-ttu-id="2849a-314">Możesz zapisywać do dzienników diagnostycznych App Service przy użyciu standardowych zapisywanie śledzenia ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2849a-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="2849a-315">Zanim można zapisywać w dziennikach, należy włączyć diagnostyki w zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="2849a-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="2849a-316">Aby włączyć diagnostykę i zapisywać w dziennikach:</span><span class="sxs-lookup"><span data-stu-id="2849a-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="2849a-317">Postępuj zgodnie z instrukcjami [włączania diagnostyki](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="2849a-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="2849a-318">Dodaj następującą instrukcję using w pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="2849a-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="2849a-319">Utwórz moduł zapisujący śledzenia do zapisania z zaplecza .NET do dzienników diagnostycznych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2849a-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="2849a-320">Ponownie opublikować projekt serwera, a dostęp do zaplecza aplikacji mobilnej na wykonanie ścieżki kodu z rejestrowaniem.</span><span class="sxs-lookup"><span data-stu-id="2849a-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="2849a-321">Pobierz i ocenić dzienniki, zgodnie z opisem w [porady: pobieranie dzienników](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="2849a-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="2849a-322"><a name="local-debug"></a>Debugowanie za pomocą uwierzytelniania lokalnego</span><span class="sxs-lookup"><span data-stu-id="2849a-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="2849a-323">Możesz uruchomić aplikację lokalnie, aby przetestować zmiany przed ich opublikowaniem w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2849a-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="2849a-324">Dla większości zapleczy Azure Mobile Apps, naciśnij klawisz *F5* while w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2849a-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="2849a-325">Istnieją pewne dodatkowe kwestie przy użyciu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2849a-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="2849a-326">Musi być oparta na chmurze aplikacji mobilnej z aplikacji usługi uwierzytelniania/autoryzacji skonfigurowany, a klient musi mieć określony jako host alternatywnego końcowego w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2849a-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="2849a-327">W dokumentacji platformy klienta, aby poznać konkretne kroki wymagane.</span><span class="sxs-lookup"><span data-stu-id="2849a-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="2849a-328">Upewnij się, że Twoje zaplecze aplikacji mobilnej ma [Microsoft.Azure.Mobile.Server.Authentication] zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="2849a-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="2849a-329">Następnie, w aplikacji klasy początkowej OWIN, Dodaj następujące polecenie, po `MobileAppConfiguration` zostały zastosowane do Twojej `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="2849a-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="2849a-330">W poprzednim przykładzie, należy skonfigurować *authAudience* i *authIssuer* ustawienia aplikacji w pliku Web.config plików do każdej być adresem URL katalogu aplikacji przy użyciu schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2849a-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="2849a-331">Podobnie należy ustawić *authSigningKey* jako klucza do podpisywania wartości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2849a-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="2849a-332">Aby uzyskać klucza podpisywania:</span><span class="sxs-lookup"><span data-stu-id="2849a-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="2849a-333">Przejdź do aplikacji w ramach [portalu Azure]</span><span class="sxs-lookup"><span data-stu-id="2849a-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="2849a-334">Kliknij przycisk **narzędzia**, **Kudu**, **Przejdź**.</span><span class="sxs-lookup"><span data-stu-id="2849a-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="2849a-335">W witrynie zarządzania Kudu kliknij **środowiska**.</span><span class="sxs-lookup"><span data-stu-id="2849a-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="2849a-336">Znajdź wartość *witryny sieci Web\_uwierzytelniania\_podpisywanie\_klucza*.</span><span class="sxs-lookup"><span data-stu-id="2849a-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="2849a-337">Użyj klucza podpisywania dla *authSigningKey* parametru w pliku config aplikacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="2849a-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="2849a-338">Przenośne zaplecza teraz jest przystosowany do sprawdzania poprawności tokenów podczas uruchamiania lokalnego, które klient otrzymuje token z chmurowego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="2849a-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="2849a-339">[portalu Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="2849a-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="2849a-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="2849a-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="2849a-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="2849a-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="2849a-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="2849a-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="2849a-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="2849a-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="2849a-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="2849a-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="2849a-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="2849a-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
