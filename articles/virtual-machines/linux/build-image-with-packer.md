---
title: "toocreate aaaHow obrazów maszyn wirtualnych Azure Linux z pakujący | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse pakujący toocreate obrazów maszyn wirtualnych systemu Linux na platformie Azure"
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
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="0a875-103">Jak obrazy maszyny wirtualnej systemu Linux toocreate pakujący toouse na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0a875-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="0a875-104">Każda maszyna wirtualna (VM) na platformie Azure jest tworzony z obrazu, który definiuje hello dystrybucji systemu Linux i wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0a875-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="0a875-105">Obrazy mogą obejmować wstępnie zainstalowane aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="0a875-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="0a875-106">Hello Azure Marketplace zawiera wiele obrazów pierwszy i innych firm dla najczęściej używane dystrybucje i aplikacji w środowiskach, lub można utworzyć własne niestandardowe obrazy dostosowane tooyour potrzeb.</span><span class="sxs-lookup"><span data-stu-id="0a875-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="0a875-107">W tym artykule szczegółowo sposób toouse hello otworzyć narzędzie źródła [pakujący](https://www.packer.io/) toodefine i kompilacji niestandardowych obrazów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0a875-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="0a875-108">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0a875-108">Create Azure resource group</span></span>
<span data-ttu-id="0a875-109">W trakcie kompilacji hello pakujący tworzy tymczasowy zasobów platformy Azure zbudował hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0a875-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="0a875-110">toocapture, który źródła do użycia jako obraz maszyny Wirtualnej, należy zdefiniować grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="0a875-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="0a875-111">Witaj dane wyjściowe z procesu tworzenia pakujący hello są przechowywane w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="0a875-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="0a875-112">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0a875-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0a875-113">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="0a875-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="0a875-114">Utwórz poświadczenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0a875-114">Create Azure credentials</span></span>
<span data-ttu-id="0a875-115">Pakujący jest uwierzytelniany w usłudze Azure przy użyciu nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="0a875-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="0a875-116">Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak pakujący.</span><span class="sxs-lookup"><span data-stu-id="0a875-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="0a875-117">Kontrolowanie i definiowanie uprawnień hello toowhat operacji hello service principal można wykonywać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0a875-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="0a875-118">Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i dane wyjściowe hello poświadczeń pakujący musi:</span><span class="sxs-lookup"><span data-stu-id="0a875-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="0a875-119">Przykład danych wyjściowych hello z hello poprzedzających polecenia jest następujący:</span><span class="sxs-lookup"><span data-stu-id="0a875-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="0a875-120">tooauthenticate tooAzure, należy również tooobtain identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="0a875-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="0a875-121">W następnym krokiem hello jest używany hello dane wyjściowe tych dwóch poleceń.</span><span class="sxs-lookup"><span data-stu-id="0a875-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="0a875-122">Zdefiniuj szablon pakujący</span><span class="sxs-lookup"><span data-stu-id="0a875-122">Define Packer template</span></span>
<span data-ttu-id="0a875-123">obrazy toobuild tworzenia szablonu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="0a875-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="0a875-124">W szablonie hello definiować konstruktorów i provisioners wykonujące hello rzeczywisty proces kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0a875-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="0a875-125">Ma pakujący [administracyjnej dla platformy Azure](https://www.packer.io/docs/builders/azure.html) pozwala toodefine Azure zasoby, takie jak poświadczenia główne usługi hello utworzone w hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="0a875-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="0a875-126">Utwórz plik o nazwie *ubuntu.json* i Wklej powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="0a875-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="0a875-127">Wprowadź własne wartości dla następujących hello:</span><span class="sxs-lookup"><span data-stu-id="0a875-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="0a875-128">Parametr</span><span class="sxs-lookup"><span data-stu-id="0a875-128">Parameter</span></span>                           | <span data-ttu-id="0a875-129">Gdzie tooobtain</span><span class="sxs-lookup"><span data-stu-id="0a875-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="0a875-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="0a875-130">*client_id*</span></span>                         | <span data-ttu-id="0a875-131">Pierwszy wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *appId*</span><span class="sxs-lookup"><span data-stu-id="0a875-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="0a875-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="0a875-132">*client_secret*</span></span>                     | <span data-ttu-id="0a875-133">Drugi wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *hasła*</span><span class="sxs-lookup"><span data-stu-id="0a875-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="0a875-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="0a875-134">*tenant_id*</span></span>                         | <span data-ttu-id="0a875-135">Trzeci wiersz danych wyjściowych z `az ad sp` Utwórz polecenie - *dzierżawy*</span><span class="sxs-lookup"><span data-stu-id="0a875-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="0a875-136">*IDENTYFIKATOR_SUBSKRYPCJI*</span><span class="sxs-lookup"><span data-stu-id="0a875-136">*subscription_id*</span></span>                   | <span data-ttu-id="0a875-137">Dane wyjściowe z `az account show` polecenia</span><span class="sxs-lookup"><span data-stu-id="0a875-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="0a875-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="0a875-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="0a875-139">Nazwa grupy zasobów, utworzonego w pierwszym krokiem hello</span><span class="sxs-lookup"><span data-stu-id="0a875-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="0a875-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="0a875-140">*managed_image_name*</span></span>                | <span data-ttu-id="0a875-141">Nazwę hello dysków zarządzanych w obrazu, który jest tworzony</span><span class="sxs-lookup"><span data-stu-id="0a875-141">Name for hello managed disk image that is created</span></span> |


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

<span data-ttu-id="0a875-142">Ten szablon tworzy obraz Ubuntu 16.04 LTS, instaluje NGINX, a następnie deprovisions hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0a875-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="0a875-143">Po rozwinięciu tego szablonu tooprovision poświadczeń, Dostosuj polecenia administracyjnej hello czy deprovisions hello tooread agenta programu Azure `-deprovision` zamiast `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="0a875-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="0a875-144">Witaj `+user` flagi spowoduje usunięcie wszystkich kont użytkowników z hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0a875-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="0a875-145">Utwórz obraz pakujący</span><span class="sxs-lookup"><span data-stu-id="0a875-145">Build Packer image</span></span>
<span data-ttu-id="0a875-146">Jeśli nie masz jeszcze pakujący zainstalowany na komputerze lokalnym [wykonaj instrukcje dotyczące instalacji pakujący hello](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="0a875-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="0a875-147">Utwórz hello obraz, określając pakujący Twojego pliku szablonu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0a875-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="0a875-148">Przykład danych wyjściowych hello z hello poprzedzających polecenia jest następujący:</span><span class="sxs-lookup"><span data-stu-id="0a875-148">An example of hello output from hello preceding commands is as follows:</span></span>

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
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
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
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="0a875-149">Tworzenie maszyny Wirtualnej z obrazu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0a875-149">Create VM from Azure Image</span></span>
<span data-ttu-id="0a875-150">Można teraz utworzyć Maszynę wirtualną z obrazu z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0a875-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0a875-151">Określ obraz został utworzony z hello hello `--image` parametru.</span><span class="sxs-lookup"><span data-stu-id="0a875-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="0a875-152">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* z *myPackerImage* i generuje klucze SSH, jeśli jeszcze nie istnieje:</span><span class="sxs-lookup"><span data-stu-id="0a875-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="0a875-153">Może potrwać kilka minut hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0a875-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="0a875-154">Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0a875-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="0a875-155">Ten adres jest używany tooaccess hello NGINX lokacji za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="0a875-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="0a875-156">tooallow web tooreach ruch maszyny Wirtualnej, otwórz port 80 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="0a875-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="0a875-157">Test maszyny Wirtualnej i NGINX</span><span class="sxs-lookup"><span data-stu-id="0a875-157">Test VM and NGINX</span></span>
<span data-ttu-id="0a875-158">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź `http://publicIpAddress` na pasku adresu hello.</span><span class="sxs-lookup"><span data-stu-id="0a875-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="0a875-159">Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu.</span><span class="sxs-lookup"><span data-stu-id="0a875-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="0a875-160">Strona NGINX domyślne Hello jest wyświetlana tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0a875-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Domyślna witryna serwera NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="0a875-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0a875-162">Next steps</span></span>
<span data-ttu-id="0a875-163">W tym przykładzie użyto toocreate pakujący obrazu maszyny Wirtualnej z NGINX już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="0a875-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="0a875-164">Można użyć tego obrazu maszyny Wirtualnej będą widoczne obok istniejących przepływów pracy wdrażania, takie jak toodeploy Twojego tooVMs aplikacji utworzone na podstawie hello obrazu z Ansible, Chef lub Puppet.</span><span class="sxs-lookup"><span data-stu-id="0a875-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="0a875-165">Dla szablonów pakujący dodatkowe przykładowe dla innych dystrybucjach systemu Linux, zobacz [tego repozytorium GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="0a875-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>