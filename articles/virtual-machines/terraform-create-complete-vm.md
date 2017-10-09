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
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="25baa-103">Tworzenie podstawowej infrastruktury na platformie Azure przy użyciu Terraform</span><span class="sxs-lookup"><span data-stu-id="25baa-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="25baa-104">W tym artykule opisano kroki hello należy tooprovision tootake maszynę wirtualną z podstawowej infrastruktury na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="25baa-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="25baa-105">Dowiesz się, jak skrypty Terraform toowrite i jak toovisualize hello zmiany przed były w infrastrukturze chmury.</span><span class="sxs-lookup"><span data-stu-id="25baa-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="25baa-106">Ponadto dowiesz się jak toocreate infrastruktury na platformie Azure przy użyciu Terraform.</span><span class="sxs-lookup"><span data-stu-id="25baa-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="25baa-107">tooget pracę, Utwórz plik o nazwie \terraform_azure101.tf w edytorze tekstu wyboru (Visual Studio kodu/Sublime/Vim/itp.).</span><span class="sxs-lookup"><span data-stu-id="25baa-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="25baa-108">Hello dokładną nazwę pliku hello nie jest ważne, ponieważ nazwa folderu hello jako parametr akceptuje Terraform: wszystkie skrypty w folderze hello są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="25baa-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="25baa-109">Wklej hello następującego kodu w nowym pliku hello:</span><span class="sxs-lookup"><span data-stu-id="25baa-109">Paste hello following code in hello new file:</span></span>

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
<span data-ttu-id="25baa-110">W hello `provider` sekcji hello skryptu, poinformuj Azure dostawcy zasobów tooprovision Terraform toouse w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="25baa-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="25baa-111">wartości tooget IDENTYFIKATOR_SUBSKRYPCJI, appId, hasło i tenant_id, zobacz hello [zainstalować i skonfigurować Terraform](terraform-install-configure.md) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="25baa-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="25baa-112">Jeśli utworzono hello wartości zmiennych środowiskowych w tym bloku, nie potrzebujesz tooinclude go.</span><span class="sxs-lookup"><span data-stu-id="25baa-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="25baa-113">Witaj `azurerm_resource_group` zasobu powoduje, że toocreate Terraform nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="25baa-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="25baa-114">Widać więcej typów zasobów, które są dostępne w Terraform w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="25baa-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="25baa-115">Witaj, uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="25baa-115">Execute hello script</span></span>
<span data-ttu-id="25baa-116">Po zapisaniu skryptu hello zakończyć toohello konsoli/polecenie, a następnie wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="25baa-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
<span data-ttu-id="25baa-117">Dostawca Terraform tooinitialize dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25baa-117">tooinitialize Terraform provider for Azure.</span></span> <span data-ttu-id="25baa-118">Następnie wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="25baa-118">Then type hello following:</span></span>
```
terraform plan terraformscripts
```
<span data-ttu-id="25baa-119">Przyjęto założenie, że `terraformscripts` jest hello folder, gdzie hello skrypt został zapisany.</span><span class="sxs-lookup"><span data-stu-id="25baa-119">We assume that `terraformscripts` is hello folder where hello script was saved.</span></span> <span data-ttu-id="25baa-120">My używamy hello `plan` Terraform polecenia, które analizuje hello zasoby zdefiniowane w hello skryptów.</span><span class="sxs-lookup"><span data-stu-id="25baa-120">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="25baa-121">Ich porównuje informacje o stanie toohello zapisane przez Terraform, a następnie dane wyjściowe hello planowane wykonanie _bez_ faktycznie tworzenia zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="25baa-121">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="25baa-122">Po wykonaniu hello poprzednie polecenie powinien zostać wyświetlony ekran podobny do następującego ekranu hello:</span><span class="sxs-lookup"><span data-stu-id="25baa-122">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform plan](linux/media/terraform/tf_plan2.png)

<span data-ttu-id="25baa-124">Jeśli wszystko jest poprawna, należy udostępnić tej nowej grupy zasobów na platformie Azure, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="25baa-124">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply terraformscripts
```
<span data-ttu-id="25baa-125">W portalu Azure hello, powinna zostać wyświetlona hello nowego pustej grupy zasobów o nazwie `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="25baa-125">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="25baa-126">W następującej sekcji hello można dodać maszyny wirtualnej, a wszystkie hello obsługę infrastruktury dla danej grupy zasobów toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25baa-126">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="25baa-127">Zapewnij maszyny Wirtualnej systemu Ubuntu z Terraform</span><span class="sxs-lookup"><span data-stu-id="25baa-127">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="25baa-128">Umożliwia rozszerzanie hello Terraform skryptu, który utworzyliśmy hello szczegółowe informacje, które są niezbędne tooprovision maszyny wirtualnej z systemem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="25baa-128">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="25baa-129">zasoby Hello udostępnianie w hello następujące sekcje są:</span><span class="sxs-lookup"><span data-stu-id="25baa-129">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="25baa-130">Sieć z pojedynczą podsiecią</span><span class="sxs-lookup"><span data-stu-id="25baa-130">A network with a single subnet</span></span>
* <span data-ttu-id="25baa-131">Karty interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="25baa-131">A network interface card</span></span> 
* <span data-ttu-id="25baa-132">Konto magazynu z kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="25baa-132">A storage account with a storage container</span></span>
* <span data-ttu-id="25baa-133">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="25baa-133">A public IP</span></span>
* <span data-ttu-id="25baa-134">Maszyny wirtualnej, która wykorzystuje wszystkie zasoby poprzedniej hello</span><span class="sxs-lookup"><span data-stu-id="25baa-134">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="25baa-135">Dokładnego dokumentacja dla każdego z zasobów Azure Terraform hello znajduje się w temacie hello [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="25baa-135">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="25baa-136">Pełna wersja hello Hello [skrypcie inicjowania obsługi](#complete-terraform-script) jest również udostępniany jako udogodnienie.</span><span class="sxs-lookup"><span data-stu-id="25baa-136">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="25baa-137">Rozszerzanie hello Terraform skryptu</span><span class="sxs-lookup"><span data-stu-id="25baa-137">Extend hello Terraform script</span></span>
<span data-ttu-id="25baa-138">Rozszerzanie hello skrypt, który został utworzony z hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="25baa-138">Extend hello script that was created with hello following resources:</span></span> 
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
<span data-ttu-id="25baa-139">Witaj poprzedni skrypt tworzy sieć wirtualną i podsieć w ramach tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25baa-139">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="25baa-140">Należy pamiętać, grupy zasobów toohello odwołania hello, już utworzone za pomocą "${azurerm_resource_group.helloterraform.name}" w sieci wirtualnej hello i hello definicji podsieci.</span><span class="sxs-lookup"><span data-stu-id="25baa-140">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

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
<span data-ttu-id="25baa-141">wstawki skryptu z poprzedniej Hello tworzenie publicznego adresu IP i interfejsu sieciowego, który korzysta z publicznego adresu IP hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="25baa-141">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="25baa-142">Uwaga hello odwołania toosubnet_id i public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="25baa-142">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="25baa-143">Terraform ma wbudowane narzędzie analizy toounderstand hello ten interfejs sieciowy ma zależność hello zasobów tego toobe należy utworzyć przed utworzeniem hello hello interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="25baa-143">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

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
<span data-ttu-id="25baa-144">W tym miejscu, utworzono konto magazynu i kontener magazynu w ramach tego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="25baa-144">Here, you created a storage account and defined a storage container within that storage account.</span></span> <span data-ttu-id="25baa-145">To konto magazynu służy do przechowywania wirtualnych dysków twardych (VHD) dla maszyny wirtualnej hello o toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="25baa-145">This storage account is where you store virtual hard disks (VHDs) for hello virtual machine about toobe created.</span></span>

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
<span data-ttu-id="25baa-146">Na koniec fragment poprzedniej hello tworzy maszyny wirtualnej, która wykorzystuje wszystkie zasoby hello już udostępniane.</span><span class="sxs-lookup"><span data-stu-id="25baa-146">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="25baa-147">Są one konta magazynu i kontener dla wirtualnego dysku twardego, karty sieciowej z publicznych adresów IP i podsieci, i grupy zasobów hello utworzone.</span><span class="sxs-lookup"><span data-stu-id="25baa-147">They are a storage account and container for a VHD, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="25baa-148">Należy pamiętać, właściwość vm_size hello, gdzie hello skryptu określa SKU A0 Azure.</span><span class="sxs-lookup"><span data-stu-id="25baa-148">Note hello vm_size property, where hello script specifies an Azure A0 SKU.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="25baa-149">Witaj, uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="25baa-149">Execute hello script</span></span>
<span data-ttu-id="25baa-150">Ze skryptem pełne hello zapisane zamknąć toohello wiersza polecenia/konsoli i wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="25baa-150">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply terraformscripts
```
<span data-ttu-id="25baa-151">Po pewnym czasie hello zasoby, łącznie z maszyny wirtualnej, są wyświetlane w hello `terraformtest` grupy zasobów w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="25baa-151">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="25baa-152">Zakończenie Terraform skryptu</span><span class="sxs-lookup"><span data-stu-id="25baa-152">Complete Terraform script</span></span>

<span data-ttu-id="25baa-153">Dla wygody poniżej znajdują się hello wykonania skryptu Terraform tego przepisy wszystkie infrastruktury hello omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="25baa-153">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="25baa-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25baa-154">Next steps</span></span>
<span data-ttu-id="25baa-155">Utworzono podstawowej infrastruktury na platformie Azure przy użyciu Terraform.</span><span class="sxs-lookup"><span data-stu-id="25baa-155">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="25baa-156">Dla bardziej złożonych scenariuszy, w tym przykłady, których skalowania maszyn wirtualnych i usług równoważenia obciążenia Użyj zestawów, zobacz wiele [Terraform przykłady Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="25baa-156">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="25baa-157">Aktualną listę obsługiwanych dostawców Azure, zobacz hello [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="25baa-157">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
