---
title: "wymagania wstępne hello aaaReview dla funkcji Hyper-V tooAzure replikacji (bez programu System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje warunki wstępne hello do replikacji, trybu failover i odzyskiwania lokalnych maszyn wirtualnych funkcji Hyper-V tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Krok 2: Przejrzyj wymagania wstępne hello replikacji tooAzure funkcji Hyper-V (bez VMM)

wymagania wstępne Hello są podsumowane w tabeli hello.


**Wymagania wstępne** | **Szczegóły** 
--- | --- 
**Azure** | Dowiedz się więcej na temat [wymagań platformy Azure](site-recovery-prereq.md#azure-requirements).
**Serwery lokalne** | [Dowiedz się więcej](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) o wymaganiach dla hostów funkcji Hyper-V lokalne powitania.
**Lokalne maszyny wirtualne funkcji Hyper-V** | Maszyny wirtualne mają powinna być uruchomiona tooreplicate [obsługiwanym systemie operacyjnym](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)i być zgodne z [wymagania wstępne platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Adresy URL platformy Azure** | Hosty funkcji Hyper-V muszą uzyskać dostęp do toothese adresów URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.<br/></br> Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).<br/></br> Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).



## <a name="next-steps"></a>Następne kroki

- Jeśli pełne wdrożenie robimy, przejdź zbyt[krok 3: Planowanie pojemności](hyper-v-site-walkthrough-capacity.md)
- Jeśli podczas wykonywania testu proste wdrożenie, należy przejść za[krok 4: Planowanie sieci](hyper-v-site-walkthrough-network.md).
