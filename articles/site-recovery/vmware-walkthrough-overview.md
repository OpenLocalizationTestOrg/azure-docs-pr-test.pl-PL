---
title: "aaaReplicate tooAzure maszyn wirtualnych VMware z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie kroków hello replikowania obciążeń uruchomionych na maszynach wirtualnych VMware tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>Replikowanie maszyn wirtualnych VMware tooAzure z usługą Site Recovery

Ten artykuł zawiera omówienie hello kroki wymagane tooreplicate lokalnymi VMware maszyn wirtualnych tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.


![Proces wdrażania](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Rysunek 1: Podsumowanie procesu wdrożenia**

## <a name="step-1-review-architecture-and-prerequisites"></a>Krok 1: Przegląd architektury i wymagania wstępne

Przed rozpoczęciem wdrażania, przejrzyj architektura scenariusza hello i upewnij się, że znasz wszystkie składniki hello należy toodeploy

Przejdź do zbyt[krok 1: Przejrzyj hello architektury](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Krok 2: Sprawdź wymagania wstępne dotyczące

Upewnij się, że hello wymagania wstępne zostały spełnione dla każdego składnika wdrażania:

- **Wymagania wstępne platformy Azure**: wymagane konto Microsoft Azure, sieci platformy Azure i kont magazynu.
- **Składniki usługi Site Recovery lokalnymi**: należy komputera z uruchomionym systemem lokalnymi składnikami usługi Site Recovery.
- **Lokalne wstępnych VMware**: należy tooset kont, dzięki czemu usługa Site Recovery mogą uzyskiwać dostęp do serwerów VMware i maszyn wirtualnych.
- **Maszyny wirtualne replikowane**: maszyny wirtualne mają toocomply potrzeby tooreplicate z wymaganiami platformy Azure i mieć zainstalowanie składnika usługi Mobility hello.

Przejdź do zbyt[krok 2: Przejrzyj wymagania wstępne i ograniczenia](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Krok 3: Planowanie pojemności

Jeśli pełne wdrożenie robimy należy toofigure się, jakie potrzebne zasoby replikacji. Istnieje kilka z toohelp dostępne narzędzia można to zrobić. Przejdź tooStep 2. Jeśli podczas wykonywania szybkiego skonfigurowania środowiska hello tootest można pominąć ten krok.

Przejdź do zbyt[krok 3: Planowanie pojemności](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Krok 4: Planowanie sieci

Należy toodo niektórych planowania tooensure czy maszynach wirtualnych platformy Azure są połączone toonetworks po pracy awaryjnej i czy mają one hello prawo adresów IP sieci.

Przejdź do zbyt[krok 4: Planowanie sieci](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Krok 5: Przygotowanie zasobów platformy Azure

Konfigurowanie sieci platformy Azure i magazynu przed jego uruchomieniem. Można to zrobić podczas wdrażania, ale zaleca się, że można to zrobić przed rozpoczęciem.

Przejdź do zbyt[krok 5: przygotowanie Azure](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>Krok 6: Przygotowanie VMware

Należy tooset kont używanych Site Recovery do:

- Tooautomatically serwerów wirtualizacji VMware dostępu wykryć maszyn wirtualnych.
- Dostęp do usługi mobilności hello tooinstall maszyn wirtualnych. Każda maszyna wirtualna ma tooreplicate musi mieć agent usługi mobilności hello przed można włączyć dla niego replikację.

Przejdź do zbyt[krok 6: przygotowanie VMware](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>Krok 7: Konfigurowanie magazynu

Należy tooset się tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją. Po skonfigurowaniu magazynu hello Określ sposób tooreplicate, i miejsce tooreplicate jej.

Przejdź do zbyt[kroku 7: Konfigurowanie magazynu](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Krok 8: Konfigurowanie ustawień źródłowa i docelowa

Konfigurowanie hello źródłowy i docelowy, który jest używany do replikacji. Konfigurowanie ustawień źródła obejmuje systemem składnikami usługi Site Recovery lokalne powitania tooinstall Unified Instalatora.

Przejdź do zbyt[krok 8: Konfigurowanie hello źródłowa i docelowa](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Krok 9: Konfigurowanie zasad replikacji

Skonfigurowane ustawienia zasad toospecify replikacji w maszynach wirtualnych VMware w magazynie hello.

Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>Krok 10: Zainstaluj usługę mobilności hello

musi być zainstalowany Hello usługi mobilności na każdej maszynie Wirtualnej ma tooreplicate. Istnieje kilka sposobów tooset usługi hello instalację wypychania i ściągania.

Przejdź do zbyt[kroku 10: zainstalować usługi mobilności hello](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>Krok 11: Włączanie replikacji

Po uruchomieniu hello usługi mobilności na maszynie Wirtualnej można włączyć dla niego replikację. Po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.

Przejdź do zbyt[krok 11: Włączanie replikacji](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>Krok 12: Uruchom test trybu failover

Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test pracy awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.

Przejdź do zbyt[krok 12: testować tryb failover](vmware-walkthrough-test-failover.md)
