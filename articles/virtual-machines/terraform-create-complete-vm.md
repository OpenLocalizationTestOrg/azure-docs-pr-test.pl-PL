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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="dcb37-103">Tworzenie podstawowej infrastruktury na platformie Azure przy użyciu Terraform</span><span class="sxs-lookup"><span data-stu-id="dcb37-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="dcb37-104">W tym artykule opisano kroki należy wykonać, aby udostępnić maszynę wirtualną z podstawowej infrastruktury na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb37-104">This article describes the steps you need to take to provision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="dcb37-105">Dowiesz się, jak napisać skrypty Terraform oraz sposób wizualizacji zmiany przed wprowadzeniem w infrastrukturze chmury.</span><span class="sxs-lookup"><span data-stu-id="dcb37-105">You will learn how to write Terraform scripts and how to visualize the changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="dcb37-106">Dowiesz również sposób tworzenia infrastruktury na platformie Azure przy użyciu Terraform.</span><span class="sxs-lookup"><span data-stu-id="dcb37-106">You also will learn how to create infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="dcb37-107">Aby rozpocząć, Utwórz plik o nazwie \terraform_azure101.tf w edytorze tekstu wyboru (Visual Studio kodu/Sublime/Vim/itp.).</span><span class="sxs-lookup"><span data-stu-id="dcb37-107">To get started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="dcb37-108">Dokładną nazwę pliku nie jest ważna, ponieważ Terraform przyjmuje nazwę folderu, jako parametr: wszystkie skrypty w folderze zostanie wykonana.</span><span class="sxs-lookup"><span data-stu-id="dcb37-108">The exact name of the file isn't important because Terraform accepts the folder name as a parameter: all scripts in the folder get executed.</span></span> <span data-ttu-id="dcb37-109">Wklej następujący kod w nowym pliku:</span><span class="sxs-lookup"><span data-stu-id="dcb37-109">Paste the following code in the new file:</span></span>

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
<span data-ttu-id="dcb37-110">W `provider` sekcji skryptu, poinformuj Terraform do używania dostawcy usługi Azure do udostępniania zasobów w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="dcb37-110">In the `provider` section of the script, you tell Terraform to use an Azure provider to provision resources in the script.</span></span> <span data-ttu-id="dcb37-111">Można uzyskać wartości IDENTYFIKATOR_SUBSKRYPCJI, appId, hasło i tenant_id, zobacz [zainstalować i skonfigurować Terraform](terraform-install-configure.md) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="dcb37-111">To get values for subscription_id, appId, password, and tenant_id, see the [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="dcb37-112">Po utworzeniu zmiennych środowiskowych dla wartości w tym bloku, nie trzeba uwzględnić go.</span><span class="sxs-lookup"><span data-stu-id="dcb37-112">If you have created environment variables for the values in this block, you don't need to include it.</span></span> 

<span data-ttu-id="dcb37-113">`azurerm_resource_group` Zasobu powoduje, że Terraform, aby utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="dcb37-113">The `azurerm_resource_group` resource instructs Terraform to create a new resource group.</span></span> <span data-ttu-id="dcb37-114">Widać więcej typów zasobów, które są dostępne w Terraform w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="dcb37-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-the-script"></a><span data-ttu-id="dcb37-115">Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="dcb37-115">Execute the script</span></span>
<span data-ttu-id="dcb37-116">Po zapisaniu skryptu wyjść do wiersza polecenia/konsoli, a następnie wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="dcb37-116">After you save the script, exit to the console/command line, and type the following:</span></span>
```
terraform init
```
<span data-ttu-id="dcb37-117">Aby zainicjować dostawcy Terraform dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb37-117">to initialize Terraform provider for Azure.</span></span> <span data-ttu-id="dcb37-118">Następnie wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="dcb37-118">Then type the following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="dcb37-119">Przyjęto założenie, że `terraformscripts` to folder, w którym zapisano skryptu.</span><span class="sxs-lookup"><span data-stu-id="dcb37-119">We assume that `terraformscripts` is the folder where the script was saved.</span></span> <span data-ttu-id="dcb37-120">My używamy `plan` Terraform polecenia, które sprawdza zasoby zdefiniowane w skryptach.</span><span class="sxs-lookup"><span data-stu-id="dcb37-120">We used the `plan` Terraform command, which looks at the resources defined in the scripts.</span></span> <span data-ttu-id="dcb37-121">Porównuje je ze zapisane przez Terraform informacji o stanie, a następnie generuje planowane wykonanie _bez_ faktycznie tworzenia zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb37-121">It compares them to the state information saved by Terraform and then outputs the planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="dcb37-122">Po wykonaniu poprzednich polecenia powinien zostać wyświetlony ekran podobny do następującego ekranu:</span><span class="sxs-lookup"><span data-stu-id="dcb37-122">After you execute the previous command, you should see something like the following screen:</span></span>

![Terraform plan](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="dcb37-124">Jeśli wszystko jest poprawna, należy udostępnić tej nowej grupy zasobów na platformie Azure, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dcb37-124">If everything looks correct, provision this new resource group in Azure by executing the following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="dcb37-125">W portalu Azure, zostanie wyświetlony nowy pustej grupy zasobów o nazwie `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="dcb37-125">In the Azure portal, you should see the new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="dcb37-126">W poniższej sekcji można dodać maszyny wirtualnej i infrastruktury pomocniczej dla tej maszyny wirtualnej do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="dcb37-126">In the following section, you add a virtual machine and all the supporting infrastructure for that virtual machine to the resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="dcb37-127">Zapewnij maszyny Wirtualnej systemu Ubuntu z Terraform</span><span class="sxs-lookup"><span data-stu-id="dcb37-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="dcb37-128">Umożliwia rozszerzenie skryptu Terraform utworzyliśmy szczegółowe informacje, które są niezbędne do obsługi administracyjnej maszyny wirtualnej z systemem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="dcb37-128">Let's extend the Terraform script we've created with the details that are necessary to provision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="dcb37-129">Dostępne są następujące zasoby, które można udostępnić w następujących sekcjach:</span><span class="sxs-lookup"><span data-stu-id="dcb37-129">The resources that you provision in the following sections are:</span></span>

* <span data-ttu-id="dcb37-130">Sieć z pojedynczą podsiecią</span><span class="sxs-lookup"><span data-stu-id="dcb37-130">A network with a single subnet</span></span>
* <span data-ttu-id="dcb37-131">Karty interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="dcb37-131">A network interface card</span></span> 
* <span data-ttu-id="dcb37-132">Konto magazynu z kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="dcb37-132">A storage account with a storage container</span></span>
* <span data-ttu-id="dcb37-133">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="dcb37-133">A public IP</span></span>
* <span data-ttu-id="dcb37-134">Maszyny wirtualnej, która korzysta z poprzednich zasobów</span><span class="sxs-lookup"><span data-stu-id="dcb37-134">A virtual machine that utilizes all the previous resources</span></span> 

<span data-ttu-id="dcb37-135">Dokładnego dokumentacja dla każdego z zasobów Azure Terraform, zobacz [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="dcb37-135">For thorough documentation for each of the Azure Terraform resources, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="dcb37-136">Pełna wersja [skrypcie inicjowania obsługi](#complete-terraform-script) jest również udostępniany jako udogodnienie.</span><span class="sxs-lookup"><span data-stu-id="dcb37-136">The full version of the [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-the-terraform-script"></a><span data-ttu-id="dcb37-137">Rozszerzenie skryptu Terraform</span><span class="sxs-lookup"><span data-stu-id="dcb37-137">Extend the Terraform script</span></span>
<span data-ttu-id="dcb37-138">Rozszerzenie skryptu, który został utworzony z następującymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="dcb37-138">Extend the script that was created with the following resources:</span></span> 
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
<span data-ttu-id="dcb37-139">Poprzedni skrypt tworzy sieć wirtualną i podsieć w ramach tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dcb37-139">The previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="dcb37-140">Należy pamiętać, odwołanie do grupy zasobów już utworzone za pomocą "${azurerm_resource_group.helloterraform.name}" w definicji podsieci i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dcb37-140">Note the reference to the resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both the virtual network and the subnet definition.</span></span>

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
<span data-ttu-id="dcb37-141">Poprzednie fragmenty kodu skryptu tworzenie publicznego adresu IP i utworzyć interfejsu sieciowego, który korzysta z publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="dcb37-141">The previous script snippets create a public IP and a network interface that makes use of the public IP created.</span></span> <span data-ttu-id="dcb37-142">Należy pamiętać, odwołania do subnet_id i public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="dcb37-142">Note the references to subnet_id and public_ip_address_id.</span></span> <span data-ttu-id="dcb37-143">Terraform ma wbudowane narzędzie analizy zrozumienie, że interfejs sieciowy ma zależność na zasoby, które muszą zostać utworzone przed utworzeniem interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="dcb37-143">Terraform has built-in intelligence to understand that the network interface has a dependency on the resources that need to be created before the creation of the network interface.</span></span>

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
<span data-ttu-id="dcb37-144">W tym miejscu, utworzono konto magazynu i kontener magazynu w ramach tego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="dcb37-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="dcb37-145">To konto magazynu służy do przechowywania wirtualnych dysków twardych (VHD) dla maszyny wirtualnej, która ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="dcb37-145">This storage account is where you store virtual hard disks (VHDs) for the virtual machine about to be created.</span></span>

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
<span data-ttu-id="dcb37-146">Na koniec poprzedniego fragmentu tworzy maszynę wirtualną, która wykorzystuje wszystkie zasoby, które są już udostępniane.</span><span class="sxs-lookup"><span data-stu-id="dcb37-146">Finally, the previous snippet creates a virtual machine that utilizes all the resources provisioned already.</span></span> <span data-ttu-id="dcb37-147">Są one konta magazynu i kontener dla wirtualnego dysku twardego, karty sieciowej z publicznych adresów IP i podsieci, i grupy zasobów już utworzony.</span><span class="sxs-lookup"><span data-stu-id="dcb37-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and the resource group you already created.</span></span> <span data-ttu-id="dcb37-148">Należy pamiętać, właściwość vm_size, gdzie skryptu określa SKU A0 Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb37-148">Note the vm_size property, where the script specifies an Azure A0 SKU.</span></span>

### <a name="execute-the-script"></a><span data-ttu-id="dcb37-149">Uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="dcb37-149">Execute the script</span></span>
<span data-ttu-id="dcb37-150">Pełna skrypt zapisane wyjść do wiersza polecenia/konsoli i wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="dcb37-150">With the full script saved, exit to the console/command line and type the following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="dcb37-151">Po pewnym czasie zasoby, łącznie z maszyny wirtualnej, są wyświetlane w `terraformtest` grupy zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb37-151">After some time, the resources, including a virtual machine, appear in the `terraformtest` resource group in the Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="dcb37-152">Zakończenie Terraform skryptu</span><span class="sxs-lookup"><span data-stu-id="dcb37-152">Complete Terraform script</span></span>

<span data-ttu-id="dcb37-153">Dla wygody poniżej znajdują się wykonania skryptu Terraform tego przepisy wszystkie infrastruktury omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="dcb37-153">For your convenience, below is the complete Terraform script that provisions all of the infrastructure discussed in this article.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dcb37-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dcb37-154">Next steps</span></span>
<span data-ttu-id="dcb37-155">Utworzono podstawowej infrastruktury na platformie Azure przy użyciu Terraform.</span><span class="sxs-lookup"><span data-stu-id="dcb37-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="dcb37-156">Dla bardziej złożonych scenariuszy, w tym przykłady, których skalowania maszyn wirtualnych i usług równoważenia obciążenia Użyj zestawów, zobacz wiele [Terraform przykłady Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="dcb37-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="dcb37-157">Aktualną listę obsługiwanych dostawców Azure, zobacz [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="dcb37-157">For an up-to-date list of supported Azure providers, see the [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
