---
title: "aaaAbout obrazów maszyn wirtualnych z systemem Windows | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat używania obrazów maszyn wirtualnych systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Informacje o obrazach dla maszyn wirtualnych systemu Windows
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Uzyskać informacje o znajdowaniu i używanie obrazów w modelu usługi Resource Manager hello, zobacz [tutaj](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>Praca z obrazami

Można użyć modułu Azure PowerShell hello i hello Azure toomanage portalu hello obrazy dostępne tooyour subskrypcji platformy Azure. modułu Azure PowerShell Hello zawiera więcej opcji polecenia, więc będzie można wyznaczyć dokładnie, co toosee lub wykonaj. Hello Azure portal udostępnia graficznego interfejsu użytkownika dla wielu hello codziennych zadań administracyjnych.

Oto kilka przykładów, korzystających z hello modułu Azure PowerShell.

* **Pobierz wszystkie obrazy**:`Get-AzureVMImage`zwraca listę wszystkich dostępnych w ramach Twojej bieżącej subskrypcji obrazów hello: obrazów i udostępnianych przez zespół Azure lub partnerów. Hello wynikowa lista może być duży. Witaj dalej przykładach pokazano, jak tooget krótszej listy.
* **Pobierz obraz rodzin**:`Get-AzureVMImage | select ImageFamily` pobiera listę rodzin obrazu pokazując ciągów **ImageFamily** właściwości.
* **Pobierz wszystkie obrazy w określonej rodzinie**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **Znajdź obrazów maszyn wirtualnych**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` polega na filtrowanie hello DataDiskConfiguration właściwość, która ma zastosowanie tylko obrazy tooVM tego polecenia cmdlet. W tym przykładzie filtruje także hello tooonly hello etykiety i obrazu nazwy wyjściowego.
* **Zapisz uogólniony obraz**:`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Zapisz obraz specjalne**:`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > Parametr OSState Hello jest wymagana toocreate obrazu maszyny Wirtualnej, która obejmuje hello dysku systemu operacyjnego i dołączone dyski danych. Jeśli nie używasz parametru hello hello polecenie cmdlet tworzy obrazu systemu operacyjnego. wartość Hello hello parametr wskazuje, czy obraz powitania uogólniony lub specjalizowany, oparta na Określa, czy dysk systemu operacyjnego hello zostało przygotowane do ponownego użycia.

* **Usuń obraz**:`Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Następne kroki
Możesz również [Utwórz maszynę z systemem Windows przy użyciu portalu Azure hello](tutorial.md).
