---
title: "aaaHow czy replikacja maszyny wirtualnej platformy Azure między pracy regiony platformy Azure w usłudze Azure Site Recovery?  | Microsoft Docs"
description: "Ten artykuł zawiera omówienie składników i architektury używane podczas replikowania maszyn wirtualnych platformy Azure między regiony platformy Azure przy użyciu usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>Jak działa replikacja maszyny Wirtualnej platformy Azure w usłudze Site Recovery?


W tym artykule opisano składniki hello i procesy wykonywane w replikacji i odzyskiwania maszyn wirtualnych platformy Azure (maszyn wirtualnych) z jednego regionu tooanother przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

>[!NOTE]
>Azure replikacji maszyny Wirtualnej za pomocą hello usługi Site Recovery jest obecnie w przeglądzie.

Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architectural-components"></a>Składniki architektury

powitania po diagram przedstawia ogólny widok środowiska maszyny Wirtualnej platformy Azure w określonym regionie (w tym przykładzie hello wschodnie stany USA lokalizacji). W środowisku maszyny Wirtualnej platformy Azure:
- Aplikacje mogą działać na maszynach wirtualnych z dyskami rozmieszczenie do kont magazynu.
- Witaj maszyny wirtualne mogą zostać włączone w co najmniej jednej podsieci sieci wirtualnej.

![środowisko klienta](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Dowiedz się więcej o wymaganiach wstępnych wdrożenia hello oraz wymagań dotyczących hello [macierz obsługi](site-recovery-support-matrix-azure-to-azure.md).

## <a name="replication-process"></a>Proces replikacji

### <a name="step-1"></a>Krok 1

Po włączeniu replikacji maszyny Wirtualnej platformy Azure w portalu Azure hello hello pokazane w powitania po diagram i tabeli są tworzone automatycznie w region docelowy hello zasobów. Domyślnie zasoby są tworzone zgodnie z ustawieniami region źródła. Można dostosować ustawienia obiektu docelowego hello zgodnie z potrzebami. [Dowiedz się więcej](site-recovery-replicate-azure-to-azure.md).

![Włącz proces replikacji, krok 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

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

   ![Włącz proces replikacji, krok 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > Usługa Site Recovery nigdy nie musi toohello przychodzących połączeń maszyny Wirtualnej. Witaj maszyny Wirtualnej musi tylko adresy IP/adresy URL usługi odzyskiwania tooSite łączność wychodząca, adresy IP/adresy URL uwierzytelniania usługi Office 365 i adresy IP konta magazynu pamięci podręcznej. Aby uzyskać więcej informacji, zobacz hello [sieci wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure-networking-guidance.md) artykułu.

## <a name="continuous-replication-process"></a>Proces replikacji ciągłej

Po replikacji ciągłej działa, dysk, który zapisuje są natychmiast przekazywane konta magazynu pamięci podręcznej toohello. Usługa Site Recovery przetwarza dane hello i wysyła je toohello docelowe konto magazynu. Po przetworzeniu danych hello punkty odzyskiwania są generowane w hello docelowe konto magazynu, co kilka minut.

## <a name="failover-process"></a>Proces trybu failover

Po zainicjowaniu tryb failover maszyny wirtualne są tworzone w hello docelowa grupa zasobów, wirtualnych sieci docelowej, podsieci docelowej powitalne i hello docelowego zestawu dostępności. Podczas pracy awaryjnej można użyć dowolnego punktu odzyskiwania.

![Proces trybu failover](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [sieci](site-recovery-azure-to-azure-networking-guidance.md) replikacji maszyny Wirtualnej platformy Azure.
- Wykonaj przewodnik zbyt[replikowanie maszyn wirtualnych Azure.](site-recovery-azure-to-azure.md)
