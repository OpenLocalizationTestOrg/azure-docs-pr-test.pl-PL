---
title: "Cele dotyczące wydajności i skalowalności magazynu platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o obiekty docelowe skalowalności i wydajności usługi Azure Storage, w tym pojemności, współczynnik żądań i przepustowości ruchu przychodzącego i wychodzącego dla obu kont magazynu standard i premium. Zrozumienie celów wydajności dla partycji w ramach każdej z usług Azure Storage."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: ed90e5d63e4c93f9c5054b02d2b4457b44caf6eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Cele usługi Azure Storage dotyczące skalowalności i wydajności
## <a name="overview"></a>Omówienie
W tym temacie opisano tematy dotyczące skalowalności i wydajności dla magazynu Microsoft Azure. Podsumowanie innych limitów Azure, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md).

> [!NOTE]
> Wszystkie konta magazynu Uruchom na nową topologię siecią płaską i obsługuje obiekty docelowe skalowalności i wydajności, opisane poniżej, niezależnie od tego, kiedy zostały utworzone. Aby uzyskać więcej informacji na komputerze o architekturze siecią płaską usługi Azure Storage i skalowalność, zobacz [Microsoft Azure Storage: A wysoce dostępna usługa magazynu w chmurze with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> Obiekty docelowe skalowalności i wydajności wymienione w tym miejscu wysokiej klasy elementów docelowych, ale są osiągalne. Wszystkich przypadkach, współczynnik żądań i przepustowości magazynu konta zależy od rozmiaru obiekty przechowywane, wzorce dostępu do wykorzystania, i wykonuje polecenie Typ obciążenia aplikacji. Należy przetestować usługą w celu ustalenia, czy jego wydajność, spełnia wymagania. Jeśli to możliwe zapobiec nagłym wzrostów w polu szybkość ruchu i sprawdź, czy ruch jest dobrze rozproszone na partycje.
> 
> Gdy aplikacja osiągnie limit co partycji może obsłużyć dla obciążenia, usługi Azure Storage zaczną zwracać kod błędu 503 (serwer jest zajęty) lub kod błędu 500 odpowiedzi (limit czasu operacji). W takim przypadku aplikacji należy używać zasad wykładniczego wycofywania dla ponownych prób. Wykładniczego wycofywania umożliwia obciążenia na partycji zmniejszają i ułatwić limit największego ruchu do tej partycji.
> 
> 

Wymagania aplikacji przekracza wartości docelowe skalowalności konta jednego magazynu, można skompilować aplikację do korzystania z wielu kont magazynu i partycji obiektów danych przez tych kont magazynu. Zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/) informacje dotyczące cennika woluminów.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Wartości docelowe skalowalności dla obiektów blob, kolejek, tabel i plików
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Wartości docelowe skalowalności dysków maszyny wirtualnej
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

Zobacz [rozmiarów maszyn wirtualnych systemu Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [rozmiarów maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) dodatkowe szczegóły.

## <a name="managed-virtual-machine-disks"></a>Dyski zarządzane maszyny wirtualnej

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Dyski maszyny wirtualnej niezarządzanej
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Wartości docelowe skalowalności dla Menedżera zasobów Azure
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Partycje w magazynie Azure
Każdy obiekt, który przechowuje dane, które są przechowywane w usłudze Azure Storage (obiekty BLOB, wiadomości, jednostki i plików) należy do partycji i jest identyfikowany przez klucz partycji. Partycja Określa, jak usługi Azure Storage obciążenia równoważy obiektów blob, wiadomości, jednostki i plików na serwerach, na potrzeby ruchu tych obiektów. Klucz partycji jest unikatowa i jest używana do lokalizowania obiektów blob, wiadomości lub jednostki.

W tabeli [wartości docelowe skalowalności w przypadku kont magazynu standardowego](#standard-storage-accounts) wymieniono cele wydajności dla jednej partycji dla każdej usługi.

Partycje wpływać równoważenia obciążenia i skalowalności dla każdej z usług magazynu w następujący sposób:

* **Obiekty BLOB**: Klucz partycji dla obiekt blob jest nazwa konta, nazwa kontenera + nazwa obiektu blob. Oznacza to, że każdy obiekt blob może zawierać własnej partycji, jeśli obciążenie obiektu blob żąda jej. Obiekty BLOB mogą być rozproszone na wielu serwerach w celu skalowania w poziomie do nich dostęp, ale pojedynczego obiektu blob mogą być przekazywane tylko przez jeden serwer. Obiekty BLOB można grupować logicznie w kontenerów obiektów blob, jednak niektóre powodują nie partycjonowania efekty z grupy.
* **Pliki**: Klucz partycji dla pliku jest kontem nazwa + pliku nazwa udziału. Oznacza to, że wszystkie pliki w udziale plików znajdują się również w jednej partycji.
* **Komunikaty**: Klucz partycji dla wiadomości jest nazwa konta + Nazwa kolejki, tak aby wszystkie komunikaty z kolejki są pogrupowane w jednej partycji i są obsługiwane przez jeden serwer. Różnych kolejek mogą być przetwarzane przez różne serwery w celu zrównoważenia obciążenia dla, jednak może mieć wiele kolejki konta magazynu.
* **Jednostki**: Klucz partycji jest jednostką konta Nazwa + Nazwa tabeli + partycji klucz, w którym klucz partycji to wartość wymaganego zdefiniowane przez użytkownika **PartitionKey** właściwości dla obiektu. Wszystkie jednostki z taką samą wartość klucza partycji są zgrupowane w tej samej partycji i są obsługiwane przez ten sam serwer partycji. Jest to należy zrozumieć projektowanie aplikacji. Aplikacja powinna równoważenie zalet skalowalność rozłożenie jednostek wiele partycji z zalet dostępu do danych grupowanie jednostki w jednej partycji.  

Zaletą do grupowania zestawu jednostek w tabeli w jednej partycji jest możliwa do wykonywania operacji wsadowych atomic między jednostkami w tej samej partycji, ponieważ istnieje partycja na jednym serwerze. W związku z tym jeśli chcesz wykonać operacji wsadowych na grupy jednostek, należy wziąć pod uwagę ich grupowanie z tym samym kluczem partycji. 

Z drugiej strony, jednostek, które są w tej samej tabeli, ale ma różnych kluczach partycji mogą być o zrównoważonym obciążeniu na różnych serwerach, co umożliwia zwiększenie skalowalności.

Szczegółowe zalecenia dotyczące projektowania partycjonowania strategii dla tabel można znaleźć [tutaj](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Zobacz też
* [Szczegóły cennika magazynu](https://azure.microsoft.com/pricing/details/storage/)
* [Subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md)
* [Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure](storage-premium-storage.md)
* [Replikacja usługi Azure Storage](storage-redundancy.md)
* [Wydajność magazynu Microsoft Azure i listę kontrolną skalowalności](storage-performance-checklist.md)
* [Microsoft Azure Storage: Wysokiej dostępności magazynu usługi w chmurze o wysoki poziom spójności](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

