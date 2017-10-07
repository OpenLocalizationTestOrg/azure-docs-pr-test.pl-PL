---
title: "aaaAbout dysków i wirtualne dyski twarde dla maszyn wirtualnych systemu Windows, Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Poznaj podstawy hello dysków i wirtualne dyski twarde dla systemu Windows maszyny wirtualne na platformie Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>O dyskach i wirtualne dyski twarde dla maszyn wirtualnych systemu Windows Azure
Podobnie jak dowolnego innego komputera maszynach wirtualnych platformy Azure, użyj dysków, gdy toostore miejscu systemu operacyjnego, aplikacje i dane. Wszystkie maszyny wirtualne platformy Azure są co najmniej dwa dyski — dysk systemu operacyjnego Windows i dysku tymczasowym. dysk systemu operacyjnego Hello jest tworzony z obrazu, a zarówno hello dysku systemu operacyjnego i obraz powitania są wirtualnych dysków twardych (VHD) przechowywane w koncie magazynu platformy Azure. Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde. 

W tym artykule firma Microsoft będzie porozmawiać na temat różnych zastosowań hello hello dysków i omówiono w nim hello różnych typów dysków można tworzyć i używać. W tym artykule jest również dostępny do [maszyn wirtualnych systemu Linux](storage-about-disks-and-vhds-linux.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Dysków używanych przez maszyny wirtualne

Spójrzmy na jak dyski hello są używane przez hello maszyn wirtualnych.

### <a name="operating-system-disk"></a>Dysk systemu operacyjnego
Co maszyna wirtualna ma jeden dysk systemu operacyjnego podłączonego. Ma ona zarejestrowana jako dyski SATA i oznaczone jako dysk C: hello domyślnie. Ten dysk ma maksymalną pojemność 2048 gigabajtów (GB). 

### <a name="temporary-disk"></a>Tymczasowe dysku
Każda maszyna wirtualna zawiera dysku tymczasowym. dysku tymczasowym Hello zapewnia krótkoterminowy magazyn dla aplikacji i procesów i jest zamierzone tooonly przechowywania danych, takich jak pliki strony lub wymiany. Dane na dysku tymczasowym hello mogą zostać utracone podczas [zdarzenia konserwacji](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) lub gdy użytkownik [ponownego wdrażania maszyny Wirtualnej](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Podczas standardowego ponowne uruchomienie hello maszyny Wirtualnej ma utrwalić danych hello na powitania tymczasowej stacji.

dysku tymczasowym Hello jest oznaczona jako hello dysku D: domyślnie i używany do przechowywania pagefile.sys. tooremap tego dysku tooa inną literę dysku, zobacz [zmiany hello literę dysku tymczasowym systemu Windows hello](../virtual-machines/windows/change-drive-letter.md). Hello rozmiar dysku tymczasowym hello zależy od rozmiaru hello hello maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [maszyn wirtualnych rozmiary dla systemu Windows](../virtual-machines/windows/sizes.md).

Aby uzyskać więcej informacji o używaniu dysku tymczasowym hello Azure, zobacz [opis hello tymczasowej stacji na maszynach wirtualnych Azure firmy Microsoft](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Dysk z danymi
Dysk z danymi to wirtualny dysk twardy jest danych aplikacji toostore maszyny wirtualnej podłączone tooa lub inne dane, które należy tookeep. Dyski danych są rejestrowane jako dyski SCSI i są oznaczone literą, którą można wybrać. Każdy dysk danych ma maksymalną pojemność 4095 GB. Witaj rozmiar maszyny wirtualnej hello Określa, jak wiele dysków z danymi można dołączyć tooit i hello typu magazynu, można użyć toohost hello dysków.

> [!NOTE]
> Aby uzyskać więcej informacji na temat pojemności maszyn wirtualnych, zobacz [maszyn wirtualnych rozmiary dla systemu Windows](../virtual-machines/windows/sizes.md).
> 

Azure tworzy dysk systemu operacyjnego, podczas tworzenia maszyny wirtualnej z obrazu. Jeśli używasz obrazu, który zawiera dyski danych Azure tworzy również hello dysków danych podczas tworzenia maszyny wirtualnej hello. W przeciwnym razie możesz dodać dysk danych, po utworzeniu maszyny wirtualnej hello.

Można dodać maszyny wirtualnej tooa dysków danych w dowolnym momencie przez **dołączanie** hello maszyny wirtualnej toohello dysku. Można użyć wirtualnego dysku twardego został przekazany albo skopiowane tooyour konta magazynu lub jeden tego Azure utworzy. Dołączenie dysku danych skojarzenie pliku wirtualnego dysku twardego hello z hello maszyny Wirtualnej przez umieszczenie dzierżawy na powitania wirtualnego dysku twardego nie może być usunięty z magazynu nadal będzie dołączony.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Zalecamy ostatniego: Użyj PRZYCINANIE z niezarządzanego dyski standardowe 

Jeśli używasz niezarządzane dyski standardowe (HDD), należy włączyć PRZYCINANIE. PRZYCINANIE odrzuca nieużywanych bloków na dysku hello tak rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz. Można to zapisanie kosztów, jeśli Tworzenie dużych plików, a następnie usuń je. 

Możesz uruchomić to polecenie toocheck hello PRZYCINANIA ustawienie. Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:


```
fsutil behavior query DisableDeleteNotify
```

Jeśli polecenie hello zwraca wartość 0, PRZYCINANIE włączono poprawnie. Jeśli zmienna zwraca 1, uruchom następujące polecenie tooenable PRZYCINANIE hello:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Uwaga: Obsługa funkcji usuwania rozpoczyna się od systemu Windows Server 2012 / Windows 8 lub nowszym, można znaleźć w temacie [nowy interfejs API umożliwia aplikacjom toosend "PRZYCINANIE i Usuń mapowanie" wskazówki toostorage nośnika](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Następne kroki
* [Dołączenie dysku](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd dodatkowy magazyn dla maszyny Wirtualnej.
* [Zmień hello litera dysku tymczasowego Windows hello](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) , aplikacja może używać hello D: dysku danych.

