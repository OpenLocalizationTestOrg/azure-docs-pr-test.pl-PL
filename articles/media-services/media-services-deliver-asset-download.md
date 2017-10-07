---
title: aaaDownload Media Services zasoby tooyour komputera - Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat toodownload zasoby tooyour komputera. Przykłady kodu są napisane w języku C# i używają hello SDK usługi Media Services dla platformy .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 8908a1dd-3ffb-4f18-955d-4c8e2d82fc5d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 6c6e764720caa59d8371178a2682700345f7bc57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-deliver-an-asset-by-download"></a><span data-ttu-id="48620-104">Porady: dostarczanie zasobów do pobrania</span><span class="sxs-lookup"><span data-stu-id="48620-104">How to: Deliver an Asset by Download</span></span>
<span data-ttu-id="48620-105">W tym temacie omówiono opcje do dostarczania multimediów zasoby przekazać tooMedia usług.</span><span class="sxs-lookup"><span data-stu-id="48620-105">This topic discusses options for delivering media assets uploaded tooMedia Services.</span></span> <span data-ttu-id="48620-106">W wielu scenariuszach aplikacji można dostarczać zawartości Media Services.</span><span class="sxs-lookup"><span data-stu-id="48620-106">You can deliver Media Services content in numerous application scenarios.</span></span> <span data-ttu-id="48620-107">Można pobrać zasoby media lub uzyskiwać do nich dostęp za pomocą lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="48620-107">You can download media assets, or access them by using a locator.</span></span> <span data-ttu-id="48620-108">Możesz wysłać aplikacji tooanother zawartości multimedialnej lub tooanother dostawcy zawartości.</span><span class="sxs-lookup"><span data-stu-id="48620-108">You can send media content tooanother application or tooanother content provider.</span></span> <span data-ttu-id="48620-109">Aby uzyskać lepszą wydajność i skalowalność może również udostępniać zawartość za pomocą sieci dostarczania zawartości (CDN).</span><span class="sxs-lookup"><span data-stu-id="48620-109">For improved performance and scalability, you can also deliver content by using a Content Delivery Network (CDN).</span></span>

<span data-ttu-id="48620-110">W tym przykładzie pokazano sposób toodownload nośnika zasoby z komputera lokalnego tooyour Media Services.</span><span class="sxs-lookup"><span data-stu-id="48620-110">This example shows how toodownload media assets from Media Services tooyour local computer.</span></span> <span data-ttu-id="48620-111">Witaj kod zapytania hello zadania skojarzone z kontem usługi Media Services hello według Identyfikatora zadania i uzyskuje dostęp do jego **OutputMediaAssets** kolekcji (czyli zestaw hello jeden lub więcej zasobów nośnika danych wyjściowych, który powoduje uruchomienie zadania).</span><span class="sxs-lookup"><span data-stu-id="48620-111">hello code queries hello jobs associated with hello Media Services account by job ID and accesses its **OutputMediaAssets** collection (which is hello set of one or more output media assets that results from running a job).</span></span> <span data-ttu-id="48620-112">Ten przykład przedstawia, jak toodownload dane wyjściowe nośnika, który można zastosować zasobów z zadania, ale hello tej samej metody toodownload inne zasoby.</span><span class="sxs-lookup"><span data-stu-id="48620-112">This  example shows how toodownload output media assets from a job, but you can apply hello same approach toodownload other assets.</span></span>

>[!NOTE]
><span data-ttu-id="48620-113">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="48620-113">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="48620-114">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="48620-114">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="48620-115">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="48620-115">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

    // Download hello output asset of hello specified job tooa local folder.
    static IAsset DownloadAssetToLocal( string jobId, string outputFolder)
    {
        // This method illustrates how toodownload a single asset. 
        // However, you can iterate through hello OutputAssets
        // collection, and download all assets if there are many. 

        // Get a reference toohello job. 
        IJob job = GetJob(jobId);

        // Get a reference toohello first output asset. If there were multiple 
        // output media assets you could iterate and handle each one.
        IAsset outputAsset = job.OutputMediaAssets[0];

        // Create a SAS locator toodownload hello asset
        IAccessPolicy accessPolicy = _context.AccessPolicies.Create("File Download Policy", TimeSpan.FromDays(30), AccessPermissions.Read);
        ILocator locator = _context.Locators.CreateLocator(LocatorType.Sas, outputAsset, accessPolicy);

        BlobTransferClient blobTransfer = new BlobTransferClient
        {
            NumberOfConcurrentTransfers = 20,
            ParallelTransferThreadCount = 20
        };

        var downloadTasks = new List<Task>();
        foreach (IAssetFile outputFile in outputAsset.AssetFiles)
        {
            // Use hello following event handler toocheck download progress.
            outputFile.DownloadProgressChanged += DownloadProgress;

            string localDownloadPath = Path.Combine(outputFolder, outputFile.Name);

            Console.WriteLine("File download path:  " + localDownloadPath);

            downloadTasks.Add(outputFile.DownloadAsync(Path.GetFullPath(localDownloadPath), blobTransfer, locator, CancellationToken.None));

            outputFile.DownloadProgressChanged -= DownloadProgress;
        }

        Task.WaitAll(downloadTasks.ToArray());

        return outputAsset;
    }

    static void DownloadProgress(object sender, DownloadProgressChangedEventArgs e)
    {
        Console.WriteLine(string.Format("{0} % download progress. ", e.Progress));
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="48620-116">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="48620-116">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="48620-117">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="48620-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="48620-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="48620-118">See Also</span></span>
[<span data-ttu-id="48620-119">Dostarczania transmisji strumieniowej zawartości</span><span class="sxs-lookup"><span data-stu-id="48620-119">Deliver streaming content</span></span>](media-services-deliver-streaming-content.md)

