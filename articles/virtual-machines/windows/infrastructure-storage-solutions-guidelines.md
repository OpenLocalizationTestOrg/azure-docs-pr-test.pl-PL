---
title: "Rozwiązań magazynowania dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat klucza projekt i implementację wskazówki dotyczące wdrażania rozwiązania magazynu w usług infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ba0d66c5af771ebcb3ca8e6742e15a5506d8fd61
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>Wskazówki dotyczące infrastruktury magazynu Azure dla maszyn wirtualnych systemu Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na potrzeby magazynu i zagadnienia dotyczące projektowania dla osiągnięcia wydajność optymalne maszyny wirtualnej (VM).

## <a name="implementation-guidelines-for-storage"></a>Implementacja — wskazówki dla magazynu
Decyzje:

* Czy będą używały Azure dysków zarządzane lub niezarządzane dyski?
* Czy należy użyć magazynu Standard lub Premium dla obciążenia?
* Potrzebujesz rozkładanie do tworzenia dysków większych niż 4TB?
* Potrzebujesz Rozkładanie dysku, aby osiągnąć optymalną wydajność We/Wy dla obciążenia?
* Jaki zestaw kont magazynu jest potrzebne do obsługi infrastruktury i obciążenia IT?

Zadania:

* Przegląd wymagań operacji We/Wy aplikacji, wdrażania i planowanie odpowiedniej liczby i typ konta magazynu.
* Utwórz zbiór kont magazynu, zgodnie z konwencją nazewnictwa. Można użyć programu Azure PowerShell lub w portalu.

## <a name="storage"></a>Magazyn
Usługa Azure Storage jest kluczowym elementem wdrażania i zarządzania nimi w maszynach wirtualnych (VM) i aplikacji. Usługa Azure Storage udostępnia usługi do przechowywania plików danych, danych bez struktury i komunikaty, a jest również częścią infrastruktury obsługi maszyn wirtualnych.

[Azure dysków zarządzanych](../../storage/storage-managed-disks-overview.md) obsługuje magazynu dla Ciebie w tle. W przypadku niezarządzanych dysków tworzenia kont magazynu do przechowywania dysków (pliki VHD) na maszynach wirtualnych platformy Azure. Podczas skalowania w, należy się upewnić się, że utworzona dodatkowych kont magazynu, więc nie przekracza limitu IOPS dla magazynu za pomocą dowolnego z dysków. W przypadku zarządzanych dysków obsługi magazynu nie jest już ograniczeniem limity konta magazynu (takie jak IOPS 20 000 / konta). Masz już również skopiować niestandardowe obrazy (pliki VHD) na wielu kont magazynu. Można nimi zarządzać w centralnej lokalizacji — jedno konto magazynu na region platformy Azure — i używać ich do tworzenia setki maszyn wirtualnych w ramach subskrypcji. Firma Microsoft zaleca się, że używasz dysków zarządzanych w przypadku nowych wdrożeń.

Istnieją dwa typy kont magazynu do obsługi maszyn wirtualnych:

* Dostęp do magazynu obiektów blob (używanych do przechowywania dysków maszyny Wirtualnej platformy Azure), Magazyn tabel, magazyn kolejek i magazyn plików należy podać kont magazynu w warstwie standardowa.
* [Magazyn w warstwie Premium](../../storage/storage-premium-storage.md) kont dostarczania obsługi wysokiej wydajności i małych opóźnień dysków dla intensywnych obciążeń we/wy, takich jak serwery SQL w klastrze (AlwaysOn). Magazyn w warstwie Premium obecnie obsługuje wyłącznie dyski maszyny Wirtualnej platformy Azure.

Platforma Azure tworzy maszyny wirtualne z dysku systemu operacyjnego, dysku tymczasowym i zero lub więcej dysków z danymi opcjonalne. Dysk systemu operacyjnego i dysków z danymi są stronicowe Azure, natomiast dysku tymczasowym są przechowywane lokalnie w węźle, w którym mieszka maszyny. Zachowaj ostrożność podczas projektowania aplikacji do użycia tego dysku tymczasowym tylko dla danych nietrwałe jako maszyna wirtualna może migrować między hostami podczas obsługi zdarzenia. Może spowodować utratę wszystkich danych przechowywanych na dysku tymczasowym.

Trwałości i wysokiej dostępności, są udostępniane przez podstawowego środowiska usługi Azure Storage, upewnij się, że dane pozostaje chroniona przed nieplanowana konserwacja lub sprzętu. Podczas projektowania środowiska usługi Azure Storage, można replikować magazynu maszyny Wirtualnej:

* lokalnie w danym centrum danych Azure
* w centrach danych platformy Azure w danym regionie
* w centrach danych platformy Azure w różnych regionach

Możesz przeczytać [więcej informacji na temat opcji replikacji w celu zapewnienia wysokiej dostępności](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Dysków systemu operacyjnego i dysków z danymi mieć maksymalnie rozmiar równy 4TB. Powoduje przekroczenie tego limitu przez grupując dysków z danymi do prezentowania logicznej woluminów większych niż 4TB do maszyny Wirtualnej, można użyć funkcji miejsca do magazynowania w systemie Windows Server 2012 lub nowszym.

Istnieje kilka ograniczeń skalowalności przy projektowaniu wdrożeń usługi Azure Storage — Aby uzyskać więcej informacji, zobacz [limity subskrypcji i usługi Microsoft Azure, przydziały i ograniczenia](../../azure-subscription-service-limits.md#storage-limits). Zobacz też [elementy docelowe skalowalności i wydajności magazynu Azure](../../storage/storage-scalability-targets.md).

Do przechowywania aplikacji można przechowywać danych obiektów niestrukturalnych, takich jak dokumenty, obrazy, kopie zapasowe, dane konfiguracji, dzienniki itp. przy użyciu magazynu obiektów blob. Zamiast aplikacji zapisywania dołączony do maszyny Wirtualnej wirtualny dysk aplikację można napisać bezpośrednio do magazynu obiektów blob platformy Azure. Magazyn obiektów blob udostępnia również możliwość [hot i cool warstw magazynowania](../../storage/storage-blob-storage-tiers.md) w zależności od dostępności potrzeby i ograniczenia kosztów.

## <a name="striped-disks"></a>Rozłożone dysków
Oprócz umożliwia tworzenie dysków większych niż 4TB w wielu przypadkach dla dysków z danymi przy użyciu rozkładanie zwiększa wydajność dzięki wielu obiektów blob kopii magazynu jednego woluminu. Z rozkładanie, we/wy wymagane do zapisu i odczytu danych z jednego dysku logicznego przebieg równolegle.

Azure nakłada ograniczenia dotyczące liczby dysków danych i dostępnej przepustowości, w zależności od rozmiaru maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md).

Jeśli używasz rozkładanie dysków danych Azure, należy wziąć pod uwagę następujące wytyczne:

* Podłącz odpowiednie dyski danych maksymalny dozwolony rozmiar maszyny Wirtualnej.
* Użyj funkcji miejsca do magazynowania.
* Unikaj używania opcji buforowania dysku danych Azure (zasad buforowania = None).

Aby uzyskać więcej informacji, zobacz [miejsca do magazynowania — projektowanie pod kątem wydajności](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).

## <a name="multiple-storage-accounts"></a>Wiele kont magazynu
Ta sekcja nie ma zastosowania do [dysków zarządzanych Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ponieważ nie zostanie utworzony oddzielny magazyn kont. 

Podczas projektowania środowiska usługi Azure Storage dla dysków niezarządzane, można użyć wielu kont magazynu jako liczbę maszyn wirtualnych wdrożeniem wzrostu. To rozwiązanie pomaga w rozłożeniu limit operacji We/Wy, w ramach podstawowej infrastruktury magazynu Azure, aby utrzymać optymalną wydajność dla maszyn wirtualnych i aplikacji. Podczas projektowania aplikacji, które wdrażasz należy wziąć pod uwagę wymagania we/wy, które każda maszyna wirtualna ma i Saldo limit tych maszyn wirtualnych, wielu kont magazynu Azure. Należy unikać grupowanie wszystkich wysokiej we/wy wymagających maszyn wirtualnych w celu tylko jeden lub dwa konta magazynu.

Więcej informacji na temat możliwości we/wy różnych opcji magazynu Azure i niektóre zalecamy maksymalne wartości, zobacz [elementy docelowe skalowalności i wydajności magazynu Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

