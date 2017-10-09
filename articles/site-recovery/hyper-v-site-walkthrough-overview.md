---
title: "aaaReplicate tooAzure maszyn wirtualnych funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooorchestrate replikacji, trybu failover i odzyskiwania lokalnych funkcji Hyper-V VMs tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>Replikację funkcji Hyper-V tooAzure maszyn wirtualnych (bez VMM) 

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-hyper-v-site-to-azure.md)
> * [Klasyczny portal Azure](site-recovery-hyper-v-site-to-azure-classic.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate lokalnym funkcji Hyper-V maszyny wirtualne tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure. W tym maszyn wirtualnych funkcji Hyper-V wdrożenia nie są zarządzane przez System Center Virtual Machine Manager (VMM).


Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>Krok 1: Przegląd architektury i wymagania wstępne

Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy

Przejdź do zbyt[krok 1: Przejrzyj hello architektury](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Krok 2: Sprawdź wymagania wstępne dotyczące

Upewnij się, że hello wymagania wstępne zostały spełnione dla każdego składnika wdrażania:

- **Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.
- **Wymagania wstępne funkcji Hyper-V lokalnymi**: Upewnij się, że hosty funkcji Hyper-V są przygotowane do wdrażania usługi Site Recovery.
- **Maszyny wirtualne replikowane**: maszyny wirtualne mają tooreplicate muszą toocomply z wymaganiami platformy Azure.

Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Krok 3: Planowanie pojemności

Jeśli pełne wdrożenie robimy należy toofigure się, jakie potrzebne zasoby replikacji. Istnieje kilka z toohelp dostępne narzędzia można to zrobić. Przejdź tooStep 2. Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest można pominąć ten krok.

Przejdź do zbyt[krok 3: Planowanie pojemności](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Krok 4: Planowanie sieci

Należy toodo niektórych planowania tooensure czy maszynach wirtualnych platformy Azure są połączone toonetworks po pracy awaryjnej i czy mają one hello prawo adresów IP sieci.

Przejdź do zbyt[krok 4: Planowanie sieci](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Krok 5: Przygotowanie zasobów platformy Azure

Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem. Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.

Przejdź do zbyt[krok 5: przygotowanie Azure](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>Krok 6: Przygotowanie funkcji Hyper-V

Upewnij się, że serwery funkcji Hyper-V spełniają wymagania dotyczące wdrażania usługi Site Recovery.

Przejdź do zbyt[krok 6: Przygotowanie funkcji Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Krok 7: Konfigurowanie magazynu

Należy tooset się tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją. Po skonfigurowaniu magazynu hello Określ sposób tooreplicate, i miejsce tooreplicate jej.

Przejdź do zbyt[kroku 7: Tworzenie magazynu](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Krok 8: Konfigurowanie ustawień źródłowa i docelowa

Konfigurowanie hello źródłowy i docelowy, który jest używany do replikacji. Konfigurowanie ustawień źródła obejmuje dodanie funkcji Hyper-V hosts tooa funkcji Hyper-V lokacji, instalowanie hello dostawcy usługi Site Recovery i agent usług odzyskiwania na każdym hoście funkcji Hyper-V i rejestrowanie lokacji hello w powitalne magazyn usług odzyskiwania.

Przejdź do zbyt[krok 8: Konfigurowanie hello źródłowa i docelowa](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Krok 9: Konfigurowanie zasad replikacji

Skonfigurowane ustawienia replikacji toospecify zasad dla maszyn wirtualnych funkcji Hyper-V w magazynie hello.

Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>Krok 10: Włączanie replikacji

Po utworzeniu zasad replikacji w miejscu, po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.

Przejdź do zbyt[kroku 10: Włączanie replikacji](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Krok 11: Uruchom test trybu failover

Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test pracy awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.

Przejdź do zbyt[krok 11: testować tryb failover](hyper-v-site-walkthrough-test-failover.md)
