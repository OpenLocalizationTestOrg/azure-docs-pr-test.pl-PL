---
title: "aaaCreate i zarządzanie nimi maszyny Wirtualnej systemu Windows na platformie Azure przy użyciu języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się toouse Python toocreate i zarządzaj nimi maszyny Wirtualnej systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="54775-103">Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="54775-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="54775-104">[Maszyny wirtualnej Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM), wymaga kilku obsługi zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54775-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="54775-105">W tym artykule omówiono tworzenia, zarządzania i usuwania zasobów maszyny Wirtualnej przy użyciu języka Python.</span><span class="sxs-lookup"><span data-stu-id="54775-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="54775-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="54775-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="54775-107">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54775-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="54775-108">Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="54775-108">Install packages</span></span>
> * <span data-ttu-id="54775-109">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="54775-109">Create credentials</span></span>
> * <span data-ttu-id="54775-110">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="54775-110">Create resources</span></span>
> * <span data-ttu-id="54775-111">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="54775-111">Perform management tasks</span></span>
> * <span data-ttu-id="54775-112">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="54775-112">Delete resources</span></span>
> * <span data-ttu-id="54775-113">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="54775-113">Run hello application</span></span>

<span data-ttu-id="54775-114">Trwa około 20 minut toodo następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="54775-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="54775-115">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54775-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="54775-116">Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="54775-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="54775-117">Wybierz **programowania Python** na hello obciążeń strony, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="54775-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="54775-118">W podsumowaniu hello, można stwierdzić, że **Python 3 64-bitowych (3.6.0)** jest automatycznie wybrana.</span><span class="sxs-lookup"><span data-stu-id="54775-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="54775-119">Jeśli zainstalowano program Visual Studio można dodać hello Python obciążenia przy użyciu hello uruchamiania usługi Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54775-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="54775-120">Po zainstalowaniu i uruchomieniem programu Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="54775-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="54775-121">Kliknij przycisk **szablony** > **Python** > **aplikacji Python**, wprowadź *myPythonProject* dla nazwy hello Witaj projektu, wybierz lokalizację hello hello projektu, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="54775-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="54775-122">Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="54775-122">Install packages</span></span>

1. <span data-ttu-id="54775-123">W Eksploratorze rozwiązań w obszarze *myPythonProject*, kliknij prawym przyciskiem myszy **środowiska Python**, a następnie wybierz **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="54775-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="54775-124">Na ekranie powitania Dodawanie środowiska wirtualnego Zaakceptuj domyślną nazwę hello *env*, upewnij się, że *3,6 języka Python (64-bitowy)* został wybrany do hello interpreter podstawowy, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="54775-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="54775-125">Kliknij prawym przyciskiem myszy hello *env* środowisko, które zostały utworzone, kliknij przycisk **zainstaluj pakiet języka Python**, wprowadź *azure* w hello pole wyszukiwania, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="54775-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="54775-126">Powinien zostać wyświetlony w oknie danych wyjściowych hello pakietów hello azure zostały pomyślnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="54775-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="54775-127">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="54775-127">Create credentials</span></span>

<span data-ttu-id="54775-128">Przed rozpoczęciem tego kroku upewnij się, że masz [nazwy głównej usługi Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="54775-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="54775-129">Należy również zarejestrować identyfikator aplikacji hello, klucz uwierzytelniania hello i identyfikator dzierżawcy hello, które należy w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="54775-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="54775-130">Otwórz *myPythonProject.py* pliku, który został utworzony, a następnie dodaj ten kod tooenable toorun Twojej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="54775-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="54775-131">tooimport hello kodu, który jest wymagany, Dodaj te instrukcje góry toohello hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="54775-132">Obok w hello .py pliku Dodaj zmienne po instrukcje importu hello toospecify wspólne wartości używane w hello kodu:</span><span class="sxs-lookup"><span data-stu-id="54775-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="54775-133">Zastąp **identyfikator subskrypcji** z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="54775-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="54775-134">poświadczenia usługi Active Directory hello toocreate konieczność toomake żądań, Dodaj tej funkcji po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="54775-135">Zastąp **identyfikator aplikacji**, **klucz uwierzytelniania**, i **identyfikator dzierżawcy** wartościami hello uprzednio zebrane podczas tworzenia usługi Azure Active Directory nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="54775-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="54775-136">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="54775-137">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="54775-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="54775-138">Inicjowanie zarządzania klientami</span><span class="sxs-lookup"><span data-stu-id="54775-138">Initialize management clients</span></span>

<span data-ttu-id="54775-139">Klienci zarządzania są potrzebne toocreate zasobów i zarządzanie nimi przy użyciu zestawu SDK Python hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="54775-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="54775-140">toocreate hello zarządzania klientami, Dodaj ten kod w obszarze hello **Jeśli** instrukcji następnie końcem pliku .py hello:</span><span class="sxs-lookup"><span data-stu-id="54775-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="54775-141">Tworzenie hello maszyny Wirtualnej i obsługi zasobów</span><span class="sxs-lookup"><span data-stu-id="54775-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="54775-142">Wszystkie zasoby muszą być zawarte w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54775-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="54775-143">toocreate grupę zasobów, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="54775-144">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="54775-145">[Zestawy dostępności](tutorial-availability-sets.md) ułatwić Ci maszyn wirtualnych hello toomaintain używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="54775-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="54775-146">toocreate dostępności ustawić, Dodaj tej funkcji po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="54775-147">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="54775-148">A [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) jest wymagane toocommunicate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54775-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="54775-149">toocreate publicznego adresu IP dla maszyny wirtualnej hello, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="54775-150">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="54775-151">Maszyna wirtualna musi należeć do podsieci [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54775-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="54775-152">toocreate sieci wirtualnej, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="54775-153">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="54775-154">tooadd podsieci sieci wirtualnej w toohello, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="54775-155">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="54775-156">Maszyna wirtualna musi toocommunicate interfejsu sieciowego, na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54775-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="54775-157">toocreate interfejsu sieciowego, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="54775-158">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="54775-159">Teraz, gdy utworzono hello wszystkie pomocnicze zasoby, można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54775-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="54775-160">toocreate hello maszyny wirtualnej, należy dodać tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="54775-161">W tym samouczku tworzy maszynę wirtualną z wersją systemu operacyjnego Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="54775-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="54775-162">Zobacz toolearn więcej informacji o wybieraniu inne obrazy [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą programu Windows PowerShell i hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54775-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="54775-163">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="54775-164">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="54775-164">Perform management tasks</span></span>

<span data-ttu-id="54775-165">Podczas cyklu życia hello maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54775-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="54775-166">Ponadto można toocreate kodu tooautomate powtarzających się lub złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="54775-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="54775-167">Pobierz informacje o hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54775-167">Get information about hello VM</span></span>

1. <span data-ttu-id="54775-168">tooget informacji o maszynie wirtualnej hello, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="54775-169">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="54775-170">Zatrzymaj hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54775-170">Stop hello VM</span></span>

<span data-ttu-id="54775-171">Można zatrzymać maszynę wirtualną i zachować wszystkie jego ustawienia, ale nadal toobe naliczona opłata za go lub można zatrzymać maszyny wirtualnej i jej cofnąć.</span><span class="sxs-lookup"><span data-stu-id="54775-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="54775-172">Po cofnięciu przydziału maszyny wirtualnej, wszystkie zasoby skojarzone z nim są również zakończenia deallocated i rozliczeń dla niego.</span><span class="sxs-lookup"><span data-stu-id="54775-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="54775-173">Maszyna wirtualna hello toostop bez dealokowanie, Dodaj tej funkcji po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="54775-174">Maszyna wirtualna hello toodeallocate, zmienić kod toothis połączenia power_off hello:</span><span class="sxs-lookup"><span data-stu-id="54775-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="54775-175">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="54775-176">Uruchom hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54775-176">Start hello VM</span></span>

1. <span data-ttu-id="54775-177">toostart hello maszyny wirtualnej, należy dodać tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="54775-178">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="54775-179">Zmień rozmiar hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54775-179">Resize hello VM</span></span>

<span data-ttu-id="54775-180">Wiele aspektów wdrożenia należy uwzględnić przy podejmowaniu decyzji o rozmiarze dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54775-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="54775-181">Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="54775-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="54775-182">rozmiar hello toochange hello maszyny wirtualnej, Dodaj tej funkcji po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="54775-183">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="54775-184">Dodaj toohello dysku danych maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54775-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="54775-185">Maszyny wirtualne mogą mieć jeden lub więcej [dysków z danymi](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przechowywane jako wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="54775-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="54775-186">tooadd maszyny wirtualnej toohello dysku danych, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="54775-187">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="54775-188">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="54775-188">Delete resources</span></span>

<span data-ttu-id="54775-189">Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="54775-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="54775-190">Jeśli chcesz maszyn wirtualnych hello toodelete i wszystkich hello obsługi zasobów, wszystkie masz toodo jest grupa zasobów hello delete.</span><span class="sxs-lookup"><span data-stu-id="54775-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="54775-191">grupy zasobów hello toodelete i wszystkie zasoby, Dodaj tę funkcję po hello zmienne hello .py pliku:</span><span class="sxs-lookup"><span data-stu-id="54775-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="54775-192">Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:</span><span class="sxs-lookup"><span data-stu-id="54775-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="54775-193">Zapisz *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="54775-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="54775-194">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="54775-194">Run hello application</span></span>

1. <span data-ttu-id="54775-195">toorun hello aplikacji konsoli, kliknij przycisk **Start** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54775-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="54775-196">Naciśnij klawisz **Enter** po zwróceniu hello stanu każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="54775-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="54775-197">W hello informacje o stanie, powinna zostać wyświetlona **zakończyło się pomyślnie** stan inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="54775-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="54775-198">Po utworzeniu maszyny wirtualnej hello masz hello możliwości toodelete wszystkie zasoby hello utworzonych przez Ciebie.</span><span class="sxs-lookup"><span data-stu-id="54775-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="54775-199">Przed naciśnięciem przycisku **Enter** toostart usuwanie zasobów, można wykonać kilka minut tooverify ich tworzenie w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="54775-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="54775-200">Jeśli ma hello Otwieranie portalu Azure, może być toorefresh hello bloku toosee nowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="54775-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="54775-201">Należy trwa około pięciu minut, zanim ta toorun aplikacji konsoli całkowicie od początku toofinish.</span><span class="sxs-lookup"><span data-stu-id="54775-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="54775-202">Może upłynąć kilka minut po aplikacja hello zakończy się przed wszystkimi zasobami hello i grupy zasobów hello są usuwane.</span><span class="sxs-lookup"><span data-stu-id="54775-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="54775-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54775-203">Next steps</span></span>

- <span data-ttu-id="54775-204">Jeśli wystąpiły problemy z wdrażaniem hello, następnym krokiem będzie toolook na [Rozwiązywanie problemów z wdrożeniami grup zasobów z portalu Azure](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="54775-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="54775-205">Dowiedz się więcej o hello [biblioteka języka Python platformy Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="54775-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

