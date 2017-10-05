---
title: "Pojemność Machine Learning partii wykonywania usługi zadań w wersji dedykowanej | Dokumentacja firmy Microsoft"
description: "Omówienie usług partii zadań Azure Machine Learning zadań."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="ff2a0-103">Azure usługa partia zadań dla zadania uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="ff2a0-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="ff2a0-104">Machine Learning puli partii przetwarzania zapewnia skalowalnego zarządzany przez klienta dla usługi Azure Machine Learning partii wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="ff2a0-105">Przetwarzanie wsadowe klasycznego uczenia maszynowego odbywa się w środowisku wielodostępnym ogranicza liczbę współbieżnych zadań możesz mogą przesyłać i na podstawie pierwszego w pierwszym poza są kolejkowane zadania.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="ff2a0-106">Ta niedokładność oznacza, że nie można dokładnie przewidzieć uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="ff2a0-107">Przetwarzanie wsadowe puli służy do tworzenia pul, na których można przesłać zadania wsadowe.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="ff2a0-108">Możesz kontrolować rozmiar puli, a do puli, które przesyłania zadania.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="ff2a0-109">Uruchamia zadanie BES w jego własnej przestrzeni przetwarzania przetwarzania przewidywalną wydajność i może tworzyć pule zasobów, które odpowiadają obciążenia przetwarzania, które można przesłać.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="ff2a0-110">Jak używać przetwarzania wsadowego puli</span><span class="sxs-lookup"><span data-stu-id="ff2a0-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="ff2a0-111">Przetwarzanie wsadowe puli konfiguracji nie jest obecnie dostępna za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="ff2a0-112">Aby użyć przetwarzania wsadowego puli, musisz:</span><span class="sxs-lookup"><span data-stu-id="ff2a0-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="ff2a0-113">Wywołaj CSS w celu utworzenia konta puli partii i uzyskiwanie adresu URL usługi puli i klucza autoryzacji</span><span class="sxs-lookup"><span data-stu-id="ff2a0-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="ff2a0-114">Tworzenie nowego Menedżera zasobów na podstawie usługi sieci web i plan rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="ff2a0-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="ff2a0-115">Aby utworzyć konto, wywołaj obsługi klienta firmy Microsoft i pomocy technicznej (CSS) i podaj identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="ff2a0-116">CSS będzie działać z Tobą w celu ustalenia odpowiednich pojemności dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="ff2a0-117">CSS skonfiguruje konto z maksymalną liczbę zestawów, które można utworzyć i maksymalną liczbę maszyn wirtualnych (VM), które można umieścić w każdej puli.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="ff2a0-118">Po skonfigurowaniu konta podano adres URL usługi puli i klucza autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="ff2a0-119">Po utworzeniu konta służy do wykonywania operacji zarządzania w puli na pulę partii klucz puli adres URL usługi i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![Architektura usługi puli partii.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="ff2a0-121">Pule można utworzyć przez wywołanie operacji tworzenia puli na adres URL usługi puli otrzymany od CSS.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="ff2a0-122">Podczas tworzenia puli określić usługi sieci web Machine Learning na podstawie liczby maszyn wirtualnych i adres URL swagger.json nowego Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="ff2a0-123">Ta usługa sieci web podano związek rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="ff2a0-124">Usługa puli partii używa swagger.json pulę można skojarzyć z plan rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="ff2a0-125">Można uruchamiać żadnych BES usługi sieci web, zarówno nowego Menedżera zasobów na podstawie i klasyczne, wybierz w puli.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="ff2a0-126">Można używać nowego Menedżera zasobów na podstawie usługi sieci web, ale należy pamiętać, że rozliczeń dla zadań są powiązane z plan rozliczeniowy skojarzone z tą usługą.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="ff2a0-127">Można utworzyć usługi sieci web i nowy plan rozliczeniowy specjalnie z myślą o uruchomionych puli partii zadań.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="ff2a0-128">Aby uzyskać więcej informacji na temat tworzenia usług sieci web, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="ff2a0-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="ff2a0-129">Po utworzeniu puli można przesłać zadania usługi BES, usługi sieci web przy użyciu adresu URL żądania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="ff2a0-130">Można przesłać je do puli lub przetwarzania wsadowego klasycznego.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="ff2a0-131">Aby przesłać zadanie do puli partii przetwarzania, należy dodać następujący parametr treści żądania przesłania zadania:</span><span class="sxs-lookup"><span data-stu-id="ff2a0-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="ff2a0-132">"AzureBatchPoolId": "&lt;puli identyfikator&gt;"</span><span class="sxs-lookup"><span data-stu-id="ff2a0-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="ff2a0-133">Jeśli parametr nie zostanie dodany, zadanie jest uruchamiane w środowisku procesu wsadowego klasycznego.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="ff2a0-134">Jeśli pula zawiera dostępnych zasobów, zadanie uruchamiania natychmiast.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="ff2a0-135">Pula nie ma wolnego zasobów, zadanie jest w kolejce do momentu zasób jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="ff2a0-136">Jeśli okaże się regularnie osiągnąć pojemności z pulami, czy należy zwiększenia wydajności, można wywołać CSS i pracować z przedstawicielem w celu zwiększenia przydziałami.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="ff2a0-137">Przykładowe żądanie:</span><span class="sxs-lookup"><span data-stu-id="ff2a0-137">Example Request:</span></span>

<span data-ttu-id="ff2a0-138">https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?API-Version=2.0</span><span class="sxs-lookup"><span data-stu-id="ff2a0-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="ff2a0-139">Uwagi dotyczące korzystania z przetwarzania wsadowego puli</span><span class="sxs-lookup"><span data-stu-id="ff2a0-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="ff2a0-140">Przetwarzanie wsadowe puli jest zawsze rozliczeniowy usługi i który należy skojarzyć go z Menedżera zasobów na podstawie plan rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="ff2a0-141">Rozliczenie jest przeprowadzane tylko dla liczby godzin obliczeń puli jest uruchomiony; niezależnie od liczby zadania są uruchamiane w tej puli czasu.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="ff2a0-142">Po utworzeniu puli rozliczenie jest godziny obliczeniowe poszczególnych maszyn wirtualnych w puli do czasu usunięcia puli nawet wtedy, gdy są uruchomione żadne zadania wsadowego w puli.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="ff2a0-143">Rozliczeń dla maszyn wirtualnych rozpoczyna się po zakończeniu ich inicjowania obsługi administracyjnej i zatrzymywana, gdy zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="ff2a0-144">Można użyć dowolnego z planami na [Machine Learning — cennik strony](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="ff2a0-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="ff2a0-145">Przykład rozliczeń:</span><span class="sxs-lookup"><span data-stu-id="ff2a0-145">Billing example:</span></span>

<span data-ttu-id="ff2a0-146">Jeśli z maszyn wirtualnych 2. Utwórz pulę partii i usuń go po 24 godzinach planu rozliczeniowego obciąża 48 godzin obliczeń; niezależnie od tego, ile zadania zostały uruchomione w tym okresie.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="ff2a0-147">Tworzenie puli partii z 4 maszynami wirtualnymi, usuń go po 12 godzinach planu rozliczeniowego jest również zaksięgowana 48 godzin obliczeń.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="ff2a0-148">Zaleca się, że sondowania stan zadania, aby określić, po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="ff2a0-149">Po zakończeniu operacji uruchamiania wszystkich zadań mają wywołania operacji zmiany rozmiaru puli, można ustawić liczbę maszyn wirtualnych w puli na zero.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="ff2a0-150">Jeśli krótkich puli zasobów i należy utworzyć nową pulę, na przykład rozliczyć względem innego planu rozliczeniowego, można usunąć puli zamiast tego po wszystkich zadań zakończeniu pracy.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="ff2a0-151">**Korzystanie z puli partii podczas przetwarzania**</span><span class="sxs-lookup"><span data-stu-id="ff2a0-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="ff2a0-152">**Użyj klasycznego partii podczas przetwarzania**</span><span class="sxs-lookup"><span data-stu-id="ff2a0-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="ff2a0-153">Musisz uruchomić dużej liczby zadań</span><span class="sxs-lookup"><span data-stu-id="ff2a0-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="ff2a0-154">Lub</span><span class="sxs-lookup"><span data-stu-id="ff2a0-154">Or</span></span><br/><span data-ttu-id="ff2a0-155">Musisz wiedzieć, że Twoje zadania będą uruchamiane natychmiast</span><span class="sxs-lookup"><span data-stu-id="ff2a0-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="ff2a0-156">Lub</span><span class="sxs-lookup"><span data-stu-id="ff2a0-156">Or</span></span><br/><span data-ttu-id="ff2a0-157">Należy gwarantowanej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-157">You need guaranteed throughput.</span></span> <span data-ttu-id="ff2a0-158">Na przykład trzeba uruchomić liczba zadań w określonym przedziale czasu i chcesz skalować w poziomie zasoby obliczeniowe do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="ff2a0-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="ff2a0-159">Użytkownicy korzystający z kilku zadań</span><span class="sxs-lookup"><span data-stu-id="ff2a0-159">You are running just a few jobs</span></span><br/><span data-ttu-id="ff2a0-160">I</span><span class="sxs-lookup"><span data-stu-id="ff2a0-160">And</span></span><br/> <span data-ttu-id="ff2a0-161">Nie ma potrzeby zadania, aby natychmiast uruchomić</span><span class="sxs-lookup"><span data-stu-id="ff2a0-161">You don’t need the jobs to run immediately</span></span> |
