---
title: "aaaAbout dysków i wirtualne dyski twarde dla maszyn wirtualnych systemu Linux, Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Poznaj podstawy hello dysków i wirtualne dyski twarde dla maszyn wirtualnych systemu Linux na platformie Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1155d773136677553d263c17fbf8b224035d96bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>O dyskach i wirtualne dyski twarde dla maszyn wirtualnych systemu Linux platformy Azure
Podobnie jak dowolnego innego komputera maszynach wirtualnych platformy Azure, użyj dysków, gdy toostore miejscu systemu operacyjnego, aplikacje i dane. Wszystkie maszyny wirtualne platformy Azure są co najmniej dwa dyski — dysk systemu operacyjnego Linux i dysku tymczasowym. dysk systemu operacyjnego Hello jest tworzony z obrazu, a zarówno hello dysku systemu operacyjnego i obraz powitania są faktycznie wirtualnych dysków twardych (VHD) przechowywane w koncie magazynu platformy Azure. Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde. 

W tym artykule firma Microsoft będzie porozmawiać na temat różnych zastosowań hello hello dysków i omówiono w nim hello różnych typów dysków można tworzyć i używać. W tym artykule jest również dostępny do [maszyn wirtualnych Windows](storage-about-disks-and-vhds-windows.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Dysków używanych przez maszyny wirtualne

Spójrzmy na jak dyski hello są używane przez hello maszyn wirtualnych.

## <a name="operating-system-disk"></a>Dysk systemu operacyjnego
Co maszyna wirtualna ma jeden dysk systemu operacyjnego podłączonego. Jest zarejestrowany jako dysk SATA, a etykietą /dev/sda domyślnie. Ten dysk ma maksymalną pojemność 2048 gigabajtów (GB). 

## <a name="temporary-disk"></a>Tymczasowe dysku
Każda maszyna wirtualna zawiera dysku tymczasowym. dysku tymczasowym Hello zapewnia krótkoterminowy magazyn dla aplikacji i procesów i jest zamierzone tooonly przechowywania danych, takich jak pliki strony lub wymiany. Dane na dysku tymczasowym hello mogą zostać utracone podczas [zdarzenia konserwacji](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) lub gdy użytkownik [ponownego wdrażania maszyny Wirtualnej](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Podczas standardowego ponowne uruchomienie hello maszyny Wirtualnej ma utrwalić danych hello na powitania tymczasowej stacji.

W przypadku maszyn wirtualnych systemu Linux, dysk hello jest zwykle **/dev/sdb** sformatowany i jest zainstalowany za**katalogu/mnt** przez hello agenta systemu Linux platformy Azure. Hello rozmiar dysku tymczasowym hello zależy od rozmiaru hello hello maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md).

Aby uzyskać więcej informacji o używaniu dysku tymczasowym hello Azure, zobacz [opis hello tymczasowej stacji na maszynach wirtualnych Azure firmy Microsoft](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Dysk z danymi
Dysk z danymi to wirtualny dysk twardy jest danych aplikacji toostore maszyny wirtualnej podłączone tooa lub inne dane, które należy tookeep. Dyski danych są rejestrowane jako dyski SCSI i są oznaczone literą, którą można wybrać. Każdy dysk danych ma maksymalną pojemność 4095 GB. Witaj rozmiar maszyny wirtualnej hello Określa, jak wiele dysków z danymi można dołączyć tooit i hello typu magazynu, można użyć toohost hello dysków.

> [!NOTE]
> Aby uzyskać więcej informacji o pojemności maszyn wirtualnych, zobacz [rozmiary maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md).
> 

Azure tworzy dysk systemu operacyjnego, podczas tworzenia maszyny wirtualnej z obrazu. Jeśli używasz obrazu, który zawiera dyski danych Azure tworzy również hello dysków danych podczas tworzenia maszyny wirtualnej hello. W przeciwnym razie możesz dodać dysk danych, po utworzeniu maszyny wirtualnej hello.

Można dodać maszyny wirtualnej tooa dysków danych w dowolnym momencie przez **dołączanie** hello maszyny wirtualnej toohello dysku. Można użyć wirtualnego dysku twardego został przekazany albo skopiowane tooyour konta magazynu lub jeden tego Azure utworzy. Dołączenie dysku danych skojarzenie pliku wirtualnego dysku twardego hello z hello maszyny Wirtualnej, umieszczając dzierżawy na powitania wirtualnego dysku twardego nie może być usunięty z magazynu nadal będzie dołączony.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Rozwiązywanie problemów
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Następne kroki
* [Dołączenie dysku](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd dodatkowy magazyn dla maszyny Wirtualnej.
* [Należy skonfigurować oprogramowanie RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) nadmiarowości.
* [Przechwytywanie maszyny wirtualnej systemu Linux](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) , można szybko wdrożyć dodatkowe maszyny wirtualne.

