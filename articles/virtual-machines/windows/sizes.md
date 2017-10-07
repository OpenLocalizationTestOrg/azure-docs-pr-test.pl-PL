---
title: rozmiary aaaWindows maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft
description: "Wyświetla listę różnych rozmiarów hello dostępnej dla maszyn wirtualnych systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a>Rozmiary maszyn wirtualnych systemu Windows na platformie Azure

W tym artykule opisano dostępne rozmiary hello i opcje dla hello toorun można użyć w aplikacji systemu Windows i obciążeń maszyn wirtualnych platformy Azure. Umożliwia także toobe zagadnienia dotyczące wdrażania uwagę podczas planowania toouse tych zasobów.  W tym artykule jest również dostępny do [maszyn wirtualnych systemu Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


| Typ                     | Rozmiary           |    Opis       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Zastosowania ogólne](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7 | Zrównoważona moc procesora CPU w stosunku do pamięci. Idealnym badań i rozwoju, toomedium małych baz danych i serwerów sieci web ruchu toomedium niski. |
| [Optymalizacja pod kątem obliczeń](sizes-compute.md)        | FS, F             | Duża moc procesora CPU w stosunku do pamięci. Dobrze sprawdzają się w przypadku serwerów sieci Web o średnim ruchu, urządzeń sieciowych, procesów wsadowych i serwerów aplikacji.        |
| [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Wysoki współczynnik pamięci do Procesora. Świetnie relacyjnej bazy danych serwerów, pamięci podręcznych średnia toolarge i analizy w pamięci.                 |
| [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md)        | Ls                | Wysoka przepływność dysku i operacje we/wy. Idealne rozwiązanie w przypadku danych big data oraz baz danych SQL i NoSQL.                                                         |
| [Procesor GPU](sizes-gpu.md)            | WIRTUALIZACJĄ SIECI, NC            | Celem duże Renderowanie grafiki i wideo edycji specjalne maszyn wirtualnych. Dostępne z jednego lub wielu procesorów graficznych.       |
| [Obliczenia o wysokiej wydajności](sizes-hpc.md) | H-A8 11          | Maszyny wirtualne z najszybszymi i najbardziej wydajnymi procesorami CPU oraz, opcjonalnie, interfejsami sieciowymi zapewniającymi wysoką przepływność (RDMA). 

<br> 

- Aby uzyskać informacje o cenach z hello różne rozmiary, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows). 
- ograniczenia ogólne toosee na maszynach wirtualnych Azure, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../../azure-subscription-service-limits.md).
- Koszty przechowywania są obliczane osobno na podstawie używane strony w hello konta magazynu. Aby uzyskać szczegółowe informacje [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).
- Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.



## <a name="rest-api"></a>Interfejs API REST

Dla informacji o używaniu tooquery interfejsu API REST hello rozmiarów maszyn wirtualnych zobacz następujące hello:

- [Lista dostępne rozmiary maszyny wirtualnej do zmiany rozmiaru](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [Lista dostępne rozmiary maszyny wirtualnej w ramach subskrypcji](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [Lista dostępne rozmiary maszyny wirtualnej w zestawie dostępności](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

Dowiedz się więcej na temat [jednostki (ACU) rozwiązań usługi obliczenia Azure](acu.md) ułatwia porównanie wydajności obliczeniowej różnych jednostki SKU Azure.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej na temat hello różnych rozmiarów maszyn wirtualnych, które są dostępne:
- [Zastosowania ogólne](sizes-general.md)
- [Optymalizacja pod kątem obliczeń](sizes-compute.md)
- [Optymalizacja pod kątem pamięci](../virtual-machines-windows-sizes-memory.md)
- [Optymalizacja pod kątem magazynu](../virtual-machines-windows-sizes-storage.md)
- [Optymalizacja pod kątem procesora GPU](sizes-gpu.md)
- [Obliczenia o wysokiej wydajności](sizes-hpc.md)



