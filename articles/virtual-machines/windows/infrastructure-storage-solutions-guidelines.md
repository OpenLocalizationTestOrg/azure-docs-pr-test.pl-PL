---
title: "aaaStorage rozwiązań dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello klucza projekt i implementację wskazówki dotyczące wdrażania rozwiązania magazynu w usług infrastruktury platformy Azure."
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
ms.openlocfilehash: 57c27a7305964a56e6b2d1e73dee8e7da19fa8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>Wskazówki dotyczące infrastruktury magazynu Azure dla maszyn wirtualnych systemu Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na potrzeby magazynu i zagadnienia dotyczące projektowania dla osiągnięcia wydajność optymalne maszyny wirtualnej (VM).

## <a name="implementation-guidelines-for-storage"></a>Implementacja — wskazówki dla magazynu
Decyzje:

* Czy będą toouse Azure dysków zarządzane lub niezarządzane dysków?
* Potrzebujesz toouse standardowa lub Premium magazynu dla obciążenia?
* Potrzebujesz dysków toocreate Rozkładanie dysku większych niż 4TB?
* Potrzebujesz dysku rozkładanie tooachieve optymalną wydajność We/Wy dla obciążenia?
* Jaki zestaw kont magazynu potrzebujesz toohost infrastruktury i obciążenia IT?

Zadania:

* Przegląd wymagań operacji We/Wy aplikacji hello wdrażania oraz Zaplanuj hello odpowiedniej liczby i typ konta magazynu.
* Utwórz zestaw hello kont magazynu, zgodnie z konwencją nazewnictwa. Możesz użyć programu Azure PowerShell lub portalu hello.

## <a name="storage"></a>Magazyn
Usługa Azure Storage jest kluczowym elementem wdrażania i zarządzania nimi w maszynach wirtualnych (VM) i aplikacji. Usługa Azure Storage udostępnia usługi do przechowywania plików danych, danych bez struktury i komunikaty, a jest również częścią hello infrastruktury obsługi maszyn wirtualnych.

[Azure dysków zarządzanych](../../storage/storage-managed-disks-overview.md) obsługuje magazynu dla Ciebie w tle hello. W przypadku niezarządzanych dysków tworzenia kont magazynu toohold hello dysków (pliki VHD) na maszynach wirtualnych platformy Azure. Podczas skalowania w, należy się upewnić, że utworzona dodatkowych kont magazynu, więc nie przekraczają hello limitu IOPS dla magazynu za pomocą dowolnego z dysków. W przypadku zarządzanych dysków obsługi magazynu nie jest już ograniczeniem limity konta magazynu hello (takie jak IOPS 20 000 / konta). Możesz również już toocopy kont magazynu toomultiple niestandardowych obrazów (pliki VHD). Można nimi zarządzać w centralnej lokalizacji — jedno konto magazynu na region platformy Azure — i używać ich toocreate setki maszyn wirtualnych w ramach subskrypcji. Firma Microsoft zaleca się, że używasz dysków zarządzanych w przypadku nowych wdrożeń.

Istnieją dwa typy kont magazynu do obsługi maszyn wirtualnych:

* Nadaj kont magazynu w warstwie standardowa, możesz uzyskać dostępu do magazynu tooblob (używanych do przechowywania dysków maszyny Wirtualnej platformy Azure), tabela magazynów, magazyn kolejek i magazyn plików.
* [Magazyn w warstwie Premium](../../storage/storage-premium-storage.md) kont dostarczania obsługi wysokiej wydajności i małych opóźnień dysków dla intensywnych obciążeń we/wy, takich jak serwery SQL w klastrze (AlwaysOn). Magazyn w warstwie Premium obecnie obsługuje wyłącznie dyski maszyny Wirtualnej platformy Azure.

Platforma Azure tworzy maszyny wirtualne z dysku systemu operacyjnego, dysku tymczasowym i zero lub więcej dysków z danymi opcjonalne. Hello dysku systemu operacyjnego i dysków z danymi są stronicowe Azure, natomiast dysku tymczasowym hello są przechowywane lokalnie w węźle hello, w którym mieszka hello maszyny. Zachowaj ostrożność podczas projektowania aplikacji tooonly używania tego dysku tymczasowym nietrwałe danych jako powitalne możliwość migracji maszyn wirtualnych między hostami podczas obsługi zdarzenia. Dane przechowywane na dysku tymczasowym hello mogłyby zostać utracone.

Trwałości i wysokiej dostępności jest zapewniana przez hello podstawowej usługi Azure Storage środowiska tooensure czy danych pozostaje chroniona przed nieplanowana konserwacja lub sprzętu. Podczas projektowania środowiska usługi Azure Storage, można wybrać tooreplicate magazynu maszyny Wirtualnej:

* lokalnie w danym centrum danych Azure
* w centrach danych platformy Azure w danym regionie
* w centrach danych platformy Azure w różnych regionach

Możesz przeczytać [więcej informacji na temat opcji replikacji hello wysokiej dostępności](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Dysków systemu operacyjnego i dysków z danymi mieć maksymalnie rozmiar równy 4TB. Możesz użyć funkcji miejsca do magazynowania w systemie Windows Server 2012 lub nowszym toosurpass ten limit Grupując dane dysków toopresent logicznej woluminów większych niż 4TB tooyour maszyny Wirtualnej.

Istnieje kilka ograniczeń skalowalności przy projektowaniu wdrożeń usługi Azure Storage — Aby uzyskać więcej informacji, zobacz [limity subskrypcji i usługi Microsoft Azure, przydziały i ograniczenia](../../azure-subscription-service-limits.md#storage-limits). Zobacz też [elementy docelowe skalowalności i wydajności magazynu Azure](../../storage/storage-scalability-targets.md).

Do przechowywania aplikacji można przechowywać danych obiektów niestrukturalnych, takich jak dokumenty, obrazy, kopie zapasowe, dane konfiguracji, dzienniki itp. przy użyciu magazynu obiektów blob. Zamiast aplikacji zapisywania tooa toohello dysku wirtualnego maszyny Wirtualnej aplikacja hello może zapisywać bezpośrednio tooAzure magazynu obiektów blob. Magazyn obiektów blob są także możliwość hello [hot i cool warstw magazynowania](../../storage/storage-blob-storage-tiers.md) w zależności od dostępności potrzeby i ograniczenia kosztów.

## <a name="striped-disks"></a>Rozłożone dysków
Oprócz pozwala toocreate dysków większych niż 4TB w wielu przypadkach, przy użyciu rozkładanie dysków danych zwiększa wydajność dzięki wielu obiektów blob magazynu hello tooback jednego woluminu. Rozkładanie, toowrite wymagane hello We/Wy i odczytu danych z jednego dysku logicznego będzie kontynuowana równolegle.

Azure nakłada limity hello liczba dysków danych oraz dostępnej przepustowości, w zależności od rozmiaru maszyny Wirtualnej hello. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md).

Jeśli używasz rozkładanie dysków danych Azure, należy wziąć pod uwagę następujące wytyczne hello:

* Dołącz hello dyski danych maksymalny dozwolony dla hello rozmiar maszyny Wirtualnej.
* Użyj funkcji miejsca do magazynowania.
* Unikaj używania opcji buforowania dysku danych Azure (zasad buforowania = None).

Aby uzyskać więcej informacji, zobacz [miejsca do magazynowania — projektowanie pod kątem wydajności](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).

## <a name="multiple-storage-accounts"></a>Wiele kont magazynu
Ta sekcja nie ma zastosowania zbyt[dysków zarządzanych Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ponieważ nie zostanie utworzony oddzielny magazyn kont. 

Podczas projektowania środowiska usługi Azure Storage dla dysków niezarządzane, można użyć wielu kont magazynu jako hello liczbę maszyn wirtualnych wdrożeniem wzrostu. To rozwiązanie pomaga w rozłożeniu limit hello we/wy na powitania podstawowej usługi Azure Storage infrastruktury toomaintain optymalnej wydajności dla maszyn wirtualnych i aplikacji. Podczas projektowania aplikacji hello, które wdrażasz należy wziąć pod uwagę wymagania dotyczące operacji We/Wy hello każda maszyna wirtualna ma i Saldo limit tych maszyn wirtualnych, wielu kont magazynu Azure. Spróbuj tooavoid wszystkie hello wysokiej we/wy wymagających maszyn wirtualnych na kontach magazynu toojust co najmniej dwa grupowania.

Aby uzyskać więcej informacji na temat możliwości hello we/wy hello inne opcje usługi Azure Storage, a niektóre zalecane maksymalne wartości, zobacz [elementy docelowe skalowalności i wydajności magazynu Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

