---
title: "aaaDevelop funkcje Azure za pomocą usługi Media Services"
description: "W tym temacie przedstawiono sposób tworzenia funkcje platformy Azure za pomocą usługi Media Services przy użyciu toostart hello portalu Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="b40e7-103">Tworzenie funkcji platformy Azure z programem Media Services</span><span class="sxs-lookup"><span data-stu-id="b40e7-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="b40e7-104">W tym temacie pokazano, jak tooget pracę z tworzenia usługi Azure Functions, używanego przez usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="b40e7-104">This topic shows you how tooget started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="b40e7-105">Witaj funkcji platformy Azure, zdefiniowane w tym temacie monitoruje kontenera konta magazynu o nazwie **wejściowych** dla nowych plików MP4.</span><span class="sxs-lookup"><span data-stu-id="b40e7-105">hello Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="b40e7-106">Gdy plik zostanie upuszczony do kontenera magazynu hello, wyzwalacza obiektu blob hello wykona hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="b40e7-106">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>

<span data-ttu-id="b40e7-107">Jeśli chcesz tooexplore i wdrażanie istniejących funkcji platformy Azure korzystające z usługi Azure Media Services, zapoznaj się [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="b40e7-107">If you want tooexplore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="b40e7-108">To repozytorium zawiera przykłady korzystających z usługi Media Services tooshow przepływy pracy pokrewne tooingesting zawartości bezpośrednio z magazynu obiektów blob, kodowanie i zapisywania zawartości ponownie tooblob magazynu.</span><span class="sxs-lookup"><span data-stu-id="b40e7-108">This repository contains examples that use Media Services tooshow workflows related tooingesting content directly from blob storage, encoding, and writing content back tooblob storage.</span></span> <span data-ttu-id="b40e7-109">Zawiera również przykłady sposobu toomonitor zadania powiadomienia za pomocą elementów Webhook i kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="b40e7-109">It also includes examples of how toomonitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="b40e7-110">Można również zaprojektować funkcji oparte na powitania przykłady w hello [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b40e7-110">You can also develop your Functions based on hello examples in hello [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="b40e7-111">Funkcje hello toodeploy, naciśnij klawisz hello **wdrażanie tooAzure** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b40e7-111">toodeploy hello functions, press hello **Deploy tooAzure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b40e7-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b40e7-112">Prerequisites</span></span>

- <span data-ttu-id="b40e7-113">Przed utworzeniem pierwszej funkcji, należy toohave aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b40e7-113">Before you can create your first function, you need toohave an active Azure account.</span></span> <span data-ttu-id="b40e7-114">Jeśli nie masz jeszcze konta platformy Azure, [dostępne są konta bezpłatne](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b40e7-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="b40e7-115">Jeśli zamierzasz toocreate usługi Azure Functions, wykonywać działania na Twoim koncie usługi Azure Media Services (AMS) lub nasłuchiwania tooevents wysyłane przez usługę Media Services, należy utworzyć konta usługi AMS zgodnie z opisem [tutaj](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b40e7-115">If you are going toocreate Azure Functions that perform actions on your Azure Media Services (AMS) account or listen tooevents sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="b40e7-116">Opis elementu [jak toouse Azure funkcji](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b40e7-116">Understanding of [how toouse Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="b40e7-117">Sprawdź również:</span><span class="sxs-lookup"><span data-stu-id="b40e7-117">Also, review:</span></span>
    - [<span data-ttu-id="b40e7-118">Środowisko Azure functions powiązania protokołu HTTP i elementu webhook</span><span class="sxs-lookup"><span data-stu-id="b40e7-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="b40e7-119">Jak ustawienia aplikacji tooconfigure funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b40e7-119">How tooconfigure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="b40e7-120">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="b40e7-120">Considerations</span></span>

-  <span data-ttu-id="b40e7-121">Środowisko Azure Functions do uruchamiania planu zużycie hello ma limit czasu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="b40e7-121">Azure Functions running under hello Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="b40e7-122">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="b40e7-122">Create a function app</span></span>

1. <span data-ttu-id="b40e7-123">Przejdź toohello [portalu Azure](http://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b40e7-123">Go toohello [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="b40e7-124">Tworzenie aplikacji funkcji, zgodnie z opisem [tutaj](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b40e7-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="b40e7-125">Konto magazynu w hello **StorageConnection** zmiennej środowiskowej (patrz następny krok hello) musi należeć do hello tym samym regionie co aplikacja.</span><span class="sxs-lookup"><span data-stu-id="b40e7-125">A storage account that you specify in hello **StorageConnection** environment variable (see hello next step) should be in hello same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="b40e7-126">Konfiguruj ustawienia aplikacji — funkcja</span><span class="sxs-lookup"><span data-stu-id="b40e7-126">Configure function app settings</span></span>

<span data-ttu-id="b40e7-127">Podczas tworzenia usługi Media Services funkcje, jest przydatne tooadd zmiennych środowiskowych, które będą używane w całej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b40e7-127">When developing Media Services functions, it is handy tooadd environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="b40e7-128">Ustawienia aplikacji tooconfigure, kliknij łącze Konfiguruj ustawienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b40e7-128">tooconfigure app settings, click hello Configure App Settings link.</span></span> <span data-ttu-id="b40e7-129">Aby uzyskać więcej informacji, zobacz [jak ustawienia aplikacji funkcji platformy Azure tooconfigure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b40e7-129">For more information, see  [How tooconfigure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="b40e7-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b40e7-130">For example:</span></span>

![Ustawienia](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="b40e7-132">Funkcja Hello, zdefiniowana w tym artykule przyjęto założenie, że masz następujące zmienne środowiskowe w ustawieniach aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="b40e7-132">hello function, defined in this article, assumes you have hello following environment variables in your app settings:</span></span>

<span data-ttu-id="b40e7-133">**AMSAccount** : *nazwa konta usługi AMS* (np. testams)</span><span class="sxs-lookup"><span data-stu-id="b40e7-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="b40e7-134">**AMSKey** : *klucz konta usługi AMS* (np. IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="b40e7-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="b40e7-135">**MediaServicesStorageAccountName** : *nazwy konta magazynu* (np. testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="b40e7-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="b40e7-136">**MediaServicesStorageAccountKey** : *klucz konta magazynu* (np. xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="b40e7-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="b40e7-137">**StorageConnection** : *połączenia z magazynem* (np. DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="b40e7-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="b40e7-138">Tworzenie funkcji</span><span class="sxs-lookup"><span data-stu-id="b40e7-138">Create a function</span></span>

<span data-ttu-id="b40e7-139">Po wdrożeniu aplikacji funkcji można znaleźć wśród **usługi aplikacji** usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b40e7-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="b40e7-140">Wybierz aplikację funkcji, a następnie kliknij przycisk **nową funkcję**.</span><span class="sxs-lookup"><span data-stu-id="b40e7-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="b40e7-141">Wybierz hello **C#** języka i **przetwarzania danych** scenariusza.</span><span class="sxs-lookup"><span data-stu-id="b40e7-141">Choose hello **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="b40e7-142">Wybierz **BlobTrigger** szablonu.</span><span class="sxs-lookup"><span data-stu-id="b40e7-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="b40e7-143">Ta funkcja zostanie wyzwolone przy każdym obiektu blob jest przekazywany do hello **wejściowych** kontenera.</span><span class="sxs-lookup"><span data-stu-id="b40e7-143">This function will be triggered whenever a blob is uploaded into hello **input** container.</span></span> <span data-ttu-id="b40e7-144">Witaj **wejściowych** nazwa została określona w hello **ścieżki**, w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="b40e7-144">hello **input** name is specified in hello **Path**, in hello next step.</span></span>

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="b40e7-146">Po wybraniu **BlobTrigger**, niektóre formanty więcej będą wyświetlane na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="b40e7-146">Once you select **BlobTrigger**, some more controls will appear on hello page.</span></span>

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="b40e7-148">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b40e7-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="b40e7-149">Pliki</span><span class="sxs-lookup"><span data-stu-id="b40e7-149">Files</span></span>

<span data-ttu-id="b40e7-150">Funkcja Azure jest skojarzony z plików kodu i innych plików, które zostały opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b40e7-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="b40e7-151">Domyślnie funkcja jest skojarzony z **function.json** i **run.csx** plików (C#).</span><span class="sxs-lookup"><span data-stu-id="b40e7-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="b40e7-152">Konieczne będzie tooadd **project.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="b40e7-152">You will need tooadd a **project.json** file.</span></span> <span data-ttu-id="b40e7-153">Hello pozostałej części tej sekcji przedstawiono definicje hello tych plików.</span><span class="sxs-lookup"><span data-stu-id="b40e7-153">hello rest of this section shows hello definitions for these files.</span></span>

![Pliki](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="b40e7-155">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="b40e7-155">function.json</span></span>

<span data-ttu-id="b40e7-156">Plik function.json Hello definiuje powiązania funkcji hello i innych ustawień konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="b40e7-156">hello function.json file defines hello function bindings and other configuration settings.</span></span> <span data-ttu-id="b40e7-157">środowiska uruchomieniowego Hello korzysta z tego pliku toodetermine hello zdarzenia toomonitor i sposób wykonywania funkcji toopass dane i zwracanych danych z.</span><span class="sxs-lookup"><span data-stu-id="b40e7-157">hello runtime uses this file toodetermine hello events toomonitor and how toopass data into and return data from function execution.</span></span> <span data-ttu-id="b40e7-158">Aby uzyskać więcej informacji, zobacz [Azure functions powiązania protokołu HTTP i webhook](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="b40e7-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="b40e7-159">Zestaw hello **wyłączone** właściwości zbyt**true** funkcja hello tooprevent wstrzymywane.</span><span class="sxs-lookup"><span data-stu-id="b40e7-159">Set hello **disabled** property too**true** tooprevent hello function from being executed.</span></span> 


<span data-ttu-id="b40e7-160">Oto przykład **function.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="b40e7-160">Here is an example of **function.json** file.</span></span>

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a><span data-ttu-id="b40e7-161">Project.JSON</span><span class="sxs-lookup"><span data-stu-id="b40e7-161">project.json</span></span>

<span data-ttu-id="b40e7-162">Plik project.json Hello zawiera zależności.</span><span class="sxs-lookup"><span data-stu-id="b40e7-162">hello project.json file contains dependencies.</span></span> <span data-ttu-id="b40e7-163">Oto przykład **project.json** plik zawierający hello wymagane .NET Azure Media Services pakietów z pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="b40e7-163">Here is an example of **project.json** file that includes hello required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="b40e7-164">Należy pamiętać, że hello numery wersji ulegnie zmianie z najnowszymi aktualizacjami pakiety toohello, należy się upewnić, hello najnowsze wersje.</span><span class="sxs-lookup"><span data-stu-id="b40e7-164">Note that hello version numbers will change with latest updates toohello packages, so you should confirm hello most recent versions.</span></span> 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a><span data-ttu-id="b40e7-165">Run.csx</span><span class="sxs-lookup"><span data-stu-id="b40e7-165">run.csx</span></span>

<span data-ttu-id="b40e7-166">Jest to hello C# kod dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="b40e7-166">This is hello C# code for your function.</span></span>  <span data-ttu-id="b40e7-167">Funkcja Hello zdefiniowana poniżej monitorów kontenera konta magazynu o nazwie **wejściowych** (tzn. jak określono w ścieżce hello) dla nowych plików MP4.</span><span class="sxs-lookup"><span data-stu-id="b40e7-167">hello function defined below monitors a storage account container named **input** (that is what was specified in hello path) for new MP4 files.</span></span> <span data-ttu-id="b40e7-168">Gdy plik zostanie upuszczony do kontenera magazynu hello, wyzwalacza obiektu blob hello wykona hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="b40e7-168">Once a file is dropped into hello storage container, hello blob trigger will execute hello function.</span></span>
    
<span data-ttu-id="b40e7-169">przykład Witaj zdefiniowane w tej sekcji przedstawiono</span><span class="sxs-lookup"><span data-stu-id="b40e7-169">hello example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="b40e7-170">jak tooingest zasób do usługi Media Services konta (przez kopiowanie obiektu blob do elementu zawartości AMS) i</span><span class="sxs-lookup"><span data-stu-id="b40e7-170">how tooingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="b40e7-171">jak toosubmit zadania kodowania, która używa Media Encoder Standard "adaptacyjne przesyłanie strumieniowe" wstępnie.</span><span class="sxs-lookup"><span data-stu-id="b40e7-171">how toosubmit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="b40e7-172">W scenariuszu Witaj świecie rzeczywistym najprawdopodobniej mają tootrack postęp zadania, a następnie opublikuj z zakodowanym elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="b40e7-172">In hello real life scenario, you most likely want tootrack job progress and then publish your encoded asset.</span></span> <span data-ttu-id="b40e7-173">Aby uzyskać więcej informacji, zobacz [elementów Webhook Azure Użyj toomonitor Media Services zadania powiadomienia](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b40e7-173">For more information, see [Use Azure WebHooks toomonitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="b40e7-174">Aby uzyskać więcej przykładów, zobacz [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="b40e7-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="b40e7-175">Po zakończeniu definiowania funkcji kliknij **Zapisz i uruchom**.</span><span class="sxs-lookup"><span data-stu-id="b40e7-175">Once you are done defining your function click **Save and Run**.</span></span>

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get hello destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of hello destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a><span data-ttu-id="b40e7-176">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="b40e7-176">Test your function</span></span>

<span data-ttu-id="b40e7-177">tootest funkcji, należy tooupload plik MP4 do hello **wejściowych** kontenera hello konta magazynu, który określono w parametrach połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="b40e7-177">tootest your function, you need tooupload an MP4 file into hello **input** container of hello storage account that you specified in hello connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="b40e7-178">Następny krok</span><span class="sxs-lookup"><span data-stu-id="b40e7-178">Next step</span></span>

<span data-ttu-id="b40e7-179">W tym momencie wszystko jest gotowe toostart opracowanie aplikacji usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="b40e7-179">At this point, you are ready toostart developing a Media Services application.</span></span> 
 
<span data-ttu-id="b40e7-180">Aby uzyskać więcej szczegółów i kompletnych rozwiązań/przykłady korzystania z usługi Azure Functions i aplikacje logiki z przepływami pracy niestandardowe tworzenie zawartości toocreate usługi Azure Media Services, zobacz hello [Media Services .NET funkcje Integraiton przykładem w witrynie GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="b40e7-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services toocreate custom content creation workflows, see hello [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="b40e7-181">Zobacz też [elementów Webhook Azure Użyj toomonitor Media Services zadania powiadomienia z platformą .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b40e7-181">Also, see [Use Azure WebHooks toomonitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="b40e7-182">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="b40e7-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b40e7-183">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="b40e7-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

