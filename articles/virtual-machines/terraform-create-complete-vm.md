---
title: "Tworzenie podstawowej infrastruktury na platformie Azure przy użyciu Terraform | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć zasobów platformy Azure przy użyciu Terraform"
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
ms.openlocfilehash: 9660a95b440c2e4311829979e270d9f10099f624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a>Tworzenie podstawowej infrastruktury na platformie Azure przy użyciu Terraform
W tym artykule opisano kroki należy wykonać, aby udostępnić maszynę wirtualną z podstawowej infrastruktury na platformie Azure. Dowiesz się, jak napisać skrypty Terraform oraz sposób wizualizacji zmiany przed wprowadzeniem w infrastrukturze chmury. Dowiesz również sposób tworzenia infrastruktury na platformie Azure przy użyciu Terraform.

Aby rozpocząć, Utwórz plik o nazwie \terraform_azure101.tf w edytorze tekstu wyboru (Visual Studio kodu/Sublime/Vim/itp.). Dokładną nazwę pliku nie jest ważna, ponieważ Terraform przyjmuje nazwę folderu, jako parametr: wszystkie skrypty w folderze zostanie wykonana. Wklej następujący kod w nowym pliku:

~~~~
# Configure the Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have to include this block
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
W `provider` sekcji skryptu, poinformuj Terraform do używania dostawcy usługi Azure do udostępniania zasobów w skrypcie. Można uzyskać wartości IDENTYFIKATOR_SUBSKRYPCJI, appId, hasło i tenant_id, zobacz [zainstalować i skonfigurować Terraform](terraform-install-configure.md) przewodnik. Po utworzeniu zmiennych środowiskowych dla wartości w tym bloku, nie trzeba uwzględnić go. 

`azurerm_resource_group` Zasobu powoduje, że Terraform, aby utworzyć nową grupę zasobów. Widać więcej typów zasobów, które są dostępne w Terraform w dalszej części tego artykułu.

## <a name="execute-the-script"></a>Uruchom skrypt
Po zapisaniu skryptu wyjść do wiersza polecenia/konsoli, a następnie wpisz następujące polecenie:
```
terraform init
```
Aby zainicjować dostawcy Terraform dla platformy Azure. Następnie wpisz następujące polecenie:
```
terraform plan terraformscripts
```
Przyjęto założenie, że `terraformscripts` to folder, w którym zapisano skryptu. My używamy `plan` Terraform polecenia, które sprawdza zasoby zdefiniowane w skryptach. Porównuje je ze zapisane przez Terraform informacji o stanie, a następnie generuje planowane wykonanie _bez_ faktycznie tworzenia zasobów na platformie Azure. 

Po wykonaniu poprzednich polecenia powinien zostać wyświetlony ekran podobny do następującego ekranu:

![Terraform plan](linux/media/terraform/tf_plan2.png)

Jeśli wszystko jest poprawna, należy udostępnić tej nowej grupy zasobów na platformie Azure, wykonując następujące czynności: 
```
terraform apply terraformscripts
```
W portalu Azure, zostanie wyświetlony nowy pustej grupy zasobów o nazwie `terraformtest`. W poniższej sekcji można dodać maszyny wirtualnej i infrastruktury pomocniczej dla tej maszyny wirtualnej do grupy zasobów.

## <a name="provision-an-ubuntu-vm-with-terraform"></a>Zapewnij maszyny Wirtualnej systemu Ubuntu z Terraform
Umożliwia rozszerzenie skryptu Terraform utworzyliśmy szczegółowe informacje, które są niezbędne do obsługi administracyjnej maszyny wirtualnej z systemem Ubuntu. Dostępne są następujące zasoby, które można udostępnić w następujących sekcjach:

* Sieć z pojedynczą podsiecią
* Karty interfejsu sieciowego 
* Konto magazynu z kontenera magazynu
* Publiczny adres IP
* Maszyny wirtualnej, która korzysta z poprzednich zasobów 

Dokładnego dokumentacja dla każdego z zasobów Azure Terraform, zobacz [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).

Pełna wersja [skrypcie inicjowania obsługi](#complete-terraform-script) jest również udostępniany jako udogodnienie.

### <a name="extend-the-terraform-script"></a>Rozszerzenie skryptu Terraform
Rozszerzenie skryptu, który został utworzony z następującymi zasobami: 
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
Poprzedni skrypt tworzy sieć wirtualną i podsieć w ramach tej sieci wirtualnej. Należy pamiętać, odwołanie do grupy zasobów już utworzone za pomocą "${azurerm_resource_group.helloterraform.name}" w definicji podsieci i sieci wirtualnej.

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
Poprzednie fragmenty kodu skryptu tworzenie publicznego adresu IP i utworzyć interfejsu sieciowego, który korzysta z publicznego adresu IP. Należy pamiętać, odwołania do subnet_id i public_ip_address_id. Terraform ma wbudowane narzędzie analizy zrozumienie, że interfejs sieciowy ma zależność na zasoby, które muszą zostać utworzone przed utworzeniem interfejsu sieciowego.

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
W tym miejscu, utworzono konto magazynu i kontener magazynu w ramach tego konta magazynu. To konto magazynu służy do przechowywania wirtualnych dysków twardych (VHD) dla maszyny wirtualnej, która ma zostać utworzony.

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
Na koniec poprzedniego fragmentu tworzy maszynę wirtualną, która wykorzystuje wszystkie zasoby, które są już udostępniane. Są one konta magazynu i kontener dla wirtualnego dysku twardego, karty sieciowej z publicznych adresów IP i podsieci, i grupy zasobów już utworzony. Należy pamiętać, właściwość vm_size, gdzie skryptu określa SKU A0 Azure.

### <a name="execute-the-script"></a>Uruchom skrypt
Pełna skrypt zapisane wyjść do wiersza polecenia/konsoli i wpisz następujące polecenie:
```
terraform apply terraformscripts
```
Po pewnym czasie zasoby, łącznie z maszyny wirtualnej, są wyświetlane w `terraformtest` grupy zasobów w portalu Azure.

## <a name="complete-terraform-script"></a>Zakończenie Terraform skryptu

Dla wygody poniżej znajdują się wykonania skryptu Terraform tego przepisy wszystkie infrastruktury omówione w tym artykule.

```
variable "resourcesname" {
  default = "helloterraform"
}

# Configure the Microsoft Azure Provider
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
Utworzono podstawowej infrastruktury na platformie Azure przy użyciu Terraform. Dla bardziej złożonych scenariuszy, w tym przykłady, których skalowania maszyn wirtualnych i usług równoważenia obciążenia Użyj zestawów, zobacz wiele [Terraform przykłady Azure](https://github.com/hashicorp/terraform/tree/master/examples). Aktualną listę obsługiwanych dostawców Azure, zobacz [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).
