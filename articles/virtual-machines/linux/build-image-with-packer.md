---
title: "Tworzenie obrazów maszyn wirtualnych systemu Linux platformy Azure z pakujący | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać pakujący do tworzenia obrazów maszyn wirtualnych systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 49a74648bd3953647d581c4e7c548985c5000f17
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="fce90-103">Jak używać pakujący do tworzenia obrazów maszyny wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="fce90-103">How to use Packer to create Linux virtual machine images in Azure</span></span>
<span data-ttu-id="fce90-104">Każda maszyna wirtualna (VM) na platformie Azure jest tworzony z obrazu, który definiuje dystrybucji systemu Linux i wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fce90-104">Each virtual machine (VM) in Azure is created from an image that defines the Linux distribution and OS version.</span></span> <span data-ttu-id="fce90-105">Obrazy mogą obejmować wstępnie zainstalowane aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="fce90-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="fce90-106">Portalu Azure Marketplace zawiera wiele obrazów pierwszy i innych firm najczęściej używane dystrybucje i środowisk aplikacji, lub można utworzyć własne niestandardowe obrazy dostosowane do potrzeb użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fce90-106">The Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="fce90-107">W tym artykule szczegółowo przedstawiają, jak korzystać z narzędzia typu open source [pakujący](https://www.packer.io/) do definiowania i tworzenie niestandardowych obrazów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fce90-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="fce90-108">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fce90-108">Create Azure resource group</span></span>
<span data-ttu-id="fce90-109">Podczas procesu tworzenia pakujący tworzy tymczasowy zasobów Azure zbudował źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fce90-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="fce90-110">Aby przechwycić tego źródła do użycia jako obraz maszyny Wirtualnej, należy zdefiniować grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="fce90-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="fce90-111">Dane wyjściowe z procesu tworzenia pakujący znajduje się w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="fce90-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="fce90-112">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fce90-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fce90-113">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="fce90-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="fce90-114">Utwórz poświadczenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fce90-114">Create Azure credentials</span></span>
<span data-ttu-id="fce90-115">Pakujący jest uwierzytelniany w usłudze Azure przy użyciu nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="fce90-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="fce90-116">Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak pakujący.</span><span class="sxs-lookup"><span data-stu-id="fce90-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="fce90-117">Kontrolowanie i definiowanie uprawnień określające, jakie operacje nazwy głównej usługi można wykonać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fce90-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="fce90-118">Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i poświadczenia, które wymaga pakujący wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="fce90-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="fce90-119">Przykład danych wyjściowych z poprzedniego polecenia jest następujący:</span><span class="sxs-lookup"><span data-stu-id="fce90-119">An example of the output from the preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="fce90-120">Aby uwierzytelniać na platformie Azure, również należy uzyskać identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="fce90-120">To authenticate to Azure, you also need to obtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="fce90-121">Dane wyjściowe z tych dwóch poleceń należy użyć w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="fce90-121">You use the output from these two commands in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="fce90-122">Zdefiniuj szablon pakujący</span><span class="sxs-lookup"><span data-stu-id="fce90-122">Define Packer template</span></span>
<span data-ttu-id="fce90-123">Aby tworzyć obrazy, należy utworzyć szablon w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="fce90-123">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="fce90-124">W szablonie należy zdefiniować producentów i provisioners wykonujące procesu tworzenia rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="fce90-124">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="fce90-125">Ma pakujący [administracyjnej dla platformy Azure](https://www.packer.io/docs/builders/azure.html) który można zdefiniować zasobów platformy Azure, takich jak poświadczenia główne usługi utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="fce90-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="fce90-126">Utwórz plik o nazwie *ubuntu.json* i wklej następującą zawartość.</span><span class="sxs-lookup"><span data-stu-id="fce90-126">Create a file named *ubuntu.json* and paste the following content.</span></span> <span data-ttu-id="fce90-127">Wprowadź własne wartości dla następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="fce90-127">Enter your own values for the following:</span></span>

| <span data-ttu-id="fce90-128">Parametr</span><span class="sxs-lookup"><span data-stu-id="fce90-128">Parameter</span></span>                           | <span data-ttu-id="fce90-129">Gdzie można uzyskać</span><span class="sxs-lookup"><span data-stu-id="fce90-129">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="fce90-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="fce90-130">*client_id*</span></span>                         | <span data-ttu-id="fce90-131">Pierwszy wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *appId*</span><span class="sxs-lookup"><span data-stu-id="fce90-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="fce90-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="fce90-132">*client_secret*</span></span>                     | <span data-ttu-id="fce90-133">Drugi wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *hasła*</span><span class="sxs-lookup"><span data-stu-id="fce90-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="fce90-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="fce90-134">*tenant_id*</span></span>                         | <span data-ttu-id="fce90-135">Trzeci wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *dzierżawy*</span><span class="sxs-lookup"><span data-stu-id="fce90-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="fce90-136">*IDENTYFIKATOR_SUBSKRYPCJI*</span><span class="sxs-lookup"><span data-stu-id="fce90-136">*subscription_id*</span></span>                   | <span data-ttu-id="fce90-137">Dane wyjściowe z `az account show` polecenia</span><span class="sxs-lookup"><span data-stu-id="fce90-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="fce90-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="fce90-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="fce90-139">Nazwa grupy zasobów, utworzonego w pierwszym kroku</span><span class="sxs-lookup"><span data-stu-id="fce90-139">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="fce90-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="fce90-140">*managed_image_name*</span></span>                | <span data-ttu-id="fce90-141">Nazwa obrazu dysków zarządzanych w tworzonym</span><span class="sxs-lookup"><span data-stu-id="fce90-141">Name for the managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="fce90-142">Ten szablon tworzy obraz Ubuntu 16.04 LTS, instaluje NGINX, a następnie deprovisions maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fce90-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="fce90-143">Po rozwinięciu na ten szablon służy do poświadczeń użytkownika należy dostosować polecenie administracyjnej deprovisions agentem Azure, aby odczytać `-deprovision` zamiast `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="fce90-143">If you expand on this template to provision user credentials, adjust the provisioner command that deprovisions the Azure agent to read `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="fce90-144">`+user` Flagi usuwa wszystkie konta użytkowników ze źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fce90-144">The `+user` flag removes all user accounts from the source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="fce90-145">Utwórz obraz pakujący</span><span class="sxs-lookup"><span data-stu-id="fce90-145">Build Packer image</span></span>
<span data-ttu-id="fce90-146">Jeśli nie masz jeszcze pakujący zainstalowany na komputerze lokalnym [postępuj zgodnie z instrukcjami instalacji pakujący](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="fce90-146">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="fce90-147">Utworzyć obraz, określając pakujący Twojego pliku szablonu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fce90-147">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="fce90-148">Przykład danych wyjściowych z poprzedniego polecenia jest następujący:</span><span class="sxs-lookup"><span data-stu-id="fce90-148">An example of the output from the preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH to become available...
==> azure-arm: Connected to SSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! The waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able to login as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying the machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="fce90-149">Tworzenie maszyny Wirtualnej z obrazu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fce90-149">Create VM from Azure Image</span></span>
<span data-ttu-id="fce90-150">Można teraz utworzyć Maszynę wirtualną z obrazu z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fce90-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fce90-151">Określ obraz został utworzony z `--image` parametru.</span><span class="sxs-lookup"><span data-stu-id="fce90-151">Specify the Image you created with the `--image` parameter.</span></span> <span data-ttu-id="fce90-152">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* z *myPackerImage* i generuje klucze SSH, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="fce90-152">The following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fce90-153">Trwa kilka minut, aby utworzyć maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="fce90-153">It takes a few minutes to create the VM.</span></span> <span data-ttu-id="fce90-154">Po utworzeniu maszyny Wirtualnej, zanotuj `publicIpAddress` wyświetlanych przez wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fce90-154">Once the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="fce90-155">Ten adres jest używany do uzyskania dostępu do witryny NGINX za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="fce90-155">This address is used to access the NGINX site via a web browser.</span></span>

<span data-ttu-id="fce90-156">Aby zezwolić na ruch w sieci web do maszyny Wirtualnej, należy otworzyć port 80 z Internetu z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="fce90-156">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="fce90-157">Test maszyny Wirtualnej i NGINX</span><span class="sxs-lookup"><span data-stu-id="fce90-157">Test VM and NGINX</span></span>
<span data-ttu-id="fce90-158">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź `http://publicIpAddress` na pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="fce90-158">Now you can open a web browser and enter `http://publicIpAddress` in the address bar.</span></span> <span data-ttu-id="fce90-159">Podaj własny publicznego adresu IP z maszyny Wirtualnej utworzyć procesu.</span><span class="sxs-lookup"><span data-stu-id="fce90-159">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="fce90-160">Jak w poniższym przykładzie zostanie wyświetlona strona NGINX domyślne:</span><span class="sxs-lookup"><span data-stu-id="fce90-160">The default NGINX page is displayed as in the following example:</span></span>

![Domyślna witryna serwera NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="fce90-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fce90-162">Next steps</span></span>
<span data-ttu-id="fce90-163">W tym przykładzie użyto pakujący do utworzenia obrazu maszyny Wirtualnej z NGINX już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="fce90-163">In this example, you used Packer to create a VM image with NGINX already installed.</span></span> <span data-ttu-id="fce90-164">Można tego obrazu maszyny Wirtualnej będą widoczne obok istniejących przepływów pracy wdrażania, takie jak wdrożyć aplikację na maszyny wirtualne utworzone na podstawie obrazu z Ansible, Chef lub Puppet.</span><span class="sxs-lookup"><span data-stu-id="fce90-164">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="fce90-165">Dla szablonów pakujący dodatkowe przykładowe dla innych dystrybucjach systemu Linux, zobacz [tego repozytorium GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="fce90-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>