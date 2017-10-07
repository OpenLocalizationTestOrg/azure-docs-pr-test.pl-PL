---
title: zestaw skalowania maszyny wirtualnej platformy Azure aaaCreate | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie skali maszyny wirtualnej systemu Linux lub Windows Azure ustawiony za pomocą interfejsu wiersza polecenia Azure, programu PowerShell, szablonu lub Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="296db-103">Tworzenie i wdrażanie zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="296db-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="296db-104">Zestawy skalowania maszyn wirtualnych ułatwiają możesz toodeploy i zarządzaj nimi wiele identycznych maszyn wirtualnych jako zestaw.</span><span class="sxs-lookup"><span data-stu-id="296db-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="296db-105">Zestawy skalowania w przypadku aplikacji o dużej skali zapewnić warstwy obliczeniowej wysoce skalowalnemu i dostosowania i obsługują obrazów platformy systemu Windows, Linux platformy obrazów niestandardowych obrazów i rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="296db-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="296db-106">Aby uzyskać więcej informacji na temat zestawów skalowania, zobacz [zestawy skalowania maszyny wirtualnej](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="296db-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="296db-107">Ten samouczek pokazuje, jak toocreate zestawu skalowania maszyn wirtualnych **bez** przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="296db-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="296db-108">Aby uzyskać informacje o sposobie toouse hello portalu Azure, zobacz [jak toocreate, zestawu skalowania maszyn wirtualnych, z portalu Azure hello](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="296db-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="296db-109">Aby uzyskać więcej informacji na temat zasobów usługi Azure Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="296db-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="296db-110">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="296db-110">Sign in tooAzure</span></span>

<span data-ttu-id="296db-111">Jeśli używasz interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub Azure PowerShell toocreate skali ustawiona, należy najpierw toosign w tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="296db-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="296db-112">Aby uzyskać więcej informacji na temat sposobu tooinstall, konfigurowanie i zaloguj się tooAzure z wiersza polecenia platformy Azure lub programu PowerShell, zobacz [wprowadzenie Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) lub [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="296db-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="296db-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="296db-113">Create a resource group</span></span>

<span data-ttu-id="296db-114">Należy najpierw toocreate grupę zasobów, której zestawu skalowania maszyn wirtualnych hello jest skojarzony z.</span><span class="sxs-lookup"><span data-stu-id="296db-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="296db-115">Tworzenie z interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="296db-115">Create from Azure CLI</span></span>

<span data-ttu-id="296db-116">Z wiersza polecenia platformy Azure można utworzyć ustawianie przy minimalnym nakładzie pracy skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="296db-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="296db-117">W przypadku pominięcia wartości domyślne, są one udostępniane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="296db-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="296db-118">Na przykład jeśli nie określisz żadnych informacji sieci wirtualnej, sieci wirtualnej jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="296db-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="296db-119">W przypadku pominięcia hello następujące części, ich są tworzone automatycznie:</span><span class="sxs-lookup"><span data-stu-id="296db-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="296db-120">Moduł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="296db-120">A load balancer</span></span>
- <span data-ttu-id="296db-121">Sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="296db-121">A virtual network</span></span>
- <span data-ttu-id="296db-122">Publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="296db-122">A public IP address</span></span>

<span data-ttu-id="296db-123">Podczas wybierania hello obraz maszyny wirtualnej, które mają toouse na zestaw skali maszyny wirtualnej hello, masz kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="296db-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="296db-124">URN</span><span class="sxs-lookup"><span data-stu-id="296db-124">URN</span></span>  
<span data-ttu-id="296db-125">Witaj identyfikator zasobu:</span><span class="sxs-lookup"><span data-stu-id="296db-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="296db-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="296db-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="296db-127">URN alias</span><span class="sxs-lookup"><span data-stu-id="296db-127">URN alias</span></span>  
<span data-ttu-id="296db-128">Witaj przyjaznej nazwy URN:</span><span class="sxs-lookup"><span data-stu-id="296db-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="296db-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="296db-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="296db-130">Identyfikator zasobu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="296db-130">Custom resource id</span></span>  
<span data-ttu-id="296db-131">Ścieżka tooan Hello zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="296db-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="296db-132">**/Subscriptions/Subscription-GUID/resourceGroups/MyResourceGroup/Providers/Microsoft.COMPUTE/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="296db-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="296db-133">Zasób sieci Web</span><span class="sxs-lookup"><span data-stu-id="296db-133">Web resource</span></span>  
<span data-ttu-id="296db-134">Ścieżka tooan Hello identyfikator URI protokołu HTTP:</span><span class="sxs-lookup"><span data-stu-id="296db-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="296db-135">**http://contoso.blob.Core.Windows.NET/vhds/osdiskimage.VHD**</span><span class="sxs-lookup"><span data-stu-id="296db-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="296db-136">Można uzyskać listę dostępnych obrazów z `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="296db-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="296db-137">Ustawianie skalowania maszyny wirtualnej toocreate, należy określić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="296db-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="296db-138">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="296db-138">Resource group</span></span> 
- <span data-ttu-id="296db-139">Nazwa</span><span class="sxs-lookup"><span data-stu-id="296db-139">Name</span></span>
- <span data-ttu-id="296db-140">Obraz systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="296db-140">Operating system image</span></span>
- <span data-ttu-id="296db-141">Informacje dotyczące uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="296db-141">Authentication information</span></span> 
 
<span data-ttu-id="296db-142">Witaj poniższy przykład tworzy zestaw skalowania podstawowej maszyny wirtualnej (ten krok może potrwać kilka minut).</span><span class="sxs-lookup"><span data-stu-id="296db-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="296db-143">Po zakończeniu działania polecenia hello trzeba będzie teraz Twojego zestaw utworzony skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="296db-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="296db-144">Adres IP hello tooget hello maszyny wirtualnej może być konieczne, dzięki czemu można łączyć tooit.</span><span class="sxs-lookup"><span data-stu-id="296db-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="296db-145">Wiele różnych informacji o maszynie wirtualnej hello (łącznie z adresem IP hello) można uzyskać z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="296db-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="296db-146">Utwórz na podstawie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="296db-146">Create from PowerShell</span></span>

<span data-ttu-id="296db-147">PowerShell jest bardziej skomplikowany toouse niż wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="296db-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="296db-148">Interfejsu wiersza polecenia Azure zawiera ustawienia domyślne dla zasobów związanych z siecią (na przykład usługi równoważenia obciążenia, adresów IP i sieci wirtualne), natomiast nie obsługuje programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="296db-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="296db-149">Odwołanie do obrazu przy użyciu programu PowerShell jest zbyt nieco bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="296db-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="296db-150">Obrazy można uzyskać z hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="296db-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="296db-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="296db-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="296db-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="296db-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="296db-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="296db-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="296db-154">Hello pracy polecenia cmdlet mogą być przekazywane w potoku w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="296db-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="296db-155">Poniżej przedstawiono przykład sposobu tooget wszystkie obrazy dla hello **zachodnie stany USA 2** region z wydawcą o nazwie hello **microsoft** w nim.</span><span class="sxs-lookup"><span data-stu-id="296db-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="296db-156">Witaj przepływ pracy tworzenia zestawu skali maszyny wirtualnej jest następujący:</span><span class="sxs-lookup"><span data-stu-id="296db-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="296db-157">Utwórz obiekt konfiguracji, który przechowuje informacje o zestawie skali hello.</span><span class="sxs-lookup"><span data-stu-id="296db-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="296db-158">Odwołanie hello podstawowy obraz systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="296db-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="296db-159">Skonfiguruj ustawienia systemu operacyjnego hello: uwierzytelnianie, prefiks nazwy maszyny Wirtualnej i użytkownika/hasło.</span><span class="sxs-lookup"><span data-stu-id="296db-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="296db-160">Konfigurowanie sieci.</span><span class="sxs-lookup"><span data-stu-id="296db-160">Configure networking.</span></span>
5. <span data-ttu-id="296db-161">Utwórz zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="296db-161">Create hello scale set.</span></span>

<span data-ttu-id="296db-162">W tym przykładzie tworzy zestaw na komputerze, na którym został zainstalowany program Windows Server 2016 podstawowe skalowania dwa wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="296db-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="296db-163">Przy użyciu obrazu niestandardowego maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="296db-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="296db-164">Jeśli tworzysz skali ustawiony na podstawie własny obraz niestandardowy, zamiast odwołujące się do obrazu maszyny wirtualnej z galerii hello hello _AzureRmVmssStorageProfile zestaw_ polecenie będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="296db-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="296db-165">Tworzenie na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="296db-165">Create from a template</span></span>

<span data-ttu-id="296db-166">Można wdrożyć skali maszyny wirtualnej ustawić przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="296db-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="296db-167">Można utworzyć własny szablon lub użyj jednej z hello [repozytorium szablonu](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="296db-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="296db-168">Szablony te można wdrożyć bezpośrednio tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="296db-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="296db-169">toocreate własny szablon, Utwórz plik tekstowy w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="296db-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="296db-170">Aby uzyskać ogólne informacje o tym, jak toocreate i dostosować szablon, zobacz [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="296db-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="296db-171">Dostępny jest przykładowy szablon [w serwisie GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="296db-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="296db-172">Aby uzyskać więcej informacji na temat sposobu toocreate i użyj tego przykładowe, zobacz [zestaw wielkości co najmniej](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="296db-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="296db-173">Utwórz w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="296db-173">Create from Visual Studio</span></span>

<span data-ttu-id="296db-174">Z programem Visual Studio można Tworzenie projektu grupy zasobów platformy Azure i dodać szablon tooit zestawu skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="296db-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="296db-175">Można wybrać, czy ma tooimport go z usługi GitHub lub hello Galeria aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="296db-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="296db-176">Wdrożenie skryptu PowerShell zostanie również wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="296db-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="296db-177">Aby uzyskać więcej informacji, zobacz [jak toocreate, zestawu skalowania maszyn wirtualnych, z programem Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="296db-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="296db-178">Utwórz na podstawie hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="296db-178">Create from hello Azure portal</span></span>

<span data-ttu-id="296db-179">Witaj portalu Azure oferują wygodny sposób tooquickly utworzyć zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="296db-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="296db-180">Aby uzyskać więcej informacji, zobacz [jak toocreate, zestawu skalowania maszyn wirtualnych, z portalu Azure hello](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="296db-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="296db-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="296db-181">Next steps</span></span>

<span data-ttu-id="296db-182">Dowiedz się więcej o [dysków z danymi](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="296db-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="296db-183">Dowiedz się, jak za[zarządzania aplikacjami](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="296db-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
