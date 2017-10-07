---
title: "wprowadzenie do dostarczania zawartości na żądanie przy użyciu platformy .NET aaaGet | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello wdrażania aplikacji dostarczania zawartości na żądanie usłudze Azure Media Services przy użyciu platformy .NET."
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
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="a9ae8-103">Wprowadzenie do dostarczania zawartości na żądanie przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a9ae8-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="a9ae8-104">Ten samouczek przedstawia kroki wdrażania podstawowej usługi dostarczania zawartości wideo na żądanie (VoD) z aplikacją Azure Media Services (AMS) przy użyciu zestawu .NET SDK usługi Azure Media Services hello hello.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9ae8-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a9ae8-105">Prerequisites</span></span>

<span data-ttu-id="a9ae8-106">Samouczek hello toocomplete wymagane są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="a9ae8-107">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-107">An Azure account.</span></span> <span data-ttu-id="a9ae8-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a9ae8-109">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-109">A Media Services account.</span></span> <span data-ttu-id="a9ae8-110">Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="a9ae8-111">.NET Framework 4.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="a9ae8-112">Program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-112">Visual Studio.</span></span>

<span data-ttu-id="a9ae8-113">W tym samouczku opisano hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="a9ae8-114">Początek (przy użyciu portalu Azure hello) punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="a9ae8-115">Tworzenie i konfigurowanie projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="a9ae8-116">Połącz toohello konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="a9ae8-117">Ładowanie pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-117">Upload a video file.</span></span>
3. <span data-ttu-id="a9ae8-118">Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="a9ae8-119">Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresów URL.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="a9ae8-120">Odtwarzanie zawartości.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="a9ae8-121">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a9ae8-121">Overview</span></span>
<span data-ttu-id="a9ae8-122">Ten samouczek przedstawia kroki hello wdrażania aplikacji do dostarczania zawartości wideo na żądanie (VoD) przy użyciu usługi Azure Media Services (AMS) zestawu SDK dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="a9ae8-123">Samouczek Hello wprowadza hello podstawowy przepływ pracy usług Media Services i hello najczęściej obiekty i zadania programowania wymagane do tworzenia usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="a9ae8-124">Po ukończeniu hello samouczka hello będzie toostream może być lub pobrać progresywnie przykładowy plik nośnika, który przekazany, zakodowany i pobierane.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="a9ae8-125">Model AMS</span><span class="sxs-lookup"><span data-stu-id="a9ae8-125">AMS model</span></span>

<span data-ttu-id="a9ae8-126">Witaj poniższej ilustracji przedstawiono niektóre obiekty hello najczęściej używane podczas tworzenia aplikacji VoD hello Media Services OData modelu.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="a9ae8-127">Kliknij przycisk tooview obraz powitania pełny jego rozmiar.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="a9ae8-128">Możesz wyświetlić hello całego modelu [tutaj](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="a9ae8-129">Uruchom przy użyciu portalu Azure hello punkty końcowe przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="a9ae8-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="a9ae8-130">Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie plików wideo przy użyciu przesyłania strumieniowego adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="a9ae8-131">Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver adaptacyjnej szybkości bitowej MP4 zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługi Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, bez konieczności toostore wstępnie umieszczone wersje każdego z tych formatach.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="a9ae8-132">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a9ae8-133">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="a9ae8-134">toostart hello punktu końcowego przesyłania strumieniowego, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="a9ae8-135">Zaloguj się w hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a9ae8-136">W oknie Ustawienia powitania kliknij punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="a9ae8-137">Kliknij przycisk domyślny hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="a9ae8-138">zostanie wyświetlone okno Szczegóły punktu KOŃCOWEGO przesyłania STRUMIENIOWEGO domyślne Hello.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="a9ae8-139">Kliknij ikonę Start hello.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="a9ae8-140">Kliknij przycisk toosave przycisk Zapisz hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a9ae8-141">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9ae8-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="a9ae8-142">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="a9ae8-143">Utwórz nowy folder (folder może być dowolnym miejscu na dysku lokalnym) i skopiuj plik plik MP4 tooencode i strumienia, lub pobrać progresywnie.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="a9ae8-144">W tym przykładzie ścieżki "C:\VideoFiles" hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="a9ae8-145">Połącz toohello konta usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="a9ae8-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="a9ae8-146">Korzystając z usługi Media Services z platformą .NET, należy użyć hello **CloudMediaContext** klasy dla większości zadań programowania Media Services: Łączenie konta usług tooMedia; tworzenia, aktualizowania, uzyskiwanie dostępu do i usuwanie następujących hello obiekty: zasoby, pliki zasobów, zadań, zasad dostępu, lokalizatorów itp.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="a9ae8-147">Zastąp domyślną klasę Program hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="a9ae8-148">Witaj kod pokazuje, jak połączenia hello tooread wartości z pliku App.config hello i jak toocreate hello **CloudMediaContext** obiektu w kolejności tooconnect tooMedia usług.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="a9ae8-149">Aby uzyskać więcej informacji, zobacz [łączenie toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="a9ae8-150">Upewnij się, że tooupdate hello pliku nazwa i ścieżka toowhere posiadanego pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="a9ae8-151">Witaj **Main** funkcja wywołuje metody, które będą zdefiniowane dalszej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ae8-152">Możesz będą występować błędy kompilacji do momentu dodania definicje dla wszystkich funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

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
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="a9ae8-153">Tworzenie nowego elementu zawartości i przekazywanie pliku wideo</span><span class="sxs-lookup"><span data-stu-id="a9ae8-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="a9ae8-154">Za pomocą usługi Media Services można przekazać (lub pozyskać) pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="a9ae8-155">Witaj **zasobów** może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżki i napisów plików (i hello metadane dotyczące tych plików.)  Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="a9ae8-156">pliki Hello w hello zasobów są nazywane **plików zasobów**.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="a9ae8-157">Witaj **UploadFile** określonych poniżej wywołania metody **CreateFromFile** (określone w rozszerzenia zestawu .NET SDK).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="a9ae8-158">**CreateFromFile** powoduje utworzenie nowego elementu zawartości, do których hello jest przekazywany określony plik źródłowy.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="a9ae8-159">Witaj **CreateFromFile** ma metodę **AssetCreationOptions** które pozwalają określić jedną z hello następujące opcje tworzenia zasobów:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="a9ae8-160">**None** — szyfrowanie nie jest stosowane.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-160">**None** - No encryption is used.</span></span> <span data-ttu-id="a9ae8-161">Jest to wartość domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-161">This is hello default value.</span></span> <span data-ttu-id="a9ae8-162">Należy pamiętać, że w przypadku korzystania z tej opcji zawartość nie jest chroniona w trakcie przesyłania lub przechowywania w magazynie.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="a9ae8-163">Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="a9ae8-164">**StorageEncrypted** — Użyj tej opcji tooencrypt zawartości lokalnie, przy użyciu szyfrowania 256-bitowego szyfrowania AES (Advanced Standard), a następnie przekazanie jej tooAzure magazynu, w którym są przechowywane szyfrowane, gdy.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="a9ae8-165">Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="a9ae8-166">Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych z silne szyfrowanie przechowywanych na dysku.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="a9ae8-167">**CommonEncryptionProtected** — za pomocą tej opcji można przekazać zawartość, która jest już zaszyfrowana i chroniona za pomocą wspólnego szyfrowania lub technologii PlayReady DRM (np. pliki Smooth Streaming chronione za pomocą technologii PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="a9ae8-168">**EnvelopeEncryptionProtected** — ta opcja umożliwia przekazanie plików w formacie HLS zaszyfrowanych z użyciem standardu AES.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="a9ae8-169">Należy pamiętać, że pliki hello musi zostały zakodowane i zaszyfrowane przez Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="a9ae8-170">Witaj **CreateFromFile** metoda pozwala także określić wywołanie zwrotne w kolejności tooreport hello postępu przekazywania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="a9ae8-171">Poniższy przykład hello, możemy określić **Brak** hello opcji zasobów.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="a9ae8-172">Dodaj hello następujące metody toohello Program klasy.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-172">Add hello following method toohello Program class.</span></span>

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


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="a9ae8-173">Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="a9ae8-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="a9ae8-174">Po pozyskaniu elementów zawartości do usługi Media Services, nośnik, mogą zostać zakodowane, poddane transmultipleksacji, oznaczone znakiem wodnym i tak dalej, przed przekazaniem tooclients.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="a9ae8-175">Te działania są zaplanowane i uruchomienia wielu tła roli wystąpień tooensure wysokiej wydajności i dostępności.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="a9ae8-176">Te działania są nazywane zadaniami, a każde zadanie składa się z niepodzielnych zadań, które hello rzeczywistą pracę w pliku trwałego hello.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="a9ae8-177">Jak wspomniano wcześniej, podczas pracy z usługą Azure Media Services, jest jednym z najbardziej typowych scenariuszy hello dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="a9ae8-178">Usługi Media Services można dynamicznie pakietu do jednego z następujących formatów hello zestaw plików MP4 z adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="a9ae8-179">tootake korzyści z dynamicznego tworzenia pakietów, potrzebujesz tooencode lub transkoduj plik (źródłowy) mezzanine do zestawu plików MP4 lub Smooth Streaming plików.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="a9ae8-180">Witaj następującego kodu pokazuje, jak zadania toosubmit kodowania.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="a9ae8-181">Witaj zadanie zawiera jedno zadanie, które określa plik mezzanine hello tootranscode do zestawu z adaptacyjną szybkością transmisji bitów MP4s przy użyciu **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="a9ae8-182">Hello kod przesyła zadanie hello i czeka, dopóki zostanie zakończona.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="a9ae8-183">Po zakończeniu zadania hello może być możliwe toostream zawartości lub pobrać progresywnie pliki MP4, które zostały utworzone w wyniku transkodowania.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="a9ae8-184">Dodaj hello następujące metody toohello Program klasy.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-184">Add hello following method toohello Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
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

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="a9ae8-185">Publikowanie hello zawartości i uzyskiwanie adresów URL do przesyłania strumieniowego i pobierania progresywnego</span><span class="sxs-lookup"><span data-stu-id="a9ae8-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="a9ae8-186">toostream lub pobierania zawartości, należy najpierw należy zbyt opublikować, przez utworzenie lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="a9ae8-187">Lokalizatory zapewniają toofiles dostępu do zawartych w hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="a9ae8-188">Usługa Media Services obsługuje dwa typy lokalizatorów: OnDemandOrigin lokalizatory nośniki używane toostream (na przykład MPEG DASH, HLS lub Smooth Streaming) i lokalizatorów podpis dostępu (SAS) używane pliki multimedialne toodownload (Aby uzyskać więcej informacji o lokalizatory sygnatury dostępu Współdzielonego, zobacz [to](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="a9ae8-189">Informacje na temat formatów adresów URL</span><span class="sxs-lookup"><span data-stu-id="a9ae8-189">Some details about URL formats</span></span>

<span data-ttu-id="a9ae8-190">Po utworzeniu lokalizatorów hello można tworzyć adresy URL hello, które może być używane toostream lub pobierania plików.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="a9ae8-191">Przykładowe Hello w tym samouczku dane wyjściowe obejmują adresów URL, które można wkleić w odpowiednich przeglądarkach.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="a9ae8-192">W tej sekcji przedstawiono jedynie krótkie przykłady różnych formatów.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="a9ae8-193">Adres URL przesyłania strumieniowego MPEG DASH ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="a9ae8-194">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="a9ae8-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="a9ae8-195">Adres URL dla protokołu HLS ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="a9ae8-196">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="a9ae8-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="a9ae8-197">Adres URL dla protokołu Smooth Streaming ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="a9ae8-198">{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="a9ae8-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="a9ae8-199">Pliki toodownload adres URL SAS używany ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="a9ae8-200">{nazwa kontenera obiektów blob}/{nazwa elementu zawartości}/{nazwa pliku}/{sygnatura dostępu współdzielonego}</span><span class="sxs-lookup"><span data-stu-id="a9ae8-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="a9ae8-201">Rozszerzenia .NET SDK usługi Media Services zapewniają wygodne metody pomocnicze czy powrotu sformatowane adresy URL dla hello opublikowanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="a9ae8-202">Hello poniższym kodzie użyto rozszerzeń zestawu .NET SDK toocreate lokalizatory i tooget przesyłania strumieniowego i pobierania progresywnego adresów URL.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="a9ae8-203">Kod Hello przedstawiono również sposób tooa lokalny folder plików toodownload.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="a9ae8-204">Dodaj hello następujące metody toohello Program klasy.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-204">Add hello following method toohello Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
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

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="a9ae8-205">Testowanie przez odtwarzanie zawartości</span><span class="sxs-lookup"><span data-stu-id="a9ae8-205">Test by playing your content</span></span>

<span data-ttu-id="a9ae8-206">Po uruchomieniu program hello zdefiniowane w poprzedniej sekcji hello hello podobne następujące toohello będą wyświetlane w oknie konsoli hello adresów URL.</span><span class="sxs-lookup"><span data-stu-id="a9ae8-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="a9ae8-207">Adresy URL przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="a9ae8-208">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="a9ae8-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="a9ae8-209">HLS</span><span class="sxs-lookup"><span data-stu-id="a9ae8-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="a9ae8-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="a9ae8-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="a9ae8-211">Adresy URL pobierania progresywnego (audio i wideo):</span><span class="sxs-lookup"><span data-stu-id="a9ae8-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="a9ae8-212">toostream wideo, wklej adres URL w polu tekstowym adres URL hello w hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="a9ae8-213">tootest progresywnego pobierania, wklej adres URL do przeglądarki (na przykład program Internet Explorer, Chrome lub Safari).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="a9ae8-214">Aby uzyskać więcej informacji zobacz następujące tematy hello:</span><span class="sxs-lookup"><span data-stu-id="a9ae8-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="a9ae8-215">Odtwarzanie zawartości w istniejących odtwarzaczach</span><span class="sxs-lookup"><span data-stu-id="a9ae8-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="a9ae8-216">Opracowywanie aplikacji odtwarzacza wideo</span><span class="sxs-lookup"><span data-stu-id="a9ae8-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="a9ae8-217">Osadzanie plików wideo adaptacyjnego przesyłania strumieniowego MPEG-DASH w aplikacji HTML5 z implementacją DASH.js</span><span class="sxs-lookup"><span data-stu-id="a9ae8-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="a9ae8-218">Pobieranie przykładu</span><span class="sxs-lookup"><span data-stu-id="a9ae8-218">Download sample</span></span>
<span data-ttu-id="a9ae8-219">Witaj Poniższy przykładowy kod zawiera hello kod, który został utworzony w tym samouczku: [próbki](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="a9ae8-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9ae8-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9ae8-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a9ae8-221">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a9ae8-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
