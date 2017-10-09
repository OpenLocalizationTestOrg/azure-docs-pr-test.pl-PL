---
title: "aaaAzure dołączonych dysków danych maszyny wirtualnej skali zestawy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse dołączonych dysków z danymi z zestawy skalowania maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Zestawy skalowania maszyn wirtualnych platformy Azure i dołączone dyski danych
[Zestawy skalowania maszyn wirtualnych](/azure/virtual-machine-scale-sets/) platformy Azure obsługują teraz maszyny wirtualne z dołączonymi dyskami danych. Dyski danych mogą być definiowane w profilu magazynu powitania dla zestawów skalowania, które zostały utworzone z dyskami zarządzane Azure. Wcześniej hello tylko bezpośrednio dołączonego magazynu i opcje maszyn wirtualnych w zestawach skali zostały dysku hello systemu operacyjnego i dysków tymczasowego.

> [!NOTE]
>  Podczas tworzenia skali ustawiony za pomocą dysków dołączonych danych zdefiniowany nadal potrzebujesz toomount i format hello dyski z wewnątrz toouse maszyny Wirtualnej je (jak tylko dla autonomicznych maszyn wirtualnych platformy Azure). Toodo wygodny sposób jest toouse rozszerzenia niestandardowego skryptu, który wywołuje toopartition skrypty standardowe i formatowanie hello dysków danych maszyny wirtualnej.

## <a name="create-a-scale-set-with-attached-data-disks"></a>Tworzenie zestawu skalowania z dołączonymi dyskami danych
Toocreate prosty sposób skonfigurować skali z dysków dołączonych jest toouse hello [interfejsu wiersza polecenia Azure](https://github.com/Azure/azure-cli) _vmss utworzyć_ polecenia. Witaj poniższy przykład tworzy odpowiednio grupy zasobów platformy Azure oraz zestaw skali maszyny Wirtualnej 10 Ubuntu maszyn wirtualnych mających dyski 2 dołączonych danych, 50 GB i 100 GB.
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
Należy pamiętać, że hello _vmss utworzyć_ polecenia domyślnie niektóre wartości konfiguracji, jeśli nie zostanie określony. toosee hello dostępne opcje przesłonić spróbuj:
```bash
az vmss create --help
```
Inny toocreate sposób skalowania ustawiony za pomocą dysków dołączonych danych jest toodefine skali ustawiona w szablonie usługi Azure Resource Manager obejmują _dataDisks_ części hello _storageProfile_i wdrażanie hello szablon. Hello 50 GB i 100 GB dysku w powyższym przykładzie byłoby zdefiniowane w szablonie hello następująco:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
Widać pełną, gotowe toodeploy przykładem szablonu zestaw skali z dysku dołączonym zdefiniowane w tym miejscu: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>Dodawanie danych skali istniejącego dysku tooan ustawić
> [!NOTE]
>  Można dołączać zestaw skali tooa dysków danych, która została utworzona z [dysków zarządzanych Azure](./virtual-machine-scale-sets-managed-disks.md).

Można dodać dysku danych tooa skalowania maszyny Wirtualnej ustawić za pomocą interfejsu wiersza polecenia Azure _dołączyć dysku vmss az_ polecenia. Należy pamiętać o określeniu właściwości lun, która nie jest jeszcze używana. Poniższy przykład CLI Hello dodaje toolun dysk 50 GB 3:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

Poniższy przykład PowerShell Hello dodaje toolun dysk 50 GB 3:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> Różne rozmiary maszyny Wirtualnej mają różne limity na powitania liczby dołączone dyski, które obsługują. Sprawdź hello [właściwości rozmiar maszyny wirtualnej](../virtual-machines/windows/sizes.md) przed dodaniem nowego dysku.

Możesz także dodać dysk, dodając nowe toohello wpis _dataDisks_ właściwości w hello _storageProfile_ skalę Ustaw definicji i stosowania hello zmiany. tootest, Znajdź istniejącej definicji zestawu skali w hello [Eksploratora zasobów Azure](https://resources.azure.com/). Wybierz _Edytuj_ i Dodaj nowy dysk toohello listę dysków z danymi. Na przykład za pomocą powyższego przykładu hello:
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

Następnie wybierz _PUT_ tooapply hello zmienia tooyour zestaw skali. Ten przykład sprawdzi się w przypadku korzystania z takiego rozmiaru maszyny wirtualnej, który zapewnia obsługę więcej niż dwóch dołączonych dysków danych.

> [!NOTE]
> Po wprowadzeniu zmiany skali tooa ustawić definicji, takie jak dodawanie lub usuwanie dysk z danymi, stosuje tooall nowo tworzone maszyny wirtualne, ale tylko w przypadku maszyn wirtualnych tooexisting hello _upgradePolicy_ właściwość jest ustawiona zbyt "Automatyczny". Jeśli jest ustawiona zbyt "Manual", należy toomanually zastosować hello nowego modelu tooexisting maszyn wirtualnych. Można to zrobić w portalu hello przy użyciu hello _AzureRmVmssInstance aktualizacji_ PowerShell polecenia lub przy użyciu hello _vmss az update wystąpienia_ polecenia interfejsu wiersza polecenia.

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>Dodawanie zestawu skalowania istniejących tooan dysków danych wstępnie wypełnione 
> Podczas dodawania dysków tooan istniejących zestawu skalowania modelu, zgodnie z projektem, dysku hello tworzony jest zawsze pusta. Ten scenariusz obejmuje też nowe wystąpienia utworzone przez zestaw skali hello. To zachowanie jest ponieważ definicji scaleset hello ma dysk danych puste. W kolejności toocreate wstępnie wypełnione dysków z danymi dla modelu zestawu skali istniejących można wybrać jedną z poniższych dwóch opcji:

* Kopiowanie danych z hello wystąpienie 0 wirtualna toohello danych dyski w hello innych maszyn wirtualnych przez uruchomienie skryptu niestandardowego.
* Tworzenie zarządzanego obrazu w przypadku dysku hello systemu operacyjnego oraz danych dysku (z danymi hello wymagane) i Utwórz nowe scaleset z hello obrazu. W ten sposób każdy nowej maszyny Wirtualnej utworzone będzie mieć danych na dysku czy znajduje się w definicji hello hello scaleset. Ponieważ ta definicja będzie odnosić się tooan obrazu dysku danych, który został dostosowany danych, co maszyny wirtualnej na powitania scaleset automatycznie rozpocznie pracę z tych zmian.

> Witaj toocreate sposób niestandardowego obrazu można znaleźć tutaj: [tworzenie zarządzanego obrazu uogólniony maszyny wirtualnej na platformie Azure](/azure/virtual-machines/windows/capture-image-resource/) 

> Witaj użytkownik potrzebuje toocapture hello 0 maszyny Wirtualnej, która ma hello wymagane dane wystąpienia, a następnie użyj tego wirtualnego dysku twardego dla definicji obraz powitania.

## <a name="removing-a-data-disk-from-a-scale-set"></a>Usuwanie dysku danych z zestawu skalowania
Dysk danych można usunąć z zestawu skalowania maszyn wirtualnych przy użyciu polecenia _az vmss disk detach_ interfejsu wiersza polecenia platformy Azure. Na przykład hello następujące polecenie usuwa hello dysk zdefiniowane w jednostce lun 2:
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
Podobnie można również usunąć dysk z skali ustawiony przez usunięcie wpisu z hello _dataDisks_ właściwości w hello _storageProfile_ i stosowanie hello zmiany. 

## <a name="additional-notes"></a>Uwagi dodatkowe
Pomoc dla dysków Azure zarządzane i skalę zestawu dysków dołączonych danych jest dostępna w wersji interfejsu API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) lub nowszej hello Microsoft.Compute interfejsu API.

W implementacji początkowej hello dołączono dysk wsparcia dla zestawów skalowania nie można dołączyć lub odłączyć dysków danych z poszczególnych maszyn wirtualnych w zestawie skalowania.

W witrynie Azure Portal obsługa dołączonych dysków danych w zestawach skalowania jest wstępnie ograniczona. W zależności od wymagań, których można użyć szablonów platformy Azure interfejsu wiersza polecenia programu PowerShell, zestawy SDK i interfejsu API REST toomanage dołączone dyski.


