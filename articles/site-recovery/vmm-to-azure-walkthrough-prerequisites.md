---
title: "wymagania wstępne hello aaaReview dla funkcji Hyper-V tooAzure replikację (z programu System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje warunki wstępne hello do replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V lokalnymi w tooAzure chmur programu VMM, za pomocą usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>Krok 2: Przejrzyj wymagania wstępne hello replikacji tooAzure funkcji Hyper-V (w programie VMM)

Po przejrzeniu jest hello [architektura scenariusza](vmm-to-azure-walkthrough-architecture.md), przeczytaj ten artykuł toomake się, że rozumiesz hello wymagania wstępne wdrożenia. 

## <a name="prerequisites-and-limitations"></a>Wymagania wstępne i ograniczenia

**Wymaganie** | **Szczegóły**
--- | ---
**Konto platformy Azure** | Potrzebujesz [konta platformy Microsoft Azure](http://azure.microsoft.com/).
**Magazyn platformy Azure** | Należy toostore replikowane dane konta magazynu platformy Azure.<br/><br/> Konto magazynu Hello musi znajdować się w hello magazyn usług odzyskiwania Azure i tym samym regionie co hello.<br/><br/>Możesz używać [magazynu geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) lub magazynu lokalnie nadmiarowego. Zalecamy magazyn geograficznie nadmiarowy. Z magazynu geograficznie nadmiarowego dane są odporne w przypadku regionalnej awarii lub jeśli nie można odzyskać regionu podstawowego hello.<br/><br/> Możesz używać standardowego konta usługi Azure Storage lub konta usługi Azure [Premium Storage](../storage/common/storage-premium-storage.md). Usługa Premium Storage może obsługiwać obciążenia intensywnie korzystające z operacji we/wy i zwykle jest używana dla maszyn wirtualnych wymagających spójnej wysokiej wydajności we/wy i małych opóźnień. Jeśli używasz usługi Premium Storage do przechowywania replikowanych danych, potrzebujesz też standardowego konta magazynu. Konta standard storage przechowuje dzienników replikacji, które przechwytują zachodzące zmiany lokalne tooon danych.
**Sieć platformy Azure** | Należy [sieć platformy Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md), Połącz toowhich maszynach wirtualnych Azure po w tryb failover. Hello Azure sieć musi znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello.
**Lokalne serwery programu VMM** | Potrzebujesz co najmniej jednego serwera programu VMM z uruchomionym programem System Center 2012 R2 lub nowszym.<br/><br/> Każdy serwer programu VMM musi mieć co najmniej jedną chmurę prywatną. Każda chmura potrzebuje co najmniej jednej grupy hostów.<br/><br/> Serwer VMM Hello musi mieć dostęp do Internetu.
**Lokalna funkcja Hyper-V** | Serwery hosta funkcji Hyper-V musi działać co najmniej Windows Server 2012 R2 z włączonej roli Hyper-V hello lub Microsoft Hyper-V Server 2012 R2. musi być zainstalowana Hello najnowsze aktualizacje.<br/><br/> Witaj hosta funkcji Hyper-V muszą znajdować się w grupie hostów programu VMM (znajdujące się w chmurze VMM).<br/><br/> Host musi mieć przynajmniej jednej maszyny wirtualnej, które mają tooreplicated.<br/><br/> Hosty funkcji Hyper-V musi być połączony toohello internet tooAzure replikacji, bezpośrednio lub za pomocą serwera proxy. Serwery funkcji Hyper-V muszą mieć hello poprawki opisanej w artykule [2961977](https://support.microsoft.com/kb/2961977).
**Lokalne maszyny wirtualne funkcji Hyper-V** | Maszyny wirtualne mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). Nazwa maszyny Wirtualnej Hello można modyfikować po włączeniu replikacji. 




## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 3: Planowanie pojemności](vmm-to-azure-walkthrough-capacity.md)
