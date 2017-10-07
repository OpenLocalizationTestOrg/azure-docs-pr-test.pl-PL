---
title: "tooencode aaaHow zasobów platformy Azure przy użyciu standardu Media Encoder Standard | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Media Encoder Standard tooencode nośnika zawartości w usłudze Azure Media Services. Przykłady kodu za pomocą interfejsu API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="aaceb-104">Jak tooencode zasobów przy użyciu standardu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="aaceb-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aaceb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="aaceb-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="aaceb-106">REST</span><span class="sxs-lookup"><span data-stu-id="aaceb-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="aaceb-107">Portal</span><span class="sxs-lookup"><span data-stu-id="aaceb-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="aaceb-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="aaceb-108">Overview</span></span>
<span data-ttu-id="aaceb-109">toodeliver wideo za pośrednictwem hello Internet, trzeba skompresować hello nośnika.</span><span class="sxs-lookup"><span data-stu-id="aaceb-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="aaceb-110">Cyfrowe pliki wideo większych i może być zbyt duży toodeliver za pośrednictwem Internetu hello, lub dla klientów urządzeń toodisplay poprawnie.</span><span class="sxs-lookup"><span data-stu-id="aaceb-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="aaceb-111">Kodowanie jest procesem hello kompresji audio i wideo, więc klienci mogą wyświetlać multimediów.</span><span class="sxs-lookup"><span data-stu-id="aaceb-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="aaceb-112">Zadania kodowania są jednym z najbardziej typowych operacji przetwarzania hello w usłudze Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="aaceb-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="aaceb-113">Utworzysz kodowania plików multimedialnych tooconvert zadań z jednego tooanother kodowania.</span><span class="sxs-lookup"><span data-stu-id="aaceb-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="aaceb-114">Podczas kodowania, można użyć hello Media Services wbudowanych kodera (Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="aaceb-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="aaceb-115">Umożliwia także kodera świadczonych przez partnera usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="aaceb-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="aaceb-116">Kodery innych firm są dostępne za pośrednictwem hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="aaceb-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="aaceb-117">Można określić szczegółów hello kodowania zadań za pomocą ciągi ustawień wstępnych zdefiniowane dla kodera lub za pomocą plików konfiguracji wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="aaceb-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="aaceb-118">typy hello toosee ustawień, które są dostępne, zobacz [ustawień wstępnych zadań dla standardu Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="aaceb-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="aaceb-119">Każde zadanie może zawierać jeden lub więcej zadań, w zależności od typu hello przetwarzania, które mają tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="aaceb-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="aaceb-120">Za pomocą interfejsu API REST hello można utworzyć zadania i ich zadania pokrewne w jeden z dwóch sposobów:</span><span class="sxs-lookup"><span data-stu-id="aaceb-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="aaceb-121">Zadania mogą być zdefiniowano w tekście za pośrednictwem właściwości nawigacji zadania hello na jednostkach zadania.</span><span class="sxs-lookup"><span data-stu-id="aaceb-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="aaceb-122">Użyj przetwarzanie wsadowe OData.</span><span class="sxs-lookup"><span data-stu-id="aaceb-122">Use OData batch processing.</span></span>

<span data-ttu-id="aaceb-123">Firma Microsoft zaleca zawsze kodowanie plików źródłowych do adaptacyjnej szybkości bitowej MP4 zestawu, a następnie wykonać konwersję hello zestaw toohello pożądany format przy użyciu [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="aaceb-124">Jeśli dane wyjściowe zawartości jest szyfrowany w magazynie, musisz skonfigurować zasady dostarczania elementu zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="aaceb-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="aaceb-125">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad dostarczania elementów zawartości](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="aaceb-126">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="aaceb-126">Considerations</span></span>

<span data-ttu-id="aaceb-127">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="aaceb-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="aaceb-128">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="aaceb-129">Przed rozpoczęciem odwołujące się do procesory multimediów, sprawdź, czy ma hello identyfikator prawidłowy nośnik procesora.</span><span class="sxs-lookup"><span data-stu-id="aaceb-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="aaceb-130">Aby uzyskać więcej informacji, zobacz [uzyskać procesory multimediów](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="aaceb-131">Połączenie usług tooMedia</span><span class="sxs-lookup"><span data-stu-id="aaceb-131">Connect tooMedia Services</span></span>

<span data-ttu-id="aaceb-132">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="aaceb-133">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="aaceb-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="aaceb-134">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="aaceb-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="aaceb-135">Utwórz zadanie z jednego zadania kodowania</span><span class="sxs-lookup"><span data-stu-id="aaceb-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="aaceb-136">Podczas pracy z hello interfejsu API REST usług Media hello następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="aaceb-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="aaceb-137">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="aaceb-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="aaceb-138">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usług Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="aaceb-139">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="aaceb-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="aaceb-140">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="aaceb-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="aaceb-141">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="aaceb-142">Gdy przy użyciu formatu JSON i określając toouse hello **__metadata** — słowo kluczowe w żądaniu hello (na przykład tooreferences obiektu połączonego), należy ustawić hello **Zaakceptuj** nagłówka zbyt[format trybu informacji pełnej JSON ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Zaakceptuj: application/json; odata = pełne.</span><span class="sxs-lookup"><span data-stu-id="aaceb-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="aaceb-143">Hello poniższy przykład przedstawia toocreate i post zadania jednego zadania konfiguracji tooencode wideo w określonej rozdzielczości i jakości.</span><span class="sxs-lookup"><span data-stu-id="aaceb-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="aaceb-144">Podczas kodowania przy użyciu Media Encoder Standard, można użyć ustawienia konfiguracji zadania określony [tutaj](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="aaceb-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="aaceb-145">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="aaceb-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="aaceb-146">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="aaceb-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="aaceb-147">Ustaw nazwę zawartości wyjściowej hello</span><span class="sxs-lookup"><span data-stu-id="aaceb-147">Set hello output asset's name</span></span>
<span data-ttu-id="aaceb-148">Witaj poniższy przykład pokazuje, jak tooset hello assetName atrybutu:</span><span class="sxs-lookup"><span data-stu-id="aaceb-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="aaceb-149">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="aaceb-149">Considerations</span></span>
* <span data-ttu-id="aaceb-150">Taskbody — właściwości należy użyć literału XML toodefine hello numer wejściowego lub wyjściowego zasobów, które są używane przez zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="aaceb-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="aaceb-151">temat zadania Hello zawiera hello definicji schematu XML dla hello XML.</span><span class="sxs-lookup"><span data-stu-id="aaceb-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="aaceb-152">W definicji taskbody — Witaj, wartość każdego wewnętrzny <inputAsset> i <outputAsset> musi być ustawiona jako JobInputAsset(value) lub JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="aaceb-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="aaceb-153">Zadanie może mieć wielu zasobów danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="aaceb-153">A task can have multiple output assets.</span></span> <span data-ttu-id="aaceb-154">Jako dane wyjściowe zadania w ramach zadania jeden JobOutputAsset(x) można można użyć tylko raz.</span><span class="sxs-lookup"><span data-stu-id="aaceb-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="aaceb-155">JobInputAsset lub JobOutputAsset można określić jako zasób wprowadzania zadania.</span><span class="sxs-lookup"><span data-stu-id="aaceb-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="aaceb-156">Zadania musi nie tworzą cyklu.</span><span class="sxs-lookup"><span data-stu-id="aaceb-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="aaceb-157">parametr wartość Hello przekazujesz tooJobInputAsset lub JobOutputAsset reprezentuje hello wartość indeksu dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="aaceb-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="aaceb-158">zasoby rzeczywiste hello są definiowane w hello InputMediaAssets i OutputMediaAssets właściwości nawigacji na powitania definicję jednostki.</span><span class="sxs-lookup"><span data-stu-id="aaceb-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="aaceb-159">Ponieważ usługi Media Services jest oparty na OData v3, hello poszczególne zasoby w hello InputMediaAssets i kolekcje właściwości nawigacji OutputMediaAssets są przywoływane przez "__metadata: identyfikator uri" pary nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="aaceb-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="aaceb-160">InputMediaAssets mapuje tooone lub więcej zasobów, które zostały utworzone w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="aaceb-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="aaceb-161">OutputMediaAssets są tworzone przez hello system.</span><span class="sxs-lookup"><span data-stu-id="aaceb-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="aaceb-162">Nie odwołujących się do istniejącego zasobu.</span><span class="sxs-lookup"><span data-stu-id="aaceb-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="aaceb-163">OutputMediaAssets może nosić przy użyciu atrybutu assetName hello.</span><span class="sxs-lookup"><span data-stu-id="aaceb-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="aaceb-164">Jeśli ten atrybut nie jest obecny, a następnie nazwę hello hello OutputMediaAsset jest niezależnie od wartości tekst wewnętrzny hello hello <outputAsset> element jest z sufiksem hello Nazwa zadania wartość lub wartość identyfikatora zadania hello (w przypadku hello, w których właściwość Name hello nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="aaceb-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="aaceb-165">Na przykład jeśli zostanie ustawiona wartość assetName zbyt "Test", a następnie hello nazwa OutputMediaAsset właściwość jest ustawiona zbyt "Sample."</span><span class="sxs-lookup"><span data-stu-id="aaceb-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="aaceb-166">Jednak jeśli nie zostały ustawione na wartość assetName, ale ustawiona nazwa zadania hello zbyt "NewJob", a następnie hello nazwa OutputMediaAsset się "_NewJob JobOutputAsset (wartość)".</span><span class="sxs-lookup"><span data-stu-id="aaceb-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="aaceb-167">Utwórz zadanie z zadaniami łańcuchowa</span><span class="sxs-lookup"><span data-stu-id="aaceb-167">Create a job with chained tasks</span></span>
<span data-ttu-id="aaceb-168">W wielu scenariuszach aplikacji deweloperzy mają toocreate szereg przetwarzania zadań.</span><span class="sxs-lookup"><span data-stu-id="aaceb-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="aaceb-169">W usłudze Media Services można utworzyć serię zadań łańcuchowych.</span><span class="sxs-lookup"><span data-stu-id="aaceb-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="aaceb-170">Każde zadanie wykonuje kroki przetwarzania różnych i używać procesorów innego nośnika.</span><span class="sxs-lookup"><span data-stu-id="aaceb-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="aaceb-171">zadania Hello łańcuchowej oddać zasobów z jednego zadania tooanother, wykonywanie liniowej sekwencji zadań na powitania zasobów.</span><span class="sxs-lookup"><span data-stu-id="aaceb-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="aaceb-172">Jednak hello zadania wykonywane w ramach zadania nie są wymagane toobe w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="aaceb-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="aaceb-173">Podczas tworzenia zadania łańcuchowa hello łańcuchowej **ITask** obiekty są tworzone w jednej **IJob** obiektu.</span><span class="sxs-lookup"><span data-stu-id="aaceb-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="aaceb-174">Obecnie istnieje limit 30 zadań dla zadania.</span><span class="sxs-lookup"><span data-stu-id="aaceb-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="aaceb-175">Jeśli potrzebujesz toochain ponad 30 zadań, należy utworzyć więcej niż jedno zadanie toocontain hello zadania.</span><span class="sxs-lookup"><span data-stu-id="aaceb-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="aaceb-176">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="aaceb-176">Considerations</span></span>
<span data-ttu-id="aaceb-177">Tworzenie łańcuchów tooenable zadań:</span><span class="sxs-lookup"><span data-stu-id="aaceb-177">tooenable task chaining:</span></span>

* <span data-ttu-id="aaceb-178">Zadanie musi mieć co najmniej dwa zadania.</span><span class="sxs-lookup"><span data-stu-id="aaceb-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="aaceb-179">Musi istnieć co najmniej jedno zadanie, którego dane wejściowe są dane wyjściowe hello inne zadanie w zadaniu hello.</span><span class="sxs-lookup"><span data-stu-id="aaceb-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="aaceb-180">Przetwarzanie wsadowe OData</span><span class="sxs-lookup"><span data-stu-id="aaceb-180">Use OData batch processing</span></span>
<span data-ttu-id="aaceb-181">Witaj poniższy przykład pokazuje, jak toouse OData partii toocreate przetwarzania zadania i zadania.</span><span class="sxs-lookup"><span data-stu-id="aaceb-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="aaceb-182">Informacje dotyczące przetwarzania wsadowego znajdują się w temacie [przetwarzanie wsadowe Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="aaceb-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="aaceb-183">Utwórz zadanie przy użyciu obiekt JobTemplate</span><span class="sxs-lookup"><span data-stu-id="aaceb-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="aaceb-184">Podczas przetwarzania wielu zasobów za pomocą zbiór typowych zadań, użyj ustawienia zadania domyślny obiekt JobTemplate toospecify hello lub tooset hello kolejność zadań.</span><span class="sxs-lookup"><span data-stu-id="aaceb-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="aaceb-185">Witaj poniższy przykład pokazuje, jak obiekt JobTemplate z TaskTemplate, który jest toocreate zdefiniowanymi w tekście.</span><span class="sxs-lookup"><span data-stu-id="aaceb-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="aaceb-186">Witaj TaskTemplate używa hello Media Encoder Standard jako hello MediaProcessor tooencode hello zawartości pliku.</span><span class="sxs-lookup"><span data-stu-id="aaceb-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="aaceb-187">Jednak inne MediaProcessors może służyć także.</span><span class="sxs-lookup"><span data-stu-id="aaceb-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="aaceb-188">W przeciwieństwie do innych jednostek usługi Media Services musi Zdefiniuj nowy identyfikator GUID dla każdego TaskTemplate i umieścić w hello taskTemplateId i właściwość identyfikatora w treści na żądanie.</span><span class="sxs-lookup"><span data-stu-id="aaceb-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="aaceb-189">Schemat identyfikacji zawartości Hello wykonaj schematu hello opisanego w zidentyfikować Azure Media Services jednostek.</span><span class="sxs-lookup"><span data-stu-id="aaceb-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="aaceb-190">Ponadto nie można zaktualizować JobTemplates.</span><span class="sxs-lookup"><span data-stu-id="aaceb-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="aaceb-191">Zamiast tego należy utworzyć nową zaktualizowanych zmian.</span><span class="sxs-lookup"><span data-stu-id="aaceb-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="aaceb-192">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="aaceb-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="aaceb-193">powitania po przykładzie pokazano, jak toocreate zadania, który odwołuje się do identyfikatora obiekt JobTemplate:</span><span class="sxs-lookup"><span data-stu-id="aaceb-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="aaceb-194">W przypadku powodzenia powitania po odpowiedzi jest zwracany:</span><span class="sxs-lookup"><span data-stu-id="aaceb-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="aaceb-195">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="aaceb-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aaceb-196">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="aaceb-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="aaceb-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aaceb-197">Next steps</span></span>
<span data-ttu-id="aaceb-198">Teraz, znając toocreate tooencode zadania usługi zasobów, zobacz temat [jak toocheck zadania postępu za pomocą usługi Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="aaceb-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="aaceb-199">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="aaceb-199">See also</span></span>
[<span data-ttu-id="aaceb-200">Pobierz procesory multimediów</span><span class="sxs-lookup"><span data-stu-id="aaceb-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
