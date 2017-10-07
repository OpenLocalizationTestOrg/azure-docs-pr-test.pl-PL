---
title: "toocreate aaaHow obrazów maszyny Wirtualnej systemu Windows Azure z pakujący | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse pakujący toocreate obrazów maszyn wirtualnych systemu Windows na platformie Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="3fdab-103">Jak obrazy maszyny wirtualnej systemu Windows toocreate pakujący toouse na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3fdab-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="3fdab-104">Każda maszyna wirtualna (VM) na platformie Azure jest tworzony z obrazu, który definiuje hello dystrybucji systemu Windows i wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3fdab-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="3fdab-105">Obrazy mogą obejmować wstępnie zainstalowane aplikacje i konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="3fdab-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="3fdab-106">Hello Azure Marketplace zawiera wiele obrazów pierwszy i innych firm dla najbardziej typowych systemu operacyjnego i środowisk aplikacji albo można utworzyć własne niestandardowe obrazy dostosowane tooyour potrzeb.</span><span class="sxs-lookup"><span data-stu-id="3fdab-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="3fdab-107">W tym artykule szczegółowo sposób toouse hello otworzyć narzędzie źródła [pakujący](https://www.packer.io/) toodefine i kompilacji niestandardowych obrazów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3fdab-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="3fdab-108">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3fdab-108">Create Azure resource group</span></span>
<span data-ttu-id="3fdab-109">W trakcie kompilacji hello pakujący tworzy tymczasowy zasobów platformy Azure zbudował hello źródłowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3fdab-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="3fdab-110">toocapture, który źródła do użycia jako obraz maszyny Wirtualnej, należy zdefiniować grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="3fdab-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="3fdab-111">Witaj dane wyjściowe z procesu tworzenia pakujący hello są przechowywane w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3fdab-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="3fdab-112">Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="3fdab-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="3fdab-113">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="3fdab-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="3fdab-114">Utwórz poświadczenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3fdab-114">Create Azure credentials</span></span>
<span data-ttu-id="3fdab-115">Pakujący jest uwierzytelniany w usłudze Azure przy użyciu nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="3fdab-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="3fdab-116">Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak pakujący.</span><span class="sxs-lookup"><span data-stu-id="3fdab-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="3fdab-117">Kontrolowanie i definiowanie uprawnień hello toowhat operacji hello service principal można wykonywać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3fdab-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="3fdab-118">Utwórz usługę podmiotu zabezpieczeń z [AzureRmADServicePrincipal nowy](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) i przypisz uprawnienia dla toocreate główna usługi hello i zarządzanie zasobami za pomocą [AzureRmRoleAssignment nowy](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="3fdab-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="3fdab-119">tooauthenticate tooAzure, należy również tooobtain Azure identyfikatorów dzierżawcy i subskrypcji z [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="3fdab-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="3fdab-120">Za pomocą tych dwóch identyfikatorów w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="3fdab-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="3fdab-121">Zdefiniuj szablon pakujący</span><span class="sxs-lookup"><span data-stu-id="3fdab-121">Define Packer template</span></span>
<span data-ttu-id="3fdab-122">obrazy toobuild tworzenia szablonu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="3fdab-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="3fdab-123">W szablonie hello definiować konstruktorów i provisioners wykonujące hello rzeczywisty proces kompilacji.</span><span class="sxs-lookup"><span data-stu-id="3fdab-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="3fdab-124">Ma pakujący [administracyjnej dla platformy Azure](https://www.packer.io/docs/builders/azure.html) pozwala toodefine Azure zasoby, takie jak poświadczenia główne usługi hello utworzone w hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="3fdab-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="3fdab-125">Utwórz plik o nazwie *windows.json* i Wklej powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="3fdab-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="3fdab-126">Wprowadź własne wartości dla następujących hello:</span><span class="sxs-lookup"><span data-stu-id="3fdab-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="3fdab-127">Parametr</span><span class="sxs-lookup"><span data-stu-id="3fdab-127">Parameter</span></span>                           | <span data-ttu-id="3fdab-128">Gdzie tooobtain</span><span class="sxs-lookup"><span data-stu-id="3fdab-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="3fdab-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="3fdab-129">*client_id*</span></span>                         | <span data-ttu-id="3fdab-130">Identyfikator podmiotu zabezpieczeń usługi widoku z`$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="3fdab-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="3fdab-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="3fdab-131">*client_secret*</span></span>                     | <span data-ttu-id="3fdab-132">Hasło określone w`$securePassword`</span><span class="sxs-lookup"><span data-stu-id="3fdab-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="3fdab-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="3fdab-133">*tenant_id*</span></span>                         | <span data-ttu-id="3fdab-134">Dane wyjściowe z `$sub.TenantId` polecenia</span><span class="sxs-lookup"><span data-stu-id="3fdab-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="3fdab-135">*IDENTYFIKATOR_SUBSKRYPCJI*</span><span class="sxs-lookup"><span data-stu-id="3fdab-135">*subscription_id*</span></span>                   | <span data-ttu-id="3fdab-136">Dane wyjściowe z `$sub.SubscriptionId` polecenia</span><span class="sxs-lookup"><span data-stu-id="3fdab-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="3fdab-137">*Identyfikator obiektu*</span><span class="sxs-lookup"><span data-stu-id="3fdab-137">*object_id*</span></span>                         | <span data-ttu-id="3fdab-138">Identyfikator obiekt główny usługi widoku z`$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="3fdab-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="3fdab-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="3fdab-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="3fdab-140">Nazwa grupy zasobów, utworzonego w pierwszym krokiem hello</span><span class="sxs-lookup"><span data-stu-id="3fdab-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="3fdab-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="3fdab-141">*managed_image_name*</span></span>                | <span data-ttu-id="3fdab-142">Nazwę hello dysków zarządzanych w obrazu, który jest tworzony</span><span class="sxs-lookup"><span data-stu-id="3fdab-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="3fdab-143">Ten szablon tworzy Maszynę wirtualną systemu Windows Server 2016, instaluje usługi IIS, a następnie stanowi uogólnienie hello maszyny Wirtualnej przy użyciu narzędzia Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3fdab-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="3fdab-144">Utwórz obraz pakujący</span><span class="sxs-lookup"><span data-stu-id="3fdab-144">Build Packer image</span></span>
<span data-ttu-id="3fdab-145">Jeśli nie masz jeszcze pakujący zainstalowany na komputerze lokalnym [wykonaj instrukcje dotyczące instalacji pakujący hello](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="3fdab-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="3fdab-146">Utwórz hello obraz, określając pakujący Twojego pliku szablonu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3fdab-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="3fdab-147">Przykład danych wyjściowych hello z hello poprzedzających polecenia jest następujący:</span><span class="sxs-lookup"><span data-stu-id="3fdab-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="3fdab-148">Go zajmuje kilka minut hello toobuild pakujący maszynę Wirtualną, uruchom hello provisioners i czyszczenie hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3fdab-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="3fdab-149">Tworzenie maszyny Wirtualnej z obrazu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3fdab-149">Create VM from Azure Image</span></span>
<span data-ttu-id="3fdab-150">Ustaw nazwę użytkownika i hasło administratora dla maszyn wirtualnych hello z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="3fdab-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="3fdab-151">Można teraz utworzyć Maszynę wirtualną z obrazu z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3fdab-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="3fdab-152">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* z *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="3fdab-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="3fdab-153">Może potrwać kilka minut hello toocreate maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3fdab-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="3fdab-154">Test maszyny Wirtualnej i IIS</span><span class="sxs-lookup"><span data-stu-id="3fdab-154">Test VM and IIS</span></span>
<span data-ttu-id="3fdab-155">Uzyskaj hello publicznego adresu IP maszyny Wirtualnej z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="3fdab-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="3fdab-156">Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="3fdab-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="3fdab-157">W przeglądarce sieci web tooa można następnie wprowadzić hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="3fdab-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Domyślna witryna usług IIS](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="3fdab-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3fdab-159">Next steps</span></span>
<span data-ttu-id="3fdab-160">W tym przykładzie użyto toocreate pakujący obrazu maszyny Wirtualnej z już zainstalowanymi usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="3fdab-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="3fdab-161">Można użyć tego obrazu maszyny Wirtualnej będą widoczne obok istniejących przepływów pracy wdrażania, takie jak toodeploy Twojego tooVMs aplikacji utworzone na podstawie hello obrazu za pomocą usługi Team Services, Ansible, Chef lub Puppet.</span><span class="sxs-lookup"><span data-stu-id="3fdab-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="3fdab-162">Dla szablonów pakujący dodatkowe przykładowe dla innych dystrybucjach systemu Windows, temacie [tego repozytorium GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="3fdab-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>