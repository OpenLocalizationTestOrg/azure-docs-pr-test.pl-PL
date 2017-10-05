---
title: "Korzystanie z usługi Azure Media Services do prowadzenia transmisji strumieniowych na żywo ze strumieniami o różnych szybkościach transmisji bitów | Microsoft Docs"
description: "Ten samouczek przedstawia kroki tworzenia kanału, który odbiera strumień na żywo o pojedynczej szybkości transmisji bitów i koduje go jako strumień o wielokrotnej szybkości transmisji bitów przy użyciu zestawu SDK programu .NET."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22d63ff5e9fd33db8711b0c5125ab0882b9f6a74
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-using-azure-media-services-to-create-multi-bitrate-streams-with-net"></a><span data-ttu-id="cc464-103">Transmisja strumieniowa na żywo korzystająca z usługi Azure Media Services do tworzenia strumieni o wielokrotnej szybkości transmisji bitów z użyciem programu .NET</span><span class="sxs-lookup"><span data-stu-id="cc464-103">How to perform live streaming using Azure Media Services to create multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc464-104">Portal</span><span class="sxs-lookup"><span data-stu-id="cc464-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="cc464-105">.NET</span><span class="sxs-lookup"><span data-stu-id="cc464-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="cc464-106">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="cc464-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="cc464-107">Do ukończenia tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc464-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="cc464-108">Aby uzyskać szczegółowe informacje, zobacz temat [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="cc464-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="cc464-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cc464-109">Overview</span></span>
<span data-ttu-id="cc464-110">Ten samouczek przedstawia kroki tworzenia **kanału**, który odbiera strumień na żywo o pojedynczej szybkości transmisji bitów i koduje go jako strumień o wielokrotnej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="cc464-110">This tutorial walks you through the steps of creating a **Channel** that receives a single-bitrate live stream and encodes it to multi-bitrate stream.</span></span>

<span data-ttu-id="cc464-111">Aby uzyskać więcej informacji o pojęciach związanych z kanałami obsługującymi kodowanie na żywo, zobacz temat [Korzystanie z usługi Azure Media Services do prowadzenia transmisji strumieniowych na żywo ze strumieniami o wielokrotnej szybkości transmisji bitów](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="cc464-111">For more conceptual information related to Channels that are enabled for live encoding, see [Live streaming using Azure Media Services to create multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="cc464-112">Typowy scenariusz transmisji strumieniowej na żywo</span><span class="sxs-lookup"><span data-stu-id="cc464-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="cc464-113">W poniższych krokach opisano zadania związane z tworzeniem typowych aplikacji transmisji strumieniowej na żywo.</span><span class="sxs-lookup"><span data-stu-id="cc464-113">The following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="cc464-114">Obecnie maksymalny zalecany czas trwania wydarzenia na żywo wynosi 8 godzin.</span><span class="sxs-lookup"><span data-stu-id="cc464-114">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="cc464-115">Skontaktuj się pod adresem amslived@microsoft.com, jeśli chcesz uruchomić kanał na dłuższe okresy.</span><span class="sxs-lookup"><span data-stu-id="cc464-115">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="cc464-116">Podłącz kamerę wideo do komputera.</span><span class="sxs-lookup"><span data-stu-id="cc464-116">Connect a video camera to a computer.</span></span> <span data-ttu-id="cc464-117">Uruchom i skonfiguruj lokalny koder na żywo, który wysyła strumień o pojedynczej szybkości transmisji bitów przy użyciu jednego z następujących protokołów: RTMP, Smooth Streaming lub RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="cc464-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of the following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="cc464-118">Aby uzyskać więcej informacji, zobacz temat [Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="cc464-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="cc464-119">Ten krok można również wykonać po utworzeniu kanału.</span><span class="sxs-lookup"><span data-stu-id="cc464-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="cc464-120">Utwórz i uruchom kanał.</span><span class="sxs-lookup"><span data-stu-id="cc464-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="cc464-121">Pobierz adres URL pozyskiwania kanału.</span><span class="sxs-lookup"><span data-stu-id="cc464-121">Retrieve the Channel ingest URL.</span></span>

    <span data-ttu-id="cc464-122">Koder na żywo używa adresu URL pozyskiwania do wysyłania strumienia do kanału.</span><span class="sxs-lookup"><span data-stu-id="cc464-122">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>

4. <span data-ttu-id="cc464-123">Pobierz adres URL podglądu kanału.</span><span class="sxs-lookup"><span data-stu-id="cc464-123">Retrieve the Channel preview URL.</span></span>

    <span data-ttu-id="cc464-124">Użyj tego adresu URL, aby sprawdzić, czy kanał prawidłowo odbiera strumień na żywo.</span><span class="sxs-lookup"><span data-stu-id="cc464-124">Use this URL to verify that your channel is properly receiving the live stream.</span></span>

5. <span data-ttu-id="cc464-125">Utwórz zasób.</span><span class="sxs-lookup"><span data-stu-id="cc464-125">Create an asset.</span></span>
6. <span data-ttu-id="cc464-126">Aby zasób był dynamicznie szyfrowany podczas odtwarzania , należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cc464-126">If you want for the asset to be dynamically encrypted during playback, do the following:</span></span>
7. <span data-ttu-id="cc464-127">Utwórz klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="cc464-127">Create a content key.</span></span>
8. <span data-ttu-id="cc464-128">Skonfiguruj zasady autoryzacji klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="cc464-128">Configure the content key's authorization policy.</span></span>
9. <span data-ttu-id="cc464-129">Skonfiguruj zasady dostarczania zasobu (stosowane podczas pakowania dynamicznego i szyfrowania dynamicznego).</span><span class="sxs-lookup"><span data-stu-id="cc464-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="cc464-130">Utwórz program i określ użycie utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="cc464-130">Create a program and specify to use the asset that you created.</span></span>
11. <span data-ttu-id="cc464-131">Opublikuj zasób skojarzony z programem przez utworzenie lokalizatora OnDemand.</span><span class="sxs-lookup"><span data-stu-id="cc464-131">Publish the asset associated with the program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="cc464-132">Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**.</span><span class="sxs-lookup"><span data-stu-id="cc464-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="cc464-133">Punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="cc464-133">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

12. <span data-ttu-id="cc464-134">Uruchom program, gdy wszystko będzie gotowe do rozpoczęcia przesyłania strumieniowego i archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="cc464-134">Start the program when you are ready to start streaming and archiving.</span></span>
13. <span data-ttu-id="cc464-135">Opcjonalnie można przesłać do kodera na żywo sygnał o rozpoczęciu reklamy.</span><span class="sxs-lookup"><span data-stu-id="cc464-135">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="cc464-136">Reklama jest wstawiana do strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="cc464-136">The advertisement is inserted in the output stream.</span></span>
14. <span data-ttu-id="cc464-137">Zatrzymaj program w dowolnym momencie, w którym chcesz zatrzymać przesyłanie strumieniowe i archiwizowanie wydarzenia.</span><span class="sxs-lookup"><span data-stu-id="cc464-137">Stop the program whenever you want to stop streaming and archiving the event.</span></span>
15. <span data-ttu-id="cc464-138">Usuń program (opcjonalnie można również usunąć zasób).</span><span class="sxs-lookup"><span data-stu-id="cc464-138">Delete the Program (and optionally delete the asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="cc464-139">Zawartość</span><span class="sxs-lookup"><span data-stu-id="cc464-139">What you'll learn</span></span>
<span data-ttu-id="cc464-140">W tym temacie opisano sposób wykonywania różnych operacji na kanałach i programach przy użyciu zestawu SDK .NET usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="cc464-140">This topic shows you how to execute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="cc464-141">Ponieważ czas trwania wielu operacji jest długi, użyto interfejsów API platformy .NET służących do zarządzania operacjami długotrwałymi.</span><span class="sxs-lookup"><span data-stu-id="cc464-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="cc464-142">W temacie przedstawiono sposób wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cc464-142">The topic shows how to do the following:</span></span>

1. <span data-ttu-id="cc464-143">Tworzenie i uruchamianie kanału.</span><span class="sxs-lookup"><span data-stu-id="cc464-143">Create and start a channel.</span></span> <span data-ttu-id="cc464-144">Używane są interfejsy API do operacji długotrwałych.</span><span class="sxs-lookup"><span data-stu-id="cc464-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="cc464-145">Pobieranie punktu końcowego odbioru (wejścia) kanału.</span><span class="sxs-lookup"><span data-stu-id="cc464-145">Get the channels ingest (input) endpoint.</span></span> <span data-ttu-id="cc464-146">Ten punkt końcowy należy przekazać do kodera, który może wysyłać strumień na żywo o pojedynczej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="cc464-146">This endpoint should be provided to the encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="cc464-147">Pobieranie punktu końcowego podglądu.</span><span class="sxs-lookup"><span data-stu-id="cc464-147">Get the preview endpoint.</span></span> <span data-ttu-id="cc464-148">Ten punkt końcowy jest używany do podglądu strumienia.</span><span class="sxs-lookup"><span data-stu-id="cc464-148">This endpoint is used to preview your stream.</span></span>
4. <span data-ttu-id="cc464-149">Tworzenie zasobu, który będzie używany do przechowywania zawartości.</span><span class="sxs-lookup"><span data-stu-id="cc464-149">Create an asset that will be used to store your content.</span></span> <span data-ttu-id="cc464-150">Należy również skonfigurować zasady dostarczania zasobów zgodnie z tym przykładem.</span><span class="sxs-lookup"><span data-stu-id="cc464-150">The asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="cc464-151">Tworzenie programu i określanie użycia wcześniej utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="cc464-151">Create a program and specify to use the asset that was created earlier.</span></span> <span data-ttu-id="cc464-152">Uruchamianie programu.</span><span class="sxs-lookup"><span data-stu-id="cc464-152">Start the program.</span></span> <span data-ttu-id="cc464-153">Używane są interfejsy API do operacji długotrwałych.</span><span class="sxs-lookup"><span data-stu-id="cc464-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="cc464-154">Tworzenie lokalizatora dla zasobu, tak aby zawartość została opublikowana i mogła być przesłana strumieniowo do klientów.</span><span class="sxs-lookup"><span data-stu-id="cc464-154">Create a locator for the asset, so the content gets published and can be streamed to your clients.</span></span>
7. <span data-ttu-id="cc464-155">Wyświetlanie i ukrywanie plansz.</span><span class="sxs-lookup"><span data-stu-id="cc464-155">Show and hide slates.</span></span> <span data-ttu-id="cc464-156">Uruchamianie i zatrzymywanie anonsów.</span><span class="sxs-lookup"><span data-stu-id="cc464-156">Start and stop advertisements.</span></span> <span data-ttu-id="cc464-157">Używane są interfejsy API do operacji długotrwałych.</span><span class="sxs-lookup"><span data-stu-id="cc464-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="cc464-158">Czyszczenie kanału i wszystkich skojarzonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="cc464-158">Clean up your channel and all the associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc464-159">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cc464-159">Prerequisites</span></span>
<span data-ttu-id="cc464-160">Następujące elementy są wymagane do wykonania czynności przedstawionych w samouczku.</span><span class="sxs-lookup"><span data-stu-id="cc464-160">The following are required to complete the tutorial.</span></span>

* <span data-ttu-id="cc464-161">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc464-161">An Azure account.</span></span> <span data-ttu-id="cc464-162">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cc464-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cc464-163">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="cc464-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="cc464-164">Otrzymasz kredyt, który można wykorzystać do wypróbowania płatnych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="cc464-164">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="cc464-165">Nawet po wyczerpaniu kredytu możesz zachować konto i korzystać z bezpłatnych usług i funkcji platformy Azure, takich jak Web Apps w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="cc464-165">Even after the credits are used up, you can keep the account and use free Azure services and features, such as the Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="cc464-166">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="cc464-166">A Media Services account.</span></span> <span data-ttu-id="cc464-167">Aby utworzyć konto usługi Media Services, zobacz temat [Tworzenie konta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="cc464-167">To create a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="cc464-168">Visual Studio 2010 z dodatkiem SP1 (Professional, Premium, Ultimate lub Express) lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="cc464-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="cc464-169">Należy użyć zestawu .NET SDK usługi Media Services w wersji 3.2.0.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cc464-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="cc464-170">Kamera internetowa i koder, który może wysyłać strumień na żywo o pojedynczej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="cc464-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="cc464-171">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="cc464-171">Considerations</span></span>
* <span data-ttu-id="cc464-172">Obecnie maksymalny zalecany czas trwania wydarzenia na żywo wynosi 8 godzin.</span><span class="sxs-lookup"><span data-stu-id="cc464-172">Currently, the max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="cc464-173">Skontaktuj się z nami pod adresem amslived@microsoft.com, jeśli chcesz uruchomić kanał na dłużej.</span><span class="sxs-lookup"><span data-stu-id="cc464-173">Please contact amslived at Microsoft.com if you need to run a Channel for longer periods of time.</span></span>
* <span data-ttu-id="cc464-174">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="cc464-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="cc464-175">Należy używać tego samego identyfikatora zasad, jeśli zawsze są używane uprawnienia dotyczące tych samych dni lub tego samego dostępu, na przykład dla lokalizatorów przeznaczonych do długotrwałego stosowania (nieprzekazywanych zasad).</span><span class="sxs-lookup"><span data-stu-id="cc464-175">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="cc464-176">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="cc464-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="cc464-177">Pobieranie przykładu</span><span class="sxs-lookup"><span data-stu-id="cc464-177">Download sample</span></span>

<span data-ttu-id="cc464-178">Przykład opisany w tym artykule możesz pobrać [tutaj](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span><span class="sxs-lookup"><span data-stu-id="cc464-178">You can download the sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="cc464-179">Konfigurowanie środowiska deweloperskiego przy użyciu zestawu .NET SDK usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="cc464-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="cc464-180">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cc464-180">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="cc464-181">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="cc464-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
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

            // The channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use the previewEndpoint to preview and verify 
            // that the input from the encoder is actually reaching the Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of the live feed as it reaches the Channel. 
            // This can be a valuable tool to check whether your live feed is actually reaching the Channel. 
            // The thumbnail is exposed via the same end-point as the Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if the channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
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
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set to StreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on the Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order to be able to publish and stream the video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
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

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with the channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting to track ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, the operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if the operation has been completed. 
        /// If the operation succeeded, the created entity Id is returned in the out parameter.
        /// </summary> 
        /// <param name="operationId">The operation Id.</param> 
        /// <param name="channel">
        /// If the operation succeeded, 
        /// the entity Id associated with the sucessful operation is returned in the out parameter.</param>
        /// <returns>Returns false if the operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle the failure. 
                // For example, throw an exception. 
                // Use the following information in the exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="cc464-182">Następny krok</span><span class="sxs-lookup"><span data-stu-id="cc464-182">Next step</span></span>
<span data-ttu-id="cc464-183">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="cc464-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cc464-184">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="cc464-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


