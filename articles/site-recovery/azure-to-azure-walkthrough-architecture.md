---
title: "Architektura hello aaaReview replikacji maszyn wirtualnych Azure między regiony platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania maszyn wirtualnych platformy Azure między regiony platformy Azure przy użyciu usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a>Krok 1: Przegląd architektury hello replikacji maszyny Wirtualnej Azure między regiony platformy Azure


Po przejrzeniu hello [czynności przeglądu](azure-to-azure-walkthrough-overview.md) dla tego wdrożenia, przeczytaj ten artykuł toounderstand hello składniki i procesy stosowane podczas replikacji i odzyskiwania maszyn wirtualnych platformy Azure (maszyny wirtualne) z jedną tooanother region platformy Azure, przy użyciu [Usługi azure Site Recovery](site-recovery-overview.md).

- Po zakończeniu hello artykuł ma przejrzysty działania region tooanother replikacji maszyny Wirtualnej platformy Azure.
- Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>Azure replikacji maszyny Wirtualnej za pomocą hello usługi Site Recovery jest obecnie w przeglądzie.



## <a name="architectural-components"></a>Składniki architektury

powitania po diagram przedstawia ogólny widok środowiska maszyny Wirtualnej platformy Azure w określonym regionie (w tym przykładzie hello wschodnie stany USA lokalizacji). W środowisku maszyny Wirtualnej platformy Azure:
- Aplikacje mogą działać na maszynach wirtualnych z dyskami rozmieszczenie do kont magazynu.
- Witaj maszyny wirtualne mogą zostać włączone w co najmniej jednej podsieci sieci wirtualnej.

![środowisko klienta](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a>Proces replikacji

### <a name="step-1"></a>Krok 1

Po włączeniu replikacji maszyny Wirtualnej platformy Azure w portalu Azure hello hello pokazane w powitania po diagram i tabeli są tworzone automatycznie w region docelowy hello zasobów. Domyślnie zasoby są tworzone zgodnie z ustawieniami region źródła. Można dostosować ustawienia obiektu docelowego hello zgodnie z potrzebami. [Dowiedz się więcej](site-recovery-replicate-azure-to-azure.md).

![Włącz proces replikacji, krok 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

**Zasób** | **Szczegóły**
--- | ---
**Docelowa grupa zasobów** | Witaj toowhich grupy zasobów należy replikowanych maszyn wirtualnych po pracy awaryjnej.
**Docelowy sieci wirtualnej** | sieć wirtualna Hello w którym replikowanych maszyn wirtualnych znajdują się po pracy awaryjnej. Mapowanie sieci jest tworzony między sieciami wirtualnymi źródłowym i docelowym i na odwrót.
**Konta magazynu pamięci podręcznej** | Przed zmian w źródle, które maszyny wirtualne są replikowane toohello docelowe konto magazynu, są śledzone i wysłane konta magazynu pamięci podręcznej toohello w miejscu docelowym hello. Dzięki temu minimalny wpływ na produkcji aplikacje działające na powitania maszyny Wirtualnej.
**Konta magazynu docelowego**  | Konta magazynu w hello docelowej lokalizacji toowhich hello dane są replikowane.
**Docelowy zestawów dostępności**  | Zestawy dostępności w których hello replikowane maszyny wirtualne znajdują się po pracy awaryjnej.

### <a name="step-2"></a>Krok 2

Ponieważ replikacja jest włączona, hello rozszerzenia usługi Site Recovery usługi mobilności jest automatycznie instalowany na powitania maszyny Wirtualnej. występuje Hello następujące czynności:

1. Witaj maszyny Wirtualnej jest zarejestrowany z usługą Site Recovery.

2. Ciągła replikacja jest skonfigurowana dla hello maszyny Wirtualnej. Zapisuje dane na powitania maszyny Wirtualnej dyski są stale toohello konta magazynu pamięci podręcznej w lokalizacji źródłowej hello transferu.

   ![Włącz proces replikacji, krok 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  Należy pamiętać, że Site Recovery nigdy nie wymaga ruchu przychodzącego toohello łączności maszyny Wirtualnej. Wychodzące tylko adresów URL/IP usługa odzyskiwania tooSite łączności, adresy URL/IP uwierzytelnianie usługi Office 365 i adresy IP konta magazynu pamięci podręcznej jest wymagana. 

## <a name="continuous-replication-process"></a>Proces replikacji ciągłej

Po replikacji ciągłej działa, dysk, który zapisuje są natychmiast przekazywane konta magazynu pamięci podręcznej toohello. Usługa Site Recovery przetwarza dane hello i wysyła je toohello docelowe konto magazynu. Po przetworzeniu danych hello punkty odzyskiwania są generowane w hello docelowe konto magazynu, co kilka minut.

## <a name="failover-process"></a>Proces trybu failover

Po zainicjowaniu tryb failover maszyny wirtualne są tworzone w hello docelowa grupa zasobów, wirtualnych sieci docelowej, podsieci docelowej powitalne i hello docelowego zestawu dostępności. Podczas pracy awaryjnej można użyć dowolnego punktu odzyskiwania.

![Proces trybu failover](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](azure-to-azure-walkthrough-prerequisites.md)
