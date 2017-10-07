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
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure przy użyciu języka Python

[Maszyny wirtualnej Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM), wymaga kilku obsługi zasobów platformy Azure. W tym artykule omówiono tworzenia, zarządzania i usuwania zasobów maszyny Wirtualnej przy użyciu języka Python. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie projektu programu Visual Studio
> * Instalowanie pakietów
> * Utwórz poświadczenia
> * Tworzenie zasobów
> * Wykonywanie zadań zarządzania
> * Usuwanie zasobów
> * Uruchamianie aplikacji hello

Trwa około 20 minut toodo następujące kroki.

## <a name="create-a-visual-studio-project"></a>Tworzenie projektu programu Visual Studio

1. Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Wybierz **programowania Python** na hello obciążeń strony, a następnie kliknij przycisk **zainstalować**. W podsumowaniu hello, można stwierdzić, że **Python 3 64-bitowych (3.6.0)** jest automatycznie wybrana. Jeśli zainstalowano program Visual Studio można dodać hello Python obciążenia przy użyciu hello uruchamiania usługi Visual Studio.
2. Po zainstalowaniu i uruchomieniem programu Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.
3. Kliknij przycisk **szablony** > **Python** > **aplikacji Python**, wprowadź *myPythonProject* dla nazwy hello Witaj projektu, wybierz lokalizację hello hello projektu, a następnie kliknij **OK**.

## <a name="install-packages"></a>Instalowanie pakietów

1. W Eksploratorze rozwiązań w obszarze *myPythonProject*, kliknij prawym przyciskiem myszy **środowiska Python**, a następnie wybierz **Dodaj środowisko wirtualne**.
2. Na ekranie powitania Dodawanie środowiska wirtualnego Zaakceptuj domyślną nazwę hello *env*, upewnij się, że *3,6 języka Python (64-bitowy)* został wybrany do hello interpreter podstawowy, a następnie kliknij przycisk **Utwórz**.
3. Kliknij prawym przyciskiem myszy hello *env* środowisko, które zostały utworzone, kliknij przycisk **zainstaluj pakiet języka Python**, wprowadź *azure* w hello pole wyszukiwania, a następnie naciśnij klawisz Enter.

Powinien zostać wyświetlony w oknie danych wyjściowych hello pakietów hello azure zostały pomyślnie zainstalowane. 

## <a name="create-credentials"></a>Utwórz poświadczenia

Przed rozpoczęciem tego kroku upewnij się, że masz [nazwy głównej usługi Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Należy również zarejestrować identyfikator aplikacji hello, klucz uwierzytelniania hello i identyfikator dzierżawcy hello, które należy w kolejnym kroku.

1. Otwórz *myPythonProject.py* pliku, który został utworzony, a następnie dodaj ten kod tooenable toorun Twojej aplikacji:

    ```python
    if __name__ == "__main__":
    ```

2. tooimport hello kodu, który jest wymagany, Dodaj te instrukcje góry toohello hello .py pliku:

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. Obok w hello .py pliku Dodaj zmienne po instrukcje importu hello toospecify wspólne wartości używane w hello kodu:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Zastąp **identyfikator subskrypcji** z identyfikatorem subskrypcji.

4. poświadczenia usługi Active Directory hello toocreate konieczność toomake żądań, Dodaj tej funkcji po hello zmienne hello .py pliku:

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Zastąp **identyfikator aplikacji**, **klucz uwierzytelniania**, i **identyfikator dzierżawcy** wartościami hello uprzednio zebrane podczas tworzenia usługi Azure Active Directory nazwy głównej usługi.

5. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Tworzenie zasobów
 
### <a name="initialize-management-clients"></a>Inicjowanie zarządzania klientami

Klienci zarządzania są potrzebne toocreate zasobów i zarządzanie nimi przy użyciu zestawu SDK Python hello na platformie Azure. toocreate hello zarządzania klientami, Dodaj ten kod w obszarze hello **Jeśli** instrukcji następnie końcem pliku .py hello:

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

### <a name="create-hello-vm-and-supporting-resources"></a>Tworzenie hello maszyny Wirtualnej i obsługi zasobów

Wszystkie zasoby muszą być zawarte w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).

1. toocreate grupę zasobów, Dodaj tę funkcję po hello zmienne hello .py pliku:

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Zestawy dostępności](tutorial-availability-sets.md) ułatwić Ci maszyn wirtualnych hello toomaintain używanych przez aplikację.

1. toocreate dostępności ustawić, Dodaj tej funkcji po hello zmienne hello .py pliku:
   
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

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

A [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) jest wymagane toocommunicate hello maszyny wirtualnej.

1. toocreate publicznego adresu IP dla maszyny wirtualnej hello, Dodaj tę funkcję po hello zmienne hello .py pliku:

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

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Maszyna wirtualna musi należeć do podsieci [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

1. toocreate sieci wirtualnej, Dodaj tę funkcję po hello zmienne hello .py pliku:

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

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd podsieci sieci wirtualnej w toohello, Dodaj tę funkcję po hello zmienne hello .py pliku:
    
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
        
4. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Maszyna wirtualna musi toocommunicate interfejsu sieciowego, na powitania sieci wirtualnej.

1. toocreate interfejsu sieciowego, Dodaj tę funkcję po hello zmienne hello .py pliku:

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

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Teraz, gdy utworzono hello wszystkie pomocnicze zasoby, można utworzyć maszyny wirtualnej.

1. toocreate hello maszyny wirtualnej, należy dodać tę funkcję po hello zmienne hello .py pliku:
   
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
    > W tym samouczku tworzy maszynę wirtualną z wersją systemu operacyjnego Windows Server hello. Zobacz toolearn więcej informacji o wybieraniu inne obrazy [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą programu Windows PowerShell i hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Wykonywanie zadań zarządzania

Podczas cyklu życia hello maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej. Ponadto można toocreate kodu tooautomate powtarzających się lub złożonych zadań.

### <a name="get-information-about-hello-vm"></a>Pobierz informacje o hello maszyny Wirtualnej

1. tooget informacji o maszynie wirtualnej hello, Dodaj tę funkcję po hello zmienne hello .py pliku:

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
2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Zatrzymaj hello maszyny Wirtualnej

Można zatrzymać maszynę wirtualną i zachować wszystkie jego ustawienia, ale nadal toobe naliczona opłata za go lub można zatrzymać maszyny wirtualnej i jej cofnąć. Po cofnięciu przydziału maszyny wirtualnej, wszystkie zasoby skojarzone z nim są również zakończenia deallocated i rozliczeń dla niego.

1. Maszyna wirtualna hello toostop bez dealokowanie, Dodaj tej funkcji po hello zmienne hello .py pliku:

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Maszyna wirtualna hello toodeallocate, zmienić kod toothis połączenia power_off hello:

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Uruchom hello maszyny Wirtualnej

1. toostart hello maszyny wirtualnej, należy dodać tę funkcję po hello zmienne hello .py pliku:

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Zmień rozmiar hello maszyny Wirtualnej

Wiele aspektów wdrożenia należy uwzględnić przy podejmowaniu decyzji o rozmiarze dla maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](sizes.md).

1. rozmiar hello toochange hello maszyny wirtualnej, Dodaj tej funkcji po hello zmienne hello .py pliku:

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

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Dodaj toohello dysku danych maszyny Wirtualnej

Maszyny wirtualne mogą mieć jeden lub więcej [dysków z danymi](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przechowywane jako wirtualne dyski twarde.

1. tooadd maszyny wirtualnej toohello dysku danych, Dodaj tę funkcję po hello zmienne hello .py pliku: 

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

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Usuwanie zasobów

Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne. Jeśli chcesz maszyn wirtualnych hello toodelete i wszystkich hello obsługi zasobów, wszystkie masz toodo jest grupa zasobów hello delete.

1. grupy zasobów hello toodelete i wszystkie zasoby, Dodaj tę funkcję po hello zmienne hello .py pliku:
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. Funkcja hello toocall, które zostały wcześniej dodane, Dodaj ten kod w obszarze hello **Jeśli** instrukcji na końcu pliku .py hello hello:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Zapisz *myPythonProject.py*.

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

1. toorun hello aplikacji konsoli, kliknij przycisk **Start** w programie Visual Studio.

2. Naciśnij klawisz **Enter** po zwróceniu hello stanu każdego zasobu. W hello informacje o stanie, powinna zostać wyświetlona **zakończyło się pomyślnie** stan inicjowania obsługi. Po utworzeniu maszyny wirtualnej hello masz hello możliwości toodelete wszystkie zasoby hello utworzonych przez Ciebie. Przed naciśnięciem przycisku **Enter** toostart usuwanie zasobów, można wykonać kilka minut tooverify ich tworzenie w hello portalu Azure. Jeśli ma hello Otwieranie portalu Azure, może być toorefresh hello bloku toosee nowych zasobów.  

    Należy trwa około pięciu minut, zanim ta toorun aplikacji konsoli całkowicie od początku toofinish. Może upłynąć kilka minut po aplikacja hello zakończy się przed wszystkimi zasobami hello i grupy zasobów hello są usuwane.


## <a name="next-steps"></a>Następne kroki

- Jeśli wystąpiły problemy z wdrażaniem hello, następnym krokiem będzie toolook na [Rozwiązywanie problemów z wdrożeniami grup zasobów z portalu Azure](../../resource-manager-troubleshoot-deployments-portal.md)
- Dowiedz się więcej o hello [biblioteka języka Python platformy Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

