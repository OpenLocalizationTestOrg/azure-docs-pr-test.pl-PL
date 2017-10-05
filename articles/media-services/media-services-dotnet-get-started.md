---
title: "Wprowadzenie do dostarczania zawartości na żądanie przy użyciu platformy .NET | Microsoft Docs"
description: "Ten samouczek przedstawia kroki wdrażania aplikacji do dostarczania zawartości na żądanie w usługach Azure Media Services z użyciem platformy .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="bbe1b-103">Wprowadzenie do dostarczania zawartości na żądanie przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="bbe1b-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="bbe1b-104">W tym samouczku przedstawiono kolejne kroki wdrażania podstawowej usługi do dostarczania zawartości wideo na żądanie (VoD) za pomocą aplikacji Azure Media Services (AMS) przy użyciu zestawu Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbe1b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bbe1b-105">Prerequisites</span></span>

<span data-ttu-id="bbe1b-106">Do wykonania czynności przedstawionych w tym samouczku są niezbędne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="bbe1b-107">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-107">An Azure account.</span></span> <span data-ttu-id="bbe1b-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bbe1b-109">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-109">A Media Services account.</span></span> <span data-ttu-id="bbe1b-110">Aby utworzyć konto usługi Media Services, zobacz temat [Jak utworzyć konto usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="bbe1b-111">.NET Framework 4.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="bbe1b-112">Program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-112">Visual Studio.</span></span>

<span data-ttu-id="bbe1b-113">W tym samouczku opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="bbe1b-114">Uruchamianie punktów końcowych przesyłania strumieniowego (przy użyciu witryny Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="bbe1b-115">Tworzenie i konfigurowanie projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="bbe1b-116">Nawiązywanie połączenia z kontem usług Media Services.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="bbe1b-117">Ładowanie pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-117">Upload a video file.</span></span>
3. <span data-ttu-id="bbe1b-118">Kodowanie pliku źródłowego do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="bbe1b-119">Publikowanie elementu zawartości i uzyskiwanie adresów URL na potrzeby przesyłania strumieniowego i pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="bbe1b-120">Odtwarzanie zawartości.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="bbe1b-121">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bbe1b-121">Overview</span></span>
<span data-ttu-id="bbe1b-122">Ten samouczek przedstawia kroki wdrażania aplikacji do dostarczania zawartości wideo na żądanie (VoD) przy użyciu zestawu SDK usług Azure Media Services (AMS) dla programu .NET.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="bbe1b-123">Samouczek przedstawia podstawowy przepływ pracy usług Media Services oraz najczęściej występujące obiekty i zadania programowania wymagane w celu projektowania usług Media Services.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="bbe1b-124">Po zakończeniu samouczka będziesz umieć przesłać strumieniowo lub pobrać progresywnie przykładowy plik multimedialny, który został wcześniej przekazany, zakodowany oraz pobrany.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="bbe1b-125">Model AMS</span><span class="sxs-lookup"><span data-stu-id="bbe1b-125">AMS model</span></span>

<span data-ttu-id="bbe1b-126">Na poniższym obrazie przedstawiono niektóre z najczęściej używanych obiektów podczas tworzenia aplikacji VoD w modelu Media Services OData.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="bbe1b-127">Kliknij obraz, aby go wyświetlić w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="bbe1b-128">Cały model możesz obejrzeć [tutaj](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="bbe1b-129">Uruchamianie punktów końcowych przesyłania strumieniowego przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bbe1b-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="bbe1b-130">Podczas pracy w usłudze Azure Media Services jednym z najbardziej typowych scenariuszy jest dostarczanie obrazu wideo za pośrednictwem przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="bbe1b-131">Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, która pozwala dostarczać kodowaną zawartość plików MP4 z adaptacyjną szybkością transmisji bitów w formatach przesyłania strumieniowego obsługiwanych przez usługę Media Services (MPEG DASH, HLS, Smooth Streaming) w odpowiednim czasie bez konieczności przechowywania wersji wstępnie utworzonych pakietów poszczególnych formatów przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="bbe1b-132">Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="bbe1b-133">Aby rozpocząć przesyłanie strumieniowe zawartości oraz korzystać z dynamicznego tworzenia pakietów i szyfrowania dynamicznego, punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="bbe1b-134">Aby uruchomić punkt końcowy przesyłania strumieniowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="bbe1b-135">Zaloguj się w [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bbe1b-136">W oknie Ustawienia kliknij pozycję Punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="bbe1b-137">Kliknij domyślny punkt końcowy przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="bbe1b-138">Zostanie wyświetlone okno SZCZEGÓŁY DOMYŚLNEGO PUNKTU KOŃCOWEGO PRZESYŁANIA STRUMIENIOWEGO.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="bbe1b-139">Kliknij ikonę Uruchom.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-139">Click the Start icon.</span></span>
5. <span data-ttu-id="bbe1b-140">Kliknij przycisk Zapisz, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="bbe1b-141">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbe1b-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="bbe1b-142">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="bbe1b-143">Utwórz nowy folder (może się on znajdować w dowolnym miejscu na dysku lokalnym) i skopiuj plik mp4, który ma zostać zakodowany i przesłany strumieniowo lub pobrany progresywnie.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="bbe1b-144">W tym przykładzie użyto ścieżki „C:\VideoFiles”.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="bbe1b-145">Nawiązywanie połączenia z kontem usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="bbe1b-145">Connect to the Media Services account</span></span>

<span data-ttu-id="bbe1b-146">Podczas korzystania z usługi Media Services z użyciem platformy .NET należy użyć klasy **CloudMediaContext** do większości zadań programowania usługi Media Services, takich jak nawiązywanie połączenia z kontem usługi Media Services oraz tworzenie, aktualizowanie, usuwanie i uzyskiwanie dostępu do następujących obiektów: elementów zawartości, plików elementów zawartości, zadań, zasad dostępu, lokalizatorów itp.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="bbe1b-147">Zastąp domyślną klasę Program poniższym kodem.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="bbe1b-148">Kod przedstawia sposób odczytywania wartości połączenia z pliku App.config oraz sposób tworzenia obiektu **CloudMediaContext** na potrzeby połączenia z usługą Media Services.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="bbe1b-149">Aby uzyskać więcej informacji, zobacz [nawiązywanie połączenia z interfejsem API usług Media Services](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="bbe1b-150">Pamiętaj o zaktualizowaniu nazwy pliku i ścieżki do lokalizacji pliku multimedialnego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="bbe1b-151">Funkcja **Main** wywołuje metody, które będą zdefiniowane w dalszej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="bbe1b-152">Błędy kompilacji będą się pojawiać do momentu dodania definicji dla wszystkich funkcji.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

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
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="bbe1b-153">Tworzenie nowego elementu zawartości i przekazywanie pliku wideo</span><span class="sxs-lookup"><span data-stu-id="bbe1b-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="bbe1b-154">Za pomocą usługi Media Services można przekazać (lub pozyskać) pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="bbe1b-155">Obiekt **Element zawartości** może zawierać pliki wideo, audio, obrazy, kolekcje miniatur, ścieżki tekstowe i pliki napisów (oraz metadane dotyczące tych plików).  Po przekazaniu plików zawartość jest bezpiecznie przechowywana w chmurze, na potrzeby dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="bbe1b-156">Pliki w elementach zawartości są nazywane **plikami elementów zawartości**.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="bbe1b-157">Zdefiniowana poniżej metoda **UploadFile** wywołuje metodę **CreateFromFile** (zdefiniowaną w rozszerzeniach zestawu SDK programu .NET).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="bbe1b-158">Metoda **CreateFromFile** tworzy nowy element zawartości, do którego jest przekazywany określony plik źródłowy.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="bbe1b-159">Metoda **CreateFromFile** przyjmuje opcje **AssetCreationOptions**, które pozwalają określić jedną z poniższych opcji tworzenia elementów zawartości:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="bbe1b-160">**None** — szyfrowanie nie jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-160">**None** - No encryption is used.</span></span> <span data-ttu-id="bbe1b-161">Jest to wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-161">This is the default value.</span></span> <span data-ttu-id="bbe1b-162">Należy pamiętać, że w przypadku korzystania z tej opcji zawartość nie jest chroniona w trakcie przesyłania lub przechowywania w magazynie.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="bbe1b-163">Jeśli planujesz dostarczać zawartość w formacie MP4 przy użyciu pobierania progresywnego, użyj tej opcji.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="bbe1b-164">**StorageEncrypted** — ta opcja umożliwia lokalne szyfrowanie wyczyszczonej zawartości przy użyciu szyfrowania 256-bitowego Advanced Encryption Standard (AES), a następnie przekazanie jej do usługi Azure Storage, gdzie jest przechowywana w formie zaszyfrowanej.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="bbe1b-165">Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie odszyfrowywane i umieszczane w systemie szyfrowania plików przed kodowaniem, a także opcjonalnie ponownie szyfrowane przed przesłaniem zwrotnym w formie nowego elementu zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="bbe1b-166">Pierwotnym zastosowaniem szyfrowania magazynu jest zabezpieczenie za pomocą silnego szyfrowania wysokiej jakości multimedialnych plików wejściowych przechowywanych na dysku.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="bbe1b-167">**CommonEncryptionProtected** — za pomocą tej opcji można przekazać zawartość, która jest już zaszyfrowana i chroniona za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (np. pliki Smooth Streaming chronione za pomocą technologii PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="bbe1b-168">**EnvelopeEncryptionProtected** — ta opcja umożliwia przekazanie plików w formacie HLS zaszyfrowanych z użyciem standardu AES.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="bbe1b-169">Należy pamiętać, że pliki muszą być zakodowane i zaszyfrowane za pomocą narzędzia Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="bbe1b-170">Metoda **CreateFromFile** pozwala także określić wywołanie zwrotne w celu raportowania postępu przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="bbe1b-171">W poniższym przykładzie dla opcji elementu zawartości określono wartość **None**.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="bbe1b-172">Dodaj następującą metodę do klasy Program.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-172">Add the following method to the Program class.</span></span>

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="bbe1b-173">Kodowanie pliku źródłowego do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="bbe1b-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="bbe1b-174">Po pozyskaniu elementów zawartości do usługi Media Services pliki multimedialne przed dostarczeniem do klientów mogą zostać zakodowane, poddane transmultipleksacji, oznaczone znakiem wodnym itp.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="bbe1b-175">Te działania są zaplanowane i uruchamiane w wielu wystąpieniach ról w tle, aby zapewnić wysoką wydajność oraz dostępność.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="bbe1b-176">Te działania są nazywane zadaniami, a każde zadanie składa się z niepodzielnych podzadań, które wykonują rzeczywistą pracę w pliku elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="bbe1b-177">Jak wspomniano wcześniej, podczas pracy z usługą Azure Media Services jednym z najbardziej typowych scenariuszy jest dostarczanie do klientów transmisji strumieniowej z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="bbe1b-178">Usługa Media Services, korzystając z funkcji dynamicznego tworzenia pakietów, może utworzyć pakiet zestawu plików MP4 z adaptacyjną szybkością transmisji bitów w jednym z następujących formatów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="bbe1b-179">Aby korzystać z dynamicznego tworzenia pakietów, zakoduj lub transkoduj plik (źródłowy) mezzanine do zestawu plików MP4 lub Smooth Streaming z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="bbe1b-180">Poniższy kod ilustruje sposób przesyłania zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="bbe1b-181">Zadanie zawiera jedno zadanie podrzędne, która określa transkodowanie pliku mezzanine do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów przy użyciu **standardu kodera multimediów**.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="bbe1b-182">Kod przesyła zadanie i oczekuje na ukończenie działania.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="bbe1b-183">Po zakończeniu zadania użytkownik będzie mógł przesłać strumieniowo element zawartości lub pobrać progresywnie pliki MP4, które zostały utworzone w wyniku transkodowania.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="bbe1b-184">Dodaj następującą metodę do klasy Program.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="bbe1b-185">Publikowanie elementu zawartości i uzyskiwanie adresów URL na potrzeby pobierania stopniowego oraz przesyłania progresywnego</span><span class="sxs-lookup"><span data-stu-id="bbe1b-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="bbe1b-186">Aby przesłać strumieniowo lub pobrać element zawartości, należy go najpierw opublikować, tworząc lokalizator.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="bbe1b-187">Lokalizatory zapewniają dostęp do plików znajdujących się w elemencie zawartości.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="bbe1b-188">Usługa Media Services obsługuje dwa typy lokalizatorów: lokalizatory OnDemandOrigin używane do strumieniowego przesyłania plików multimedialnych (na przykład w formacie MPEG DASH, HLS i Smooth Streaming) oraz lokalizatory sygnatury dostępu współdzielonego używane do pobierania plików multimedialnych (aby uzyskać więcej informacji o lokalizatorach sygnatury dostępu współdzielonego, zobacz [ten](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="bbe1b-189">Informacje na temat formatów adresów URL</span><span class="sxs-lookup"><span data-stu-id="bbe1b-189">Some details about URL formats</span></span>

<span data-ttu-id="bbe1b-190">Po utworzeniu lokalizatorów można tworzyć adresy URL umożliwiające przesyłanie strumieniowe lub pobieranie plików.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="bbe1b-191">Przykład w tym samouczku spowoduje utworzenie adresów URL, które można wkleić w odpowiednich przeglądarkach.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="bbe1b-192">W tej sekcji przedstawiono jedynie krótkie przykłady różnych formatów.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="bbe1b-193">Adres URL dla protokołu MPEG DASH ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="bbe1b-194">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="bbe1b-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="bbe1b-195">Adres URL dla protokołu HLS ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="bbe1b-196">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="bbe1b-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="bbe1b-197">Adres URL dla protokołu Smooth Streaming ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="bbe1b-198">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="bbe1b-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="bbe1b-199">Adres URL SAS używany do pobierania plików ma następujący format:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="bbe1b-200">{nazwa kontenera obiektów blob}/{nazwa elementu zawartości}/{nazwa pliku}/{sygnatura dostępu współdzielonego}</span><span class="sxs-lookup"><span data-stu-id="bbe1b-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="bbe1b-201">Rozszerzenia zestawu .NET SDK usługi Media Services zawierają wygodne metody pomocnicze, które zwracają sformatowane adresy URL dla opublikowanego elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="bbe1b-202">W poniższym kodzie użyto rozszerzeń zestawu .NET SDK, aby utworzyć lokalizatory i pobrać adresy URL przesyłania strumieniowego oraz pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="bbe1b-203">Kod przedstawia również sposób pobierania plików do folderu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="bbe1b-204">Dodaj następującą metodę do klasy Program.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="bbe1b-205">Testowanie przez odtwarzanie zawartości</span><span class="sxs-lookup"><span data-stu-id="bbe1b-205">Test by playing your content</span></span>

<span data-ttu-id="bbe1b-206">Po uruchomieniu programu zdefiniowanego w poprzedniej sekcji w oknie konsoli zostanie wyświetlony adres URL podobny do poniższego.</span><span class="sxs-lookup"><span data-stu-id="bbe1b-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="bbe1b-207">Adresy URL przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="bbe1b-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="bbe1b-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="bbe1b-209">HLS</span><span class="sxs-lookup"><span data-stu-id="bbe1b-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="bbe1b-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="bbe1b-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="bbe1b-211">Adresy URL pobierania progresywnego (audio i wideo):</span><span class="sxs-lookup"><span data-stu-id="bbe1b-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="bbe1b-212">Aby przesyłać strumieniowo zawartość wideo, wklej adres URL w polu tekstowym adresu URL w odtwarzaczu [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="bbe1b-213">Aby przetestować pobieranie progresywne, wklej adres URL do przeglądarki (np. Internet Explorer, Chrome lub Safari).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="bbe1b-214">Aby uzyskać więcej informacji, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="bbe1b-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="bbe1b-215">Odtwarzanie zawartości w istniejących odtwarzaczach</span><span class="sxs-lookup"><span data-stu-id="bbe1b-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="bbe1b-216">Opracowywanie aplikacji odtwarzacza wideo</span><span class="sxs-lookup"><span data-stu-id="bbe1b-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="bbe1b-217">Osadzanie plików wideo adaptacyjnego przesyłania strumieniowego MPEG-DASH w aplikacji HTML5 z implementacją DASH.js</span><span class="sxs-lookup"><span data-stu-id="bbe1b-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="bbe1b-218">Pobieranie przykładu</span><span class="sxs-lookup"><span data-stu-id="bbe1b-218">Download sample</span></span>
<span data-ttu-id="bbe1b-219">Następujący przykład kodu zawiera kod utworzony w tym samouczku: [przykład](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="bbe1b-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbe1b-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbe1b-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bbe1b-221">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="bbe1b-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
