---
title: Tworzenie funkcji platformy Azure z programem Media Services
description: "W tym temacie pokazano, jak rozpocząć tworzenie usługi Azure Functions w usłudze Media Services przy użyciu portalu Azure."
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
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a><span data-ttu-id="c4187-103">Tworzenie funkcji platformy Azure z programem Media Services</span><span class="sxs-lookup"><span data-stu-id="c4187-103">Develop Azure Functions with Media Services</span></span>

<span data-ttu-id="c4187-104">W tym temacie przedstawiono, jak rozpocząć pracę z tworzeniem usługi Azure Functions, używanego przez usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="c4187-104">This topic shows you how to get started with creating Azure Functions that use Media Services.</span></span> <span data-ttu-id="c4187-105">Funkcja Azure zdefiniowane w tym temacie monitoruje kontenera konta magazynu o nazwie **wejściowych** dla nowych plików MP4.</span><span class="sxs-lookup"><span data-stu-id="c4187-105">The Azure Function defined in this topic monitors a storage account container named **input** for new MP4 files.</span></span> <span data-ttu-id="c4187-106">Gdy plik zostanie upuszczony do kontenera magazynu, wyzwalacza obiektu blob wykona funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4187-106">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>

<span data-ttu-id="c4187-107">Jeśli chcesz Eksploruj i wdrożyć istniejącej usługi Azure Functions, używanego przez usługi Azure Media Services, zapoznaj się [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="c4187-107">If you want to explore and deploy existing Azure Functions that use Azure Media Services, check out [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span> <span data-ttu-id="c4187-108">To repozytorium zawiera przykłady, które za pomocą usługi Media Services można wyświetlić przepływów pracy związanych z wprowadzania zawartości bezpośrednio z magazynu obiektów blob, kodowanie i zapisywania zawartości z powrotem do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c4187-108">This repository contains examples that use Media Services to show workflows related to ingesting content directly from blob storage, encoding, and writing content back to blob storage.</span></span> <span data-ttu-id="c4187-109">Zawiera również przykłady monitorować powiadomienia zadania za pomocą elementów Webhook i kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="c4187-109">It also includes examples of how to monitor job notifications via WebHooks and Azure Queues.</span></span> <span data-ttu-id="c4187-110">Można również zaprojektować funkcji w oparciu o przykłady w [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c4187-110">You can also develop your Functions based on the examples in the [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) repository.</span></span> <span data-ttu-id="c4187-111">Aby wdrożyć funkcje, naciśnij klawisz **wdrażanie na platformie Azure** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c4187-111">To deploy the functions, press the **Deploy to Azure** button.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4187-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c4187-112">Prerequisites</span></span>

- <span data-ttu-id="c4187-113">Przed utworzeniem pierwszej funkcji musisz mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4187-113">Before you can create your first function, you need to have an active Azure account.</span></span> <span data-ttu-id="c4187-114">Jeśli nie masz jeszcze konta platformy Azure, [dostępne są konta bezpłatne](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c4187-114">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="c4187-115">Jeśli zamierzasz utworzyć usługi Azure Functions, wykonywać działania na Twoim koncie usługi Azure Media Services (AMS) lub nasłuchiwania zdarzeń wysłanych przez usługę Media Services, należy utworzyć konta usługi AMS zgodnie z opisem [tutaj](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="c4187-115">If you are going to create Azure Functions that perform actions on your Azure Media Services (AMS) account or listen to events sent by Media Services, you should create an AMS account, as described [here](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="c4187-116">Opis elementu [sposób użycia funkcji Azure](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4187-116">Understanding of [how to use Azure functions](../azure-functions/functions-overview.md).</span></span> <span data-ttu-id="c4187-117">Sprawdź również:</span><span class="sxs-lookup"><span data-stu-id="c4187-117">Also, review:</span></span>
    - [<span data-ttu-id="c4187-118">Środowisko Azure functions powiązania protokołu HTTP i elementu webhook</span><span class="sxs-lookup"><span data-stu-id="c4187-118">Azure functions HTTP and webhook bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
    - [<span data-ttu-id="c4187-119">Jak skonfigurować ustawienia aplikacji Azure — funkcja</span><span class="sxs-lookup"><span data-stu-id="c4187-119">How to configure Azure Function app settings</span></span>](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a><span data-ttu-id="c4187-120">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="c4187-120">Considerations</span></span>

-  <span data-ttu-id="c4187-121">Środowisko Azure Functions do uruchamiania planu zużycie ma limit czasu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="c4187-121">Azure Functions running under the Consumption plan have 5 minutes timeout limit.</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="c4187-122">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="c4187-122">Create a function app</span></span>

1. <span data-ttu-id="c4187-123">Przejdź do [witryny Azure Portal](http://portal.azure.com) i zaloguj się przy użyciu konta Azure.</span><span class="sxs-lookup"><span data-stu-id="c4187-123">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="c4187-124">Tworzenie aplikacji funkcji, zgodnie z opisem [tutaj](../azure-functions/functions-create-function-app-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c4187-124">Create a function app as described [here](../azure-functions/functions-create-function-app-portal.md).</span></span>

>[!NOTE]
> <span data-ttu-id="c4187-125">Konto magazynu, którą można określić w **StorageConnection** zmiennej środowiskowej (patrz następny krok) powinna być w tym samym regionie co aplikacja.</span><span class="sxs-lookup"><span data-stu-id="c4187-125">A storage account that you specify in the **StorageConnection** environment variable (see the next step) should be in the same region as your app.</span></span>

## <a name="configure-function-app-settings"></a><span data-ttu-id="c4187-126">Konfiguruj ustawienia aplikacji — funkcja</span><span class="sxs-lookup"><span data-stu-id="c4187-126">Configure function app settings</span></span>

<span data-ttu-id="c4187-127">Podczas tworzenia usługi Media Services funkcje, warto dodać zmiennych środowiskowych, które będą używane w całej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4187-127">When developing Media Services functions, it is handy to add environment variables that will be used throughout your functions.</span></span> <span data-ttu-id="c4187-128">Aby skonfigurować ustawienia aplikacji, kliknij łącze Konfiguruj ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4187-128">To configure app settings, click the Configure App Settings link.</span></span> <span data-ttu-id="c4187-129">Aby uzyskać więcej informacji, zobacz [sposób konfigurowania ustawień aplikacji funkcji platformy Azure](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span><span class="sxs-lookup"><span data-stu-id="c4187-129">For more information, see  [How to configure Azure Function app settings](../azure-functions/functions-how-to-use-azure-function-app-settings.md).</span></span> 

<span data-ttu-id="c4187-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c4187-130">For example:</span></span>

![Ustawienia](./media/media-services-azure-functions/media-services-azure-functions001.png)

<span data-ttu-id="c4187-132">Funkcja zdefiniowana w tym artykule przyjęto założenie, że masz następujące zmienne środowiskowe w ustawieniach aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c4187-132">The function, defined in this article, assumes you have the following environment variables in your app settings:</span></span>

<span data-ttu-id="c4187-133">**AMSAccount** : *nazwa konta usługi AMS* (np. testams)</span><span class="sxs-lookup"><span data-stu-id="c4187-133">**AMSAccount** : *AMS account name* (e.g. testams)</span></span>

<span data-ttu-id="c4187-134">**AMSKey** : *klucz konta usługi AMS* (np. IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)</span><span class="sxs-lookup"><span data-stu-id="c4187-134">**AMSKey** : *AMS account key* (e.g. IHOySnH+XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM=)</span></span>

<span data-ttu-id="c4187-135">**MediaServicesStorageAccountName** : *nazwy konta magazynu* (np. testamsstorage)</span><span class="sxs-lookup"><span data-stu-id="c4187-135">**MediaServicesStorageAccountName** : *storage account name* (e.g., testamsstorage)</span></span>

<span data-ttu-id="c4187-136">**MediaServicesStorageAccountKey** : *klucz konta magazynu* (np. xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="c4187-136">**MediaServicesStorageAccountKey** : *storage account key* (e.g., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX==)</span></span>

<span data-ttu-id="c4187-137">**StorageConnection** : *połączenia z magazynem* (np. DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey = xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX ==)</span><span class="sxs-lookup"><span data-stu-id="c4187-137">**StorageConnection** : *storage connection* (e.g., DefaultEndpointsProtocol=https;AccountName=testamsstorage;AccountKey=xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX==)</span></span>

## <a name="create-a-function"></a><span data-ttu-id="c4187-138">Tworzenie funkcji</span><span class="sxs-lookup"><span data-stu-id="c4187-138">Create a function</span></span>

<span data-ttu-id="c4187-139">Po wdrożeniu aplikacji funkcji można znaleźć wśród **usługi aplikacji** usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c4187-139">Once your function app is deployed, you can find it among **App Services** Azure Functions.</span></span>

1. <span data-ttu-id="c4187-140">Wybierz aplikację funkcji, a następnie kliknij przycisk **nową funkcję**.</span><span class="sxs-lookup"><span data-stu-id="c4187-140">Select your function app and click **New Function**.</span></span>
2. <span data-ttu-id="c4187-141">Wybierz **C#** języka i **przetwarzania danych** scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c4187-141">Choose the **C#** language and **Data Processing** scenario.</span></span>
3. <span data-ttu-id="c4187-142">Wybierz **BlobTrigger** szablonu.</span><span class="sxs-lookup"><span data-stu-id="c4187-142">Choose **BlobTrigger** template.</span></span> <span data-ttu-id="c4187-143">Ta funkcja zostanie wyzwolone przy każdym obiektu blob jest przekazywany do **wejściowych** kontenera.</span><span class="sxs-lookup"><span data-stu-id="c4187-143">This function will be triggered whenever a blob is uploaded into the **input** container.</span></span> <span data-ttu-id="c4187-144">**Wejściowych** nazwa została określona w **ścieżki**, w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="c4187-144">The **input** name is specified in the **Path**, in the next step.</span></span>

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. <span data-ttu-id="c4187-146">Po wybraniu **BlobTrigger**, niektóre formanty więcej będą wyświetlane na stronie.</span><span class="sxs-lookup"><span data-stu-id="c4187-146">Once you select **BlobTrigger**, some more controls will appear on the page.</span></span>

    ![Pliki](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. <span data-ttu-id="c4187-148">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c4187-148">Click **Create**.</span></span> 


## <a name="files"></a><span data-ttu-id="c4187-149">Pliki</span><span class="sxs-lookup"><span data-stu-id="c4187-149">Files</span></span>

<span data-ttu-id="c4187-150">Funkcja Azure jest skojarzony z plików kodu i innych plików, które zostały opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c4187-150">Your Azure function is associated with code files and other files that are described in this section.</span></span> <span data-ttu-id="c4187-151">Domyślnie funkcja jest skojarzony z **function.json** i **run.csx** plików (C#).</span><span class="sxs-lookup"><span data-stu-id="c4187-151">By default, a function is associated with **function.json** and **run.csx** (C#) files.</span></span> <span data-ttu-id="c4187-152">Należy dodać **project.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c4187-152">You will need to add a **project.json** file.</span></span> <span data-ttu-id="c4187-153">Pozostałej części tej sekcji przedstawiono definicje tych plików.</span><span class="sxs-lookup"><span data-stu-id="c4187-153">The rest of this section shows the definitions for these files.</span></span>

![Pliki](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a><span data-ttu-id="c4187-155">Function.JSON</span><span class="sxs-lookup"><span data-stu-id="c4187-155">function.json</span></span>

<span data-ttu-id="c4187-156">Plik function.json definiuje, powiązania funkcji i innych ustawień konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="c4187-156">The function.json file defines the function bindings and other configuration settings.</span></span> <span data-ttu-id="c4187-157">Środowisko uruchomieniowe korzysta z tego pliku, aby określić zdarzenia do monitorowania oraz sposób przekazywania danych do i zwracać dane z wykonywania funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4187-157">The runtime uses this file to determine the events to monitor and how to pass data into and return data from function execution.</span></span> <span data-ttu-id="c4187-158">Aby uzyskać więcej informacji, zobacz [Azure functions powiązania protokołu HTTP i webhook](../azure-functions/functions-reference.md#function-code).</span><span class="sxs-lookup"><span data-stu-id="c4187-158">For more information, see [Azure functions HTTP and webhook bindings](../azure-functions/functions-reference.md#function-code).</span></span>

>[!NOTE]
><span data-ttu-id="c4187-159">Ustaw **wyłączone** właściwości **true** aby zapobiec wykonywana przez funkcję.</span><span class="sxs-lookup"><span data-stu-id="c4187-159">Set the **disabled** property to **true** to prevent the function from being executed.</span></span> 


<span data-ttu-id="c4187-160">Oto przykład **function.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c4187-160">Here is an example of **function.json** file.</span></span>

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

### <a name="projectjson"></a><span data-ttu-id="c4187-161">Project.JSON</span><span class="sxs-lookup"><span data-stu-id="c4187-161">project.json</span></span>

<span data-ttu-id="c4187-162">Plik project.json zawiera zależności.</span><span class="sxs-lookup"><span data-stu-id="c4187-162">The project.json file contains dependencies.</span></span> <span data-ttu-id="c4187-163">Oto przykład **project.json** plik zawierający wymagane pakiety platformy .NET usługi Azure Media Services z pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="c4187-163">Here is an example of **project.json** file that includes the required .NET Azure Media Services packages from Nuget.</span></span> <span data-ttu-id="c4187-164">Należy pamiętać, że numery wersji ulegnie zmianie z najnowszymi aktualizacjami do pakietów, dlatego należy upewnić się, najnowsze wersje.</span><span class="sxs-lookup"><span data-stu-id="c4187-164">Note that the version numbers will change with latest updates to the packages, so you should confirm the most recent versions.</span></span> 

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
    
### <a name="runcsx"></a><span data-ttu-id="c4187-165">Run.csx</span><span class="sxs-lookup"><span data-stu-id="c4187-165">run.csx</span></span>

<span data-ttu-id="c4187-166">To jest kod C# dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4187-166">This is the C# code for your function.</span></span>  <span data-ttu-id="c4187-167">Funkcja zdefiniowana poniżej monitorów kontenera konta magazynu o nazwie **wejściowych** (tzn. jak określono w ścieżce) dla nowych plików MP4.</span><span class="sxs-lookup"><span data-stu-id="c4187-167">The function defined below monitors a storage account container named **input** (that is what was specified in the path) for new MP4 files.</span></span> <span data-ttu-id="c4187-168">Gdy plik zostanie upuszczony do kontenera magazynu, wyzwalacza obiektu blob wykona funkcji.</span><span class="sxs-lookup"><span data-stu-id="c4187-168">Once a file is dropped into the storage container, the blob trigger will execute the function.</span></span>
    
<span data-ttu-id="c4187-169">W przykładzie zdefiniowano w tej sekcji pokazano</span><span class="sxs-lookup"><span data-stu-id="c4187-169">The example defined in this section demonstrates</span></span> 

1. <span data-ttu-id="c4187-170">jak pozyskiwania zasób do konta usługi Media Services (przez kopiowanie obiektu blob do elementu zawartości AMS) i</span><span class="sxs-lookup"><span data-stu-id="c4187-170">how to ingest an asset into a Media Services account (by coping a blob into an AMS asset) and</span></span> 
2. <span data-ttu-id="c4187-171">w jaki sposób można przesłać zadania kodowania, która używa Media Encoder Standard "Adaptacyjne przesyłanie strumieniowe" wstępnie.</span><span class="sxs-lookup"><span data-stu-id="c4187-171">how to submit an encoding job that uses Media Encoder Standard's "Adaptive Streaming" preset .</span></span>

<span data-ttu-id="c4187-172">W tym scenariuszu rzeczywistych prawdopodobnie chcesz śledzić postęp zadania, a następnie opublikować z zakodowanym elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="c4187-172">In the real life scenario, you most likely want to track job progress and then publish your encoded asset.</span></span> <span data-ttu-id="c4187-173">Aby uzyskać więcej informacji, zobacz [elementów Webhook Azure używana do monitorowania usługi Media Services zadania powiadomienia](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="c4187-173">For more information, see [Use Azure WebHooks to monitor Media Services job notifications](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> <span data-ttu-id="c4187-174">Aby uzyskać więcej przykładów, zobacz [Media Services usługi Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span><span class="sxs-lookup"><span data-stu-id="c4187-174">For more examples, see [Media Services Azure Functions](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).</span></span>  

<span data-ttu-id="c4187-175">Po zakończeniu definiowania funkcji kliknij **Zapisz i uruchom**.</span><span class="sxs-lookup"><span data-stu-id="c4187-175">Once you are done defining your function click **Save and Run**.</span></span>

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
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
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

        // Get the destination asset container reference
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

        // Get hold of the destination blob
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
##<a name="test-your-function"></a><span data-ttu-id="c4187-176">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="c4187-176">Test your function</span></span>

<span data-ttu-id="c4187-177">Aby przetestować funkcję, należy przekazać plik MP4 do **wejściowych** kontenera konta magazynu, który określono w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="c4187-177">To test your function, you need to upload an MP4 file into the **input** container of the storage account that you specified in the connection string.</span></span>  

## <a name="next-step"></a><span data-ttu-id="c4187-178">Następny krok</span><span class="sxs-lookup"><span data-stu-id="c4187-178">Next step</span></span>

<span data-ttu-id="c4187-179">W tym momencie można przystąpić do rozpocząć tworzenie aplikacji usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="c4187-179">At this point, you are ready to start developing a Media Services application.</span></span> 
 
<span data-ttu-id="c4187-180">Bardziej szczegółowe informacje i kompletnych rozwiązań/przykłady korzystania z usługi Azure Functions i Logic Apps usłudze Azure Media Services do tworzenia przepływów pracy niestandardowe tworzenie zawartości, zobacz [Media Services .NET funkcje Integraiton przykładem w witrynie GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span><span class="sxs-lookup"><span data-stu-id="c4187-180">For more details and complete samples/solutions of using Azure Functions and Logic Apps with Azure Media Services to create custom content creation workflows, see the [Media Services .NET Functions Integraiton Sample on GitHub](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)</span></span>

<span data-ttu-id="c4187-181">Zobacz też [elementów Webhook Azure używana do monitorowania usługi Media Services zadania powiadomienia z platformą .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="c4187-181">Also, see [Use Azure WebHooks to monitor Media Services job notifications with .NET](media-services-dotnet-check-job-progress-with-webhooks.md).</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="c4187-182">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="c4187-182">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c4187-183">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="c4187-183">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

