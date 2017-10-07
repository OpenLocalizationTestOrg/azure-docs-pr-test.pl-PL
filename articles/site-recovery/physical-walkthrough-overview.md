---
title: "aaaReplicate fizycznych tooAzure serwerów z usługą Azure Site Recovery lokalnymi | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie kroków hello replikowania obciążenia uruchomione na lokalnym systemem Windows lub Linux serwerów fizycznych tooAzure z hello usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Replikowanie tooAzure serwery fizyczne z usługą Site Recovery

Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate lokalnego systemu Windows i Linux serwerów fizycznych tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.


## <a name="step-1-review-architecture-and-prerequisites"></a>Krok 1: Przegląd architektury i wymagania wstępne

Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy tooset hello wdrożenia.

Przejdź do zbyt[krok 1: Przejrzyj hello architektury](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Krok 2: Sprawdź wymagania wstępne dotyczące

Upewnij się, że hello wymagania wstępne zostały spełnione dla każdego składnika wdrażania:

- **Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.
- **Składniki usługi Site Recovery lokalnymi**: należy komputera z uruchomionym systemem lokalnymi składnikami usługi Site Recovery.
- **Replikowane maszyny**: serwery mają tooreplicate muszą toocomply z lokalnymi i wymagania dotyczące usługi Azure.

Przejdź do zbyt[krok 2: Przejrzyj wymagania wstępne i ograniczenia](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Krok 3: Planowanie pojemności

Jeśli pełne wdrożenie robimy należy toofigure się, jakie potrzebne zasoby replikacji. Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest, możesz pominąć ten krok.

Przejdź do zbyt[krok 3: Planowanie pojemności](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Krok 4: Planowanie sieci

Należy toodo niektórych planowania tooensure czy maszynach wirtualnych platformy Azure są połączone toonetworks po pracy awaryjnej i czy mają one hello prawo adresów IP sieci.

Przejdź do zbyt[krok 4: Planowanie sieci](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Krok 5: Przygotowanie zasobów platformy Azure

Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem. 

Przejdź do zbyt[krok 5: przygotowanie Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Krok 6: Konfigurowanie magazynu

Konfigurowanie tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją. Po skonfigurowaniu magazynu hello Określ sposób tooreplicate, i miejsce tooreplicate jej.

Przejdź do zbyt[krok 6: Konfigurowanie magazynu](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Krok 7: Konfigurowanie ustawień źródłowa i docelowa

Skonfiguruj ustawienia hello źródłowej i docelowej (Azure). Ustawienia źródła obejmuje systemem składnikami usługi Site Recovery lokalne powitania tooinstall Unified Instalatora.

Przejdź do zbyt[kroku 7: Konfigurowanie hello źródłowa i docelowa](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Krok 8: Konfigurowanie zasad replikacji

Skonfigurowaniu toospecify zasad jak fizycznych serwerów należy replikować.

Przejdź do zbyt[krok 8: Konfigurowanie zasad replikacji](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Krok 9: Instalowanie usługi mobilności hello

Witaj usługi mobilności musi być zainstalowany na każdym serwerze ma tooreplicate. Istnieje kilka sposobów tooset usługi hello, instalację wypychania i ściągania.

Przejdź zbyt[krok 9: Instalowanie usługi mobilności hello](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Krok 10: Włączanie replikacji

Po hello usługa mobilności jest uruchomiona na serwerze, można włączyć dla niego replikację. Po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.

Przejdź do zbyt[kroku 10: Włączanie replikacji](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Krok 11: Uruchom test trybu failover

Po zakończeniu replikacji początkowej i działa replikacja różnicowa, możesz uruchomić test trybu failover toomake się, że wszystko działa zgodnie z oczekiwaniami.

Przejdź do zbyt[krok 11: testować tryb failover](physical-walkthrough-test-failover.md)

