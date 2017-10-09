---
title: "aaaReplicate maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie replikowania maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM przy użyciu usługi Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM przy użyciu usługi Site Recovery w portalu Azure hello
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmm-to-azure.md)
> * [Klasyczny portal Azure](site-recovery-vmm-to-azure-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell — model klasyczny](site-recovery-deploy-with-powershell.md)


Ten artykuł zawiera omówienie tooreplicate wymagane kroki hello lokalnych maszyn wirtualnych funkcji Hyper-V (VM) zarządzanych w tooAzure chmur programu System Center Virtual Machine Manager (VMM), za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w Witaj portalu Azure.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Krok 1: Przejrzyj hello architektura scenariusza

Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy.

Przejdź do zbyt[krok 1: Przejrzyj hello architektury](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>Krok 2: Sprawdź wymagania wstępne i ograniczenia

Upewnij się, sprawdź wymagania wstępne dotyczące wdrażania hello i ograniczenia.

**Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.
**Serwery lokalne, VMM i hosty funkcji Hyper-V**: Upewnij się, że serwery VMM i hosty funkcji Hyper-V są zgodne i przygotowania się do wdrażania usługi Site Recovery.
**Maszyny wirtualne replikowane**: Sprawdź, czy maszyny wirtualne mają tooreplicate spełniają wymagania dotyczące usługi Azure.

Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Krok 3: Planowanie pojemności

Pełne wdrożenie robimy, należy najpierw toofigure się, jakie potrzebne zasoby replikacji. Istnieje kilka z toohelp dostępne narzędzia można to zrobić. Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest, możesz pominąć ten krok.

Przejdź do zbyt[krok 3: Planowanie pojemności](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Krok 4: Planowanie sieci

Należy toodo niektórych tooensure, które można skonfigurować mapowanie sieci, podczas wdrażania scenariusza hello do planowania sieci maszyn wirtualnych platformy Azure będzie tooAzure połączonych sieci wirtualnych po pracy awaryjnej, oraz że je przypisano odpowiednie IP adresów.

Przejdź do zbyt[krok 4: Planowanie sieci](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>Krok 5: Przygotowanie zasobów platformy Azure

Konfigurowanie konta platformy Azure, sieci i magazynu. Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.

Przejdź do zbyt[krok 5: przygotowanie Azure](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>Krok 6: Przygotowanie VMM i funkcji Hyper-V

Przygotuj serwery lokalne powitania, VMM i hosty funkcji Hyper-V do wdrażania usługi Site Recovery.

Przejdź do zbyt[krok 6: Przygotowanie serwerów lokalnych](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Krok 7: Konfigurowanie magazynu

Konfigurowanie magazynu usług odzyskiwania. Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.

[Krok 7: Konfigurowanie magazynu](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Krok 8: Konfigurowanie ustawień źródłowa i docelowa

Konfigurowanie hello źródłowe i docelowe lokalizacje replikacji. Dodaj magazyn toohello serwera VMM hello i pobierane pliki instalacyjne hello składników usługi Site Recovery. Uruchom Instalatora dostawcy usługi Azure Site Recovery na serwerze VMM hello. Instalator instaluje hello dostawcy na serwerze VMM hello i rejestruje hello serwer w magazynie hello. Należy zainstalować agenta usług odzyskiwania Microsoft hello na każdym hoście funkcji Hyper-V.

Przejdź zbyt[krok 8: Konfigurowanie ustawień źródłowa i docelowa](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>Krok 9: Konfigurowanie mapowania sieci

Mapa lokalnych sieci wirtualnych tooAzure sieci maszyny Wirtualnej programu VMM. Po przejściu w tryb failover maszynach wirtualnych platformy Azure są tworzone w hello sieć platformy Azure, która mapuje maszyny Wirtualnej sieci lokalnej toohello, w których hello znajduje się źródło funkcji Hyper-V.

Przejdź do zbyt[krok 9: Konfigurowanie mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>Krok 10: Konfigurowanie zasad replikacji

Określ sposób lokalnych maszyn wirtualnych będą replikowane tooAzure.

Przejdź zbyt[10 kroku: Konfigurowanie zasad replikacji](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>Krok 11: Włączanie replikacji maszyn wirtualnych

Wybierz maszyny wirtualne hello ma tooreplicate. Włączanie replikacji wyzwalaczy hello replikacji początkowej tooAzure maszynę Wirtualną, po replikacji różnicowej trwającą.

Przejdź do zbyt[krok 11: Włączanie replikacji](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>Krok 12: Uruchom test trybu failover

Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.

Przejdź do zbyt[krok 12: testować tryb failover](vmm-to-azure-walkthrough-test-failover.md)


