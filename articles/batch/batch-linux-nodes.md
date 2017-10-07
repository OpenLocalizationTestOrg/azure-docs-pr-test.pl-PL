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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Zapewnij węzły obliczeniowe systemu Linux w puli partii

W przypadku maszyn wirtualnych zarówno systemu Linux i Windows, można użyć obciążeń obliczeniowych równoległych toorun partii zadań Azure. W tym artykule szczegółowo sposób pule toocreate systemu Linux węzłach obliczeniowych w hello usługa partia zadań za pomocą obu hello [Python partii] [ py_batch_package] i [partiami platformy .NET] [ api_net] bibliotek klienckich.

> [!NOTE]
> Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r. Są one obsługiwane w pulach partii utworzyć między 10 marca 2016 i 5 2017 lipca tylko wtedy, gdy pula hello został utworzony za pomocą konfiguracji usługi w chmurze. Pule partii utworzone przed too10 marca 2016 r nie obsługują pakietów aplikacji. Aby uzyskać więcej informacji dotyczących używania aplikacji pakiety toodeploy węzły partii tooyour aplikacji, zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Konfiguracja maszyny wirtualnej
Podczas tworzenia puli węzłów obliczeniowych w partii, masz dwie opcje, z którego rozmiaru węzła hello tooselect i systemu operacyjnego: Konfiguracja usług w chmurze i konfiguracji maszyny wirtualnej.

**Konfiguracja usług Cloud Services** oferuje *tylko* węzły obliczeniowe systemu Windows. Rozmiary węzła obliczeń dostępne są wymienione w [rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md), i dostępnych systemów operacyjnych znajduje się w hello [wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Podczas tworzenia puli, która zawiera węzły usługi w chmurze Azure, można określić rozmiaru węzła hello i hello rodziny systemów operacyjnych, które zostały opisane w hello wcześniej wymienione artykułów. Dla węzły obliczeniowe pule systemu Windows, usługi w chmurze jest najczęściej używana.

**Konfiguracja maszyny wirtualnej** zawiera obrazy zarówno systemu Windows, jak i Linux dla węzły obliczeniowe. Rozmiary węzła obliczeń dostępne są wymienione w [rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) i [rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (system Windows). Podczas tworzenia puli, która zawiera węzły w konfiguracji maszyny wirtualnej, należy określić rozmiaru hello hello węzłów, hello odwołanie do obrazu maszyny wirtualnej i zainstalowane w węzłach hello hello partii węzła agenta SKU toobe.

### <a name="virtual-machine-image-reference"></a>Odwołanie do obrazu maszyny wirtualnej
Witaj partii używa usługi [zestawy skalowania maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) węzły obliczeniowe tooprovide systemu Linux. Można określić obrazu z hello [portalu Azure Marketplace][vm_marketplace], lub podaj niestandardowego obrazu, które zostały przygotowane. Aby uzyskać szczegółowe informacje o obrazach niestandardowych, zobacz [Tworzenie rozbudowanych rozwiązań przetwarzania równoległego przy użyciu usługi Batch](batch-api-basics.md#pool).

Po skonfigurowaniu odwołanie do obrazu maszyny wirtualnej, należy określić właściwości hello hello obrazu maszyny wirtualnej. Witaj następujące właściwości są wymagane, gdy utworzyć odwołanie do obrazu maszyny wirtualnej:

| **Obraz właściwości odwołania** | **Przykład** |
| --- | --- |
| Wydawca |Canonical |
| Oferta |UbuntuServer |
| SKU |14.04.4-LTS |
| Wersja |najnowsza |

> [!TIP]
> Dowiedz się więcej o tych właściwości i jak obrazy toolist Marketplace w [Nawigacja i wybierz obrazy maszyny wirtualnej systemu Linux na platformie Azure z interfejsu wiersza polecenia lub środowiska PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Należy pamiętać, że nie wszystkie obrazy Marketplace są obecnie zgodne z partii. Aby uzyskać więcej informacji, zobacz [agenta węzła jednostki SKU](#node-agent-sku).
>
>

### <a name="node-agent-sku"></a>Agent węzła jednostki SKU
agenta węzła partii Hello to program, który jest uruchamiany na każdym węźle w puli hello i udostępnia interfejs polecenia i kontroli hello między węzłem hello a hello usługa partia zadań. Istnieją różne implementacje hello węzła agenta, znany jako jednostki SKU, dla różnych systemów operacyjnych. Zasadniczo podczas tworzenia konfiguracji maszyny wirtualnej, należy najpierw określić hello odwołanie do obrazu maszyny wirtualnej, a następnie określ tooinstall agenta węzła hello na powitania obrazu. Zazwyczaj każdego agenta węzła, jednostka SKU jest zgodny z wielu obrazów maszyny wirtualnej. Oto kilka przykładów agenta węzła jednostki SKU:

* Batch.node.ubuntu 14.04
* Batch.node.centos 7
* Batch.node.Windows amd64

> [!IMPORTANT]
> Nie wszystkie obrazy maszyny wirtualnej, które są dostępne w portalu Marketplace hello są zgodne z agentów węzła partii obecnie hello. Użyj hello wsadowego zestawów SDK toolist hello dostępnego węzła agenta jednostki SKU i hello obrazy maszyny wirtualnej, z którymi są zgodne. Zobacz hello [obrazy listy maszyny wirtualnej](#list-of-virtual-machine-images) opisaną w tym artykule, aby uzyskać więcej informacji i zapoznać się z przykładami tooretrieve listę prawidłowy obrazów w czasie wykonywania.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Utwórz pulę Linux: Python partii
Witaj poniższy fragment kodu przedstawia przykładowy sposób toouse hello [Biblioteka klienta usługi partia zadań Microsoft Azure dla języka Python] [ py_batch_package] węzły obliczeniowe toocreate puli Ubuntu Server. Odwołanie hello modułu Python partii można znaleźć w dokumentacji [pakietu azure.batch] [ py_batch_docs] na odczyt hello dokumentów.

Ta Wstawka kodu tworzy [elementu ImageReference] [ py_imagereference] jawnie i określa każdego z jego właściwości (Oferta, jednostka SKU, wersja wydawcy). W kodzie produkcyjnym, jednak zaleca się używanie hello [list_node_agent_skus] [ py_list_skus] toodetermine metody, a następnie zaznacz hello dostępne obrazu węzła agenta SKU kombinacji i w czasie wykonywania.

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

Jak wspomniano wcześniej, zalecamy, aby zamiast tworzenia hello [elementu ImageReference] [ py_imagereference] jawnie, użyj hello [list_node_agent_skus] [ py_list_skus] wybierz toodynamically metody z hello aktualnie obsługiwane kombinacje obrazu agenta/Marketplace węzła. Witaj, po Python fragment kodu przedstawia sposób toouse tej metody.

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

## <a name="create-a-linux-pool-batch-net"></a>Utwórz pulę Linux: partiami platformy .NET
Witaj poniższy fragment kodu przedstawia przykładowy sposób toouse hello [partiami platformy .NET] [ nuget_batch_net] węzły obliczeniowe toocreate biblioteki klienta puli Ubuntu Server. Można znaleźć hello [dokumentacji partiami platformy .NET] [ api_net] w witrynie MSDN.

Witaj poniższy fragment kodu używa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect metody z hello listę aktualnie obsługiwanych Marketplace obrazu i węzła agenta SKU kombinacji. Ta technika jest pożądane, ponieważ lista hello obsługiwanej kombinacji mogą ulec zmianie od czasu tootime. Najczęściej są dodawane obsługiwanej kombinacji.

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

Mimo że fragment poprzedniej hello używa hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] metody toodynamically listy, a następnie zaznacz obsługiwane kombinacje jednostka SKU obrazu i węzła agenta (zalecane), można również skonfigurować [elementu ImageReference] [ net_imagereference] jawnie:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>Lista obrazów maszyny wirtualnej
Witaj poniższej tabeli wymieniono hello obrazy maszyny wirtualnej Marketplace, które są zgodne z agentów węzła partii dostępne hello datę ostatniej aktualizacji w tym artykule. Jest ważne toonote, że ta lista nie jest ostatecznym, ponieważ obrazów i agentów węzła może dodać lub usunąć w dowolnej chwili. Firma Microsoft zaleca, aby partii aplikacje i usługi zawsze używać [list_node_agent_skus] [ py_list_skus] (Python) i [ListNodeAgentSkus] [ net_list_skus] Toodetermine (partii .NET), a następnie zaznacz hello aktualnie dostępne jednostki SKU.

> [!WARNING]
> Witaj, następujące listy mogą ulec zmianie w dowolnym momencie. Zawsze używaj hello **agent węzła listy SKU** metod w toolist API partii hello hello kompatybilnej maszynie wirtualnej i agenta węzła jednostki SKU podczas wykonywania zadań wsadowych.
>
>

| **Wydawcy** | **Oferta** | **Jednostka SKU obrazu** | **Wersja** | **Agent węzła identyfikator jednostki SKU** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | najnowsza | Batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | najnowsza | Batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | najnowsza | Batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | najnowsza | Batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | najnowsza | Batch.node.centos 7 |
| OpenLogic | CentOS HPC | 7.1 | najnowsza | Batch.node.centos 7 |
| OpenLogic | CentOS | 7.2 | najnowsza | Batch.node.centos 7 |
| Oracle | Oracle Linux | 7.0 | najnowsza | Batch.node.centos 7 |
| Oracle | Oracle Linux | 7.2 | najnowsza | Batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | najnowsza | Batch.node.opensuse 13.2 |
| SUSE | openSUSE przestępnego | 42.1 | najnowsza | Batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | najnowsza | Batch.node.opensuse 42.1 |
| SUSE | SLES HPC | 12-SP1 | najnowsza | Batch.node.opensuse 42.1 |
| Microsoft reklam | data nauki-maszyny wirtualnej systemu Linux | linuxdsvm | najnowsza | Batch.node.centos 7 |
| Microsoft reklam | Standard danych nauki vm | Standard danych nauki vm | najnowsza | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008 R2 SP1 | najnowsza | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | najnowsza | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | najnowsza | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | Centrum danych 2016 | najnowsza | Batch.node.Windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016 centrum danych z kontenerów | najnowsza | Batch.node.Windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>Łączenie węzłów tooLinux przy użyciu protokołu SSH
Podczas tworzenia lub podczas rozwiązywania problemów może być konieczne toosign w węzłach toohello w puli. W przeciwieństwie do węzłów obliczeniowych systemu Windows nie można użyć protokołu RDP (Remote Desktop) tooconnect tooLinux węzłów. Zamiast tego hello usługa partia zadań umożliwia SSH dostępu w każdym węźle dla połączenia zdalnego.

Witaj poniższy fragment kodu języka Python tworzy użytkownika w każdym węźle w puli, który jest wymagany dla połączenia zdalnego. Wyświetla informacje o połączeniu hello bezpiecznej powłoki (SSH) dla każdego węzła.

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

Oto przykładowe dane wyjściowe dla hello poprzedni kod dla puli, która zawiera cztery węzły Linux:

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

Zamiast hasła można określić klucz publiczny SSH, podczas tworzenia użytkownika w węźle. W hello zestaw SDK Python, użyj hello **ssh_public_key** parametru [ComputeNodeUser][py_computenodeuser]. W środowisku .NET, użyj hello [ComputeNodeUser][net_computenodeuser].[ Parametry SshPublicKey] [ net_ssh_key] właściwości.

## <a name="pricing"></a>Cennik
Partia zadań Azure jest oparty na technologii usług Azure Cloud Services i maszyn wirtualnych platformy Azure. Hello sama usługa partii jest oferowane bezpłatnie, która oznacza, że są naliczane tylko w przypadku hello obliczeniowe zasobów, które korzystać z własnych rozwiązań partii. Po wybraniu **konfiguracji usługi w chmurze**, naliczane są opłaty oparte na powitania [cennik usługi w chmurze] [ cloud_services_pricing] struktury. Po wybraniu **konfiguracji maszyny wirtualnej**, naliczane są opłaty oparte na powitania [cennik maszyn wirtualnych] [ vm_pricing] struktury. 

W przypadku wdrożenia aplikacji tooyour partii węzłów za pomocą [pakietów aplikacji](batch-application-packages.md), naliczane są również opłaty dla zasobów usługi Azure Storage hello czy używać pakietów aplikacji. Ogólnie rzecz biorąc kosztów magazynowania Azure hello są minimalne. 

## <a name="next-steps"></a>Następne kroki
### <a name="batch-python-tutorial"></a>Samouczek języka Python dla usługi Batch
Więcej informacji na temat samouczek temat toowork z partii przy użyciu języka Python, wyewidencjonowanie [wprowadzenie powitania klienta Python usługi partia zadań Azure](batch-python-tutorial.md). Jego Pomocnika [przykładowy kod] [ github_samples_pyclient] obejmuje funkcję Pomocnika `get_vm_config_for_distro`, który zawiera inny tooobtain technika konfiguracji maszyny wirtualnej.

### <a name="batch-python-code-samples"></a>Przykłady kodu Python partii
Witaj [przykłady kodu Python] [ github_samples_py] w hello [azure partii próbek] [ github_samples] repozytorium w usłudze GitHub zawierać skrypty, które opisano, jak tooperform typowych operacji wsadowych, takie jak pula, zadania i tworzenia zadań. Witaj [README] [ github_py_readme] dołączony przykłady Python hello zawiera szczegółowe informacje dotyczące sposobu tooinstall hello wymagane pakiety.

### <a name="batch-forum"></a>Forum usługi Batch
Witaj [Forum usługi partia zadań Azure] [ forum] w witrynie MSDN jest doskonałym umieścić toodiscuss partii i zadać pytania dotyczące usługi hello. Odczyt przydatne "przypięte" ogłoszeń i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.

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
