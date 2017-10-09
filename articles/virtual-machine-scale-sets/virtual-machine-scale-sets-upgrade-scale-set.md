---
title: zestaw skalowania maszyny wirtualnej platformy Azure aaaUpgrade | Dokumentacja firmy Microsoft
description: Uaktualnij zestaw skali maszyny wirtualnej platformy Azure
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Uaktualnij zestaw skali maszyny wirtualnej
W tym artykule opisano, jak wdrożenie aktualizacji systemu operacyjnego tooan skali maszyny wirtualnej platformy Azure bez żadnego przestoju. W tym kontekście aktualizacji systemu operacyjnego obejmuje zmiana wersji hello lub SKU hello systemu operacyjnego lub zmiana hello identyfikatora URI obrazu niestandardowego. Aktualizowanie bez przestojów aktualizowanie maszyn wirtualnych co pojedynczo lub w grupach (na przykład w jednej domenie błędów w czasie) zamiast jednocześnie. W ten sposób można zachować uruchomiona żadnych maszyn wirtualnych, które nie jest uaktualniany.

niejednoznaczności tooavoid pozwala odróżnić cztery typy aktualizacji systemu operacyjnego może być tooperform:

* Zmiana wersji hello lub jednostka SKU obrazu platformy. Na przykład zmiana Ubuntu wersji 14.04.2-LTS z 14.04.201506100 too14.04.201507060 lub zmiana hello Ubuntu 15.10/najnowszej wersji too16.04.0-LTS/latest. W tym scenariuszu są omówione w tym artykule.
* Zmiana hello identyfikator URI, który wskazuje tooa nowej wersji zostanie utworzony niestandardowy obraz (**właściwości** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **obrazu** > **uri**). W tym scenariuszu są omówione w tym artykule.
* Zmiana hello odwołanie do obrazu zestawu skalowania, który został utworzony przy użyciu dysków zarządzanych platformy Azure.
* Stosowanie poprawek hello systemu operacyjnego z poziomu maszyny wirtualnej (to przykłady instalowania poprawki zabezpieczeń i uruchamiania usługi Windows Update). Ten scenariusz jest obsługiwany, ale nie zostały omówione w tym artykule.

Zestawy skalowania maszyn wirtualnych, które są wdrażane w ramach [sieć szkieletowa usług Azure](https://azure.microsoft.com/services/service-fabric/) klastra nie zostały omówione w tym miejscu. Zobacz [poprawka systemu operacyjnego Windows w klastrze usługi sieć szkieletowa](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) Aby uzyskać więcej informacji na temat stosowania poprawek sieci szkieletowej usług.

Witaj podstawowe sekwencji zmiany hello systemu operacyjnego wersji lub jednostki SKU obrazu platformy lub hello URI niestandardowy obraz wygląda następująco:

1. Pobierz modelu zestawu skali maszyny wirtualnej hello.
2. Zmień wersję hello, jednostka SKU, odwołanie do obrazu lub wartość identyfikatora URI w modelu hello.
3. Model hello aktualizacji.
4. Czy *manualUpgrade* wywołać na maszynach wirtualnych hello w zestawie skalowania hello. Ten krok ma zastosowanie tylko jeśli *upgradePolicy* ustawiono zbyt**ręcznego** w zestawie skalowania użytkownika. Jeśli ustawiono zbyt**automatyczne**, wszystkie maszyny wirtualne hello są uaktualniane na raz, powodując przestoje.

Dzięki tym informacjom pamiętać Zobaczmy, jak można zaktualizować wersji hello skali, ustaw w programie PowerShell i przy użyciu hello interfejsu API REST. Te przykłady obejmują hello przypadku obrazu platformy, ale ten artykuł zawiera odpowiednią ilość informacji w przypadku tooadapt obraz niestandardowy tooa procesu.

## <a name="powershell"></a>PowerShell
W tym przykładzie aktualizuje zestaw skali maszyny wirtualnej systemu Windows (Tworzenie toohello nową wersję 4.0.20160229. Po zaktualizowaniu modelu hello, robi aktualizacji jedno wystąpienie maszyny wirtualnej w czasie.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Aktualizowania hello identyfikatora URI dla niestandardowego obrazu zamiast zmiana wersji obrazu platformy, zastąp "zestaw hello nową wersję" hello wiersza polecenia, który zaktualizuje hello obrazu źródłowego identyfikatora URI. Na przykład jeśli zestaw skali hello został utworzony bez użycia dysków zarządzanych Azure, hello aktualizacji będzie wyglądać następująco:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Jeśli obraz niestandardowy na podstawie zestawu skalowania został utworzony przy użyciu dysków zarządzanych Azure, a następnie będzie można zaktualizować hello odwołanie do obrazu. Na przykład:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Witaj interfejsu API REST
Oto kilka przykładów Python, które używają tooroll interfejsu API REST Azure hello limit aktualizacji wersji systemu operacyjnego. Oba rozwiązania używają hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) biblioteki interfejsu API REST Azure otoki funkcje toodo GET skali hello ustawić modelu, następuje PUT z zaktualizowanym modelu. One również sprawdzić widoków wystąpień maszyny wirtualnej maszyny wirtualne hello tooidentify według domeny aktualizacji.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) jest skrypt języka Python, który został użyty tooroll limit tooa uaktualnienia systemu operacyjnego systemem skalowania maszyny wirtualnej ustawić jednej domeny aktualizacji w czasie.

![Skrypt Vmssupgrade dotyczące wybierania maszyn wirtualnych lub domeny aktualizacji](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Ten skrypt pozwala wybrać tooupdate określone maszyny wirtualne lub określ domenę aktualizacji. Obsługuje ona zmiana wersji obrazu platformy lub zmiana hello identyfikatora URI obrazu niestandardowego.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) jest Edytor ogólnego przeznaczenia dla zestawy skalowania maszyn wirtualnych, które pokazuje wirtualnej maszynie stan jako heatmap gdzie jeden wiersz odpowiada jednej domeny aktualizacji. Między innymi można zaktualizować modelu powitania dla zestawu skalowania o nowej wersji, jednostki SKU lub obraz niestandardowy identyfikator URI, a następnie wybierz tooupgrade domen błędów. Po wykonaniu tej czynności wszystkich hello maszyn wirtualnych w tej domenie aktualizacji są uaktualnionego toohello nowego modelu. Alternatywnie można wykonać uaktualnienia stopniowego na podstawie rozmiaru partii hello wybranych przez użytkownika.  

Witaj Poniższy zrzut ekranu przedstawia model dla Ubuntu 14.04-2LTS wersji 14.04.201507060 skali. Wiele więcej opcji dodano narzędzia toothis ponieważ wykonano tego zrzutu ekranu.

![Model Vmsseditor skali, ustaw dla Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Po kliknięciu **uaktualnienia** , a następnie **Pobierz szczegóły**, tooupdate start maszyn wirtualnych w UD 0.

![Trwa aktualizacja przedstawiający Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

