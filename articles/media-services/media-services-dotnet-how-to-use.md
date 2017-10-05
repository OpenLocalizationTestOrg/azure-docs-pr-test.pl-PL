---
title: "Jak skonfigurować komputer Media Services programowanie z platformą .NET"
description: "Więcej informacji na temat wymagania wstępne dotyczące usługi Media Services przy użyciu zestawu SDK usługi Media Services dla platformy .NET. Również informacje o sposobie tworzenia aplikacji programu Visual Studio."
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
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="86d7c-104">Tworzenia usługi Media Services z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="86d7c-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="86d7c-105">W tym temacie omówiono sposób rozpocząć tworzenie aplikacji usługi Media Services przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="86d7c-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="86d7c-106">**Zestawu .NET SDK usługi Azure Media Services** biblioteki umożliwia program względem usługi Media Services przy użyciu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="86d7c-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="86d7c-107">Aby ułatwić nawet tworzyć aplikacje za pomocą platformy .NET, **rozszerzenia SDK .NET usługi Azure Media Services** podano biblioteki.</span><span class="sxs-lookup"><span data-stu-id="86d7c-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="86d7c-108">Ta biblioteka zawiera zestaw metod rozszerzeń i funkcje pomocnicze, które upraszczają kodu .NET.</span><span class="sxs-lookup"><span data-stu-id="86d7c-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="86d7c-109">Zarówno biblioteki są dostępne za pośrednictwem **NuGet** i **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="86d7c-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86d7c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="86d7c-110">Prerequisites</span></span>
* <span data-ttu-id="86d7c-111">Konto usługi Media Services w nowej lub istniejącej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="86d7c-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="86d7c-112">Zobacz temat [Tworzenie konta usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="86d7c-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="86d7c-113">Systemy operacyjne: Windows 10, Windows 7, Windows 2008 R2 lub Windows 8.</span><span class="sxs-lookup"><span data-stu-id="86d7c-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="86d7c-114">Program .NET framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="86d7c-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="86d7c-115">Program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86d7c-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="86d7c-116">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86d7c-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="86d7c-117">W tej sekcji przedstawiono sposób tworzenia projektu w programie Visual Studio i skonfigurować go do tworzenia usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="86d7c-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="86d7c-118">W tym przypadku projekt jest aplikacją konsoli Windows C#, ale te same kroki instalacji podane tutaj dotyczą innych typów projektów, które można utworzyć dla aplikacji usługi Media Services (na przykład aplikacji formularzy systemu Windows lub aplikacji sieci Web programu ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="86d7c-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="86d7c-119">W tej sekcji przedstawiono sposób użycia **NuGet** można dodać rozszerzenia .NET SDK usługi Media Services i innych zależnych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="86d7c-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="86d7c-120">Alternatywnie można uzyskać najnowsze bitów .NET SDK usługi Media Services z usługi GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) lub [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), Skompiluj rozwiązanie i dodać odwołań do projektu klienta.</span><span class="sxs-lookup"><span data-stu-id="86d7c-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="86d7c-121">Wszystkie wymagane zależności uzyskać pobrane i wyodrębnione automatycznie.</span><span class="sxs-lookup"><span data-stu-id="86d7c-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="86d7c-122">Utwórz nową aplikację konsoli języka C# w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86d7c-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="86d7c-123">Wprowadź **nazwa**, **lokalizacji**, i **Nazwa rozwiązania**, a następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="86d7c-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="86d7c-124">Skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="86d7c-124">Build the solution.</span></span>
3. <span data-ttu-id="86d7c-125">Użyj **NuGet** zainstalować i dodać **rozszerzenia SDK .NET usługi Azure Media Services** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="86d7c-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="86d7c-126">Podczas instalacji tego pakietu instalowany jest również zestaw **.NET SDK usługi Media Services** oraz dodawane są wszystkie inne wymagane zależności.</span><span class="sxs-lookup"><span data-stu-id="86d7c-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="86d7c-127">Upewnij się, że masz najnowszą wersję programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="86d7c-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="86d7c-128">Aby uzyskać dodatkowe instrukcje instalacji i informacje, zobacz [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="86d7c-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="86d7c-129">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy nazwę projektu, a następnie wybierz pakiety zarządzania pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="86d7c-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="86d7c-130">Zostanie wyświetlone okno dialogowe Zarządzanie pakietami NuGet.</span><span class="sxs-lookup"><span data-stu-id="86d7c-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="86d7c-131">W galerii Online wyszukiwanie Azure MediaServices rozszerzeń, wybierz rozszerzenia SDK .NET usługi Azure Media Services, a następnie kliknij przycisk Zainstaluj.</span><span class="sxs-lookup"><span data-stu-id="86d7c-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="86d7c-132">Projekt zostanie zmodyfikowana, a odwołania do rozszerzenia SDK .NET usługi Media Services SDK .NET usługi Media Services i innych zestawów zależnych zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="86d7c-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="86d7c-133">Aby promować czyszczący Środowisko deweloperskie, należy rozważyć włączenie, Przywracanie pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="86d7c-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="86d7c-134">Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu NuGet "](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="86d7c-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="86d7c-135">Dodaj odwołanie do **System.Configuration** zestawu.</span><span class="sxs-lookup"><span data-stu-id="86d7c-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="86d7c-136">Ten zestaw zawiera System.Configuration. **ConfigurationManager** klasy, która umożliwia dostęp do plików konfiguracji (na przykład App.config).</span><span class="sxs-lookup"><span data-stu-id="86d7c-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="86d7c-137">Aby dodać odwołań za pomocą okna dialogowego Zarządzanie odwołaniami, kliknij prawym przyciskiem myszy nazwę projektu w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="86d7c-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="86d7c-138">Następnie wybierz Dodaj i odwołania.</span><span class="sxs-lookup"><span data-stu-id="86d7c-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="86d7c-139">Zostanie wyświetlone okno dialogowe Zarządzanie odwołań.</span><span class="sxs-lookup"><span data-stu-id="86d7c-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="86d7c-140">W obszarze zestawów struktury .NET Znajdź i wybierz zestawu System.Configuration i naciśnij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="86d7c-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="86d7c-141">Otwórz plik App.config i Dodaj *appSettings* sekcji w pliku.</span><span class="sxs-lookup"><span data-stu-id="86d7c-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="86d7c-142">Ustaw wartości, które są wymagane do nawiązania połączenia interfejsu API usług Media Services.</span><span class="sxs-lookup"><span data-stu-id="86d7c-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="86d7c-143">Aby uzyskać więcej informacji, zobacz [dostępu Azure Media Services API przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="86d7c-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="86d7c-144">Jeśli używasz [uwierzytelnianie użytkownika](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) pliku konfiguracji, prawdopodobnie będzie mieć wartości domeny dzierżawy usługi Azure AD i punkt końcowy interfejsu API REST usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="86d7c-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="86d7c-145">Większość przykładów kodu w dokumentacji usługi Azure Media Services zestawu, użyj typu (interactive) użytkownika uwierzytelniania do nawiązania połączenia interfejsu API usług AMS.</span><span class="sxs-lookup"><span data-stu-id="86d7c-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="86d7c-146">Ta metoda uwierzytelniania będzie działać do zarządzania i monitorowania natywnych aplikacji: aplikacje mobilne, aplikacje systemu Windows i aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="86d7c-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="86d7c-147">Ta metoda uwierzytelniania nie jest odpowiedni dla serwera, usługi sieci web, interfejsów API typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="86d7c-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="86d7c-148">Aby uzyskać więcej informacji, zobacz [dostęp do interfejsu API usług AMS przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="86d7c-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="86d7c-149">Zastąp istniejące instrukcje **using** na początku pliku Program.cs następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="86d7c-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="86d7c-150">W tym momencie można przystąpić do rozpocząć tworzenie aplikacji usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="86d7c-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="86d7c-151">Przykład</span><span class="sxs-lookup"><span data-stu-id="86d7c-151">Example</span></span>

<span data-ttu-id="86d7c-152">Oto przykład małych, który jest podłączany do interfejsu API usług AMS i wyświetla wszystkie dostępne procesory multimediów.</span><span class="sxs-lookup"><span data-stu-id="86d7c-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
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

##<a name="next-steps"></a><span data-ttu-id="86d7c-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86d7c-153">Next steps</span></span>

<span data-ttu-id="86d7c-154">Teraz [możesz połączyć się z interfejsu API usług AMS](media-services-use-aad-auth-to-access-ams-api.md) i uruchomić [tworzenie](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="86d7c-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="86d7c-155">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="86d7c-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="86d7c-156">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="86d7c-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

