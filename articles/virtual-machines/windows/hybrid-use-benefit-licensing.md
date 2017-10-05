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
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Korzyści Użyj hybrydowe platformy Azure dla systemu Windows Server i klienta systemu Windows
W przypadku klientów z Software Assurance korzyści użyć hybrydowego Azure umożliwia użyć lokalnego licencji systemu Windows Server i klienta systemu Windows i uruchamiania maszyn wirtualnych systemu Windows na platformie Azure taniego. Azure hybrydowego Użyj korzyści dla systemu Windows Server zawiera systemu Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016. Hybrydowe Użyj korzyści dla systemu Windows klienta usługi Azure obejmuje systemu Windows 10. Aby uzyskać więcej informacji, zobacz [strony licencjonowania Azure hybrydowego Użyj korzyści](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure hybrydowego Użyj korzyści dla klienta systemu Windows jest obecnie w wersji zapoznawczej za pomocą obrazu systemu Windows 10 w portalu Azure Marketplace. Tylko przedsiębiorstwa z systemem Windows 10 Enterprise E3/E5 dla poszczególnych użytkowników lub VDA systemu Windows dla każdego użytkownika (licencji subskrypcji użytkownika lub licencji subskrypcji użytkownika dodatku) kwalifikują się ("uprawniających licencji").
>
>

## <a name="ways-to-use-azure-hybrid-use-benefit"></a>Sposoby używania korzyści Użyj hybrydowe platformy Azure
Istnieje kilka różnych sposobów wdrażania maszyn wirtualnych systemu Windows z asysty Użyj hybrydowe platformy Azure:

1. Można wdrożyć maszyn wirtualnych z [określonych obrazów Marketplace](#deploy-a-vm-using-the-azure-marketplace) , które są wstępnie skonfigurowane z Azure hybrydowego Użyj korzyści - systemu Windows Server 2016, systemu Windows Server 2012 R2, Windows Server 2012 i Windows Server 2008SP1.
2. Możesz [przekazać niestandardowe wirtualna](#upload-a-windows-vhd) i [wdrażanie przy użyciu szablonu usługi Resource Manager](#deploy-a-vm-via-resource-manager) lub [programu Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-the-azure-marketplace"></a>Wdróż Maszynę wirtualną przy użyciu portalu Azure Marketplace
Następujące obrazy są dostępne w witrynie Marketplace wstępnie skonfigurowaną korzyści Użyj hybrydowe platformy Azure: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 i Windows Server 2008SP1. Te obrazy można wdrażać bezpośrednio za pomocą witryny Azure Portal, szablonów usługi Resource Manager lub programu Azure PowerShell.

Można wdrażać te obrazy bezpośrednio z portalu Azure. Do użycia w szablonach usługi Resource Manager i przy użyciu programu Azure PowerShell wyświetlić listę obrazów w następujący sposób:

W systemie Windows Server:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- Wersja 2016 Datacenter 2016.127.20170406 lub nowszy

- Wersja 2012-R2-Datacenter 4.127.20170406 lub nowszy

- Wersja 2012 Datacenter 3.127.20170406 lub nowszy

- 2.127.20170406 w wersji 2008 R2 SP1 lub nowszy

Dla klienta systemu Windows:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Przekazywanie wirtualnego dysku twardego Windows Server
Aby wdrożyć Maszynę wirtualną systemu Windows Server na platformie Azure, należy najpierw utworzyć wirtualny dysk twardy zawiera podstawowe kompilacji systemu Windows. Tego wirtualnego dysku twardego, należy odpowiednio przygotować za pomocą programu Sysprep przed przekazaniem go do platformy Azure. Możesz [Dowiedz się więcej na temat wirtualnego dysku twardego wymagań i procesu Sysprep](upload-generalized-managed.md) i [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). Utwórz kopię zapasową maszyny Wirtualnej przed uruchomieniem programu Sysprep. 

Upewnij się, że masz [zainstalowany i skonfigurowany najnowsze programu Azure PowerShell](/powershell/azure/overview). Po przygotowaniu dysk VHD, przekazanie dysku VHD do używania konta usługi Azure Storage `Add-AzureRmVhd` polecenia cmdlet w następujący sposób:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server i Dynamics można również korzystać z programu Software Assurance licencjonowania. Nadal musisz przygotować obraz systemu Windows Server instalowania składniki aplikacji i zapewnianie odpowiednio kluczy licencji, a następnie przekazywanie obrazu dysku na platformie Azure. Zapoznaj się z dokumentacją odpowiedniego do uruchamiania narzędzia Sysprep z aplikacji, takich jak [zagadnienia dotyczące instalowania programu SQL Server za pomocą programu Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) lub [Utwórz obraz referencyjny programu SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

Można również uzyskać więcej informacji [przekazywanie wirtualnego dysku twardego do procesu systemu Azure](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Wdróż Maszynę wirtualną za pomocą szablonu usługi Resource Manager
W szablonach usługi Resource Manager dodatkowy parametr dla `licenseType` można określić. Możesz przeczytać dodatkowe informacje [tworzenia szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md). Po utworzeniu dysk VHD przekazany do platformy Azure, Edytuj szablon Menedżera zasobów, aby dołączyć typ licencji w ramach dostawcy obliczeń i wdrażania szablonu w zwykły:

W systemie Windows Server:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Dla klienta systemu Windows do użycia tylko z obrazu witryny Marketplace Azure:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>Wdróż Maszynę wirtualną za pomocą programu PowerShell — Szybki Start
Podczas wdrażania maszyny Wirtualnej systemu Windows Server za pomocą programu PowerShell, masz dodatkowy parametr dla `-LicenseType`. Po utworzeniu dysk VHD przekazany do platformy Azure, utwórz maszynę Wirtualną przy użyciu `New-AzureRmVM` i określić typ licencjonowania w następujący sposób:

W systemie Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Dla klienta systemu Windows do użycia tylko z obrazu witryny Marketplace Azure:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

Możesz [odczytu bardziej szczegółowy przewodnik na temat wdrażania maszyny Wirtualnej na platformie Azure za pomocą programu PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) poniżej, lub bardziej opisowe przewodnika wykonania różnych kroków w celu odczytu [Utwórz maszynę Wirtualną z systemem Windows przy użyciu usługi Resource Manager i programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-the-licensing-benefit"></a>Sprawdź, czy maszyna wirtualna jest wykorzystania asysty licencjonowania
Po wdrożeniu maszyny Wirtualnej za pomocą metody wdrożenia programu PowerShell lub Menedżera zasobów Sprawdź typ licencji z `Get-AzureRmVM` w następujący sposób:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Wynik jest podobny do poniższego przykładu w systemie Windows Server:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Output to różni się z maszyną Wirtualną następujące wdrożenie bez licencjonowania Azure hybrydowego Użyj korzyści, takich jak wdrożyć bezpośrednio z poziomu galerii Azure maszyny Wirtualnej:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Szczegółowy przewodnik wdrażania programu PowerShell
Poniższe szczegółowe kroki programu PowerShell pokazują pełne wdrożenie maszyny wirtualnej. Możesz przeczytać więcej kontekstu rzeczywiste poleceń cmdlet i różnych składników tworzonych w [Utwórz maszynę Wirtualną z systemem Windows przy użyciu usługi Resource Manager i programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Kroku przez proces tworzenia Twojej grupy zasobów konta magazynu i sieci wirtualne, a następnie zdefiniuj maszyny Wirtualnej, a na koniec Utwórz maszyny Wirtualnej.

Po pierwsze bezpiecznie uzyskać poświadczenia, Ustaw lokalizację i nazwę grupy zasobów:

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Utwórz publiczny adres IP:

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Zdefiniuj, podsieci, karty Sieciowej i sieci Wirtualnej:

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

Nazwa maszyny Wirtualnej i Utwórz konfiguracji maszyny Wirtualnej:

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

Określ system operacyjny:

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Dodaj swoją kartę Sieciową do maszyny Wirtualnej:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Zdefiniuj konto magazynu do użycia:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Przekazanie dysku VHD, odpowiednio przygotowany i Dołącz do maszyny Wirtualnej do użycia:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Na zakończenie tworzenia maszyny Wirtualnej i typ licencjonowania wykorzystywać Azure hybrydowego Użyj korzyści:

W systemie Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Wdrażanie skali maszyny wirtualnej za pomocą szablonu usługi Resource Manager
W szablonach VMSS Resource Manager dodatkowy parametr dla `licenseType` musi być określona. Możesz przeczytać dodatkowe informacje [tworzenia szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md). Edytuj szablon Menedżera zasobów można uwzględnić właściwość licenseType jako część virtualMachineProfile zestaw skali i wdrażania szablonu w zwykły — Zobacz przykład poniżej przy użyciu obrazu systemu Windows Server 2016:


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
> Obsługa wdrażania skalowania maszyny wirtualnej, ustaw o korzyści AHUB za pomocą programu PowerShell i inne narzędzia zestawu SDK będzie dostępna wkrótce.
>

## <a name="next-steps"></a>Następne kroki
Przeczytaj więcej na temat [licencjonowania Azure hybrydowego Użyj korzyści](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

Dowiedz się więcej o [przy użyciu szablonów usługi Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Dowiedz się więcej o [korzyści Użyj hybrydowe platformy Azure i usługi Azure Site Recovery upewnij migrowanie aplikacji Azure jeszcze bardziej ekonomiczne](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
