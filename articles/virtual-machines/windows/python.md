---
title: "Tworzenie i zarządzanie nimi maszyny Wirtualnej systemu Windows na platformie Azure przy użyciu języka Python | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące sposobu korzystania z języka Python do tworzenia i zarządzania maszyny Wirtualnej systemu Windows na platformie Azure."
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
ms.openlocfilehash: bb777d41570d7b1dc97402d532519488912948e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="bedd9-103">Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="bedd9-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="bedd9-104">[Maszyny wirtualnej Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM), wymaga kilku obsługi zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bedd9-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="bedd9-105">W tym artykule omówiono tworzenia, zarządzania i usuwania zasobów maszyny Wirtualnej przy użyciu języka Python.</span><span class="sxs-lookup"><span data-stu-id="bedd9-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="bedd9-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="bedd9-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bedd9-107">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bedd9-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="bedd9-108">Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="bedd9-108">Install packages</span></span>
> * <span data-ttu-id="bedd9-109">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="bedd9-109">Create credentials</span></span>
> * <span data-ttu-id="bedd9-110">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="bedd9-110">Create resources</span></span>
> * <span data-ttu-id="bedd9-111">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="bedd9-111">Perform management tasks</span></span>
> * <span data-ttu-id="bedd9-112">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="bedd9-112">Delete resources</span></span>
> * <span data-ttu-id="bedd9-113">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bedd9-113">Run the application</span></span>

<span data-ttu-id="bedd9-114">Wykonaj te kroki trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="bedd9-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="bedd9-115">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bedd9-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="bedd9-116">Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="bedd9-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="bedd9-117">Wybierz **programowania Python** na stronie obciążeń, a następnie kliknij **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="bedd9-117">Select **Python development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="bedd9-118">Podsumowując, można stwierdzić, że **Python 3 64-bitowych (3.6.0)** jest automatycznie wybrana.</span><span class="sxs-lookup"><span data-stu-id="bedd9-118">In the summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="bedd9-119">Jeśli zainstalowano program Visual Studio można dodać obciążenia Python za pomocą składnika Uruchamianie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bedd9-119">If you have already installed Visual Studio, you can add the Python workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="bedd9-120">Po zainstalowaniu i uruchomieniem programu Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="bedd9-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="bedd9-121">Kliknij przycisk **szablony** > **Python** > **aplikacji Python**, wprowadź *myPythonProject* dla nazwy Projekt, wybierz lokalizację projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bedd9-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="bedd9-122">Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="bedd9-122">Install packages</span></span>

1. <span data-ttu-id="bedd9-123">W Eksploratorze rozwiązań w obszarze *myPythonProject*, kliknij prawym przyciskiem myszy **środowiska Python**, a następnie wybierz **Dodaj środowisko wirtualne**.</span><span class="sxs-lookup"><span data-stu-id="bedd9-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="bedd9-124">Na ekranie Dodawanie środowiska wirtualnego, zaakceptuj domyślną nazwę *env*, upewnij się, że *3,6 języka Python (64-bitowy)* został wybrany do interpreter podstawowy, a następnie kliknij przycisk **Utwórz** .</span><span class="sxs-lookup"><span data-stu-id="bedd9-124">On the Add Virtual Environment screen, accept the default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for the base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="bedd9-125">Kliknij prawym przyciskiem myszy *env* środowisko, które zostały utworzone, kliknij przycisk **zainstaluj pakiet języka Python**, wprowadź *azure* w polu wyszukiwania, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="bedd9-125">Right-click the *env* environment that you created, click **Install Python Package**, enter *azure* in the search box, and then press Enter.</span></span>

<span data-ttu-id="bedd9-126">Powinien zostać wyświetlony w oknie danych wyjściowych pakietów azure zostały pomyślnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="bedd9-126">You should see in the output windows that the azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="bedd9-127">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="bedd9-127">Create credentials</span></span>

<span data-ttu-id="bedd9-128">Przed rozpoczęciem tego kroku upewnij się, że masz [nazwy głównej usługi Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bedd9-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="bedd9-129">Należy również zarejestrować identyfikator aplikacji, klucz uwierzytelniania i Identyfikatora dzierżawy, które są potrzebne w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="bedd9-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="bedd9-130">Otwórz *myPythonProject.py* pliku, który został utworzony, a następnie dodaj ten kod, aby umożliwić aplikację do uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="bedd9-130">Open *myPythonProject.py* file that was created, and then add this code to enable your application to run:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="bedd9-131">Aby zaimportować kodu, który jest wymagany, Dodaj te instrukcje na początku pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-131">To import the code that is needed, add these statements to the top of the .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="bedd9-132">Następnie w pliku PY i Dodaj zmienne po instrukcje importu, tak aby określić wartości typowych używane w kodzie:</span><span class="sxs-lookup"><span data-stu-id="bedd9-132">Next in the .py file, add variables after the import statements to specify common values used in the code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="bedd9-133">Zastąp **identyfikator subskrypcji** z identyfikatorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bedd9-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="bedd9-134">Aby utworzyć poświadczenia usługi Active Directory, które są potrzebne do tworzenia żądań, Dodaj tej funkcji po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-134">To create the Active Directory credentials that you need to make requests, add this function after the variables in the .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="bedd9-135">Zastąp **identyfikator aplikacji**, **klucz uwierzytelniania**, i **identyfikator dzierżawcy** z wartościami, które wcześniej zebrane podczas tworzenia usługi Azure Active Directory podmiot zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bedd9-135">Replace **application-id**, **authentication-key**, and **tenant-id** with the values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="bedd9-136">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-136">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="bedd9-137">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="bedd9-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="bedd9-138">Inicjowanie zarządzania klientami</span><span class="sxs-lookup"><span data-stu-id="bedd9-138">Initialize management clients</span></span>

<span data-ttu-id="bedd9-139">Klienci zarządzania są potrzebne do tworzenia i zarządzania zasobami na platformie Azure przy użyciu zestawu SDK Python.</span><span class="sxs-lookup"><span data-stu-id="bedd9-139">Management clients are needed to create and manage resources using the Python SDK in Azure.</span></span> <span data-ttu-id="bedd9-140">Aby utworzyć zarządzania klientami, Dodaj ten kod w obszarze **Jeśli** instrukcji następnie końcem pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-140">To create the management clients, add this code under the **if** statement at then end of the .py file:</span></span>

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

### <a name="create-the-vm-and-supporting-resources"></a><span data-ttu-id="bedd9-141">Utwórz maszynę Wirtualną i obsługi zasobów</span><span class="sxs-lookup"><span data-stu-id="bedd9-141">Create the VM and supporting resources</span></span>

<span data-ttu-id="bedd9-142">Wszystkie zasoby muszą być zawarte w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bedd9-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="bedd9-143">Aby utworzyć grupę zasobów, należy dodać tej funkcji po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-143">To create a resource group, add this function after the variables in the .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="bedd9-144">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-144">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter to continue...')
    ```

<span data-ttu-id="bedd9-145">[Zestawy dostępności](tutorial-availability-sets.md) ułatwienia obsługi maszyn wirtualnych używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="bedd9-145">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

1. <span data-ttu-id="bedd9-146">Aby utworzyć zbiór dostępności, Dodaj tę funkcję po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-146">To create an availability set, add this function after the variables in the .py file:</span></span>
   
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

2. <span data-ttu-id="bedd9-147">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-147">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter to continue...')
    ```

<span data-ttu-id="bedd9-148">A [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) jest potrzebne do komunikowania się z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="bedd9-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

1. <span data-ttu-id="bedd9-149">Aby utworzyć publiczny adres IP dla maszyny wirtualnej, należy dodać tej funkcji po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-149">To create a public IP address for the virtual machine, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="bedd9-150">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-150">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="bedd9-151">Maszyna wirtualna musi należeć do podsieci [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bedd9-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="bedd9-152">Aby utworzyć sieć wirtualną, Dodaj tę funkcję po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-152">To create a virtual network, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="bedd9-153">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-153">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

3. <span data-ttu-id="bedd9-154">Aby dodać podsieci do sieci wirtualnej, należy dodać tę funkcję po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-154">To add a subnet to the virtual network, add this function after the variables in the .py file:</span></span>
    
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
        
4. <span data-ttu-id="bedd9-155">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-155">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="bedd9-156">Maszyna wirtualna musi komunikować się w sieci wirtualnej do interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="bedd9-156">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

1. <span data-ttu-id="bedd9-157">Aby utworzyć interfejsu sieciowego, należy dodać tej funkcji po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-157">To create a network interface, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="bedd9-158">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-158">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="bedd9-159">Teraz, gdy utworzono pomocnicze zasoby, można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bedd9-159">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="bedd9-160">Aby utworzyć maszynę wirtualną, Dodaj tę funkcję po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-160">To create the virtual machine, add this function after the variables in the .py file:</span></span>
   
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
    > <span data-ttu-id="bedd9-161">W tym samouczku tworzy maszynę wirtualną z wersją systemu operacyjnego Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bedd9-161">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="bedd9-162">Aby dowiedzieć się więcej o wybieraniu innych obrazów, zobacz [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą programu Windows PowerShell i interfejsu wiersza polecenia Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bedd9-162">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="bedd9-163">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-163">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="bedd9-164">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="bedd9-164">Perform management tasks</span></span>

<span data-ttu-id="bedd9-165">Podczas cyklu maszyny wirtualnej można uruchomić zadania zarządzania, takie jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bedd9-165">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="bedd9-166">Ponadto można utworzyć kod do automatyzowania zadań powtarzających się lub złożonych.</span><span class="sxs-lookup"><span data-stu-id="bedd9-166">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

### <a name="get-information-about-the-vm"></a><span data-ttu-id="bedd9-167">Uzyskiwanie informacji o Maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bedd9-167">Get information about the VM</span></span>

1. <span data-ttu-id="bedd9-168">Aby uzyskać informacje dotyczące maszyny wirtualnej, należy dodać tej funkcji po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-168">To get information about the virtual machine, add this function after the variables in the .py file:</span></span>

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
2. <span data-ttu-id="bedd9-169">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-169">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter to continue...')
    ```

### <a name="stop-the-vm"></a><span data-ttu-id="bedd9-170">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bedd9-170">Stop the VM</span></span>

<span data-ttu-id="bedd9-171">Należy zatrzymać maszynę wirtualną i zachować wszystkie jego ustawienia, ale nadal naliczane za jej lub można zatrzymać maszyny wirtualnej i jej cofnąć.</span><span class="sxs-lookup"><span data-stu-id="bedd9-171">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="bedd9-172">Po cofnięciu przydziału maszyny wirtualnej, wszystkie zasoby skojarzone z nim są również zakończenia deallocated i rozliczeń dla niego.</span><span class="sxs-lookup"><span data-stu-id="bedd9-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="bedd9-173">Aby zatrzymać maszynę wirtualną bez dealokowanie go, należy dodać tej funkcji po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-173">To stop the virtual machine without deallocating it, add this function after the variables in the .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="bedd9-174">Jeśli chcesz Cofnij Przydział maszyny wirtualnej, Zmień wywołanie power_off ten kod:</span><span class="sxs-lookup"><span data-stu-id="bedd9-174">If you want to deallocate the virtual machine, change the power_off call to this code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="bedd9-175">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-175">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="start-the-vm"></a><span data-ttu-id="bedd9-176">Uruchom maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="bedd9-176">Start the VM</span></span>

1. <span data-ttu-id="bedd9-177">Można uruchomić maszyny wirtualnej, należy dodać tę funkcję po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-177">To start the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="bedd9-178">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-178">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="resize-the-vm"></a><span data-ttu-id="bedd9-179">Zmień rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bedd9-179">Resize the VM</span></span>

<span data-ttu-id="bedd9-180">Wiele aspektów wdrożenia należy uwzględnić przy podejmowaniu decyzji o rozmiarze dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="bedd9-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="bedd9-181">Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="bedd9-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="bedd9-182">Aby zmienić rozmiar maszyny wirtualnej, należy dodać tę funkcję po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-182">To change the size of the virtual machine, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="bedd9-183">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-183">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter to continue...')
    ```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="bedd9-184">Dodaj dysk danych do maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="bedd9-184">Add a data disk to the VM</span></span>

<span data-ttu-id="bedd9-185">Maszyny wirtualne mogą mieć jeden lub więcej [dysków z danymi](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przechowywane jako wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="bedd9-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="bedd9-186">Aby dodać dysk z danymi do maszyny wirtualnej, należy dodać tej funkcji po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-186">To add a data disk to the virtual machine, add this function after the variables in the .py file:</span></span> 

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

2. <span data-ttu-id="bedd9-187">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-187">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter to continue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="bedd9-188">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="bedd9-188">Delete resources</span></span>

<span data-ttu-id="bedd9-189">Ponieważ naliczane są opłaty za zasoby używane na platformie Azure, zawsze jest dobrym rozwiązaniem, aby usunąć zasoby, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="bedd9-189">Because you are charged for resources used in Azure, it's always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="bedd9-190">Jeśli chcesz usunąć maszyn wirtualnych i pomocnicze zasoby, musisz wykonać będzie usunąć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="bedd9-190">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="bedd9-191">Aby usunąć grupę zasobów i wszystkie zasoby, Dodaj tę funkcję po zmiennych w pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-191">To delete the resource group and all resources, add this function after the variables in the .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="bedd9-192">Wywoływanie funkcji, które zostały wcześniej dodane, Dodaj ten kod w obszarze **Jeśli** instrukcji na końcu pliku .py:</span><span class="sxs-lookup"><span data-stu-id="bedd9-192">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="bedd9-193">Zapisz *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="bedd9-193">Save *myPythonProject.py*.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="bedd9-194">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bedd9-194">Run the application</span></span>

1. <span data-ttu-id="bedd9-195">Aby uruchomić aplikację konsoli, kliknij przycisk **Start** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bedd9-195">To run the console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="bedd9-196">Naciśnij klawisz **Enter** po zwróceniu stanu każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="bedd9-196">Press **Enter** after the status of each resource is returned.</span></span> <span data-ttu-id="bedd9-197">W informacjach dotyczących stanu powinna zostać wyświetlona **zakończyło się pomyślnie** stan inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="bedd9-197">In the status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="bedd9-198">Po utworzeniu maszyny wirtualnej, możesz mieć możliwość usunąć wszystkie zasoby, które należy utworzyć.</span><span class="sxs-lookup"><span data-stu-id="bedd9-198">After the virtual machine is created, you have the opportunity to delete all the resources that you create.</span></span> <span data-ttu-id="bedd9-199">Przed naciśnięciem przycisku **Enter** zacząć usuwanie zasobów może potrwać kilka minut, aby sprawdzić ich tworzenie w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bedd9-199">Before you press **Enter** to start deleting resources, you could take a few minutes to verify their creation in the Azure portal.</span></span> <span data-ttu-id="bedd9-200">Jeśli masz portalu Azure, Otwórz, może być konieczne odświeżyć bloku, aby zobaczyć nowe zasoby.</span><span class="sxs-lookup"><span data-stu-id="bedd9-200">If you have the Azure portal open, you might have to refresh the blade to see new resources.</span></span>  

    <span data-ttu-id="bedd9-201">Zakończ powinno zająć około pięciu minut dla tej aplikacji konsoli uruchomić zupełnie od początku.</span><span class="sxs-lookup"><span data-stu-id="bedd9-201">It should take about five minutes for this console application to run completely from start to finish.</span></span> <span data-ttu-id="bedd9-202">Może upłynąć kilka minut po aplikacji zostało zakończone przed wszystkie zasoby i grupy zasobów są usuwane.</span><span class="sxs-lookup"><span data-stu-id="bedd9-202">It may take several minutes after the application has finished before all the resources and the resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bedd9-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bedd9-203">Next steps</span></span>

- <span data-ttu-id="bedd9-204">Jeśli wystąpiły problemy dotyczące wdrożenia, następnym krokiem powinno być zapoznanie się z artykułem [Troubleshooting resource group deployments with Azure Portal](../../resource-manager-troubleshoot-deployments-portal.md) (Rozwiązywanie problemów z wdrożeniami grup zasobów za pomocą witryny Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="bedd9-204">If there were issues with the deployment, a next step would be to look at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="bedd9-205">Dowiedz się więcej o [biblioteka języka Python platformy Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="bedd9-205">Learn more about the [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

