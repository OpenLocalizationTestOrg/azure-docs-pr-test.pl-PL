---
title: "aaaReplicate maszynach wirtualnych platformy Azure między regiony platformy Azure | Dokumentacja firmy Microsoft"
description: "Podsumowanie hello kroki wymagane tooreplicate maszynach wirtualnych platformy Azure między regiony platformy Azure z usługą Azure Site Recovery hello w hello portalu Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Replikowanie maszyn wirtualnych Azure między regionami z usługą Azure Site Recovery

>Ten artykuł zawiera omówienie tooreplicate wymagane kroki hello Azure maszynach wirtualnych (VM) w jednym regionie Azure tooAzure maszyn wirtualnych w innym regionie. 

>[!NOTE]
>
> Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.

Opublikuj komentarze i pytania u dołu hello tym artykułem lub na powitania [forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="step-1-review-architecture"></a>Krok 1: Przegląd architektury

Przed rozpoczęciem wdrażania zapoznaj się hello scenariusz architektury i składników hello należy toodeploy.

Przejdź do zbyt[krok 1: Przejrzyj hello architektury](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Krok 2: Sprawdź wymagania wstępne dotyczące

Sprawdź, czy ma hello Azure wymagania wstępne w miejscach, w tym subskrypcji, sieci wirtualne, konta magazynu i wymagania dotyczące maszyny Wirtualnej.

Przejdź do zbyt[krok 2: Sprawdź wymagania wstępne i ograniczenia](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>Krok 3: Planowanie sieci

Sprawdź, czy łączność wychodząca jest skonfigurowany na maszynach wirtualnych Azure ma tooreplicate i że zostały skonfigurowane połączenia z lokalnym.

Przejdź do zbyt[krok 4: Planowanie sieci](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>Krok 4: Tworzenie magazynu 

Należy tooset się tooorchestrate magazyn usług odzyskiwania i Zarządzanie replikacją i określ region źródła hello.

Przejdź do zbyt[krok 4: Tworzenie magazynu](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>Krok 5: Włączanie replikacji


Replikacja tooenable, skonfigurować ustawienia lokalizacji docelowej, skonfigurować zasady replikacji i wybierz hello maszynach wirtualnych platformy Azure, które mają tooreplicate. Po włączeniu replikacji początkowej dla maszyny Wirtualnej hello występuje.

Przejdź do zbyt[krok 5: Włączanie replikacji](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>Krok 6: Uruchamianie testowego trybu failover

Po zakończeniu replikacji początkowej, a replikacja różnicowa jest uruchomiony, możesz uruchomić test pracy awaryjnej toomake się, że wszystko działa zgodnie z oczekiwaniami.

Przejdź do zbyt[krok 6: testować tryb failover](azure-to-azure-walkthrough-test-failover.md)


