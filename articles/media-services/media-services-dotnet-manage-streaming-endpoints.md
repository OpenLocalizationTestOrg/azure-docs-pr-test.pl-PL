---
title: "aaaManage punkty końcowe przy użyciu zestawu .NET SDK przesyłania strumieniowego. | Microsoft Docs"
description: "W tym temacie przedstawiono sposób toomanage punktów końcowych przesyłania strumieniowego z hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="1fca3-104">Zarządzanie punktów końcowych przesyłania strumieniowego przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1fca3-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="1fca3-105">Upewnij się, że hello tooreview [omówienie](media-services-streaming-endpoints-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="1fca3-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="1fca3-106">Sprawdź również [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="1fca3-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="1fca3-107">Kod Hello w tym temacie przedstawiono, jak hello toodo następujące zadania za pomocą hello zestawu .NET SDK usługi Azure Media Services:</span><span class="sxs-lookup"><span data-stu-id="1fca3-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="1fca3-108">Sprawdź, czy domyślne hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1fca3-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="1fca3-109">Utwórz/Dodaj nowy punkt końcowy przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1fca3-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="1fca3-110">Można toohave wiele punktów końcowych przesyłania strumieniowego, jeśli planujesz toohave różnych CDN lub CDN i bezpośredni dostęp.</span><span class="sxs-lookup"><span data-stu-id="1fca3-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1fca3-111">Rozliczenie jest przeprowadzane tylko w przypadku przesyłania strumieniowego punktu końcowego jest w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="1fca3-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="1fca3-112">Zaktualizuj hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1fca3-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="1fca3-113">Upewnij się hello toocall Funkcja Update().</span><span class="sxs-lookup"><span data-stu-id="1fca3-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="1fca3-114">Usuń hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1fca3-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="1fca3-115">Nie można usunąć domyślnej Hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1fca3-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="1fca3-116">Aby uzyskać informacje o sposobie tooscale hello punktu końcowego przesyłania strumieniowego, zobacz [to](media-services-portal-scale-streaming-endpoints.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="1fca3-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="1fca3-117">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1fca3-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="1fca3-118">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1fca3-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="1fca3-119">Dodaj kod, który zarządza punktów końcowych przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="1fca3-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="1fca3-120">Zastąp kod hello w pliku Program.cs hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="1fca3-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
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

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="1fca3-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1fca3-121">Next steps</span></span>
<span data-ttu-id="1fca3-122">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1fca3-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1fca3-123">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="1fca3-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

