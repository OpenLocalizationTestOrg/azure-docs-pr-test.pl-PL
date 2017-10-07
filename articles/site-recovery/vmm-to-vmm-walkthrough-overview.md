---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V tooa lokacja dodatkowa programu VMM z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie replikowania maszyn wirtualnych funkcji Hyper-V tooa lokacja dodatkowa programu VMM przy użyciu hello portalu Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w VMM chmur tooa lokacja dodatkowa programu VMM

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmm-to-vmm.md)
> * [Portal klasyczny](site-recovery-vmm-to-vmm-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate maszynach wirtualnych funkcji Hyper-V (VM) zarządzane w chmurach programu System Center Virtual Machine Manager (VMM), lokalizacji dodatkowej VMM tooa lokalnymi przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md)w hello portalu Azure.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Krok 1: Przejrzyj hello architektura scenariusza

Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy.

Przejdź za[krok 1: Przejrzyj architektura hello](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>Krok 2: Sprawdź wymagania wstępne i ograniczenia

Upewnij się, sprawdź wymagania wstępne dotyczące wdrażania hello i ograniczenia.

**Wymagania wstępne platformy Azure**: potrzebujesz subskrypcji Microsoft Azure i usług odzyskiwania Azure magazyn, tooorchestrate i zarządzać replikacją.
**Serwery lokalne, VMM i hosty funkcji Hyper-V**: Upewnij się, że serwery VMM i hosty funkcji Hyper-V są zgodne i przygotowania się do wdrażania usługi Site Recovery.

Przejdź za[krok 2: Sprawdź wymagania wstępne i ograniczenia](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>Krok 3: Planowanie sieci

Należy toodo niektórych tooensure skonfigurowanie mapowania sieci między sieciami maszyny Wirtualnej VMM podczas wdrażania scenariusza hello do planowania sieci.

Przejdź za[krok 3: Planowanie sieci](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>Krok 4: Przygotowanie VMM i funkcji Hyper-V

Przygotowanie hello serwery VMM i hosty funkcji Hyper-V do wdrażania usługi Site Recovery.

Przejdź za[krok 4: Przygotowanie serwerów lokalnych](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>Krok 5: Konfigurowanie magazynu

Konfigurowanie magazynu usług odzyskiwania. Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.

[Krok 5: Konfigurowanie magazynu](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>Krok 6: Konfigurowanie ustawień źródłowa i docelowa

Konfigurowanie hello lokalizacja źródłowa i docelowa replikacji programu VMM. Dodaj magazyn toohello serwery VMM hello i pobierane pliki instalacyjne hello składników usługi Site Recovery. Uruchom Instalatora dostawcy usługi Azure Site Recovery na serwerze VMM hello. Instalator instaluje hello dostawcy na serwerze VMM hello i rejestruje hello serwer w magazynie hello. Należy zainstalować agenta usług odzyskiwania Microsoft hello na każdym hoście funkcji Hyper-V.

Przejdź za[krok 6: Konfigurowanie ustawień źródłowa i docelowa hello](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>Krok 7. Konfigurowanie mapowania sieci

Mapowanie sieci maszyny Wirtualnej programu VMM w hello lokalizacja źródłowa i docelowa. Po przejściu w tryb failover maszyny wirtualne są tworzone w sieci docelowej hello tego toohello mapy źródłowej sieci maszyny Wirtualnej w których hello znajduje się źródło maszyny Wirtualnej funkcji Hyper-V.

Przejdź za[kroku 7: Konfigurowanie mapowania sieci](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>Krok 8: Konfigurowanie zasad replikacji

Określ, jak będą replikowane maszyny wirtualne między lokacjami programu VMM.

Przejdź za[krok 8: Skonfiguruj zasady replikacji](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>Krok 9: Włączanie replikacji maszyn wirtualnych

Wybierz maszyny wirtualne hello ma tooreplicate. Włączanie maszyny Wirtualnej dla replikacji wyzwalaczy hello replikacji początkowej toohello dodatkowej lokacji, następuje replikacja różnicowa trwającą.

Przejdź za[krok 9: Włączanie replikacji](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>Krok 10: Uruchom test trybu failover

Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.

Przejdź za[kroku 10: testować tryb failover](vmm-to-vmm-walkthrough-test-failover.md).
