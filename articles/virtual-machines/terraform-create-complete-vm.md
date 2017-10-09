---
title: "aaaCreate podstawowej infrastruktury na platformie Azure przy użyciu Terraform | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure zasobów przy użyciu Terraform"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 916a838c118f28b3fbd373188e0acb2afc655081
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Tworzenie podstawowej infrastruktury na platformie Azure przy użyciu Terraform
W tym artykule opisano kroki hello należy tooprovision tootake maszynę wirtualną z podstawowej infrastruktury na platformie Azure. Dowiesz się, jak skrypty Terraform toowrite i jak toovisualize hello zmiany przed były w infrastrukturze chmury. Ponadto dowiesz się jak toocreate infrastruktury na platformie Azure przy użyciu Terraform.

tooget pracę, Utwórz plik o nazwie \terraform_azure101.tf w edytorze tekstu wyboru (Visual Studio kodu/Sublime/Vim/itp.). Hello dokładną nazwę pliku hello nie jest ważne, ponieważ nazwa folderu hello jako parametr akceptuje Terraform: wszystkie skrypty w folderze hello są wykonywane. Wklej hello następującego kodu w nowym pliku hello:

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group 
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
W hello `provider` sekcji hello skryptu, poinformuj Azure dostawcy zasobów tooprovision Terraform toouse w skrypcie hello. wartości tooget IDENTYFIKATOR_SUBSKRYPCJI, appId, hasło i tenant_id, zobacz hello [zainstalować i skonfigurować Terraform](terraform-install-configure.md) przewodnik. Jeśli utworzono hello wartości zmiennych środowiskowych w tym bloku, nie potrzebujesz tooinclude go. 

Witaj `azurerm_resource_group` zasobu powoduje, że toocreate Terraform nową grupę zasobów. Widać więcej typów zasobów, które są dostępne w Terraform w dalszej części tego artykułu.

## <a name="execute-hello-script"></a>Witaj, uruchom skrypt
Po zapisaniu skryptu hello zakończyć toohello konsoli/polecenie, a następnie wpisz następujące hello:
```
terraform init
```
Dostawca Terraform tooinitialize dla platformy Azure. Następnie wpisz następujące hello:
```
terraform plan terraformscripts
```
Przyjęto założenie, że `terraformscripts` jest hello folder, gdzie hello skrypt został zapisany. My używamy hello `plan` Terraform polecenia, które analizuje hello zasoby zdefiniowane w hello skryptów. Ich porównuje informacje o stanie toohello zapisane przez Terraform, a następnie dane wyjściowe hello planowane wykonanie _bez_ faktycznie tworzenia zasobów na platformie Azure. 

Po wykonaniu hello poprzednie polecenie powinien zostać wyświetlony ekran podobny do następującego ekranu hello:

![Terraform plan](linux/media/terraform/tf_plan2.png)

Jeśli wszystko jest poprawna, należy udostępnić tej nowej grupy zasobów na platformie Azure, wykonując następujące hello: 
```
terraform apply terraformscripts
```
W portalu Azure hello, powinna zostać wyświetlona hello nowego pustej grupy zasobów o nazwie `terraformtest`. W następującej sekcji hello można dodać maszyny wirtualnej, a wszystkie hello obsługę infrastruktury dla danej grupy zasobów toohello maszyny wirtualnej.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Zapewnij maszyny Wirtualnej systemu Ubuntu z Terraform
Umożliwia rozszerzanie hello Terraform skryptu, który utworzyliśmy hello szczegółowe informacje, które są niezbędne tooprovision maszyny wirtualnej z systemem Ubuntu. zasoby Hello udostępnianie w hello następujące sekcje są:

* Sieć z pojedynczą podsiecią
* Karty interfejsu sieciowego 
* Konto magazynu z kontenera magazynu
* Publiczny adres IP
* Maszyny wirtualnej, która wykorzystuje wszystkie zasoby poprzedniej hello 

Dokładnego dokumentacja dla każdego z zasobów Azure Terraform hello znajduje się w temacie hello [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).

Pełna wersja hello Hello [skrypcie inicjowania obsługi](#complete-terraform-script) jest również udostępniany jako udogodnienie.

### <a name="extend-hello-terraform-script"></a>Rozszerzanie hello Terraform skryptu
Rozszerzanie hello skrypt, który został utworzony z hello następujące zasoby: 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
Witaj poprzedni skrypt tworzy sieć wirtualną i podsieć w ramach tej sieci wirtualnej. Należy pamiętać, grupy zasobów toohello odwołania hello, już utworzone za pomocą "${azurerm_resource_group.helloterraform.name}" w sieci wirtualnej hello i hello definicji podsieci.

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}
~~~~
wstawki skryptu z poprzedniej Hello tworzenie publicznego adresu IP i interfejsu sieciowego, który korzysta z publicznego adresu IP hello utworzony. Uwaga hello odwołania toosubnet_id i public_ip_address_id. Terraform ma wbudowane narzędzie analizy toounderstand hello ten interfejs sieciowy ma zależność hello zasobów tego toobe należy utworzyć przed utworzeniem hello hello interfejsu sieciowego.

~~~~
# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}
~~~~
W tym miejscu, utworzono konto magazynu i kontener magazynu w ramach tego konta magazynu. To konto magazynu służy do przechowywania wirtualnych dysków twardych (VHD) dla maszyny wirtualnej hello o toobe utworzony.

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
~~~~
Na koniec fragment poprzedniej hello tworzy maszyny wirtualnej, która wykorzystuje wszystkie zasoby hello już udostępniane. Są one konta magazynu i kontener dla wirtualnego dysku twardego, karty sieciowej z publicznych adresów IP i podsieci, i grupy zasobów hello utworzone. Należy pamiętać, właściwość vm_size hello, gdzie hello skryptu określa SKU A0 Azure.

### <a name="execute-hello-script"></a>Witaj, uruchom skrypt
Ze skryptem pełne hello zapisane zamknąć toohello wiersza polecenia/konsoli i wpisz następujące hello:
```
terraform apply terraformscripts
```
Po pewnym czasie hello zasoby, łącznie z maszyny wirtualnej, są wyświetlane w hello `terraformtest` grupy zasobów w hello portalu Azure.

## <a name="complete-terraform-script"></a>Zakończenie Terraform skryptu

Dla wygody poniżej znajdują się hello wykonania skryptu Terraform tego przepisy wszystkie infrastruktury hello omówione w tym artykule.

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure hello Microsoft Azure Provider
provider "azurerm" {
  subscription_id = "XXX"
  client_id       = "XXX"
  client_secret   = "XXX"
  tenant_id       = "XXX"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}

# create virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "tfvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "tfsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}


# create public IPs
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "TerraformDemo"
    }
}

# create network interface
resource "azurerm_network_interface" "helloterraformnic" {
    name = "tfni"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    ip_configuration {
        name = "testconfiguration1"
        subnet_id = "${azurerm_subnet.helloterraformsubnet.id}"
        private_ip_address_allocation = "static"
        private_ip_address = "10.0.2.5"
        public_ip_address_id = "${azurerm_public_ip.helloterraformips.id}"
    }
}

# create a random id
resource "random_id" "randomId" {
  byte_length = 4
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "tfstorage${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "westus"
    account_type = "Standard_LRS"

    tags {
        environment = "staging"
    }
}

# create storage container
resource "azurerm_storage_container" "helloterraformstoragestoragecontainer" {
    name = "vhd"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    storage_account_name = "${azurerm_storage_account.helloterraformstorage.name}"
    container_access_type = "private"
    depends_on = ["azurerm_storage_account.helloterraformstorage"]
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_A0"

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "14.04.2-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        vhd_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}${azurerm_storage_container.helloterraformstoragestoragecontainer.name}/myosdisk.vhd"
        caching = "ReadWrite"
        create_option = "FromImage"
    }

    os_profile {
        computer_name = "hostname"
        admin_username = "testadmin"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }

    tags {
        environment = "staging"
    }
}
```

## <a name="next-steps"></a>Następne kroki
Utworzono podstawowej infrastruktury na platformie Azure przy użyciu Terraform. Dla bardziej złożonych scenariuszy, w tym przykłady, których skalowania maszyn wirtualnych i usług równoważenia obciążenia Użyj zestawów, zobacz wiele [Terraform przykłady Azure](https://github.com/hashicorp/terraform/tree/master/examples). Aktualną listę obsługiwanych dostawców Azure, zobacz hello [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).
