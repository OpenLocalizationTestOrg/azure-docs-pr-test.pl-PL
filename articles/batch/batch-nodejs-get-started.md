---
title: "aaaTutorial — Biblioteka klienta użyj hello partii zadań Azure dla środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawowych pojęciach dotyczących partii zadań Azure i utworzenie rozwiązania do prostych przy użyciu środowiska Node.js."
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
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="bed61-103">Wprowadzenie do zestawu SDK usługi Batch dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="bed61-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bed61-104">.NET</span><span class="sxs-lookup"><span data-stu-id="bed61-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="bed61-105">Python</span><span class="sxs-lookup"><span data-stu-id="bed61-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="bed61-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="bed61-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="bed61-107">Dowiedz się hello podstawy tworzenia klienta przy użyciu środowiska Node.js [Azure partii Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="bed61-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="bed61-108">W tym artykule poznamy scenariusz dotyczący aplikacji usługi Batch i sposób jej konfigurowania przy użyciu klienta Node.js.</span><span class="sxs-lookup"><span data-stu-id="bed61-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bed61-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bed61-109">Prerequisites</span></span>
<span data-ttu-id="bed61-110">W tym artykule założono, że masz praktyczną wiedzę dotyczącą języka Node.js oraz znasz system Linux.</span><span class="sxs-lookup"><span data-stu-id="bed61-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="bed61-111">Przyjęto założenie, że masz konto platformy Azure Instalatorowi dostępu prawa toocreate partii i usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="bed61-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="bed61-112">Firma Microsoft zaleca odczytu [omówienie techniczne usługi partia zadań Azure](batch-technical-overview.md) przed przejściem przez hello kroki opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="bed61-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="bed61-113">Scenariusz samouczek Hello</span><span class="sxs-lookup"><span data-stu-id="bed61-113">hello tutorial scenario</span></span>
<span data-ttu-id="bed61-114">Daj nam poznać hello partii przepływ pracy scenariusza.</span><span class="sxs-lookup"><span data-stu-id="bed61-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="bed61-115">Mamy prostego skryptu napisane w języku Python, który pobiera csv wszystkie pliki z kontenera magazynu obiektów Blob platformy Azure i konwertuje je tooJSON.</span><span class="sxs-lookup"><span data-stu-id="bed61-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="bed61-116">tooprocess konta magazynu wielu kontenerów równolegle, możemy wdrożyć skryptu hello Azure wsadowym.</span><span class="sxs-lookup"><span data-stu-id="bed61-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="bed61-117">Architektura usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="bed61-117">Azure Batch Architecture</span></span>
<span data-ttu-id="bed61-118">Witaj Poniższy diagram przedstawia sposób mogą być skalowane skrypt w języku Python hello przy użyciu partii zadań Azure i klienta środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="bed61-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Scenariusze dotyczące usługi Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="bed61-120">powitania klienta node.js wdraża zadania wsadowego z przygotowanie zadania (szczegółowo omówiono później) i zestaw zadań, w zależności od hello liczba kontenerów w hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bed61-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="bed61-121">Skrypty hello można pobrać z repozytorium github hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="bed61-122">Klient Node.js</span><span class="sxs-lookup"><span data-stu-id="bed61-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="bed61-123">Przygotowanie skryptów powłoki zadań</span><span class="sxs-lookup"><span data-stu-id="bed61-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="bed61-124">Procesor tooJSON csv Python</span><span class="sxs-lookup"><span data-stu-id="bed61-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="bed61-125">powitania klienta Node.js łącza hello określony nie zawiera toobe kod wdrożony jako aplikacja funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="bed61-126">Toohello następujące linki do instrukcji toocreate, co może się odwoływać.</span><span class="sxs-lookup"><span data-stu-id="bed61-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - <span data-ttu-id="bed61-127">[Create function app](../azure-functions/functions-create-first-azure-function.md) (Tworzenie aplikacji funkcji)</span><span class="sxs-lookup"><span data-stu-id="bed61-127">[Create function app](../azure-functions/functions-create-first-azure-function.md)</span></span>
> - <span data-ttu-id="bed61-128">[Create timer trigger function](../azure-functions/functions-bindings-timer.md) (Tworzenie funkcji wyzwalanej czasomierzem)</span><span class="sxs-lookup"><span data-stu-id="bed61-128">[Create timer trigger function](../azure-functions/functions-bindings-timer.md)</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="bed61-129">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bed61-129">Build hello application</span></span>

<span data-ttu-id="bed61-130">Teraz Poinformuj nas wykonaj proces hello krok po kroku do tworzenia powitania klienta Node.js:</span><span class="sxs-lookup"><span data-stu-id="bed61-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="bed61-131">Krok 1. Instalowanie zestawu SDK usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="bed61-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="bed61-132">Należy zainstalować zestaw SDK usługi partia zadań Azure dla środowiska Node.js przy użyciu polecenia install npm hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="bed61-133">To polecenie instaluje najnowszą wersję hello węzła partii zadań azure SDK.</span><span class="sxs-lookup"><span data-stu-id="bed61-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="bed61-134">W aplikacji funkcji platformy Azure, można przejść za poleceń instalacji npm hello toorun kartę Ustawienia "Konsoli Kudu" hello Azure funkcji.</span><span class="sxs-lookup"><span data-stu-id="bed61-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="bed61-135">W tym wielkość tooinstall zestawu SDK usługi partia zadań Azure dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="bed61-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="bed61-136">Krok 2. Tworzenie konta usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="bed61-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="bed61-137">Można go utworzyć, korzystając z hello [portalu Azure](batch-account-create-portal.md) lub z wiersza polecenia ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="bed61-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="bed61-138">Poniżej przedstawiono toocreate polecenia hello, jeden za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="bed61-139">Utwórz grupę zasobów, Pomiń ten krok, jeśli masz już konto, w którym ma hello toocreate konta usługi partia zadań:</span><span class="sxs-lookup"><span data-stu-id="bed61-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="bed61-140">Następnie utwórz konto usługi Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="bed61-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="bed61-141">Każde konto usługi Batch ma odpowiadające mu klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="bed61-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="bed61-142">Klucze te są toocreate wymagane dalsze zasobów konta usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="bed61-143">Dobrym rozwiązaniem w środowisku produkcyjnym jest toostore usługi Azure Key Vault toouse tych kluczy.</span><span class="sxs-lookup"><span data-stu-id="bed61-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="bed61-144">Następnie można utworzyć usługi głównej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="bed61-145">Za pomocą tej aplikacji hello główna usługi można utworzyć kluczy token tooaccess OAuth z hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="bed61-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="bed61-146">Skopiuj i Zapisz hello toobe klucza używane w kolejnych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="bed61-147">Krok 3. Tworzenie klienta usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="bed61-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="bed61-148">Poniższy fragment kodu najpierw importuje moduł Node.js partii zadań azure hello, a następnie tworzy klienta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="bed61-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="bed61-149">Należy toofirst utworzyć obiekt SharedKeyCredentials kluczem hello partii konta kopiowane z hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="bed61-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

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

<span data-ttu-id="bed61-150">Hello identyfikator URI usługi partia zadań Azure można znaleźć na karcie Przegląd hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="bed61-151">Jest w formacie hello:</span><span class="sxs-lookup"><span data-stu-id="bed61-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="bed61-152">Można znaleźć toohello zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="bed61-152">Refer toohello screenshot:</span></span>

![Identyfikator URI usługi Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="bed61-154">Krok 4. Tworzenie puli usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="bed61-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="bed61-155">Pula usługi Azure Batch składa się z wielu maszyn wirtualnych (znanych także jako węzły usługi Batch).</span><span class="sxs-lookup"><span data-stu-id="bed61-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="bed61-156">Usługa partia zadań Azure wdraża hello zadania na tych węzłach i zarządza nimi.</span><span class="sxs-lookup"><span data-stu-id="bed61-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="bed61-157">Można określić następujące parametry konfiguracji pulę hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="bed61-158">Typ obrazu maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bed61-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="bed61-159">Rozmiar węzłów maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bed61-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="bed61-160">Liczba węzłów maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bed61-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="bed61-161">Hello rozmiaru i liczby węzłów maszyny wirtualnej dużej mierze zależą hello liczba zadań, które mają toorun w równoległej, a także samo zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="bed61-162">Zaleca się testowanie toodetermine hello idealne liczby i rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="bed61-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="bed61-163">Witaj poniższy fragment kodu tworzy hello obiektów parametru konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bed61-163">hello following code snippet creates hello configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="bed61-164">Aby hello listę dostępnych dla partii zadań Azure i ich identyfikatorów jednostki SKU obrazów maszyny Wirtualnej systemu Linux, zobacz [listy obrazów maszyny wirtualnej](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="bed61-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="bed61-165">Konfiguracja puli hello jest zdefiniowany, można tworzyć hello puli partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="bed61-166">Hello polecenia puli partii tworzy węzły maszyny wirtualnej platformy Azure i przygotować je toobe tooreceive gotowe zadania tooexecute.</span><span class="sxs-lookup"><span data-stu-id="bed61-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="bed61-167">Każda pula powinna mieć unikatowy identyfikator, który będzie potrzebny w kolejnych krokach samouczka.</span><span class="sxs-lookup"><span data-stu-id="bed61-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="bed61-168">Witaj następującego fragmentu kodu tworzy puli partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="bed61-169">Możesz sprawdzić stan powitania po utworzeniu puli hello i sprawdź, czy stan hello jest "active" przed przejściem dalej z przesyłaniem puli toothat zadania.</span><span class="sxs-lookup"><span data-stu-id="bed61-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

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

<span data-ttu-id="bed61-170">Poniżej znajduje się obiekt wyniku próbki zwracane przez funkcję pool.get hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-170">Following is a sample result object returned by hello pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="bed61-171">Krok 4. Przesyłanie zadania usługi Azure Batch</span><span class="sxs-lookup"><span data-stu-id="bed61-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="bed61-172">Zadanie usługi Azure Batch jest logiczną grupą podobnych zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="bed61-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="bed61-173">W naszym scenariuszu jest "Proces tooJSON csv".</span><span class="sxs-lookup"><span data-stu-id="bed61-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="bed61-174">Każde przedstawione tutaj zadanie podrzędne może przetwarzać pliki csv zawarte we wszystkich kontenerach usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="bed61-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="bed61-175">Te zadania będą uruchamiane równolegle i wdrażane na wielu węzłach zorkiestrowana przez usługi partia zadań Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bed61-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="bed61-176">Można użyć hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) właściwości toospecify maksymalna liczba zadań, które można uruchomić jednocześnie w jednym węźle.</span><span class="sxs-lookup"><span data-stu-id="bed61-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="bed61-177">Zadanie podrzędne przygotowania</span><span class="sxs-lookup"><span data-stu-id="bed61-177">Preparation task</span></span>

<span data-ttu-id="bed61-178">węzły maszyny Wirtualnej Hello tworzone są puste Ubuntu węzłów.</span><span class="sxs-lookup"><span data-stu-id="bed61-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="bed61-179">Często konieczne tooinstall zestaw programów jako warunki wstępne.</span><span class="sxs-lookup"><span data-stu-id="bed61-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="bed61-180">Zazwyczaj dla systemu Linux węzłów może mieć skrypt powłoki, który instaluje hello wymagania wstępne, przed hello zadania rzeczywistego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="bed61-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="bed61-181">Jednak może to być dowolny inny programowalny i wykonywalny skrypt.</span><span class="sxs-lookup"><span data-stu-id="bed61-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="bed61-182">Witaj [skryptu powłoki](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) w tym przykładzie instaluje narzędzie pip Python i hello zestawu SDK usługi Magazyn Azure dla języka Python.</span><span class="sxs-lookup"><span data-stu-id="bed61-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="bed61-183">Możesz przekazać skrypt hello na konto magazynu Azure i generowania skryptu hello tooaccess identyfikatora URI połączenia SAS.</span><span class="sxs-lookup"><span data-stu-id="bed61-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="bed61-184">Ten proces można również zautomatyzować, używając hello zestawu Node.js SDK usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="bed61-185">Zadanie przygotowanie zadania działa tylko na powitania węzłach maszyny Wirtualnej, których hello konkretne zadanie wymaga toorun.</span><span class="sxs-lookup"><span data-stu-id="bed61-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="bed61-186">Jeśli chcesz toobe wymagania wstępne zainstalowane we wszystkich węzłach, niezależnie od zadania hello, które będą uruchamiane w nim, można użyć hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) właściwości podczas dodawania puli.</span><span class="sxs-lookup"><span data-stu-id="bed61-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="bed61-187">Możesz użyć powitania po definicji zadania przygotowanie odwołania.</span><span class="sxs-lookup"><span data-stu-id="bed61-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="bed61-188">Przygotowanie zadania jest określana podczas przesyłania hello zadania partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="bed61-189">Poniżej są hello parametry konfiguracji zadania przygotowania:</span><span class="sxs-lookup"><span data-stu-id="bed61-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="bed61-190">**Identyfikator**: Unikatowy identyfikator hello przygotowanie zadania</span><span class="sxs-lookup"><span data-stu-id="bed61-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="bed61-191">**commandLine**: plik wykonywalny zadania hello tooexecute wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bed61-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="bed61-192">**resourceFiles**: Tablica obiektów zawierających szczegóły dotyczące plików potrzebne toobe pobierane dla toorun tego zadania.</span><span class="sxs-lookup"><span data-stu-id="bed61-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="bed61-193">Poniżej przedstawiono dostępne opcje</span><span class="sxs-lookup"><span data-stu-id="bed61-193">Following are its options</span></span>
    - <span data-ttu-id="bed61-194">blobSource: hello identyfikatora URI połączenia SAS hello pliku</span><span class="sxs-lookup"><span data-stu-id="bed61-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="bed61-195">Ścieżka pliku: toodownload ścieżka lokalna i Zapisz plik hello</span><span class="sxs-lookup"><span data-stu-id="bed61-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="bed61-196">fileMode: dotyczy wyłącznie węzłów systemu Linux, opcja fileMode jest w formacie ósemkowym i domyślnie ma wartość 0770</span><span class="sxs-lookup"><span data-stu-id="bed61-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="bed61-197">**waitForSuccess**: zestaw tootrue, hello zadanie nie zostanie uruchomione na przygotowanie niepowodzeń zadań</span><span class="sxs-lookup"><span data-stu-id="bed61-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="bed61-198">**runElevated**: ustaw ją tootrue, jeśli zadanie hello toorun wymagane są podniesione uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="bed61-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="bed61-199">Poniższy fragment kodu przedstawia hello przygotowanie zadania skryptu konfiguracji próbki:</span><span class="sxs-lookup"><span data-stu-id="bed61-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="bed61-200">Jeśli nie ma żadnych toobe wymagania wstępne zainstalowane dla Twojego toorun zadań, możesz pominąć hello przygotowanie zadania.</span><span class="sxs-lookup"><span data-stu-id="bed61-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="bed61-201">Następujący kod tworzy zadanie o nazwie wyświetlanej „process csv files” (konwertowanie plików csv).</span><span class="sxs-lookup"><span data-stu-id="bed61-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="bed61-202">Krok 5. Przesyłanie zadań podrzędnych usługi Azure Batch do zadania</span><span class="sxs-lookup"><span data-stu-id="bed61-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="bed61-203">Po utworzeniu zadania konwertującego pliki csv można utworzyć dla niego zadania podrzędne.</span><span class="sxs-lookup"><span data-stu-id="bed61-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="bed61-204">Zakładając, że mamy cztery kontenery, będziemy mieć cztery zadania toocreate, po jednej dla każdego kontenera.</span><span class="sxs-lookup"><span data-stu-id="bed61-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="bed61-205">Jeśli przyjrzymy się hello [skrypt w języku Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), przyjmuje dwa parametry:</span><span class="sxs-lookup"><span data-stu-id="bed61-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="bed61-206">Nazwa kontenera: hello pliki toodownload kontenera magazynu z</span><span class="sxs-lookup"><span data-stu-id="bed61-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="bed61-207">wzorzec: opcjonalny parametr wzorca nazwy plików</span><span class="sxs-lookup"><span data-stu-id="bed61-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="bed61-208">Zakładając, że mamy cztery kontenery "con1", "con2", "con3", "con4" poniższy kod przedstawia przesyłanie dla zadań toohello partii zadań Azure zadania "proces csv" utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="bed61-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="bed61-209">Kod Hello dodaje wielu zadań toohello puli.</span><span class="sxs-lookup"><span data-stu-id="bed61-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="bed61-210">I poszczególnych zadań hello jest wykonywana w węźle hello puli maszyny wirtualne utworzone.</span><span class="sxs-lookup"><span data-stu-id="bed61-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="bed61-211">Jeśli hello liczba zadań przekracza hello liczbę maszyn wirtualnych w puli lub hello właściwości maxTasksPerNode, zadania hello poczekaj, aż węzeł ma zostać udostępnione.</span><span class="sxs-lookup"><span data-stu-id="bed61-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="bed61-212">Takie ograniczenia są zapewniane przez usługę Azure Batch automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bed61-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="bed61-213">Hello portal przedstawiono szczegółowe widoki na powitania zadania i stany zadania.</span><span class="sxs-lookup"><span data-stu-id="bed61-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="bed61-214">Można również użyć listy hello i uzyskać funkcje w hello węzła zestawu SDK platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bed61-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="bed61-215">Szczegółowe informacje znajdują się w dokumentacji hello [łącze](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="bed61-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bed61-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bed61-216">Next steps</span></span>

- <span data-ttu-id="bed61-217">Przejrzyj hello [funkcji partii omówienie Azure](batch-api-basics.md) artykułu, w którym firma Microsoft zaleca, jeśli masz nową usługę toohello.</span><span class="sxs-lookup"><span data-stu-id="bed61-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="bed61-218">Zobacz hello [odwołania Node.js partii](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) hello tooexplore interfejsu API partii.</span><span class="sxs-lookup"><span data-stu-id="bed61-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

