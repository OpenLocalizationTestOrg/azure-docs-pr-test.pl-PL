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
ms.openlocfilehash: 52591009ee7cb906402b8bca2ce63794ac7afcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-basic-infrastructure-in-azure-by-using-terraform"></a><span data-ttu-id="ca629-103">Tworzenie podstawowej infrastruktury na platformie Azure przy użyciu Terraform</span><span class="sxs-lookup"><span data-stu-id="ca629-103">Create basic infrastructure in Azure by using Terraform</span></span>
<span data-ttu-id="ca629-104">W tym artykule opisano kroki hello należy tooprovision tootake maszynę wirtualną z podstawowej infrastruktury na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ca629-104">This article describes hello steps you need tootake tooprovision a virtual machine, together with underlying infrastructure, into Azure.</span></span> <span data-ttu-id="ca629-105">Dowiesz się, jak skrypty Terraform toowrite i jak toovisualize hello zmiany przed były w infrastrukturze chmury.</span><span class="sxs-lookup"><span data-stu-id="ca629-105">You will learn how toowrite Terraform scripts and how toovisualize hello changes before you make them in your cloud infrastructure.</span></span> <span data-ttu-id="ca629-106">Ponadto dowiesz się jak toocreate infrastruktury na platformie Azure przy użyciu Terraform.</span><span class="sxs-lookup"><span data-stu-id="ca629-106">You also will learn how toocreate infrastructure in Azure by using Terraform.</span></span>

<span data-ttu-id="ca629-107">tooget pracę, Utwórz plik o nazwie \terraform_azure101.tf w edytorze tekstu wyboru (Visual Studio kodu/Sublime/Vim/itp.).</span><span class="sxs-lookup"><span data-stu-id="ca629-107">tooget started, create a file called \terraform_azure101.tf in your text editor of choice (Visual Studio Code/Sublime/Vim/etc.).</span></span> <span data-ttu-id="ca629-108">Hello dokładną nazwę pliku hello nie jest ważne, ponieważ nazwa folderu hello jako parametr akceptuje Terraform: wszystkie skrypty w folderze hello są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="ca629-108">hello exact name of hello file isn't important because Terraform accepts hello folder name as a parameter: all scripts in hello folder get executed.</span></span> <span data-ttu-id="ca629-109">Wklej hello następującego kodu w nowym pliku hello:</span><span class="sxs-lookup"><span data-stu-id="ca629-109">Paste hello following code in hello new file:</span></span>

~~~~
# Configure hello Microsoft Azure Provider
# NOTE: if you defined these values as environment variables, you do not have tooinclude this block
provider "azurerm" {
  subscription_id = "your_subscription_id_from_script_execution"
  client_id       = "your_appId_from_script_execution"
  client_secret   = "your_password_from_script_execution"
  tenant_id       = "your_tenant_id_from_script_execution"
}

# create a resource group if it doesn't exist
resource "azurerm_resource_group" "helloterraform" {
    name = "terraformtest"
    location = "West US"
}
~~~~
<span data-ttu-id="ca629-110">W hello `provider` sekcji hello skryptu, poinformuj Azure dostawcy zasobów tooprovision Terraform toouse w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="ca629-110">In hello `provider` section of hello script, you tell Terraform toouse an Azure provider tooprovision resources in hello script.</span></span> <span data-ttu-id="ca629-111">wartości tooget IDENTYFIKATOR_SUBSKRYPCJI, appId, hasło i tenant_id, zobacz hello [zainstalować i skonfigurować Terraform](terraform-install-configure.md) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="ca629-111">tooget values for subscription_id, appId, password, and tenant_id, see hello [Install and configure Terraform](terraform-install-configure.md) guide.</span></span> <span data-ttu-id="ca629-112">Jeśli utworzono hello wartości zmiennych środowiskowych w tym bloku, nie potrzebujesz tooinclude go.</span><span class="sxs-lookup"><span data-stu-id="ca629-112">If you have created environment variables for hello values in this block, you don't need tooinclude it.</span></span> 

<span data-ttu-id="ca629-113">Witaj `azurerm_resource_group` zasobu powoduje, że toocreate Terraform nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="ca629-113">hello `azurerm_resource_group` resource instructs Terraform toocreate a new resource group.</span></span> <span data-ttu-id="ca629-114">Widać więcej typów zasobów, które są dostępne w Terraform w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ca629-114">You can see more resource types that are available in Terraform later in this article.</span></span>

## <a name="execute-hello-script"></a><span data-ttu-id="ca629-115">Witaj, uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="ca629-115">Execute hello script</span></span>
<span data-ttu-id="ca629-116">Po zapisaniu skryptu hello zakończyć toohello konsoli/polecenie, a następnie wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ca629-116">After you save hello script, exit toohello console/command line, and type hello following:</span></span>
```
terraform init
```
 <span data-ttu-id="ca629-117">Dostawca Terraform hello tooinitialize dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca629-117">tooinitialize hello Terraform provider for Azure.</span></span> <span data-ttu-id="ca629-118">Zmień katalog hello zbyt**terraformscripts**, i hello problem następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ca629-118">Then change hello directory too**terraformscripts**, and issue hello following command:</span></span>
```
terraform plan
```
<span data-ttu-id="ca629-119">My używamy hello `plan` Terraform polecenia, które analizuje hello zasoby zdefiniowane w hello skryptów.</span><span class="sxs-lookup"><span data-stu-id="ca629-119">We used hello `plan` Terraform command, which looks at hello resources defined in hello scripts.</span></span> <span data-ttu-id="ca629-120">Ich porównuje informacje o stanie toohello zapisane przez Terraform, a następnie dane wyjściowe hello planowane wykonanie _bez_ faktycznie tworzenia zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ca629-120">It compares them toohello state information saved by Terraform and then outputs hello planned execution _without_ actually creating resources in Azure.</span></span> 

<span data-ttu-id="ca629-121">Po wykonaniu hello poprzednie polecenie powinien zostać wyświetlony ekran podobny do następującego ekranu hello:</span><span class="sxs-lookup"><span data-stu-id="ca629-121">After you execute hello previous command, you should see something like hello following screen:</span></span>

![Terraform plan](./media/terraform/tf_plan2.png)

<span data-ttu-id="ca629-123">Jeśli wszystko jest poprawna, należy udostępnić tej nowej grupy zasobów na platformie Azure, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ca629-123">If everything looks correct, provision this new resource group in Azure by executing hello following:</span></span> 
```
terraform apply
```
<span data-ttu-id="ca629-124">W portalu Azure hello, powinna zostać wyświetlona hello nowego pustej grupy zasobów o nazwie `terraformtest`.</span><span class="sxs-lookup"><span data-stu-id="ca629-124">In hello Azure portal, you should see hello new empty resource group called `terraformtest`.</span></span> <span data-ttu-id="ca629-125">W następującej sekcji hello można dodać maszyny wirtualnej, a wszystkie hello obsługę infrastruktury dla danej grupy zasobów toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ca629-125">In hello following section, you add a virtual machine and all hello supporting infrastructure for that virtual machine toohello resource group.</span></span>

## <a name="provision-an-ubuntu-vm-with-terraform"></a><span data-ttu-id="ca629-126">Zapewnij maszyny Wirtualnej systemu Ubuntu z Terraform</span><span class="sxs-lookup"><span data-stu-id="ca629-126">Provision an Ubuntu VM with Terraform</span></span>
<span data-ttu-id="ca629-127">Umożliwia rozszerzanie hello Terraform skryptu, który utworzyliśmy hello szczegółowe informacje, które są niezbędne tooprovision maszyny wirtualnej z systemem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ca629-127">Let's extend hello Terraform script we've created with hello details that are necessary tooprovision a virtual machine running Ubuntu.</span></span> <span data-ttu-id="ca629-128">zasoby Hello udostępnianie w hello następujące sekcje są:</span><span class="sxs-lookup"><span data-stu-id="ca629-128">hello resources that you provision in hello following sections are:</span></span>

* <span data-ttu-id="ca629-129">Sieć z pojedynczą podsiecią</span><span class="sxs-lookup"><span data-stu-id="ca629-129">A network with a single subnet</span></span>
* <span data-ttu-id="ca629-130">Karty interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="ca629-130">A network interface card</span></span> 
* <span data-ttu-id="ca629-131">Konto magazynu dla hello diagnostyki maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ca629-131">A storage account for hello virtual machine diagnostics</span></span>
* <span data-ttu-id="ca629-132">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="ca629-132">A public IP</span></span>
* <span data-ttu-id="ca629-133">Maszyny wirtualnej, która wykorzystuje wszystkie zasoby poprzedniej hello</span><span class="sxs-lookup"><span data-stu-id="ca629-133">A virtual machine that utilizes all hello previous resources</span></span> 

<span data-ttu-id="ca629-134">Dokładnego dokumentacja dla każdego z zasobów Azure Terraform hello znajduje się w temacie hello [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="ca629-134">For thorough documentation for each of hello Azure Terraform resources, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>

<span data-ttu-id="ca629-135">Pełna wersja hello Hello [skrypcie inicjowania obsługi](#complete-terraform-script) jest również udostępniany jako udogodnienie.</span><span class="sxs-lookup"><span data-stu-id="ca629-135">hello full version of hello [provisioning script](#complete-terraform-script) is also provided for convenience.</span></span>

### <a name="extend-hello-terraform-script"></a><span data-ttu-id="ca629-136">Rozszerzanie hello Terraform skryptu</span><span class="sxs-lookup"><span data-stu-id="ca629-136">Extend hello Terraform script</span></span>
<span data-ttu-id="ca629-137">Rozszerzanie hello skrypt, który został utworzony z hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="ca629-137">Extend hello script that was created with hello following resources:</span></span> 
~~~~
# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}
~~~~
<span data-ttu-id="ca629-138">Witaj poprzedni skrypt tworzy sieć wirtualną i podsieć w ramach tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ca629-138">hello previous script creates a virtual network and a subnet within that virtual network.</span></span> <span data-ttu-id="ca629-139">Należy pamiętać, grupy zasobów toohello odwołania hello, już utworzone za pomocą "${azurerm_resource_group.helloterraform.name}" w sieci wirtualnej hello i hello definicji podsieci.</span><span class="sxs-lookup"><span data-stu-id="ca629-139">Note hello reference toohello resource group you have created already via "${azurerm_resource_group.helloterraform.name}" in both hello virtual network and hello subnet definition.</span></span>

~~~~
# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="ca629-140">wstawki skryptu z poprzedniej Hello tworzenie publicznego adresu IP i interfejsu sieciowego, który korzysta z publicznego adresu IP hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="ca629-140">hello previous script snippets create a public IP and a network interface that makes use of hello public IP created.</span></span> <span data-ttu-id="ca629-141">Uwaga hello odwołania toosubnet_id i public_ip_address_id.</span><span class="sxs-lookup"><span data-stu-id="ca629-141">Note hello references toosubnet_id and public_ip_address_id.</span></span> <span data-ttu-id="ca629-142">Terraform ma wbudowane narzędzie analizy toounderstand hello ten interfejs sieciowy ma zależność hello zasobów tego toobe należy utworzyć przed utworzeniem hello hello interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="ca629-142">Terraform has built-in intelligence toounderstand that hello network interface has a dependency on hello resources that need toobe created before hello creation of hello network interface.</span></span>

~~~~
# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="ca629-143">W tym miejscu utworzono konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="ca629-143">Here, you created a storage account.</span></span> <span data-ttu-id="ca629-144">To konto magazynu jest, gdzie hello maszyny wirtualnej będzie przechowywać jego szczegóły diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="ca629-144">This storage account is where hello virtual machine will store its diagnostics details.</span></span>

~~~~
# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
~~~~
<span data-ttu-id="ca629-145">Na koniec fragment poprzedniej hello tworzy maszyny wirtualnej, która wykorzystuje wszystkie zasoby hello już udostępniane.</span><span class="sxs-lookup"><span data-stu-id="ca629-145">Finally, hello previous snippet creates a virtual machine that utilizes all hello resources provisioned already.</span></span> <span data-ttu-id="ca629-146">Są one konto magazynu diagnostyki maszyny wirtualnej hello, karty sieciowej z publicznych adresów IP i określonej podsieci i grupy zasobów hello utworzone.</span><span class="sxs-lookup"><span data-stu-id="ca629-146">They are a storage account for hello virtual machine diagnostics, a network interface with public IP and subnet specified, and hello resource group you already created.</span></span> <span data-ttu-id="ca629-147">Należy pamiętać, właściwość vm_size hello, gdzie hello skryptu Określa standardowy SKU DS1v2 Azure.</span><span class="sxs-lookup"><span data-stu-id="ca629-147">Note hello vm_size property, where hello script specifies an Azure Standard DS1v2 SKU.</span></span>

<span data-ttu-id="ca629-148">Jesteś toosupply wymagany klucz publiczny SSH.</span><span class="sxs-lookup"><span data-stu-id="ca629-148">You are required toosupply an SSH public key.</span></span> <span data-ttu-id="ca629-149">Umieść hello wartość klucza publicznego w sekcji hello **... WSTAW PUBLICZNY KLUCZ OPENSSH TUTAJ...**  powyżej.</span><span class="sxs-lookup"><span data-stu-id="ca629-149">Place hello public key value into hello section **... INSERT OPENSSH PUBLIC KEY HERE ...** above.</span></span> <span data-ttu-id="ca629-150">Można użyć istniejącego ssh parę kluczy lub wykonaj hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) lub [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) pary kluczy hello toogenerate dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ca629-150">You can use an existing ssh key pair or follow hello [Windows](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows) or [Linux/macOS](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys) documentation toogenerate hello key pair.</span></span>

### <a name="execute-hello-script"></a><span data-ttu-id="ca629-151">Witaj, uruchom skrypt</span><span class="sxs-lookup"><span data-stu-id="ca629-151">Execute hello script</span></span>
<span data-ttu-id="ca629-152">Ze skryptem pełne hello zapisane zamknąć toohello wiersza polecenia/konsoli i wpisz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ca629-152">With hello full script saved, exit toohello console/command line and type hello following:</span></span>
```
terraform apply
```
<span data-ttu-id="ca629-153">Po pewnym czasie hello zasoby, łącznie z maszyny wirtualnej, są wyświetlane w hello `terraformtest` grupy zasobów w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ca629-153">After some time, hello resources, including a virtual machine, appear in hello `terraformtest` resource group in hello Azure portal.</span></span>

## <a name="complete-terraform-script"></a><span data-ttu-id="ca629-154">Zakończenie Terraform skryptu</span><span class="sxs-lookup"><span data-stu-id="ca629-154">Complete Terraform script</span></span>

<span data-ttu-id="ca629-155">Dla wygody poniżej znajdują się hello wykonania skryptu Terraform tego przepisy wszystkie infrastruktury hello omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ca629-155">For your convenience, below is hello complete Terraform script that provisions all of hello infrastructure discussed in this article.</span></span>

```
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

# create a virtual network
resource "azurerm_virtual_network" "helloterraformnetwork" {
    name = "acctvn"
    address_space = ["10.0.0.0/16"]
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"

    tags {
        environment = "Terraform Demo"
    }
}

# create subnet
resource "azurerm_subnet" "helloterraformsubnet" {
    name = "acctsub"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    virtual_network_name = "${azurerm_virtual_network.helloterraformnetwork.name}"
    address_prefix = "10.0.2.0/24"
}

# create public IP
resource "azurerm_public_ip" "helloterraformips" {
    name = "terraformtestip"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    public_ip_address_allocation = "dynamic"

    tags {
        environment = "Terraform Demo"
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

    tags {
        environment = "Terraform Demo"
    }
}

# create a random id
resource "random_id" "randomId" {
  keepers = {
    # Generate a new id only when a new resource group is defined
    resource_group = "${azurerm_resource_group.helloterraform.name}"
  }

  byte_length = 8
}

# create storage account
resource "azurerm_storage_account" "helloterraformstorage" {
    name                = "diag${random_id.randomId.hex}"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    location = "West US"
    account_type = "Standard_LRS"

    tags {
        environment = "Terraform Demo"
    }
}

# create virtual machine
resource "azurerm_virtual_machine" "helloterraformvm" {
    name = "terraformvm"
    location = "West US"
    resource_group_name = "${azurerm_resource_group.helloterraform.name}"
    network_interface_ids = ["${azurerm_network_interface.helloterraformnic.id}"]
    vm_size = "Standard_DS1_v2"

    os_profile {
        computer_name = "hostname"
        admin_username = "azureuser"
        admin_password = ""
    }

    os_profile_linux_config {
        disable_password_authentication = true

        ssh_keys {
            path = "/home/azureuser/.ssh/authorized_keys"
            key_data = "... INSERT OPENSSH PUBLIC KEY HERE ..."
        }
    }

    storage_image_reference {
        publisher = "Canonical"
        offer = "UbuntuServer"
        sku = "16.04.0-LTS"
        version = "latest"
    }

    storage_os_disk {
        name = "myosdisk"
        managed_disk_type = "Premium_LRS"
        create_option = "FromImage"
    } 

    boot_diagnostics {
        enabled = "true"
        storage_uri = "${azurerm_storage_account.helloterraformstorage.primary_blob_endpoint}"
    }

    tags {
        environment = "Terraform Demo"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="ca629-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca629-156">Next steps</span></span>
<span data-ttu-id="ca629-157">Utworzono podstawowej infrastruktury na platformie Azure przy użyciu Terraform.</span><span class="sxs-lookup"><span data-stu-id="ca629-157">You have created basic infrastructure in Azure by using Terraform.</span></span> <span data-ttu-id="ca629-158">Dla bardziej złożonych scenariuszy, w tym przykłady, których skalowania maszyn wirtualnych i usług równoważenia obciążenia Użyj zestawów, zobacz wiele [Terraform przykłady Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="ca629-158">For more complex scenarios, including examples that use load balancers and virtual machine scale sets, see numerous [Terraform examples for Azure](https://github.com/hashicorp/terraform/tree/master/examples).</span></span> <span data-ttu-id="ca629-159">Aktualną listę obsługiwanych dostawców Azure, zobacz hello [dokumentacji Terraform](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="ca629-159">For an up-to-date list of supported Azure providers, see hello [Terraform documentation](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span>
