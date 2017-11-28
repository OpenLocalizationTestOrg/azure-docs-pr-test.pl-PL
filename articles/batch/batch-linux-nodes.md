---
title: "węzły - partii zadań Azure obliczeniowe aaaRun systemu Linux na maszynie wirtualnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprocess Twojego równoległe obliczeniowe obciążeń w puli maszyn wirtualnych systemu Linux w partii zadań Azure."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="6f81d-103">Zapewnij węzły obliczeniowe systemu Linux w puli partii</span><span class="sxs-lookup"><span data-stu-id="6f81d-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="6f81d-104">W przypadku maszyn wirtualnych zarówno systemu Linux i Windows, można użyć obciążeń obliczeniowych równoległych toorun partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="6f81d-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="6f81d-105">W tym artykule szczegółowo sposób pule toocreate systemu Linux węzłach obliczeniowych w hello usługa partia zadań za pomocą obu hello [Python partii] [ py_batch_package] i [partiami platformy .NET] [ api_net] bibliotek klienckich.</span><span class="sxs-lookup"><span data-stu-id="6f81d-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="6f81d-106">Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6f81d-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="6f81d-107">Są one obsługiwane w pulach partii utworzyć między 10 marca 2016 i 5 2017 lipca tylko wtedy, gdy pula hello został utworzony za pomocą konfiguracji usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6f81d-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="6f81d-108">Pule partii utworzone przed too10 marca 2016 r nie obsługują pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f81d-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="6f81d-109">Aby uzyskać więcej informacji dotyczących używania aplikacji pakiety toodeploy węzły partii tooyour aplikacji, zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6f81d-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="6f81d-110">Konfiguracja maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6f81d-110">Virtual machine configuration</span></span>
<span data-ttu-id="6f81d-111">Podczas tworzenia puli węzłów obliczeniowych w partii, masz dwie opcje, z którego rozmiaru węzła hello tooselect i systemu operacyjnego: Konfiguracja usług w chmurze i konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f81d-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="6f81d-112">**Konfiguracja usług Cloud Services** oferuje *tylko* węzły obliczeniowe systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6f81d-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="6f81d-113">Rozmiary węzła obliczeń dostępne są wymienione w [rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md), i dostępnych systemów operacyjnych znajduje się w hello [wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="6f81d-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="6f81d-114">Podczas tworzenia puli, która zawiera węzły usługi w chmurze Azure, można określić rozmiaru węzła hello i hello rodziny systemów operacyjnych, które zostały opisane w hello wcześniej wymienione artykułów.</span><span class="sxs-lookup"><span data-stu-id="6f81d-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="6f81d-115">Dla węzły obliczeniowe pule systemu Windows, usługi w chmurze jest najczęściej używana.</span><span class="sxs-lookup"><span data-stu-id="6f81d-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="6f81d-116">**Konfiguracja maszyny wirtualnej** zawiera obrazy zarówno systemu Windows, jak i Linux dla węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="6f81d-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="6f81d-117">Rozmiary węzła obliczeń dostępne są wymienione w [rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) i [rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (system Windows).</span><span class="sxs-lookup"><span data-stu-id="6f81d-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="6f81d-118">Podczas tworzenia puli, która zawiera węzły w konfiguracji maszyny wirtualnej, należy określić rozmiaru hello hello węzłów, hello odwołanie do obrazu maszyny wirtualnej i zainstalowane w węzłach hello hello partii węzła agenta SKU toobe.</span><span class="sxs-lookup"><span data-stu-id="6f81d-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="6f81d-119">Odwołanie do obrazu maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6f81d-119">Virtual machine image reference</span></span>
<span data-ttu-id="6f81d-120">Witaj partii używa usługi [zestawy skalowania maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) węzły obliczeniowe tooprovide systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="6f81d-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="6f81d-121">Można określić obrazu z hello [portalu Azure Marketplace][vm_marketplace], lub podaj niestandardowego obrazu, które zostały przygotowane.</span><span class="sxs-lookup"><span data-stu-id="6f81d-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="6f81d-122">Aby uzyskać szczegółowe informacje o obrazach niestandardowych, zobacz [Tworzenie rozbudowanych rozwiązań przetwarzania równoległego przy użyciu usługi Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="6f81d-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="6f81d-123">Po skonfigurowaniu odwołanie do obrazu maszyny wirtualnej, należy określić właściwości hello hello obrazu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f81d-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="6f81d-124">Witaj następujące właściwości są wymagane, gdy utworzyć odwołanie do obrazu maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="6f81d-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="6f81d-125">**Obraz właściwości odwołania**</span><span class="sxs-lookup"><span data-stu-id="6f81d-125">**Image reference properties**</span></span> | <span data-ttu-id="6f81d-126">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="6f81d-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="6f81d-127">Wydawca</span><span class="sxs-lookup"><span data-stu-id="6f81d-127">Publisher</span></span> |<span data-ttu-id="6f81d-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="6f81d-128">Canonical</span></span> |
| <span data-ttu-id="6f81d-129">Oferta</span><span class="sxs-lookup"><span data-stu-id="6f81d-129">Offer</span></span> |<span data-ttu-id="6f81d-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-130">UbuntuServer</span></span> |
| <span data-ttu-id="6f81d-131">SKU</span><span class="sxs-lookup"><span data-stu-id="6f81d-131">SKU</span></span> |<span data-ttu-id="6f81d-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="6f81d-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="6f81d-133">Wersja</span><span class="sxs-lookup"><span data-stu-id="6f81d-133">Version</span></span> |<span data-ttu-id="6f81d-134">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="6f81d-135">Dowiedz się więcej o tych właściwości i jak obrazy toolist Marketplace w [Nawigacja i wybierz obrazy maszyny wirtualnej systemu Linux na platformie Azure z interfejsu wiersza polecenia lub środowiska PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f81d-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6f81d-136">Należy pamiętać, że nie wszystkie obrazy Marketplace są obecnie zgodne z partii.</span><span class="sxs-lookup"><span data-stu-id="6f81d-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="6f81d-137">Aby uzyskać więcej informacji, zobacz [agenta węzła jednostki SKU](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="6f81d-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="6f81d-138">Agent węzła jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="6f81d-138">Node agent SKU</span></span>
<span data-ttu-id="6f81d-139">agenta węzła partii Hello to program, który jest uruchamiany na każdym węźle w puli hello i udostępnia interfejs polecenia i kontroli hello między węzłem hello a hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="6f81d-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="6f81d-140">Istnieją różne implementacje hello węzła agenta, znany jako jednostki SKU, dla różnych systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="6f81d-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="6f81d-141">Zasadniczo podczas tworzenia konfiguracji maszyny wirtualnej, należy najpierw określić hello odwołanie do obrazu maszyny wirtualnej, a następnie określ tooinstall agenta węzła hello na powitania obrazu.</span><span class="sxs-lookup"><span data-stu-id="6f81d-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="6f81d-142">Zazwyczaj każdego agenta węzła, jednostka SKU jest zgodny z wielu obrazów maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f81d-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="6f81d-143">Oto kilka przykładów agenta węzła jednostki SKU:</span><span class="sxs-lookup"><span data-stu-id="6f81d-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="6f81d-144">Batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6f81d-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="6f81d-145">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-145">batch.node.centos 7</span></span>
* <span data-ttu-id="6f81d-146">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="6f81d-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f81d-147">Nie wszystkie obrazy maszyny wirtualnej, które są dostępne w portalu Marketplace hello są zgodne z agentów węzła partii obecnie hello.</span><span class="sxs-lookup"><span data-stu-id="6f81d-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="6f81d-148">Użyj hello wsadowego zestawów SDK toolist hello dostępnego węzła agenta jednostki SKU i hello obrazy maszyny wirtualnej, z którymi są zgodne.</span><span class="sxs-lookup"><span data-stu-id="6f81d-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="6f81d-149">Zobacz hello [obrazy listy maszyny wirtualnej](#list-of-virtual-machine-images) opisaną w tym artykule, aby uzyskać więcej informacji i zapoznać się z przykładami tooretrieve listę prawidłowy obrazów w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6f81d-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="6f81d-150">Utwórz pulę Linux: Python partii</span><span class="sxs-lookup"><span data-stu-id="6f81d-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="6f81d-151">Witaj poniższy fragment kodu przedstawia przykładowy sposób toouse hello [Biblioteka klienta usługi partia zadań Microsoft Azure dla języka Python] [ py_batch_package] węzły obliczeniowe toocreate puli Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="6f81d-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="6f81d-152">Odwołanie hello modułu Python partii można znaleźć w dokumentacji [pakietu azure.batch] [ py_batch_docs] na odczyt hello dokumentów.</span><span class="sxs-lookup"><span data-stu-id="6f81d-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="6f81d-153">Ta Wstawka kodu tworzy [elementu ImageReference] [ py_imagereference] jawnie i określa każdego z jego właściwości (Oferta, jednostka SKU, wersja wydawcy).</span><span class="sxs-lookup"><span data-stu-id="6f81d-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="6f81d-154">W kodzie produkcyjnym, jednak zaleca się używanie hello [list_node_agent_skus] [ py_list_skus] toodetermine metody, a następnie zaznacz hello dostępne obrazu węzła agenta SKU kombinacji i w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6f81d-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="6f81d-155">Jak wspomniano wcześniej, zalecamy, aby zamiast tworzenia hello [elementu ImageReference] [ py_imagereference] jawnie, użyj hello [list_node_agent_skus] [ py_list_skus] wybierz toodynamically metody z hello aktualnie obsługiwane kombinacje obrazu agenta/Marketplace węzła.</span><span class="sxs-lookup"><span data-stu-id="6f81d-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="6f81d-156">Witaj, po Python fragment kodu przedstawia sposób toouse tej metody.</span><span class="sxs-lookup"><span data-stu-id="6f81d-156">hello following Python snippet shows how toouse this method.</span></span>

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="6f81d-157">Utwórz pulę Linux: partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="6f81d-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="6f81d-158">Witaj poniższy fragment kodu przedstawia przykładowy sposób toouse hello [partiami platformy .NET] [ nuget_batch_net] węzły obliczeniowe toocreate biblioteki klienta puli Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="6f81d-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="6f81d-159">Można znaleźć hello [dokumentacji partiami platformy .NET] [ api_net] w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="6f81d-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="6f81d-160">Witaj poniższy fragment kodu używa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect metody z hello listę aktualnie obsługiwanych Marketplace obrazu i węzła agenta SKU kombinacji.</span><span class="sxs-lookup"><span data-stu-id="6f81d-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="6f81d-161">Ta technika jest pożądane, ponieważ lista hello obsługiwanej kombinacji mogą ulec zmianie od czasu tootime.</span><span class="sxs-lookup"><span data-stu-id="6f81d-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="6f81d-162">Najczęściej są dodawane obsługiwanej kombinacji.</span><span class="sxs-lookup"><span data-stu-id="6f81d-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

<span data-ttu-id="6f81d-163">Mimo że fragment poprzedniej hello używa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] metody toodynamically listy, a następnie zaznacz obsługiwane kombinacje jednostka SKU obrazu i węzła agenta (zalecane), można również skonfigurować [elementu ImageReference] [ net_imagereference] jawnie:</span><span class="sxs-lookup"><span data-stu-id="6f81d-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="6f81d-164">Lista obrazów maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6f81d-164">List of virtual machine images</span></span>
<span data-ttu-id="6f81d-165">Witaj poniższej tabeli wymieniono hello obrazy maszyny wirtualnej Marketplace, które są zgodne z agentów węzła partii dostępne hello datę ostatniej aktualizacji w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="6f81d-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="6f81d-166">Jest ważne toonote, że ta lista nie jest ostatecznym, ponieważ obrazów i agentów węzła może dodać lub usunąć w dowolnej chwili.</span><span class="sxs-lookup"><span data-stu-id="6f81d-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="6f81d-167">Firma Microsoft zaleca, aby partii aplikacje i usługi zawsze używać [list_node_agent_skus] [ py_list_skus] (Python) i [ListNodeAgentSkus] [ net_list_skus] Toodetermine (partii .NET), a następnie zaznacz hello aktualnie dostępne jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="6f81d-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="6f81d-168">Witaj, następujące listy mogą ulec zmianie w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="6f81d-168">hello following list may change at any time.</span></span> <span data-ttu-id="6f81d-169">Zawsze używaj hello **agent węzła listy SKU** metod w toolist API partii hello hello kompatybilnej maszynie wirtualnej i agenta węzła jednostki SKU podczas wykonywania zadań wsadowych.</span><span class="sxs-lookup"><span data-stu-id="6f81d-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="6f81d-170">**Wydawcy**</span><span class="sxs-lookup"><span data-stu-id="6f81d-170">**Publisher**</span></span> | <span data-ttu-id="6f81d-171">**Oferta**</span><span class="sxs-lookup"><span data-stu-id="6f81d-171">**Offer**</span></span> | <span data-ttu-id="6f81d-172">**Jednostka SKU obrazu**</span><span class="sxs-lookup"><span data-stu-id="6f81d-172">**Image SKU**</span></span> | <span data-ttu-id="6f81d-173">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="6f81d-173">**Version**</span></span> | <span data-ttu-id="6f81d-174">**Agent węzła identyfikator jednostki SKU**</span><span class="sxs-lookup"><span data-stu-id="6f81d-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="6f81d-175">Canonical</span><span class="sxs-lookup"><span data-stu-id="6f81d-175">Canonical</span></span> | <span data-ttu-id="6f81d-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-176">UbuntuServer</span></span> | <span data-ttu-id="6f81d-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="6f81d-177">14.04.5-LTS</span></span> | <span data-ttu-id="6f81d-178">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-178">latest</span></span> | <span data-ttu-id="6f81d-179">Batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6f81d-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="6f81d-180">Canonical</span><span class="sxs-lookup"><span data-stu-id="6f81d-180">Canonical</span></span> | <span data-ttu-id="6f81d-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-181">UbuntuServer</span></span> | <span data-ttu-id="6f81d-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="6f81d-182">16.04.0-LTS</span></span> | <span data-ttu-id="6f81d-183">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-183">latest</span></span> | <span data-ttu-id="6f81d-184">Batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6f81d-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="6f81d-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="6f81d-185">Credativ</span></span> | <span data-ttu-id="6f81d-186">Debian</span><span class="sxs-lookup"><span data-stu-id="6f81d-186">Debian</span></span> | <span data-ttu-id="6f81d-187">8</span><span class="sxs-lookup"><span data-stu-id="6f81d-187">8</span></span> | <span data-ttu-id="6f81d-188">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-188">latest</span></span> | <span data-ttu-id="6f81d-189">Batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="6f81d-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="6f81d-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6f81d-190">OpenLogic</span></span> | <span data-ttu-id="6f81d-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="6f81d-191">CentOS</span></span> | <span data-ttu-id="6f81d-192">7.0</span><span class="sxs-lookup"><span data-stu-id="6f81d-192">7.0</span></span> | <span data-ttu-id="6f81d-193">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-193">latest</span></span> | <span data-ttu-id="6f81d-194">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="6f81d-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6f81d-195">OpenLogic</span></span> | <span data-ttu-id="6f81d-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="6f81d-196">CentOS</span></span> | <span data-ttu-id="6f81d-197">7.1</span><span class="sxs-lookup"><span data-stu-id="6f81d-197">7.1</span></span> | <span data-ttu-id="6f81d-198">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-198">latest</span></span> | <span data-ttu-id="6f81d-199">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="6f81d-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6f81d-200">OpenLogic</span></span> | <span data-ttu-id="6f81d-201">CentOS HPC</span><span class="sxs-lookup"><span data-stu-id="6f81d-201">CentOS-HPC</span></span> | <span data-ttu-id="6f81d-202">7.1</span><span class="sxs-lookup"><span data-stu-id="6f81d-202">7.1</span></span> | <span data-ttu-id="6f81d-203">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-203">latest</span></span> | <span data-ttu-id="6f81d-204">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="6f81d-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6f81d-205">OpenLogic</span></span> | <span data-ttu-id="6f81d-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="6f81d-206">CentOS</span></span> | <span data-ttu-id="6f81d-207">7.2</span><span class="sxs-lookup"><span data-stu-id="6f81d-207">7.2</span></span> | <span data-ttu-id="6f81d-208">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-208">latest</span></span> | <span data-ttu-id="6f81d-209">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="6f81d-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="6f81d-210">Oracle</span></span> | <span data-ttu-id="6f81d-211">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="6f81d-211">Oracle-Linux</span></span> | <span data-ttu-id="6f81d-212">7.0</span><span class="sxs-lookup"><span data-stu-id="6f81d-212">7.0</span></span> | <span data-ttu-id="6f81d-213">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-213">latest</span></span> | <span data-ttu-id="6f81d-214">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="6f81d-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="6f81d-215">Oracle</span></span> | <span data-ttu-id="6f81d-216">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="6f81d-216">Oracle-Linux</span></span> | <span data-ttu-id="6f81d-217">7.2</span><span class="sxs-lookup"><span data-stu-id="6f81d-217">7.2</span></span> | <span data-ttu-id="6f81d-218">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-218">latest</span></span> | <span data-ttu-id="6f81d-219">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="6f81d-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="6f81d-220">SUSE</span></span> | <span data-ttu-id="6f81d-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6f81d-221">openSUSE</span></span> | <span data-ttu-id="6f81d-222">13.2</span><span class="sxs-lookup"><span data-stu-id="6f81d-222">13.2</span></span> | <span data-ttu-id="6f81d-223">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-223">latest</span></span> | <span data-ttu-id="6f81d-224">Batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="6f81d-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="6f81d-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="6f81d-225">SUSE</span></span> | <span data-ttu-id="6f81d-226">openSUSE przestępnego</span><span class="sxs-lookup"><span data-stu-id="6f81d-226">openSUSE-Leap</span></span> | <span data-ttu-id="6f81d-227">42.1</span><span class="sxs-lookup"><span data-stu-id="6f81d-227">42.1</span></span> | <span data-ttu-id="6f81d-228">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-228">latest</span></span> | <span data-ttu-id="6f81d-229">Batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6f81d-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6f81d-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="6f81d-230">SUSE</span></span> | <span data-ttu-id="6f81d-231">SLES</span><span class="sxs-lookup"><span data-stu-id="6f81d-231">SLES</span></span> | <span data-ttu-id="6f81d-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="6f81d-232">12-SP1</span></span> | <span data-ttu-id="6f81d-233">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-233">latest</span></span> | <span data-ttu-id="6f81d-234">Batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6f81d-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6f81d-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="6f81d-235">SUSE</span></span> | <span data-ttu-id="6f81d-236">SLES HPC</span><span class="sxs-lookup"><span data-stu-id="6f81d-236">SLES-HPC</span></span> | <span data-ttu-id="6f81d-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="6f81d-237">12-SP1</span></span> | <span data-ttu-id="6f81d-238">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-238">latest</span></span> | <span data-ttu-id="6f81d-239">Batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="6f81d-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="6f81d-240">Microsoft reklam</span><span class="sxs-lookup"><span data-stu-id="6f81d-240">microsoft-ads</span></span> | <span data-ttu-id="6f81d-241">data nauki-maszyny wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="6f81d-241">linux-data-science-vm</span></span> | <span data-ttu-id="6f81d-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="6f81d-242">linuxdsvm</span></span> | <span data-ttu-id="6f81d-243">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-243">latest</span></span> | <span data-ttu-id="6f81d-244">Batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="6f81d-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="6f81d-245">Microsoft reklam</span><span class="sxs-lookup"><span data-stu-id="6f81d-245">microsoft-ads</span></span> | <span data-ttu-id="6f81d-246">Standard danych nauki vm</span><span class="sxs-lookup"><span data-stu-id="6f81d-246">standard-data-science-vm</span></span> | <span data-ttu-id="6f81d-247">Standard danych nauki vm</span><span class="sxs-lookup"><span data-stu-id="6f81d-247">standard-data-science-vm</span></span> | <span data-ttu-id="6f81d-248">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-248">latest</span></span> | <span data-ttu-id="6f81d-249">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="6f81d-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6f81d-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6f81d-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-251">WindowsServer</span></span> | <span data-ttu-id="6f81d-252">2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="6f81d-252">2008-R2-SP1</span></span> | <span data-ttu-id="6f81d-253">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-253">latest</span></span> | <span data-ttu-id="6f81d-254">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="6f81d-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6f81d-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6f81d-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-256">WindowsServer</span></span> | <span data-ttu-id="6f81d-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="6f81d-257">2012-Datacenter</span></span> | <span data-ttu-id="6f81d-258">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-258">latest</span></span> | <span data-ttu-id="6f81d-259">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="6f81d-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6f81d-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6f81d-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-261">WindowsServer</span></span> | <span data-ttu-id="6f81d-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="6f81d-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="6f81d-263">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-263">latest</span></span> | <span data-ttu-id="6f81d-264">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="6f81d-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6f81d-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6f81d-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-266">WindowsServer</span></span> | <span data-ttu-id="6f81d-267">Centrum danych 2016</span><span class="sxs-lookup"><span data-stu-id="6f81d-267">2016-Datacenter</span></span> | <span data-ttu-id="6f81d-268">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-268">latest</span></span> | <span data-ttu-id="6f81d-269">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="6f81d-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="6f81d-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="6f81d-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="6f81d-271">WindowsServer</span></span> | <span data-ttu-id="6f81d-272">2016 centrum danych z kontenerów</span><span class="sxs-lookup"><span data-stu-id="6f81d-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="6f81d-273">najnowsza</span><span class="sxs-lookup"><span data-stu-id="6f81d-273">latest</span></span> | <span data-ttu-id="6f81d-274">Batch.node.Windows amd64</span><span class="sxs-lookup"><span data-stu-id="6f81d-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="6f81d-275">Łączenie węzłów tooLinux przy użyciu protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="6f81d-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="6f81d-276">Podczas tworzenia lub podczas rozwiązywania problemów może być konieczne toosign w węzłach toohello w puli.</span><span class="sxs-lookup"><span data-stu-id="6f81d-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="6f81d-277">W przeciwieństwie do węzłów obliczeniowych systemu Windows nie można użyć protokołu RDP (Remote Desktop) tooconnect tooLinux węzłów.</span><span class="sxs-lookup"><span data-stu-id="6f81d-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="6f81d-278">Zamiast tego hello usługa partia zadań umożliwia SSH dostępu w każdym węźle dla połączenia zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6f81d-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="6f81d-279">Witaj poniższy fragment kodu języka Python tworzy użytkownika w każdym węźle w puli, który jest wymagany dla połączenia zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6f81d-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="6f81d-280">Wyświetla informacje o połączeniu hello bezpiecznej powłoki (SSH) dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="6f81d-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="6f81d-281">Oto przykładowe dane wyjściowe dla hello poprzedni kod dla puli, która zawiera cztery węzły Linux:</span><span class="sxs-lookup"><span data-stu-id="6f81d-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="6f81d-282">Zamiast hasła można określić klucz publiczny SSH, podczas tworzenia użytkownika w węźle.</span><span class="sxs-lookup"><span data-stu-id="6f81d-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="6f81d-283">W hello zestaw SDK Python, użyj hello **ssh_public_key** parametru [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="6f81d-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="6f81d-284">W środowisku .NET, użyj hello [ComputeNodeUser][net_computenodeuser].[ Parametry SshPublicKey] [ net_ssh_key] właściwości.</span><span class="sxs-lookup"><span data-stu-id="6f81d-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="6f81d-285">Cennik</span><span class="sxs-lookup"><span data-stu-id="6f81d-285">Pricing</span></span>
<span data-ttu-id="6f81d-286">Partia zadań Azure jest oparty na technologii usług Azure Cloud Services i maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f81d-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="6f81d-287">Hello sama usługa partii jest oferowane bezpłatnie, która oznacza, że są naliczane tylko w przypadku hello obliczeniowe zasobów, które korzystać z własnych rozwiązań partii.</span><span class="sxs-lookup"><span data-stu-id="6f81d-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="6f81d-288">Po wybraniu **konfiguracji usługi w chmurze**, naliczane są opłaty oparte na powitania [cennik usługi w chmurze] [ cloud_services_pricing] struktury.</span><span class="sxs-lookup"><span data-stu-id="6f81d-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="6f81d-289">Po wybraniu **konfiguracji maszyny wirtualnej**, naliczane są opłaty oparte na powitania [cennik maszyn wirtualnych] [ vm_pricing] struktury.</span><span class="sxs-lookup"><span data-stu-id="6f81d-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="6f81d-290">W przypadku wdrożenia aplikacji tooyour partii węzłów za pomocą [pakietów aplikacji](batch-application-packages.md), naliczane są również opłaty dla zasobów usługi Azure Storage hello czy używać pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f81d-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="6f81d-291">Ogólnie rzecz biorąc kosztów magazynowania Azure hello są minimalne.</span><span class="sxs-lookup"><span data-stu-id="6f81d-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6f81d-292">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f81d-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="6f81d-293">Samouczek języka Python dla usługi Batch</span><span class="sxs-lookup"><span data-stu-id="6f81d-293">Batch Python tutorial</span></span>
<span data-ttu-id="6f81d-294">Więcej informacji na temat samouczek temat toowork z partii przy użyciu języka Python, wyewidencjonowanie [wprowadzenie powitania klienta Python usługi partia zadań Azure](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6f81d-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="6f81d-295">Jego Pomocnika [przykładowy kod] [ github_samples_pyclient] obejmuje funkcję Pomocnika `get_vm_config_for_distro`, który zawiera inny tooobtain technika konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6f81d-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="6f81d-296">Przykłady kodu Python partii</span><span class="sxs-lookup"><span data-stu-id="6f81d-296">Batch Python code samples</span></span>
<span data-ttu-id="6f81d-297">Witaj [przykłady kodu Python] [ github_samples_py] w hello [azure partii próbek] [ github_samples] repozytorium w usłudze GitHub zawierać skrypty, które opisano, jak tooperform typowych operacji wsadowych, takie jak pula, zadania i tworzenia zadań.</span><span class="sxs-lookup"><span data-stu-id="6f81d-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="6f81d-298">Witaj [README] [ github_py_readme] dołączony przykłady Python hello zawiera szczegółowe informacje dotyczące sposobu tooinstall hello wymagane pakiety.</span><span class="sxs-lookup"><span data-stu-id="6f81d-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="6f81d-299">Forum usługi Batch</span><span class="sxs-lookup"><span data-stu-id="6f81d-299">Batch forum</span></span>
<span data-ttu-id="6f81d-300">Witaj [Forum usługi partia zadań Azure] [ forum] w witrynie MSDN jest doskonałym umieścić toodiscuss partii i zadać pytania dotyczące usługi hello.</span><span class="sxs-lookup"><span data-stu-id="6f81d-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="6f81d-301">Odczyt przydatne "przypięte" ogłoszeń i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.</span><span class="sxs-lookup"><span data-stu-id="6f81d-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
