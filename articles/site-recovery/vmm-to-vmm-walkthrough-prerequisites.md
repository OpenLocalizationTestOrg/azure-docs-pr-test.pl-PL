---
title: "wymagania wstępne hello aaaReview dla funkcji Hyper-V replikacji tooa lokacja dodatkowa programu VMM z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje warunki wstępne hello replikowania maszyn wirtualnych funkcji Hyper-V tooa lokacja dodatkowa programu VMM z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Krok 2: Przeglądanie hello wymagania wstępne i ograniczenia dotyczące maszyny Wirtualnej funkcji Hyper-V replikacji tooa lokacja dodatkowa programu VMM


Po przejrzeniu hello [architektura scenariusza](vmm-to-vmm-walkthrough-architecture.md), przeczytaj ten artykuł toomake się zapoznać wymagania wstępne dotyczące wdrażania hello, podczas replikacji maszyn wirtualnych funkcji Hyper-V lokalnymi (VM) zarządzanych w System Center wirtualnego Machine Manager (VMM) chmur tooa dodatkowej lokacji przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Wymagania wstępne i ograniczenia

**Wymaganie** | **Szczegóły**
--- | ---
**Azure** | A [Microsoft Azure](http://azure.microsoft.com/) subskrypcji.<br/><br/> Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).<br/><br/> [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery/) o cenach usługi Site Recovery.<br/><br/> Sprawdź, czy hello obsługiwane regiony usługi Site Recovery, w obszarze dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
**Serwery programu VMM** | Firma Microsoft zaleca się, że masz dwoma serwerami VMM, w lokacji głównej hello i jeden w hello dodatkowej.<br/><br/> Replikacji między chmurami na jednym serwerze VMM jest obsługiwana.<br/><br/> Serwery VMM powinna być uruchomiona co najmniej System Center 2012 SP1 z najnowszymi aktualizacjami hello.<br/><br/> Serwery VMM wymagają dostępu do Internetu.
**Chmury VMM** | Każdy serwer VMM musi dysponować co najmniej jedną chmurę, a wszystkie chmury musi mieć zestawu profilu pojemności funkcji Hyper-V hello. <br/><br/>Chmury muszą zawierać co najmniej jedną grupę hostów programu VMM.<br/><br/> Jeśli masz tylko jeden serwer VMM, wymaga co najmniej dwa chmur, tooact jako podstawowego i pomocniczego.
**Funkcja Hyper-V** | Serwery funkcji Hyper-V musi działać co najmniej Windows Server 2012 z rolą hello funkcji Hyper-V, i mieć hello zainstalowane najnowsze aktualizacje.<br/><br/> Serwer funkcji Hyper-V powinien zawierać co najmniej jedną maszynę wirtualną.<br/><br/>  Serwery hosta funkcji Hyper-V powinien znajdować się w grupach hostów w hello głównych i dodatkowych chmurach VMM.<br/><br/> Po uruchomieniu funkcji Hyper-V w klastrze systemu Windows Server 2012 R2 zainstaluj [zaktualizować 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Po uruchomieniu w systemie Windows Server 2012 Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie w przypadku statycznej klastra oparte na adresie IP. Należy ręcznie skonfigurować hello brokera klastra. [Dowiedz się więcej](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Serwery funkcji Hyper-V wymagają dostępu do Internetu.




## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 3: Planowanie sieci](vmm-to-vmm-walkthrough-network.md).
