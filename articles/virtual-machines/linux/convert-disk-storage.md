---
title: "aaaConvert Azure zarządzanego magazynu dysków z toopremium standardowe i na odwrót | Dokumentacja firmy Microsoft"
description: "Jak tooconvert Azure zarządzane dyski magazynu z toopremium standardowe i na odwrót, przy użyciu wiersza polecenia platformy Azure."
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Konwertuj Azure zarządzanego magazynu dysków z toopremium standardowe i na odwrót

Zarządzane dysków oferuje dwie opcje magazynu: [Premium](../../storage/storage-premium-storage.md) (oparte na dysk SSD) i [standardowe](../../storage/storage-standard-storage.md) (oparte na dysk twardy). Pozwala ona tooeasily przełączanie między Witaj dwie opcje z minimalnym czasem przestojów na podstawie Twoich potrzeb wydajności. Ta funkcja nie jest dostępna dla niezarządzanego dysków. Ale możesz z łatwością [skonwertuj dyski toomanaged](convert-unmanaged-to-managed-disks.md) tooeasily przełączanie między Witaj dwie opcje.

W tym artykule opisano sposób tooconvert zarządzania dysków z toopremium standardowe i na odwrót przy użyciu wiersza polecenia platformy Azure. Jeśli konieczne tooinstall lub uaktualnić go, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli.md). 

## <a name="before-you-begin"></a>Przed rozpoczęciem

* Hello konwersja wymaga ponownego uruchomienia hello maszyny Wirtualnej, więc planowanie migracji hello magazynu dysków w istniejącym oknie obsługi. 
* Jeśli używane są niezarządzane dysków, najpierw [skonwertuj dyski toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch tego artykułu między Witaj dwie opcje magazynu. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Konwertuj hello wszystkie zarządzane dyski maszyny wirtualnej z toopremium standardowe i na odwrót

W hello poniższy przykład, zostanie przedstawiony sposób tooswitch hello wszystkie dyski maszyny Wirtualnej z magazynu standardowego toopremium. toouse premium zarządzane dyski, należy użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium. W tym przykładzie również zmienia rozmiar tooa, który obsługuje magazyn w warstwie premium.

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Konwertuj dysk zarządzanego z toopremium standardowe i na odwrót

Dla obciążenia i testowania możesz toohave kombinację dysków warstwy standardowa i premium tooreduce koszt. Można wykonać je przez uaktualnienie magazynu toopremium tylko dyski hello, które wymagają lepszą wydajność. W hello poniższy przykład, zostanie przedstawiony sposób tooswitch jednego dysku maszyny wirtualnej z magazynu standardowego toopremium i na odwrót. toouse premium zarządzane dyski, należy użyć maszyny Wirtualnej [rozmiar maszyny Wirtualnej](sizes.md) obsługującym magazyn w warstwie premium. W tym przykładzie również zmienia rozmiar tooa, który obsługuje magazyn w warstwie premium.

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a>Następne kroki

Podjąć tylko do odczytu kopię maszyny Wirtualnej za pomocą [migawki](snapshot-copy-managed-disk.md).

