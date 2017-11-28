---
title: "aaaDedicated pojemności Machine Learning partii wykonywania usługi zadań | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="f2257-103">Azure usługa partia zadań dla zadania uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="f2257-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="f2257-104">Machine Learning puli partii przetwarzania przewiduje hello usługi wykonywania wsadowego Azure maszyny Learning skalowalnego zarządzany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="f2257-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="f2257-105">Klasycznym przetwarzania wsadowego dla uczenia maszynowego odbywa się w środowisku wielodostępnym limity które hello liczbę współbieżnych zadań mogą przesyłać i zadania są umieszczane w kolejce na podstawie pierwszego w pierwszym poza.</span><span class="sxs-lookup"><span data-stu-id="f2257-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="f2257-106">Ta niedokładność oznacza, że nie można dokładnie przewidzieć uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="f2257-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="f2257-107">Przetwarzanie wsadowe puli umożliwia pule toocreate, na których można przesłać zadania wsadowe.</span><span class="sxs-lookup"><span data-stu-id="f2257-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="f2257-108">Możesz kontrolować rozmiar hello hello puli i przesłaniu zadania hello puli toowhich.</span><span class="sxs-lookup"><span data-stu-id="f2257-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="f2257-109">Zadania usługi BES działa w własne przetwarzania, zapewniając miejsca przetwarzania przewidywalną wydajność i pule zasobów toocreate możliwości hello, które odpowiadają obciążenie toohello przesyłania.</span><span class="sxs-lookup"><span data-stu-id="f2257-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="f2257-110">Jak toouse przetwarzania wsadowego puli</span><span class="sxs-lookup"><span data-stu-id="f2257-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="f2257-111">Przetwarzanie wsadowe puli konfiguracji nie jest obecnie dostępna za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2257-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="f2257-112">toouse puli partii przetwarzania, musi:</span><span class="sxs-lookup"><span data-stu-id="f2257-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="f2257-113">Wywołanie CSS toocreate konto puli partii i uzyskiwanie adresu URL usługi puli i klucz autoryzacji</span><span class="sxs-lookup"><span data-stu-id="f2257-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="f2257-114">Tworzenie nowego Menedżera zasobów na podstawie usługi sieci web i plan rozliczeniowy</span><span class="sxs-lookup"><span data-stu-id="f2257-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="f2257-115">toocreate Twojego konta, wywołaj obsługi klienta firmy Microsoft i pomocy technicznej (CSS) i podaj identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f2257-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="f2257-116">CSS będzie działać z możesz toodetermine hello odpowiednie pojemności dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="f2257-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="f2257-117">CSS skonfiguruje konto z hello maksymalna liczba pul można tworzyć i hello maksymalną liczbę maszyn wirtualnych (VM), które można umieścić w każdej puli.</span><span class="sxs-lookup"><span data-stu-id="f2257-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="f2257-118">Po skonfigurowaniu konta podano adres URL usługi puli i klucza autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="f2257-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="f2257-119">Po utworzeniu konta, możesz użyć hello puli adres URL usługi i autoryzacji klucza tooperform puli zarządzania operacji w Twojej puli partii.</span><span class="sxs-lookup"><span data-stu-id="f2257-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Architektura usługi puli partii.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="f2257-121">Pule można utworzyć przez wywołanie metody operacji tworzenia puli hello na adres URL usługi puli hello tego tooyou CSS, pod warunkiem.</span><span class="sxs-lookup"><span data-stu-id="f2257-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="f2257-122">Podczas tworzenia puli określić hello liczbę maszyn wirtualnych i adres URL hello swagger.json hello nowego Menedżera zasobów na podstawie usługi sieci web uczenie maszynowe.</span><span class="sxs-lookup"><span data-stu-id="f2257-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="f2257-123">Ta usługa sieci web podano tooestablish hello rozliczeń skojarzenia.</span><span class="sxs-lookup"><span data-stu-id="f2257-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="f2257-124">Hello usługi puli partii używa hello swagger.json tooassociate hello puli z plan rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="f2257-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="f2257-125">Można uruchamiać żadnych BES usługi sieci web, zarówno nowego Menedżera zasobów na podstawie i klasyczne, wybierz w puli hello.</span><span class="sxs-lookup"><span data-stu-id="f2257-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="f2257-126">Można użyć nowego Menedżera zasobów na podstawie usługi sieci web, ale należy pamiętać, że hello rozliczeń dla zadań hello są powiązane z hello plan rozliczeniowy skojarzone z tą usługą.</span><span class="sxs-lookup"><span data-stu-id="f2257-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="f2257-127">Możesz toocreate usługi sieci web i rozliczeń nowy plan specjalnie z myślą o uruchomionych puli partii zadań.</span><span class="sxs-lookup"><span data-stu-id="f2257-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="f2257-128">Aby uzyskać więcej informacji na temat tworzenia usług sieci web, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f2257-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="f2257-129">Po utworzeniu puli przesłać hello BES zadania za pomocą polecenia hello adresu URL żądania wsadowe usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="f2257-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="f2257-130">Możesz wybrać toosubmit on tooa puli lub tooclassic przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="f2257-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="f2257-131">toosubmit przetwarzania zadania tooBatch puli, Dodaj powitania po treści żądania przesłania zadania toohello parametru:</span><span class="sxs-lookup"><span data-stu-id="f2257-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="f2257-132">"AzureBatchPoolId": "&lt;puli identyfikator&gt;"</span><span class="sxs-lookup"><span data-stu-id="f2257-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="f2257-133">Jeśli nie zostanie dodany parametr hello, hello zadanie jest uruchamiane w środowisku procesu wsadowego klasycznego hello.</span><span class="sxs-lookup"><span data-stu-id="f2257-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="f2257-134">Jeśli pula hello ma dostępne zasoby, hello zadania uruchamiania natychmiast.</span><span class="sxs-lookup"><span data-stu-id="f2257-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="f2257-135">Hello pula nie ma wolnego zasobów, zadanie jest w kolejce do momentu zasób jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="f2257-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="f2257-136">Jeśli okaże się regularnie osiągnąć pojemności hello z pulami, czy należy zwiększenia wydajności, można wywołać CSS i pracować z reprezentatywny tooincrease przydziałami.</span><span class="sxs-lookup"><span data-stu-id="f2257-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="f2257-137">Przykładowe żądanie:</span><span class="sxs-lookup"><span data-stu-id="f2257-137">Example Request:</span></span>

<span data-ttu-id="f2257-138">https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?API-Version=2.0</span><span class="sxs-lookup"><span data-stu-id="f2257-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

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

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="f2257-139">Uwagi dotyczące korzystania z przetwarzania wsadowego puli</span><span class="sxs-lookup"><span data-stu-id="f2257-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="f2257-140">Przetwarzanie wsadowe puli jest zawsze włączone usługą płatną i wymaga który tooassociate go za pomocą Menedżera zasobów na podstawie plan rozliczeniowy.</span><span class="sxs-lookup"><span data-stu-id="f2257-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="f2257-141">Rozliczenie jest przeprowadzane tylko hello liczbę godzin obliczeń puli hello jest uruchomiony; niezależnie od hello liczba zadania są uruchamiane w tej puli czasu.</span><span class="sxs-lookup"><span data-stu-id="f2257-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="f2257-142">Po utworzeniu puli rozliczenie jest hello godziny obliczeń dla poszczególnych maszyn wirtualnych w puli hello aż do usunięcia puli hello, nawet jeśli w puli hello są uruchomione żadne zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="f2257-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="f2257-143">Rozliczeń dla maszyn wirtualnych hello rozpoczyna się po zakończeniu ich inicjowania obsługi administracyjnej i zatrzymywana, gdy zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="f2257-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="f2257-144">Można użyć dowolnego z planami hello na powitania [Machine Learning — cennik strony](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="f2257-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="f2257-145">Przykład rozliczeń:</span><span class="sxs-lookup"><span data-stu-id="f2257-145">Billing example:</span></span>

<span data-ttu-id="f2257-146">Jeśli z maszyn wirtualnych 2. Utwórz pulę partii i usuń go po 24 godzinach planu rozliczeniowego obciąża 48 godzin obliczeń; niezależnie od tego, ile zadania zostały uruchomione w tym okresie.</span><span class="sxs-lookup"><span data-stu-id="f2257-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="f2257-147">Tworzenie puli partii z 4 maszynami wirtualnymi, usuń go po 12 godzinach planu rozliczeniowego jest również zaksięgowana 48 godzin obliczeń.</span><span class="sxs-lookup"><span data-stu-id="f2257-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="f2257-148">Firma Microsoft zaleca sondowania toodetermine stan zadania hello, po ukończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="f2257-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="f2257-149">Po zakończeniu operacji uruchamiania wszystkich zadań ma wywoływać hello numer hello tooset operacji zmiany rozmiaru puli maszyn wirtualnych w hello toozero puli.</span><span class="sxs-lookup"><span data-stu-id="f2257-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="f2257-150">Gdy krótka puli zasobów i należy toocreate nowej puli, na przykład toobill z innego planu rozliczeniowego, można usunąć puli hello zamiast tego po wszystkich zadań zakończeniu pracy.</span><span class="sxs-lookup"><span data-stu-id="f2257-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="f2257-151">**Korzystanie z puli partii podczas przetwarzania**</span><span class="sxs-lookup"><span data-stu-id="f2257-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="f2257-152">**Użyj klasycznego partii podczas przetwarzania**</span><span class="sxs-lookup"><span data-stu-id="f2257-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="f2257-153">Należy toorun dużej liczby zadań</span><span class="sxs-lookup"><span data-stu-id="f2257-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="f2257-154">Lub</span><span class="sxs-lookup"><span data-stu-id="f2257-154">Or</span></span><br/><span data-ttu-id="f2257-155">Należy tooknow, że Twoje zadania będą uruchamiane natychmiast</span><span class="sxs-lookup"><span data-stu-id="f2257-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="f2257-156">Lub</span><span class="sxs-lookup"><span data-stu-id="f2257-156">Or</span></span><br/><span data-ttu-id="f2257-157">Należy gwarantowanej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="f2257-157">You need guaranteed throughput.</span></span> <span data-ttu-id="f2257-158">Na przykład konieczne toorun liczba zadań w określonym przedziale czasu, a chcesz tooscale limit Twojego toomeet zasoby obliczeniowe potrzeb.</span><span class="sxs-lookup"><span data-stu-id="f2257-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="f2257-159">Użytkownicy korzystający z kilku zadań</span><span class="sxs-lookup"><span data-stu-id="f2257-159">You are running just a few jobs</span></span><br/><span data-ttu-id="f2257-160">I</span><span class="sxs-lookup"><span data-stu-id="f2257-160">And</span></span><br/> <span data-ttu-id="f2257-161">Nie trzeba natychmiast hello toorun zadania</span><span class="sxs-lookup"><span data-stu-id="f2257-161">You don’t need hello jobs toorun immediately</span></span> |
