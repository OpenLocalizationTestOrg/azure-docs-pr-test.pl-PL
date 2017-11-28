---
title: "Korzyści Użyj hybrydowe platformy Azure dla okna serwera i klienta systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zmaksymalizować korzyści programu Windows Software Assurance w celu przełączenia lokalnej licencji Azure"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: 210635624946ddb293427167e9d476c377bcc9b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="f9860-103">Korzyści Użyj hybrydowe platformy Azure dla systemu Windows Server i klienta systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f9860-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="f9860-104">W przypadku klientów z Software Assurance korzyści użyć hybrydowego Azure umożliwia użyć lokalnego licencji systemu Windows Server i klienta systemu Windows i uruchamiania maszyn wirtualnych systemu Windows na platformie Azure taniego.</span><span class="sxs-lookup"><span data-stu-id="f9860-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you to use your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="f9860-105">Azure hybrydowego Użyj korzyści dla systemu Windows Server zawiera systemu Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f9860-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="f9860-106">Hybrydowe Użyj korzyści dla systemu Windows klienta usługi Azure obejmuje systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f9860-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="f9860-107">Aby uzyskać więcej informacji, zobacz [strony licencjonowania Azure hybrydowego Użyj korzyści](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="f9860-107">For more information, please see the [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="f9860-108">Azure hybrydowego Użyj korzyści dla klienta systemu Windows jest obecnie w wersji zapoznawczej za pomocą obrazu systemu Windows 10 w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9860-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using the Windows 10 image in the Azure Marketplace.</span></span> <span data-ttu-id="f9860-109">Tylko przedsiębiorstwa z systemem Windows 10 Enterprise E3/E5 dla poszczególnych użytkowników lub VDA systemu Windows dla każdego użytkownika (licencji subskrypcji użytkownika lub licencji subskrypcji użytkownika dodatku) kwalifikują się ("uprawniających licencji").</span><span class="sxs-lookup"><span data-stu-id="f9860-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-to-use-azure-hybrid-use-benefit"></a><span data-ttu-id="f9860-110">Sposoby używania korzyści Użyj hybrydowe platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f9860-110">Ways to use Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="f9860-111">Istnieje kilka różnych sposobów wdrażania maszyn wirtualnych systemu Windows z asysty Użyj hybrydowe platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="f9860-111">There are a couple of different ways to deploy Windows VMs with the Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="f9860-112">Można wdrożyć maszyn wirtualnych z [określonych obrazów Marketplace](#deploy-a-vm-using-the-azure-marketplace) , które są wstępnie skonfigurowane z Azure hybrydowego Użyj korzyści - systemu Windows Server 2016, systemu Windows Server 2012 R2, Windows Server 2012 i Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="f9860-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="f9860-113">Możesz [przekazać niestandardowe wirtualna](#upload-a-windows-vhd) i [wdrażanie przy użyciu szablonu usługi Resource Manager](#deploy-a-vm-via-resource-manager) lub [programu Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="f9860-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-the-azure-marketplace"></a><span data-ttu-id="f9860-114">Wdróż Maszynę wirtualną przy użyciu portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f9860-114">Deploy a VM using the Azure Marketplace</span></span>
<span data-ttu-id="f9860-115">Następujące obrazy są dostępne w witrynie Marketplace wstępnie skonfigurowaną korzyści Użyj hybrydowe platformy Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 i Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="f9860-115">Following images are available in the Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="f9860-116">Te obrazy można wdrażać bezpośrednio za pomocą witryny Azure Portal, szablonów usługi Resource Manager lub programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9860-116">These images can be deployed directly from the Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="f9860-117">Można wdrażać te obrazy bezpośrednio z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f9860-117">You can deploy these images directly from the Azure portal.</span></span> <span data-ttu-id="f9860-118">Do użycia w szablonach usługi Resource Manager i przy użyciu programu Azure PowerShell wyświetlić listę obrazów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f9860-118">For use in Resource Manager templates and with Azure PowerShell, view the list of images as follows:</span></span>

<span data-ttu-id="f9860-119">W systemie Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f9860-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="f9860-120">Wersja 2016 Datacenter 2016.127.20170406 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="f9860-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="f9860-121">Wersja 2012-R2-Datacenter 4.127.20170406 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="f9860-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="f9860-122">Wersja 2012 Datacenter 3.127.20170406 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="f9860-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="f9860-123">2.127.20170406 w wersji 2008 R2 SP1 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="f9860-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="f9860-124">Dla klienta systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="f9860-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="f9860-125">Przekazywanie wirtualnego dysku twardego Windows Server</span><span class="sxs-lookup"><span data-stu-id="f9860-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="f9860-126">Aby wdrożyć Maszynę wirtualną systemu Windows Server na platformie Azure, należy najpierw utworzyć wirtualny dysk twardy zawiera podstawowe kompilacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f9860-126">To deploy a Windows Server VM in Azure, you first need to create a VHD that contains your base Windows build.</span></span> <span data-ttu-id="f9860-127">Tego wirtualnego dysku twardego, należy odpowiednio przygotować za pomocą programu Sysprep przed przekazaniem go do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9860-127">This VHD must be appropriately prepared via Sysprep before you upload it to Azure.</span></span> <span data-ttu-id="f9860-128">Możesz [Dowiedz się więcej na temat wirtualnego dysku twardego wymagań i procesu Sysprep](upload-generalized-managed.md) i [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="f9860-128">You can [read more about the VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="f9860-129">Utwórz kopię zapasową maszyny Wirtualnej przed uruchomieniem programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="f9860-129">Back up the VM before running Sysprep.</span></span> 

<span data-ttu-id="f9860-130">Upewnij się, że masz [zainstalowany i skonfigurowany najnowsze programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f9860-130">Make sure you have [installed and configured the latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="f9860-131">Po przygotowaniu dysk VHD, przekazanie dysku VHD do używania konta usługi Azure Storage `Add-AzureRmVhd` polecenia cmdlet w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f9860-131">Once you have prepared your VHD, upload the VHD to your Azure Storage account using the `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="f9860-132">Microsoft SQL Server, SharePoint Server i Dynamics można również korzystać z programu Software Assurance licencjonowania.</span><span class="sxs-lookup"><span data-stu-id="f9860-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="f9860-133">Nadal musisz przygotować obraz systemu Windows Server instalowania składniki aplikacji i zapewnianie odpowiednio kluczy licencji, a następnie przekazywanie obrazu dysku na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f9860-133">You still need to prepare the Windows Server image by installing your application components and providing license keys accordingly, then uploading the disk image to Azure.</span></span> <span data-ttu-id="f9860-134">Zapoznaj się z dokumentacją odpowiedniego do uruchamiania narzędzia Sysprep z aplikacji, takich jak [zagadnienia dotyczące instalowania programu SQL Server za pomocą programu Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) lub [Utwórz obraz referencyjny programu SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9860-134">Review the appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="f9860-135">Można również uzyskać więcej informacji [przekazywanie wirtualnego dysku twardego do procesu systemu Azure](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="f9860-135">You can also read more about [uploading the VHD to Azure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="f9860-136">Wdróż Maszynę wirtualną za pomocą szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f9860-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="f9860-137">W szablonach usługi Resource Manager dodatkowy parametr dla `licenseType` można określić.</span><span class="sxs-lookup"><span data-stu-id="f9860-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="f9860-138">Możesz przeczytać dodatkowe informacje [tworzenia szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f9860-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="f9860-139">Po utworzeniu dysk VHD przekazany do platformy Azure, Edytuj szablon Menedżera zasobów, aby dołączyć typ licencji w ramach dostawcy obliczeń i wdrażania szablonu w zwykły:</span><span class="sxs-lookup"><span data-stu-id="f9860-139">Once you have your VHD uploaded to Azure, edit you Resource Manager template to include the license type as part of the compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="f9860-140">W systemie Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f9860-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="f9860-141">Dla klienta systemu Windows do użycia tylko z obrazu witryny Marketplace Azure:</span><span class="sxs-lookup"><span data-stu-id="f9860-141">For Windows Client to use with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="f9860-142">Wdróż Maszynę wirtualną za pomocą programu PowerShell — Szybki Start</span><span class="sxs-lookup"><span data-stu-id="f9860-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="f9860-143">Podczas wdrażania maszyny Wirtualnej systemu Windows Server za pomocą programu PowerShell, masz dodatkowy parametr dla `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="f9860-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="f9860-144">Po utworzeniu dysk VHD przekazany do platformy Azure, utwórz maszynę Wirtualną przy użyciu `New-AzureRmVM` i określić typ licencjonowania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f9860-144">Once you have your VHD uploaded to Azure, you create a VM using `New-AzureRmVM` and specify the licensing type as follows:</span></span>

<span data-ttu-id="f9860-145">W systemie Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f9860-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="f9860-146">Dla klienta systemu Windows do użycia tylko z obrazu witryny Marketplace Azure:</span><span class="sxs-lookup"><span data-stu-id="f9860-146">For Windows Client to use with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="f9860-147">Możesz [odczytu bardziej szczegółowy przewodnik na temat wdrażania maszyny Wirtualnej na platformie Azure za pomocą programu PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) poniżej, lub bardziej opisowe przewodnika wykonania różnych kroków w celu odczytu [Utwórz maszynę Wirtualną z systemem Windows przy użyciu usługi Resource Manager i programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9860-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on the different steps to [create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-the-licensing-benefit"></a><span data-ttu-id="f9860-148">Sprawdź, czy maszyna wirtualna jest wykorzystania asysty licencjonowania</span><span class="sxs-lookup"><span data-stu-id="f9860-148">Verify your VM is utilizing the licensing benefit</span></span>
<span data-ttu-id="f9860-149">Po wdrożeniu maszyny Wirtualnej za pomocą metody wdrożenia programu PowerShell lub Menedżera zasobów Sprawdź typ licencji z `Get-AzureRmVM` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f9860-149">Once you have deployed your VM through either the PowerShell or Resource Manager deployment method, verify the license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="f9860-150">Wynik jest podobny do poniższego przykładu w systemie Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f9860-150">The output is similar to the following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="f9860-151">Output to różni się z maszyną Wirtualną następujące wdrożenie bez licencjonowania Azure hybrydowego Użyj korzyści, takich jak wdrożyć bezpośrednio z poziomu galerii Azure maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f9860-151">This output contrasts with the following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from the Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="f9860-152">Szczegółowy przewodnik wdrażania programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9860-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="f9860-153">Poniższe szczegółowe kroki programu PowerShell pokazują pełne wdrożenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9860-153">The following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="f9860-154">Możesz przeczytać więcej kontekstu rzeczywiste poleceń cmdlet i różnych składników tworzonych w [Utwórz maszynę Wirtualną z systemem Windows przy użyciu usługi Resource Manager i programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9860-154">You can read more context as to the actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f9860-155">Kroku przez proces tworzenia Twojej grupy zasobów konta magazynu i sieci wirtualne, a następnie zdefiniuj maszyny Wirtualnej, a na koniec Utwórz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f9860-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="f9860-156">Po pierwsze bezpiecznie uzyskać poświadczenia, Ustaw lokalizację i nazwę grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="f9860-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="f9860-157">Utwórz publiczny adres IP:</span><span class="sxs-lookup"><span data-stu-id="f9860-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="f9860-158">Zdefiniuj, podsieci, karty Sieciowej i sieci Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f9860-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="f9860-159">Nazwa maszyny Wirtualnej i Utwórz konfiguracji maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f9860-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="f9860-160">Określ system operacyjny:</span><span class="sxs-lookup"><span data-stu-id="f9860-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="f9860-161">Dodaj swoją kartę Sieciową do maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f9860-161">Add your NIC to the VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="f9860-162">Zdefiniuj konto magazynu do użycia:</span><span class="sxs-lookup"><span data-stu-id="f9860-162">Define the storage account to use:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="f9860-163">Przekazanie dysku VHD, odpowiednio przygotowany i Dołącz do maszyny Wirtualnej do użycia:</span><span class="sxs-lookup"><span data-stu-id="f9860-163">Upload your VHD, suitably prepared, and attach to your VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="f9860-164">Na zakończenie tworzenia maszyny Wirtualnej i typ licencjonowania wykorzystywać Azure hybrydowego Użyj korzyści:</span><span class="sxs-lookup"><span data-stu-id="f9860-164">Finally, create your VM and define the licensing type to utilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="f9860-165">W systemie Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f9860-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="f9860-166">Wdrażanie skali maszyny wirtualnej za pomocą szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f9860-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="f9860-167">W szablonach VMSS Resource Manager dodatkowy parametr dla `licenseType` musi być określona.</span><span class="sxs-lookup"><span data-stu-id="f9860-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="f9860-168">Możesz przeczytać dodatkowe informacje [tworzenia szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f9860-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="f9860-169">Edytuj szablon Menedżera zasobów można uwzględnić właściwość licenseType jako część virtualMachineProfile zestaw skali i wdrażania szablonu w zwykły — Zobacz przykład poniżej przy użyciu obrazu systemu Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="f9860-169">Edit your Resource Manager template to include the licenseType property as part of the scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="f9860-170">Obsługa wdrażania skalowania maszyny wirtualnej, ustaw o korzyści AHUB za pomocą programu PowerShell i inne narzędzia zestawu SDK będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="f9860-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="f9860-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9860-171">Next steps</span></span>
<span data-ttu-id="f9860-172">Przeczytaj więcej na temat [licencjonowania Azure hybrydowego Użyj korzyści](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="f9860-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="f9860-173">Dowiedz się więcej o [przy użyciu szablonów usługi Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9860-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f9860-174">Dowiedz się więcej o [korzyści Użyj hybrydowe platformy Azure i usługi Azure Site Recovery upewnij migrowanie aplikacji Azure jeszcze bardziej ekonomiczne](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="f9860-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications to Azure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
