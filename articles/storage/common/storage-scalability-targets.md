---
title: "aaaAzure cele dotyczące wydajności i skalowalności magazynu | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello elementy docelowe skalowalności i wydajności usługi Azure Storage, w tym pojemności, współczynnik żądań i przepustowości ruchu przychodzącego i wychodzącego dla obu kont magazynu standard i premium. Zrozumienie celów wydajności dla partycji w ramach każdej z usług Azure Storage hello."
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
ms.openlocfilehash: 7afe4366a02887b4e3d9781c26c8adda81adce95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Cele usługi Azure Storage dotyczące skalowalności i wydajności
## <a name="overview"></a>Omówienie
W tym temacie opisano hello tematy dotyczące skalowalności i wydajności dla magazynu Microsoft Azure. Podsumowanie innych limitów Azure, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../../azure-subscription-service-limits.md).

> [!NOTE]
> Wszystkie konta magazynu Uruchom na powitania nową siecią płaską topologię i obsługuje cele wydajności i skalowalności hello opisane poniżej, niezależnie od tego, kiedy zostały utworzone. Aby uzyskać więcej informacji na powitania usługi Azure Storage siecią płaską architektury i skalowalność, zobacz [Microsoft Azure Storage: A wysoce dostępna usługa magazynu w chmurze with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> Witaj skalowalność i wydajność cele wymienione w tym miejscu wysokiej klasy elementów docelowych, ale są osiągalne. We wszystkich przypadkach, szybkość i przepustowości konta magazynu zależy od rozmiaru hello obiekty przechowywane, Żądanie hello hello wzorce dostępu do użycia oraz hello typ obciążenia, który wykonuje aplikacji. Można toodetermine Twojego usługi tootest się, czy jego wydajność, spełnia wymagania. Jeśli to możliwe zapobiec nagłym największego hello szybkość ruchu i sprawdź, czy ruch jest dobrze rozproszone na partycje.
> 
> Gdy aplikacja osiągnie limit hello co partycji może obsłużyć dla obciążenia, usługi Azure Storage rozpocznie się kod błędu tooreturn 503 (serwer jest zajęty) lub kod błędu: 500 odpowiedzi (limit czasu operacji). W takim przypadku aplikacji hello należy używać zasad wykładniczego wycofywania dla ponownych prób. Hello wykładniczego wycofywania umożliwia obciążenia hello hello partycji toodecrease i tooease limit wzrostów w ruchu toothat partycji.
> 
> 

Aplikacji hello musi przekroczyć hello wartości docelowe skalowalności konta magazynu jednego, można utworzyć wiele kont magazynu toouse Twojej aplikacji i partycji obiektów danych przez tych kont magazynu. Zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/) informacje dotyczące cennika woluminów.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Wartości docelowe skalowalności dla obiektów blob, kolejek, tabel i plików
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Wartości docelowe skalowalności dysków maszyny wirtualnej
[!INCLUDE [azure-storage-limits-vm-disks](../../../includes/azure-storage-limits-vm-disks.md)]

Zobacz [rozmiarów maszyn wirtualnych systemu Windows](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [rozmiarów maszyn wirtualnych systemu Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) dodatkowe szczegóły.

## <a name="managed-virtual-machine-disks"></a>Dyski zarządzane maszyny wirtualnej

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Dyski maszyny wirtualnej niezarządzanej
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Wartości docelowe skalowalności dla Menedżera zasobów Azure
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Partycje w magazynie Azure
Każdy obiekt, który przechowuje dane, które są przechowywane w usłudze Azure Storage (obiekty BLOB, wiadomości, jednostki i plików) należy tooa partycji i jest identyfikowany przez klucz partycji. partycja Hello Określa, jak obciążenia usługi Azure Storage równoważy obiektów blob, wiadomości, jednostki i plików na serwerach toomeet hello ruchu potrzeb tych obiektów. Klucz partycji Hello jest unikatowy i jest używany toolocate obiektów blob, wiadomości lub jednostki.

Hello tabeli pokazano powyżej [wartości docelowe skalowalności w przypadku kont magazynu standardowego](#standard-storage-accounts) list hello cele wydajności dla jednej partycji dla każdej usługi.

Partycje wpływać równoważenia obciążenia i skalowalności dla każdej z usług magazynu hello w hello następujące sposoby:

* **Obiekty BLOB**: hello klucza partycji dla obiekt blob jest nazwa konta, nazwa kontenera + nazwa obiektu blob. Oznacza to, że każdy obiekt blob może zawierać własnej partycji, jeśli obciążenie hello blob żąda jej. Obiekty BLOB mogą być rozproszone na wielu serwerach w kolejności tooscale limit toothem dostępu, ale pojedynczego obiektu blob mogą być przekazywane tylko przez jeden serwer. Obiekty BLOB można grupować logicznie w kontenerów obiektów blob, jednak niektóre powodują nie partycjonowania efekty z grupy.
* **Pliki**: hello klucza partycji dla pliku jest kontem nazwa + pliku nazwa udziału. Oznacza to, że wszystkie pliki w udziale plików znajdują się również w jednej partycji.
* **Komunikaty**: hello klucza partycji dla wiadomości jest nazwa konta hello + Nazwa kolejki, więc wszystkie wiadomości w kolejce są pogrupowane w jednej partycji i są obsługiwane przez jeden serwer. Różnych kolejek mogą być przetwarzane przez różne serwery toobalance hello obciążenia dla, jednak może mieć wiele kolejki konta magazynu.
* **Jednostki**: hello klucza partycji dla jednostki jest nazwa konta + Nazwa tabeli + klucza partycji, gdzie klucz partycji hello jest wartością hello hello wymagane użytkownika **PartitionKey** właściwości hello jednostki. Wszystkie jednostki z samą wartość klucza partycji są zgrupowane w hello sam partycji i są obsługiwane przez hello sam hello partycji serwera. Jest to ważne toounderstand punktu projektowanie aplikacji. Aplikacja powinna równoważenie zalet skalowalność hello rozłożenie jednostek wiele partycji z hello danych access zalety grupowanie jednostki w jednej partycji.  

Zaletą toogrouping zestawu jednostek w tabeli w jednej partycji jest możliwe tooperform operacji wsadowych atomic między jednostkami w hello sam partycji, ponieważ istnieje partycja na jednym serwerze. W związku z tym, jeśli chcesz tooperform operacji wsadowych na grupy jednostek, należy wziąć pod uwagę zgrupować je za pomocą hello tego samego klucza partycji. 

Na hello drugiej strony, jednostek, które znajdują się w hello sam tabeli, ale ma różnych kluczach partycji mogą być obsługiwane na różnych serwerach, dzięki czemu możliwe toohave większą skalowalność.

Szczegółowe zalecenia dotyczące projektowania partycjonowania strategii dla tabel można znaleźć [tutaj](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Zobacz też
* [Szczegóły cennika magazynu](https://azure.microsoft.com/pricing/details/storage/)
* [Subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../../azure-subscription-service-limits.md)
* [Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure](../storage-premium-storage.md)
* [Replikacja usługi Azure Storage](../storage-redundancy.md)
* [Wydajność magazynu Microsoft Azure i listę kontrolną skalowalności](../storage-performance-checklist.md)
* [Microsoft Azure Storage: Wysokiej dostępności magazynu usługi w chmurze o wysoki poziom spójności](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

