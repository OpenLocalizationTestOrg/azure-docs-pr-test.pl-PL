---
title: "aaaMigrate maszyn wirtualnych IaaS platformy Azure między regiony platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj maszyn wirtualnych Azure IaaS toomigrate usługi Azure Site Recovery z jednego tooanother region platformy Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Migracja maszyn wirtualnych Azure IaaS między regiony platformy Azure z usługą Azure Site Recovery
## <a name="overview"></a>Omówienie
Usługa Site Recovery tooAzure Zapraszamy! W tym artykule należy użyć, jeśli maszyny wirtualne Azure toomigrate między regiony platformy Azure. Przed rozpoczęciem należy pamiętać, że:

* Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: Azure Resource Manager i model klasyczny. Azure ma dwa portale — klasyczny portal Azure obsługującym hello klasycznego modelu wdrażania hello i hello portalu Azure z obsługą oba modele wdrażania. Witaj podstawowe kroki migracji są hello sama czy w przypadku konfigurowania usługi Site Recovery w Menedżerze zasobów lub w klasycznym. Jednak hello instrukcje interfejsu użytkownika i zrzuty ekranu w tym artykule dotyczą hello portalu Azure.
* **Obecnie można wykonywać migrację tylko z jednego regionu tooanother. Możesz w trybie Failover maszyny wirtualne z jednego tooanother region platformy Azure, ale nie jest możliwy ich powrót ponownie.**

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Wymagania wstępne
Oto, co jest potrzebne dla tego wdrożenia:

* **Maszyny wirtualne IaaS**: hello ma toomigrate maszyn wirtualnych. Należy przeprowadzić migrację tych maszyn wirtualnych, traktując je jako maszyn fizycznych.

## <a name="deployment-steps"></a>Kroki wdrażania
W tej sekcji opisano kroki wdrażania hello hello nowego portalu Azure.

1. [Tworzenie magazynu](site-recovery-vmware-to-azure.md).
2. [Włącz replikację](site-recovery-vmware-to-azure.md). Włącz replikację hello maszyn wirtualnych toomigrate, a następnie wybierz pozycję Azure jako źródła. 
3. [Uruchomić nieplanowany tryb failover](site-recovery-failover.md). Po zakończeniu replikacji początkowej można uruchomić nieplanowanego trybu failover z jednym tooanother region platformy Azure. Opcjonalnie możesz utworzyć plan odzyskiwania i uruchomić nieplanowanego trybu failover, toomigrate wiele maszyn wirtualnych między regionami. [Dowiedz się więcej](site-recovery-create-recovery-plans.md) o planach odzyskiwania.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o innych scenariuszy replikacji w [co to jest Azure Site Recovery?](site-recovery-overview.md)
