---
title: "Jak wykonać transmisję strumieniową na żywo za pomocą koderów lokalnych przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "W tym temacie pokazano, jak kodowanie na żywo za pomocą koderów lokalnych przy użyciu platformy .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 15908152-d23c-4d55-906a-3bfd74927db5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/18/2017
ms.author: cenkdin;juliako
ms.openlocfilehash: 3ef6065f5b9e05e0ea5716548699943a2c877bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-net"></a><span data-ttu-id="db197-103">Jak wykonać transmisję strumieniową na żywo za pomocą koderów lokalnych przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="db197-103">How to perform live streaming with on-premises encoders using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db197-104">Portal</span><span class="sxs-lookup"><span data-stu-id="db197-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="db197-105">.NET</span><span class="sxs-lookup"><span data-stu-id="db197-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="db197-106">REST</span><span class="sxs-lookup"><span data-stu-id="db197-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="db197-107">Ten samouczek przedstawia kroki tworzenia przy użyciu zestawu SDK .NET usługi Azure Media Services **kanału** skonfigurowanego do dostarczania w formie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="db197-107">This tutorial walks you through the steps of using the Azure Media Services .NET SDK to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db197-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="db197-108">Prerequisites</span></span>
<span data-ttu-id="db197-109">Do wykonania czynności przedstawionych w tym samouczku są niezbędne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="db197-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="db197-110">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="db197-110">An Azure account.</span></span>
* <span data-ttu-id="db197-111">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="db197-111">A Media Services account.</span></span>    <span data-ttu-id="db197-112">Aby utworzyć konto usługi Media Services, zobacz temat [Jak utworzyć konto usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="db197-112">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="db197-113">Konfigurowanie środowiska deweloperów.</span><span class="sxs-lookup"><span data-stu-id="db197-113">Set up your dev environment.</span></span> <span data-ttu-id="db197-114">Aby uzyskać więcej informacji, zobacz [konfigurowania środowiska](media-services-set-up-computer.md).</span><span class="sxs-lookup"><span data-stu-id="db197-114">For more information, see [Set up your environment](media-services-set-up-computer.md).</span></span>
* <span data-ttu-id="db197-115">Kamera internetowa.</span><span class="sxs-lookup"><span data-stu-id="db197-115">A webcam.</span></span> <span data-ttu-id="db197-116">Na przykład [koder Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="db197-116">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="db197-117">Zaleca się następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="db197-117">Recommended to review the following articles:</span></span>

* [<span data-ttu-id="db197-118">Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="db197-118">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="db197-119">Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="db197-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="db197-120">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db197-120">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="db197-121">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="db197-121">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="example"></a><span data-ttu-id="db197-122">Przykład</span><span class="sxs-lookup"><span data-stu-id="db197-122">Example</span></span>
<span data-ttu-id="db197-123">W poniższym przykładzie pokazano, jak wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="db197-123">The following code example demonstrates how to achieve the following tasks:</span></span>

* <span data-ttu-id="db197-124">Łączenie się z usługą Media Services</span><span class="sxs-lookup"><span data-stu-id="db197-124">Connect to Media Services</span></span>
* <span data-ttu-id="db197-125">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="db197-125">Create a channel</span></span>
* <span data-ttu-id="db197-126">Aktualizacja kanału</span><span class="sxs-lookup"><span data-stu-id="db197-126">Update the channel</span></span>
* <span data-ttu-id="db197-127">Pobrać wejściowy punkt końcowy kanału.</span><span class="sxs-lookup"><span data-stu-id="db197-127">Retrieve the channel’s input endpoint.</span></span> <span data-ttu-id="db197-128">Wejściowy punkt końcowy należy przekazać do kodera na żywo w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="db197-128">The input endpoint should be provided to the on-premises live encoder.</span></span> <span data-ttu-id="db197-129">Kodera na żywo konwertuje sygnały z kamery do strumieni, które są wysyłane do tego kanału danych wejściowych (pozyskiwania) punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="db197-129">The live encoder converts signals from the camera to streams that are sent to the channel’s input (ingest) endpoint.</span></span>
* <span data-ttu-id="db197-130">Pobieranie punktu końcowego podglądu kanału</span><span class="sxs-lookup"><span data-stu-id="db197-130">Retrieve the channel’s preview endpoint</span></span>
* <span data-ttu-id="db197-131">Tworzenie i uruchamianie programu</span><span class="sxs-lookup"><span data-stu-id="db197-131">Create and start a program</span></span>
* <span data-ttu-id="db197-132">Utwórz Lokalizator musiał uzyskać dostęp do programu</span><span class="sxs-lookup"><span data-stu-id="db197-132">Create a locator needed to access the program</span></span>
* <span data-ttu-id="db197-133">Tworzenie i uruchamianie StreamingEndpoint</span><span class="sxs-lookup"><span data-stu-id="db197-133">Create and start a StreamingEndpoint</span></span>
* <span data-ttu-id="db197-134">Aktualizowanie punktu końcowego przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="db197-134">Update the streaming endpoint</span></span>
* <span data-ttu-id="db197-135">Zamknij zasobów</span><span class="sxs-lookup"><span data-stu-id="db197-135">Shut down resources</span></span>

>[!IMPORTANT]
><span data-ttu-id="db197-136">Upewnij się, że punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, ma stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="db197-136">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
>[!NOTE]
><span data-ttu-id="db197-137">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="db197-137">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="db197-138">Należy używać tego samego identyfikatora zasad, jeśli zawsze są używane uprawnienia dotyczące tych samych dni lub tego samego dostępu, na przykład dla lokalizatorów przeznaczonych do długotrwałego stosowania (nieprzekazywanych zasad).</span><span class="sxs-lookup"><span data-stu-id="db197-138">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="db197-139">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="db197-139">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="db197-140">Aby uzyskać informacje na temat konfigurowania kodera na żywo, zobacz [Obsługa protokołu RTMP usługi multimediów Azure i kodery na żywo](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span><span class="sxs-lookup"><span data-stu-id="db197-140">For information on how to configure a live encoder, see [Azure Media Services RTMP Support and Live Encoders](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/).</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSLiveTest
    {
        class Program
        {
        private const string StreamingEndpointName = "streamingendpoint001";
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

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

            IChannel channel = CreateAndStartChannel();

            // Set the Live Encoder to point to the channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            // Use the previewEndpoint to preview and verify
            // that the input from the encoder is actually reaching the Channel.
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            IProgram program = CreateAndStartProgram(channel);
            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);
            IStreamingEndpoint streamingEndpoint = CreateAndStartStreamingEndpoint(false);

            // Once you are done streaming, clean up your resources.
            Cleanup(streamingEndpoint, channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            //If you want to change the Smooth fragments to HLS segment ratio, you would set the ChannelCreationOptions’s Output property.

            IChannel channel = _context.Channels.Create(
            new ChannelCreationOptions
            {
            Name = ChannelName,
            Input = CreateChannelInput(),
            Preview = CreateChannelPreview()
            });

            //Starting and stopping Channels can take some time to execute. To determine the state of operations after calling Start or Stop, query the IChannel.State .

            channel.Start();

            return channel;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTMP,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                    {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access to IP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    // Setting 0.0.0.0 for Address and 0 for SubnetPrefixLength
                    // will allow access to IP addresses.
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForChannel(IChannel channel)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            channel.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            channel.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            channel.Update();
        }

        public static IProgram CreateAndStartProgram(IChannel channel)
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            // Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
            // however each Program must have a unique name within your Media Services account.
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            program.Start();

            return program;
        }

        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            

            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                "Live Stream Policy",
                ArchiveWindowLength,
                AccessPermissions.Read
                )
            );

            return locator;
        }

        public static IStreamingEndpoint CreateAndStartStreamingEndpoint(bool createNew)
        {
            IStreamingEndpoint streamingEndpoint = null;
            if (createNew)
            {
            var options = new StreamingEndpointCreationOptions
            {
                Name = StreamingEndpointName,
                ScaleUnits = 1,
                AccessControl = GetAccessControl(),
                CacheControl = GetCacheControl()
            };

            streamingEndpoint = _context.StreamingEndpoints.Create(options);
            }
            else
            {
            streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            }


            if (streamingEndpoint.State == StreamingEndpointState.Stopped)
            streamingEndpoint.Start();

            return streamingEndpoint;
        }

        private static StreamingEndpointAccessControl GetAccessControl()
        {
            return new StreamingEndpointAccessControl
            {
            IPAllowList = new List<IPRange>
                {
                new IPRange
                {
                    Name = "Allow all",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                }
                },

            AkamaiSignatureHeaderAuthenticationKeyList = new List<AkamaiSignatureHeaderAuthenticationKey>
                {
                new AkamaiSignatureHeaderAuthenticationKey
                {
                    Identifier = "My key",
                    Expiration = DateTime.UtcNow + TimeSpan.FromDays(365),
                    Base64Key = Convert.ToBase64String(GenerateRandomBytes(16))
                }
                }
            };
        }

        private static byte[] GenerateRandomBytes(int length)
        {
            var bytes = new byte[length];
            using (var rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(bytes);
            }

            return bytes;
        }

        private static StreamingEndpointCacheControl GetCacheControl()
        {
            return new StreamingEndpointCacheControl
            {
            MaxAge = TimeSpan.FromSeconds(1000)
            };
        }

        public static void UpdateCrossSiteAccessPoliciesForStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            var clientPolicy =
            @"<?xml version=""1.0"" encoding=""utf-8""?>
            <access-policy>
                <cross-domain-access>
                <policy>
                    <allow-from http-request-headers=""*"" http-methods=""*"">
                    <domain uri=""*""/>
                    </allow-from>
                    <grant-to>
                       <resource path=""/"" include-subpaths=""true""/>
                    </grant-to>
                </policy>
                </cross-domain-access>
            </access-policy>";

            var xdomainPolicy =
            @"<?xml version=""1.0"" ?>
            <cross-domain-policy>
                <allow-access-from domain=""*"" />
            </cross-domain-policy>";

            streamingEndpoint.CrossSiteAccessPolicies.ClientAccessPolicy = clientPolicy;
            streamingEndpoint.CrossSiteAccessPolicies.CrossDomainPolicy = xdomainPolicy;

            streamingEndpoint.Update();
        }

        public static void Cleanup(IStreamingEndpoint streamingEndpoint,
                        IChannel channel)
        {
            if (streamingEndpoint != null)
            {
            streamingEndpoint.Stop();
            if(streamingEndpoint.Name != "default")
                streamingEndpoint.Delete();
            }

            IAsset asset;
            if (channel != null)
            {

            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                program.Stop();
                program.Delete();

                if (asset != null)
                {
                foreach (var l in asset.Locators)
                    l.Delete();

                asset.Delete();
                }
            }

            channel.Stop();
            channel.Delete();
            }
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="db197-141">Następny krok</span><span class="sxs-lookup"><span data-stu-id="db197-141">Next Step</span></span>
<span data-ttu-id="db197-142">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="db197-142">Review Media Services learning paths</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="db197-143">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="db197-143">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

