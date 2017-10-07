---
title: "aaaCommon PowerShell poleceń maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Typowe tooget poleceń programu PowerShell Rozpoczęto tworzenie i zarządzanie nimi maszyn wirtualnych systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Typowe polecenia programu PowerShell do tworzenia i zarządzania maszynami wirtualnymi Azure

W tym artykule omówiono niektóre powitalne polecenia programu Azure PowerShell, można użyć toocreate i zarządzania maszynami wirtualnymi w Twojej subskrypcji platformy Azure.  Szczegółowe, aby uzyskać pomoc dotyczącą przełączniki wiersza polecenia i opcje, można użyć **Get-Help** *polecenia*.

Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.

Te zmienne mogą być przydatne dla Ciebie, jeśli więcej niż jedno z poleceń hello uruchomione w tym artykule:

- $location - lokalizacji hello hello maszyny wirtualnej. Można użyć [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind [regionu geograficznego](https://azure.microsoft.com/regions/) działający za Ciebie.
- $myResourceGroup - hello nazwę grupy zasobów hello, która zawiera hello maszyny wirtualnej.
- $myVM — nazwa hello hello maszyny wirtualnej.

## <a name="create-a-vm"></a>Tworzenie maszyny wirtualnej

| Zadanie | Polecenie |
| ---- | ------- |
| Utwórz konfigurację maszyny Wirtualnej |$vm = [AzureRmVMConfig nowy](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) - VMName $myVM - VMSize "Standard_D1_v1"<BR></BR><BR></BR>konfiguracja maszyny Wirtualnej Hello jest używane ustawienia toodefine lub aktualizacji hello maszyny Wirtualnej. Konfiguracja Hello jest inicjowana z nazwą hello hello maszyny Wirtualnej i jej [rozmiar](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Dodaj ustawienia konfiguracji |$vm = [AzureRmVMOperatingSystem zestaw](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) - VM $vm-Windows - ComputerName $myVM-poświadczeń $cred - ProvisionVMAgent - EnableAutoUpdate<BR></BR><BR></BR>Ustawienia systemu operacyjnego, w tym [poświadczenia](https://technet.microsoft.com/library/hh849815.aspx) są dodawane obiekt konfiguracji toohello utworzonego wcześniej za pomocą polecenia New-AzureRmVMConfig. |
| Dodawanie interfejsu sieciowego |$vm = [AzureRmVMNetworkInterface Dodaj](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) - VM $vm-$identyfikator karty sieciowej. Identyfikator<BR></BR><BR></BR>Maszyna wirtualna musi mieć [interfejsu sieciowego](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate w sieci wirtualnej. Można również użyć [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve istniejącego obiektu interfejsu sieciowego. |
| Określ obraz platformy |$vm = [AzureRmVMSourceImage zestaw](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) - VM $vm - PublisherName "publisher_name"-oferty "publisher_offer" - jednostki SKU "product_sku"-"najnowszej" wersji<BR></BR><BR></BR>[Informacji zawartych w obrazie](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) jest dodawany obiekt konfiguracji toohello utworzonego wcześniej za pomocą polecenia New-AzureRmVMConfig. Obiekt Hello zwrócony z tego polecenia jest używana tylko po ustawieniu toouse dysku hello systemu operacyjnego obrazu platformy. |
| Ustaw toouse dysku systemu operacyjnego obrazu platformy |$vm = [AzureRmVMOSDisk zestaw](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) - VM $vm-Name "myOSDisk" - VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" - CreateOption FromImage<BR></BR><BR></BR>Nazwa Hello hello dysku systemu operacyjnego i jego lokalizacji w [magazynu](../../storage/common/storage-powershell-guide-full.md) dodaniu toohello obiekt konfiguracji, która została wcześniej utworzona. |
| Ustaw uogólniony obraz toouse dysku systemu operacyjnego |$vm = set AzureRmVMOSDisk - VM $vm-- SourceImageUri "myOSDisk" Name "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk. -VhdUri VHD {guid}""https://mystore1.blob.core.windows.net/vhds/disk_name.vhd"- CreateOption FromImage-systemu Windows<BR></BR><BR></BR>nazwy Hello hello dysk systemu operacyjnego, hello lokalizacji obrazu źródłowego hello i lokalizację dysku hello w [magazynu](../../storage/common/storage-powershell-guide-full.md) dodaniu toohello obiekt konfiguracji. |
| Ustaw obraz specjalne toouse dysku systemu operacyjnego |$vm = set AzureRmVMOSDisk - VM $vm-- VhdUri "myOSDisk" Name "http://mystore1.blob.core.windows.net/vhds/" Attach - CreateOption - systemu Windows |
| Tworzenie maszyny wirtualnej |[Nowy AzureRmVM]() - ResourceGroupName $myResourceGroup-lokalizacji $location - VM $vm<BR></BR><BR></BR>Wszystkie zasoby są tworzone w [grupy zasobów](../../azure-resource-manager/powershell-azure-resource-manager.md). Przed uruchomieniem tego polecenia, uruchom nowy AzureRmVMConfig, AzureRmVMOperatingSystem zestaw AzureRmVMSourceImage zestawu, Dodaj AzureRmVMNetworkInterface i AzureRmVMOSDisk zestawu. |

## <a name="get-information-about-vms"></a>Pobierz informacje o maszynach wirtualnych

| Zadanie | Polecenie |
| ---- | ------- |
| Lista maszyn wirtualnych, w ramach subskrypcji |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Lista maszyn wirtualnych, w grupie zasobów |Get-AzureRmVM - ResourceGroupName $myResourceGroup<BR></BR><BR></BR>tooget listę zasobów grup w ramach subskrypcji, użyj [Get-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Uzyskiwanie informacji o maszynie wirtualnej |Get-AzureRmVM - ResourceGroupName $myResourceGroup-Name $myVM |

## <a name="manage-vms"></a>Zarządzanie maszynami wirtualnymi
| Zadanie | Polecenie |
| --- | --- |
| Uruchamianie maszyny wirtualnej |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) - ResourceGroupName $myResourceGroup-Name $myVM |
| Zatrzymywanie maszyny wirtualnej |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) - ResourceGroupName $myResourceGroup-Name $myVM |
| Uruchom ponownie uruchomionej maszyny Wirtualnej |[Ponowne uruchomienie AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) - ResourceGroupName $myResourceGroup-Name $myVM |
| Usuwanie maszyny wirtualnej |[Usuń AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) - ResourceGroupName $myResourceGroup-Name $myVM |
| Generalize maszyny Wirtualnej |[Zestaw AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) - ResourceGroupName $myResourceGroup-Name $myVM-uogólniony<BR></BR><BR></BR>Uruchom to polecenie przed uruchomieniem AzureRmVMImage Zapisz. |
| Przechwytywanie maszyny wirtualnej |[Zapisz AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) - ResourceGroupName $myResourceGroup - VMName $myVM - DestinationContainerName "myImageContainer" - VHDNamePrefix "myImagePrefix"-"C:\filepath\filename.json" ścieżki<BR></BR><BR></BR>Maszyna wirtualna musi być [przygotowany, zamknij i uogólniony](prepare-for-upload-vhd-image.md) toocreate toobe użyć obrazu. Przed uruchomieniem tego polecenia, uruchom zestaw AzureRmVm. |
| Aktualizacja maszyny Wirtualnej |[Aktualizacja AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) - ResourceGroupName $myResourceGroup - VM $vm<BR></BR><BR></BR>Pobierz hello bieżącej konfiguracji maszyny Wirtualnej przy użyciu Get AzureRmVM, zmiany ustawień konfiguracji na powitania obiektu maszyny Wirtualnej, a następnie uruchom to polecenie. |
| Dodaj tooa dysku danych maszyny Wirtualnej |[Dodaj AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) - VM $vm-- VhdUri "myDataDisk" Name "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" - LUN #-buforowanie ReadWrite - DiskSizeinGB # - CreateOption pusta<BR></BR><BR></BR>Użyj obiektu maszyny Wirtualnej hello tooget Get AzureRmVM. Określ numer LUN hello i rozmiar hello hello dysku. Uruchom AzureRmVM aktualizacji tooapply hello konfiguracji zmiany toohello maszyny Wirtualnej. Nie zainicjowano Hello dysku, który można dodać. |
| Usuwanie dysku danych z maszyny wirtualnej |[Usuń AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) - VM $vm-Name "myDataDisk"<BR></BR><BR></BR>Użyj obiektu maszyny Wirtualnej hello tooget Get AzureRmVM. Uruchom AzureRmVM aktualizacji tooapply hello konfiguracji zmiany toohello maszyny Wirtualnej. |
| Dodaj tooa rozszerzenia maszyny Wirtualnej |[AzureRmVMExtension zestawu](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) - ResourceGroupName $myResourceGroup — lokalizacji $location - VMName $myVM-Name "extensionName" — wydawcy "publisherName" — typu "extensionType" - TypeHandlerVersion "#. #" — Ustawienia $Settings - ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Uruchom to polecenie z odpowiednią hello [informacje o konfiguracji](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) hello rozszerzenia, które mają tooinstall. |
| Usuwanie rozszerzenia maszyny wirtualnej |[Usuń AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) - ResourceGroupName $myResourceGroup-Name "extensionName" - VMName $myVM |

## <a name="next-steps"></a>Następne kroki
* Zobacz hello podstawowe czynności w przypadku tworzenia maszyny wirtualnej w [Utwórz maszynę Wirtualną z systemem Windows przy użyciu usługi Resource Manager i programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

