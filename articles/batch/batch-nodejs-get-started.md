---
title: "Samouczek — korzystanie z biblioteki klienta usługi Azure Batch dla środowiska Node.js | Microsoft Docs"
description: "Podstawowe pojęcia dotyczące usługi Azure Batch i tworzenie prostego rozwiązania przy użyciu języka Node.js."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: c48171d8634a651718a0775183414f463c6a468c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="70346-103">Wprowadzenie do zestawu SDK usługi Batch dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="70346-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="70346-104">.NET</span><span class="sxs-lookup"><span data-stu-id="70346-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="70346-105">Python</span><span class="sxs-lookup"><span data-stu-id="70346-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="70346-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="70346-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="70346-107">Poznaj podstawy tworzenia klienta usługi Batch w języku Node.js przy użyciu [zestawu SDK usługi Azure Batch dla środowiska Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="70346-107">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="70346-108">W tym artykule poznamy scenariusz dotyczący aplikacji usługi Batch i sposób jej konfigurowania przy użyciu klienta Node.js.</span><span class="sxs-lookup"><span data-stu-id="70346-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="70346-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="70346-109">Prerequisites</span></span>
<span data-ttu-id="70346-110">W tym artykule założono, że masz praktyczną wiedzę dotyczącą języka Node.js oraz znasz system Linux.</span><span class="sxs-lookup"><span data-stu-id="70346-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="70346-111">Przyjęto również założenie, że masz skonfigurowane konto platformy Azure z prawami dostępu do tworzenia usług Batch i Storage.</span><span class="sxs-lookup"><span data-stu-id="70346-111">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span></span>

<span data-ttu-id="70346-112">Zalecane jest przeczytanie artykułu [Azure Batch Technical Overview](batch-technical-overview.md) (Omówienie techniczne usługi Azure Batch) przed wykonaniem instrukcji opisanych w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="70346-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span></span>

## <a name="the-tutorial-scenario"></a><span data-ttu-id="70346-113">Scenariusz samouczka</span><span class="sxs-lookup"><span data-stu-id="70346-113">The tutorial scenario</span></span>
<span data-ttu-id="70346-114">Przyjrzyjmy się scenariuszowi przepływu pracy w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-114">Let us understand the batch workflow scenario.</span></span> <span data-ttu-id="70346-115">Prosty skrypt napisany w języku Python pobiera wszystkie pliki csv z kontenera usługi Azure Blob Storage i konwertuje je na format JSON.</span><span class="sxs-lookup"><span data-stu-id="70346-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span></span> <span data-ttu-id="70346-116">Aby przetwarzać wiele kontenerów kont magazynów równolegle, można wdrożyć skrypt jako zadanie w ramach usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-116">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="70346-117">Architektura usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="70346-117">Azure Batch Architecture</span></span>
<span data-ttu-id="70346-118">Poniższy diagram przedstawia, w jaki sposób można skalować skrypt języka Python za pomocą klienta usługi Azure Batch i środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="70346-118">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span></span>

![Scenariusze dotyczące usługi Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="70346-120">Klient Node.js wdraża zadanie wsadowe wraz z zadaniem podrzędnym przygotowania (szczegółowo omówionym w dalszej części artykułu) i zestawem zadań podrzędnych w zależności od liczby kontenerów na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="70346-120">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span></span> <span data-ttu-id="70346-121">Skrypty można pobrać z repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="70346-121">You can download the scripts from the github repository.</span></span>

* [<span data-ttu-id="70346-122">Klient Node.js</span><span class="sxs-lookup"><span data-stu-id="70346-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="70346-123">Przygotowanie skryptów powłoki zadań</span><span class="sxs-lookup"><span data-stu-id="70346-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="70346-124">Konwerter plików csv języka Python na format JSON</span><span class="sxs-lookup"><span data-stu-id="70346-124">Python csv to JSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="70346-125">Klient Node.js w podanym linku nie zawiera konkretnego kodu, który można wdrożyć jako aplikację funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="70346-125">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span></span> <span data-ttu-id="70346-126">Użyj następujących linków, aby zapoznać się z instrukcjami tworzenia kodu.</span><span class="sxs-lookup"><span data-stu-id="70346-126">You can refer to the following links for instructions to create one.</span></span>
> - <span data-ttu-id="70346-127">[Create function app](../azure-functions/functions-create-first-azure-function.md) (Tworzenie aplikacji funkcji)</span><span class="sxs-lookup"><span data-stu-id="70346-127">[Create function app](../azure-functions/functions-create-first-azure-function.md)</span></span>
> - <span data-ttu-id="70346-128">[Create timer trigger function](../azure-functions/functions-bindings-timer.md) (Tworzenie funkcji wyzwalanej czasomierzem)</span><span class="sxs-lookup"><span data-stu-id="70346-128">[Create timer trigger function](../azure-functions/functions-bindings-timer.md)</span></span>
>
>

## <a name="build-the-application"></a><span data-ttu-id="70346-129">Kompilowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="70346-129">Build the application</span></span>

<span data-ttu-id="70346-130">Postępuj zgodnie z instrukcjami, aby utworzyć klienta Node.js:</span><span class="sxs-lookup"><span data-stu-id="70346-130">Now, let us follow the process step by step into building the Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="70346-131">Krok 1. Instalowanie zestawu SDK usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="70346-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="70346-132">Zestaw SDK usługi Azure Batch dla środowiska Node.js można zainstalować przy użyciu polecenia npm install.</span><span class="sxs-lookup"><span data-stu-id="70346-132">You can install Azure Batch SDK for Node.js using the npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="70346-133">To polecenie instaluje najnowszą wersję zestawu Node SDK usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-133">This command installs the latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="70346-134">W aplikacji funkcji platformy Azure należy przejść do karty Ustawienia, a następnie do obszaru „Konsola Kudu”, aby uruchomić polecenia npm install.</span><span class="sxs-lookup"><span data-stu-id="70346-134">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span></span> <span data-ttu-id="70346-135">W tym przypadku celem jest zainstalowanie zestawu SDK usługi Azure Batch dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="70346-135">In this case to install Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="70346-136">Krok 2. Tworzenie konta usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="70346-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="70346-137">Konto można utworzyć zarówno za pomocą witryny [Azure Portal](batch-account-create-portal.md), jak i wiersza polecenia ([PowerShell](batch-powershell-cmdlets-get-started.md) /[Interfejs wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="70346-137">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="70346-138">Poniżej przedstawiono polecenia, które umożliwiają utworzenie konta za pomocą interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="70346-138">Following are the commands to create one through Azure CLI.</span></span>

<span data-ttu-id="70346-139">Utwórz grupę zasobów. Pomiń ten krok, jeśli masz już grupę, w której chcesz utworzyć konto usługi Azure Batch:</span><span class="sxs-lookup"><span data-stu-id="70346-139">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="70346-140">Następnie utwórz konto usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="70346-141">Każde konto usługi Batch ma odpowiadające mu klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="70346-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="70346-142">Te klucze są wymagane do tworzenia dodatkowych zasobów na koncie usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-142">These keys are needed to create further resources in Azure batch account.</span></span> <span data-ttu-id="70346-143">Dobrym rozwiązaniem dla środowiska produkcyjnego jest użycie usługi Azure Key Vault do przechowywania tych kluczy.</span><span class="sxs-lookup"><span data-stu-id="70346-143">A good practice for production environment is to use Azure Key Vault to store these keys.</span></span> <span data-ttu-id="70346-144">Następnie można utworzyć jednostkę usługi dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="70346-144">You can then create a Service principal for the application.</span></span> <span data-ttu-id="70346-145">Przy użyciu tej jednostki usługi aplikacja może utworzyć token OAuth w celu uzyskania dostępu do kluczy z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="70346-145">Using this service principal the application can create an OAuth token to access keys from the key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="70346-146">Skopiuj i zachowaj klucz, ponieważ będzie potrzebny w kolejnych krokach samouczka.</span><span class="sxs-lookup"><span data-stu-id="70346-146">Copy and store the key to be used in the subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="70346-147">Krok 3. Tworzenie klienta usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="70346-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="70346-148">Poniższy fragment kodu najpierw importuje moduł Node.js usługi Azure Batch, a następnie tworzy klienta usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-148">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="70346-149">Najpierw należy utworzyć obiekt SharedKeyCredentials za pomocą klucza konta usługi Batch skopiowanego w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="70346-149">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="70346-150">Identyfikator URI usługi Azure Batch można znaleźć na karcie Przegląd witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="70346-150">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span></span> <span data-ttu-id="70346-151">Jego format to:</span><span class="sxs-lookup"><span data-stu-id="70346-151">It is of the format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="70346-152">Przyjrzyj się zrzutowi ekranu:</span><span class="sxs-lookup"><span data-stu-id="70346-152">Refer to the screenshot:</span></span>

![Identyfikator URI usługi Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="70346-154">Krok 4. Tworzenie puli usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="70346-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="70346-155">Pula usługi Azure Batch składa się z wielu maszyn wirtualnych (znanych także jako węzły usługi Batch).</span><span class="sxs-lookup"><span data-stu-id="70346-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="70346-156">Usługa Azure Batch wdraża zadania podrzędne na tych węzłach i zarządza nimi.</span><span class="sxs-lookup"><span data-stu-id="70346-156">Azure Batch service deploys the tasks on these nodes and manages them.</span></span> <span data-ttu-id="70346-157">Dla puli można zdefiniować następujące parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="70346-157">You can define the following configuration parameters for your pool.</span></span>

* <span data-ttu-id="70346-158">Typ obrazu maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="70346-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="70346-159">Rozmiar węzłów maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="70346-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="70346-160">Liczba węzłów maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="70346-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="70346-161">Rozmiar i liczba węzłów maszyny wirtualnej w dużej mierze zależy od liczby zadań podrzędnych wykonywanych równolegle, a także od ich rodzaju.</span><span class="sxs-lookup"><span data-stu-id="70346-161">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span></span> <span data-ttu-id="70346-162">Zaleca się przeprowadzenie testów w celu określenia odpowiedniej liczby i rozmiaru węzłów.</span><span class="sxs-lookup"><span data-stu-id="70346-162">We recommend testing to determine the ideal number and size.</span></span>
>
>

<span data-ttu-id="70346-163">Poniższy fragment kodu tworzy obiekty parametru konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="70346-163">The following code snippet creates the configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating the VM configuration object with the SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting the VM size to Standard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in the pool to 4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="70346-164">Lista obrazów maszyn wirtualnych systemu Linux dostępnych dla usługi Azure Batch oraz ich identyfikatorów jednostek SKU znajduje się w sekcji [Lista obrazów maszyn wirtualnych](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="70346-164">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="70346-165">Po zdefiniowaniu konfiguracji puli można przystąpić do tworzenia puli usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-165">Once the pool configuration is defined, you can create the Azure Batch pool.</span></span> <span data-ttu-id="70346-166">Polecenie dotyczące puli w ramach usługi Batch tworzy węzły maszyny wirtualnej platformy Azure i przygotowuje je do odbierania zadań podrzędnych do wykonania.</span><span class="sxs-lookup"><span data-stu-id="70346-166">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span></span> <span data-ttu-id="70346-167">Każda pula powinna mieć unikatowy identyfikator, który będzie potrzebny w kolejnych krokach samouczka.</span><span class="sxs-lookup"><span data-stu-id="70346-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="70346-168">Poniższy fragment kodu przedstawia tworzenie puli usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-168">The following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="70346-169">Przed przesłaniem zadania do tej puli należy sprawdzić stan utworzonej puli, aby upewnić się, że jest „aktywny”.</span><span class="sxs-lookup"><span data-stu-id="70346-169">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="70346-170">Poniżej przedstawiono przykładowy obiekt wyniku zwrócony przez funkcję pool.get.</span><span class="sxs-lookup"><span data-stu-id="70346-170">Following is a sample result object returned by the pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="70346-171">Krok 4. Przesyłanie zadania usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="70346-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="70346-172">Zadanie usługi Azure Batch jest logiczną grupą podobnych zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="70346-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="70346-173">W naszym scenariuszu jest to „Konwertowanie plików csv na format JSON”.</span><span class="sxs-lookup"><span data-stu-id="70346-173">In our scenario, it is "Process csv to JSON."</span></span> <span data-ttu-id="70346-174">Każde przedstawione tutaj zadanie podrzędne może przetwarzać pliki csv zawarte we wszystkich kontenerach usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="70346-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="70346-175">Dzięki usłudze Azure Batch zadania podrzędne będą wykonywane równolegle i wdrażane w wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="70346-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="70346-176">Aby określić maksymalną liczbę zadań podrzędnych uruchamianych jednocześnie w jednym węźle, można użyć właściwości [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add).</span><span class="sxs-lookup"><span data-stu-id="70346-176">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="70346-177">Zadanie podrzędne przygotowania</span><span class="sxs-lookup"><span data-stu-id="70346-177">Preparation task</span></span>

<span data-ttu-id="70346-178">Utworzone węzły maszyny wirtualnej są pustymi węzłami systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="70346-178">The VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="70346-179">Często konieczne jest zainstalowanie zestawu programów.</span><span class="sxs-lookup"><span data-stu-id="70346-179">Often, you need to install a set of programs as prerequisites.</span></span>
<span data-ttu-id="70346-180">Zazwyczaj w przypadku węzłów systemu Linux można korzystać ze skryptu powłoki, który instaluje wstępnie wymagane oprogramowanie przed uruchomieniem jakichkolwiek zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="70346-180">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span></span> <span data-ttu-id="70346-181">Jednak może to być dowolny inny programowalny i wykonywalny skrypt.</span><span class="sxs-lookup"><span data-stu-id="70346-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="70346-182">[Skrypt powłoki](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) przedstawiony w tym przykładzie instaluje narzędzie pip języka Python oraz zestaw SDK usługi Azure Storage dla języka Python.</span><span class="sxs-lookup"><span data-stu-id="70346-182">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span></span>

<span data-ttu-id="70346-183">W celu uzyskania dostępu do skryptu można go przekazać na konto usługi Azure Storage i wygenerować identyfikator URI sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="70346-183">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span></span> <span data-ttu-id="70346-184">Proces ten można też zautomatyzować przy użyciu zestawu SDK usługi Azure Storage dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="70346-184">This process can also be automated using the Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="70346-185">Zadanie podrzędne przygotowania w ramach zadania działa tylko na węzłach tej maszyny wirtualnej, na której konkretne zadanie podrzędne musi zostać uruchomione.</span><span class="sxs-lookup"><span data-stu-id="70346-185">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span></span> <span data-ttu-id="70346-186">Jeśli chcesz zainstalować wstępnie wymagane oprogramowanie we wszystkich węzłach (niezależnie od rodzaju zadania podrzędnego, które będzie w nich uruchamiane), podczas dodawania puli użyj właściwości [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add).</span><span class="sxs-lookup"><span data-stu-id="70346-186">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="70346-187">Poniżej przedstawiono definicję zadania podrzędnego przygotowania.</span><span class="sxs-lookup"><span data-stu-id="70346-187">You can use the following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="70346-188">Zadanie podrzędne przygotowania jest określane podczas przesyłania zadania usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-188">A preparation task is specified during the submission of Azure Batch job.</span></span> <span data-ttu-id="70346-189">Poniżej przedstawiono parametry konfiguracji zadania podrzędnego przygotowania:</span><span class="sxs-lookup"><span data-stu-id="70346-189">Following are the preparation task configuration parameters:</span></span>

* <span data-ttu-id="70346-190">**D**: unikatowy identyfikator zadania podrzędnego przygotowania</span><span class="sxs-lookup"><span data-stu-id="70346-190">**ID**: A unique identifier for the preparation task</span></span>
* <span data-ttu-id="70346-191">**commandLine**: wiersz polecenia służący do wykonania wykonywalnego zadania podrzędnego</span><span class="sxs-lookup"><span data-stu-id="70346-191">**commandLine**: Command line to execute the task executable</span></span>
* <span data-ttu-id="70346-192">**resourceFiles**: tablica obiektów zawierająca szczegółowe informacje o plikach, które należy pobrać w celu uruchomienia zadania podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="70346-192">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span></span>  <span data-ttu-id="70346-193">Poniżej przedstawiono dostępne opcje</span><span class="sxs-lookup"><span data-stu-id="70346-193">Following are its options</span></span>
    - <span data-ttu-id="70346-194">blobSource: identyfikator URI sygnatury dostępu współdzielonego danego pliku</span><span class="sxs-lookup"><span data-stu-id="70346-194">blobSource: The SAS URI of the file</span></span>
    - <span data-ttu-id="70346-195">filePath: ścieżka lokalna do pobrania i zapisania pliku</span><span class="sxs-lookup"><span data-stu-id="70346-195">filePath: Local path to download and save the file</span></span>
    - <span data-ttu-id="70346-196">fileMode: dotyczy wyłącznie węzłów systemu Linux, opcja fileMode jest w formacie ósemkowym i domyślnie ma wartość 0770</span><span class="sxs-lookup"><span data-stu-id="70346-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="70346-197">**waitForSuccess**: jeśli ma wartość „true”, zadanie podrzędne nie zostanie uruchomione w razie niepowodzenia zadania podrzędnego przygotowania</span><span class="sxs-lookup"><span data-stu-id="70346-197">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span></span>
* <span data-ttu-id="70346-198">**runElevated**: jeśli do uruchomienia zadania podrzędnego konieczne są podwyższone uprawnienia, należy ustawić wartość „true”.</span><span class="sxs-lookup"><span data-stu-id="70346-198">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span></span>

<span data-ttu-id="70346-199">Poniższy fragment kodu pokazuje przykładową konfigurację skryptu zadania podrzędnego przygotowania:</span><span class="sxs-lookup"><span data-stu-id="70346-199">Following code snippet shows the preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="70346-200">Jeśli nie ma konieczności instalowania żadnego wstępnie wymaganego oprogramowania w celu uruchomienia zadań podrzędnych, można pominąć zadania podrzędne przygotowania.</span><span class="sxs-lookup"><span data-stu-id="70346-200">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span></span> <span data-ttu-id="70346-201">Następujący kod tworzy zadanie o nazwie wyświetlanej „process csv files” (konwertowanie plików csv).</span><span class="sxs-lookup"><span data-stu-id="70346-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job to the pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="70346-202">Krok 5. Przesyłanie zadań podrzędnych usługi Azure Batch do zadania</span><span class="sxs-lookup"><span data-stu-id="70346-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="70346-203">Po utworzeniu zadania konwertującego pliki csv można utworzyć dla niego zadania podrzędne.</span><span class="sxs-lookup"><span data-stu-id="70346-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="70346-204">Przy założeniu, że mamy cztery kontenery, należy utworzyć cztery zadania podrzędne, po jednym dla każdego kontenera.</span><span class="sxs-lookup"><span data-stu-id="70346-204">Assuming we have four containers, we have to create four tasks, one for each container.</span></span>

<span data-ttu-id="70346-205">[Skrypt języka Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py) przyjmuje dwa parametry:</span><span class="sxs-lookup"><span data-stu-id="70346-205">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="70346-206">nazwa kontenera: kontener magazynu, z którego pobierane są pliki</span><span class="sxs-lookup"><span data-stu-id="70346-206">container name: The Storage container to download files from</span></span>
* <span data-ttu-id="70346-207">wzorzec: opcjonalny parametr wzorca nazwy plików</span><span class="sxs-lookup"><span data-stu-id="70346-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="70346-208">Zakładamy, że mamy cztery kontenery: „con1”, „con2”, „con3” i „con4”. Następujący kod przedstawia przesyłanie zadań podrzędnych do utworzonego wcześniej zadania konwertującego pliki csv usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="70346-209">Kod dodaje wiele zadań podrzędnych do puli.</span><span class="sxs-lookup"><span data-stu-id="70346-209">The code adds multiple tasks to the pool.</span></span> <span data-ttu-id="70346-210">Poszczególne zadania podrzędne są wykonywane w węźle utworzonej puli maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="70346-210">And each of the tasks is executed on a node in the pool of VMs created.</span></span> <span data-ttu-id="70346-211">Jeśli liczba zadań podrzędnych przekracza liczbę maszyn wirtualnych w puli lub wartość właściwości maxTasksPerNode, zadania podrzędne nie będą wykonywane do momentu udostępnienia węzła.</span><span class="sxs-lookup"><span data-stu-id="70346-211">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span></span> <span data-ttu-id="70346-212">Takie ograniczenia są zapewniane przez usługę Azure Batch automatycznie.</span><span class="sxs-lookup"><span data-stu-id="70346-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="70346-213">W witrynie Azure Portal zamieszczono szczegółowe widoki stanów zadań i zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="70346-213">The portal has detailed views on the tasks and job statuses.</span></span> <span data-ttu-id="70346-214">Można również skorzystać z listy, aby poznać funkcje w ramach zestawu Azure Node SDK.</span><span class="sxs-lookup"><span data-stu-id="70346-214">You can also use the list and get functions in the Azure Node SDK.</span></span> <span data-ttu-id="70346-215">Szczegółowe informacje znajdują się w dokumentacji, do której prowadzi ten [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="70346-215">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70346-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="70346-216">Next steps</span></span>

- <span data-ttu-id="70346-217">Przejrzyj artykuł [Overview of Azure Batch features](batch-api-basics.md) (Omówienie funkcji w usłudze Azure Batch), który zalecamy użytkownikom rozpoczynającym korzystanie z tej usługi.</span><span class="sxs-lookup"><span data-stu-id="70346-217">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
- <span data-ttu-id="70346-218">Zobacz [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) (Dokumentacja języka Node.js dla usługi Batch), aby poznać interfejs API usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="70346-218">See the [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) to explore the Batch API.</span></span>

