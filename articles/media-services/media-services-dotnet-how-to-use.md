---
title: "tooSet aaaHow zapasowej komputera do tworzenia usługi Media z platformą .NET"
description: "Dowiedz się więcej o wymaganiach wstępnych hello Media Services przy użyciu hello SDK usługi Media Services dla platformy .NET. Też dowiedzieć się, jak toocreate aplikacji Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="14d1c-104">Tworzenia usługi Media Services z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="14d1c-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="14d1c-105">W tym temacie omówiono sposób toostart tworzenie Media Services aplikacji przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="14d1c-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="14d1c-106">Witaj **zestawu .NET SDK usługi Azure Media Services** biblioteki umożliwia tooprogram względem usługi Media Services przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="14d1c-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="14d1c-107">toomake go nawet łatwiejsze toodevelop z platformą .NET, hello **rozszerzenia SDK .NET usługi Azure Media Services** podano biblioteki.</span><span class="sxs-lookup"><span data-stu-id="14d1c-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="14d1c-108">Ta biblioteka zawiera zestaw metod rozszerzeń i funkcje pomocnicze, które upraszczają kodu .NET.</span><span class="sxs-lookup"><span data-stu-id="14d1c-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="14d1c-109">Zarówno biblioteki są dostępne za pośrednictwem **NuGet** i **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="14d1c-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14d1c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="14d1c-110">Prerequisites</span></span>
* <span data-ttu-id="14d1c-111">Konto usługi Media Services w nowej lub istniejącej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14d1c-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="14d1c-112">Zobacz temat hello [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="14d1c-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="14d1c-113">Systemy operacyjne: Windows 10, Windows 7, Windows 2008 R2 lub Windows 8.</span><span class="sxs-lookup"><span data-stu-id="14d1c-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="14d1c-114">Program .NET framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="14d1c-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="14d1c-115">Program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14d1c-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="14d1c-116">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="14d1c-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="14d1c-117">W tej sekcji opisano sposób toocreate projektu programu Visual Studio i skonfigurować go do tworzenia usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="14d1c-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="14d1c-118">W takim przypadku projekt hello jest aplikacji konsolowej C# systemu Windows, ale hello same kroki instalacji pokazane zastosować tooother typy projektów utworzonych dla usługi Media Services w aplikacji (na przykład aplikacji formularzy systemu Windows lub aplikacji sieci Web programu ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="14d1c-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="14d1c-119">W tej sekcji przedstawiono sposób toouse **NuGet** tooadd .NET SDK usługi Media Services rozszerzenia i inne zależnej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="14d1c-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="14d1c-120">Alternatywnie można uzyskać hello najnowsze bitów .NET SDK usługi Media Services z usługi GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) lub [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), utworzenie rozwiązania hello i dodawanie projektu klienta toohello odwołania hello.</span><span class="sxs-lookup"><span data-stu-id="14d1c-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="14d1c-121">Wszystkie zależności niezbędne hello uzyskać pobrane i wyodrębnione automatycznie.</span><span class="sxs-lookup"><span data-stu-id="14d1c-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="14d1c-122">Utwórz nową aplikację konsoli języka C# w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14d1c-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="14d1c-123">Wprowadź hello **nazwa**, **lokalizacji**, i **Nazwa rozwiązania**, a następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="14d1c-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="14d1c-124">Utworzenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="14d1c-124">Build hello solution.</span></span>
3. <span data-ttu-id="14d1c-125">Użyj **NuGet** tooinstall i Dodaj **rozszerzenia SDK .NET usługi Azure Media Services** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="14d1c-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="14d1c-126">Podczas instalacji tego pakietu instalowany jest również zestaw **.NET SDK usługi Media Services** oraz dodawane są wszystkie inne wymagane zależności.</span><span class="sxs-lookup"><span data-stu-id="14d1c-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="14d1c-127">Upewnij się, że masz hello najnowszą wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="14d1c-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="14d1c-128">Aby uzyskać dodatkowe instrukcje instalacji i informacje, zobacz [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="14d1c-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="14d1c-129">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy nazwę projektu hello hello, a następnie wybierz pakiety zarządzania pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="14d1c-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="14d1c-130">zostanie wyświetlone okno dialogowe Zarządzanie pakietami NuGet Hello.</span><span class="sxs-lookup"><span data-stu-id="14d1c-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="14d1c-131">W galerii Online hello, wyszukaj rozszerzenia MediaServices Azure, wybierz rozszerzenia SDK .NET usługi Azure Media Services, a następnie kliknij przycisk Zainstaluj hello.</span><span class="sxs-lookup"><span data-stu-id="14d1c-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="14d1c-132">Projekt Hello jest modyfikowany i odwołuje się do toohello rozszerzenia SDK usługi Media Services .NET, SDK .NET usługi Media Services, i są dodawane innych zestawów zależnych.</span><span class="sxs-lookup"><span data-stu-id="14d1c-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="14d1c-133">toopromote czyszczący Środowisko deweloperskie, należy wziąć pod uwagę umożliwiające przywracanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="14d1c-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="14d1c-134">Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu NuGet "](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="14d1c-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="14d1c-135">Dodaj odwołanie za**System.Configuration** zestawu.</span><span class="sxs-lookup"><span data-stu-id="14d1c-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="14d1c-136">Ten zestaw zawiera hello System.Configuration. **ConfigurationManager** klasy czyli pliki konfiguracji używane tooaccess (na przykład App.config).</span><span class="sxs-lookup"><span data-stu-id="14d1c-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="14d1c-137">odwołania tooadd za pomocą okna dialogowego Zarządzanie odwołaniami hello, kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań hello.</span><span class="sxs-lookup"><span data-stu-id="14d1c-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="14d1c-138">Następnie wybierz Dodaj i odwołania.</span><span class="sxs-lookup"><span data-stu-id="14d1c-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="14d1c-139">zostanie wyświetlone okno dialogowe Zarządzanie odwołaniami Hello.</span><span class="sxs-lookup"><span data-stu-id="14d1c-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="14d1c-140">W obszarze zestawów struktury .NET Znajdź i wybierz zestawu System.Configuration hello i naciśnij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="14d1c-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="14d1c-141">Otwórz plik App.config hello i Dodaj *appSettings* pliku toohello sekcji.</span><span class="sxs-lookup"><span data-stu-id="14d1c-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="14d1c-142">Ustaw wartości hello, które są potrzebne tooconnect toohello Media Services API.</span><span class="sxs-lookup"><span data-stu-id="14d1c-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="14d1c-143">Aby uzyskać więcej informacji, zobacz [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="14d1c-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="14d1c-144">Jeśli używasz [uwierzytelnianie użytkownika](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) pliku konfiguracji, prawdopodobnie będzie mieć wartości domeny dzierżawy usługi Azure AD i hello punkt końcowy interfejsu API REST usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="14d1c-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="14d1c-145">Większość przykładów kodu w dokumentacji usługi Azure Media Services hello zestawu, użyj typu (interactive) użytkownika toohello tooconnect uwierzytelniania interfejsu API usług AMS.</span><span class="sxs-lookup"><span data-stu-id="14d1c-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="14d1c-146">Ta metoda uwierzytelniania będzie działać do zarządzania i monitorowania natywnych aplikacji: aplikacje mobilne, aplikacje systemu Windows i aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="14d1c-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="14d1c-147">Ta metoda uwierzytelniania nie jest odpowiedni dla serwera, usługi sieci web, interfejsów API typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14d1c-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="14d1c-148">Aby uzyskać więcej informacji, zobacz [hello dostępu do interfejsu API usług AMS przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="14d1c-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="14d1c-149">Zastąp istniejący hello **przy użyciu** instrukcje hello początku pliku Program.cs hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="14d1c-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="14d1c-150">W tym momencie wszystko jest gotowe toostart opracowanie aplikacji usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="14d1c-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="14d1c-151">Przykład</span><span class="sxs-lookup"><span data-stu-id="14d1c-151">Example</span></span>

<span data-ttu-id="14d1c-152">W tym miejscu jest mała przykład łączy toohello AMS interfejsu API, który zawiera listę wszystkich dostępnych procesorów nośnika.</span><span class="sxs-lookup"><span data-stu-id="14d1c-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="14d1c-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14d1c-153">Next steps</span></span>

<span data-ttu-id="14d1c-154">Teraz [możesz połączyć toohello interfejsu API usług AMS](media-services-use-aad-auth-to-access-ams-api.md) i uruchomić [tworzenie](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="14d1c-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="14d1c-155">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="14d1c-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="14d1c-156">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="14d1c-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

