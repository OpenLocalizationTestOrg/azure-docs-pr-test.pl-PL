---
title: "tooreplicate zasobów Azure aaaPrepare lokalnych serwerów fizycznych tooAzure przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera informacje potrzebne w miejscu na platformie Azure przed rozpoczęciem replikacji lokalnych serwerów tooAzure, przy użyciu usługi Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a>Krok 5: Przygotowanie zasobów Azure dla tooAzure replikacji serwera fizycznego


Użyj instrukcji hello, w tym artykule tooprepare Azure zasobów, dzięki czemu można replikować tooAzure serwerów lokalnych przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Przed rozpoczęciem

Upewnij się, że zostały przeczytane hello [wymagania wstępne](physical-walkthrough-prerequisites.md).

## <a name="set-up-an-azure-account"></a>Konfigurowanie konta platformy Azure

- Pobierz [konta Microsoft Azure](http://azure.microsoft.com/).
- Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
- Sprawdź, czy hello obsługiwane regiony usługi Site Recovery w obszarze **dotyczącą dostępności geograficznej** w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Dowiedz się więcej o [cenach usługi Site Recovery](site-recovery-faq.md#pricing)i uzyskać hello [szczegóły cennika](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Konfiguracja sieci platformy Azure

- Skonfiguruj sieć platformy Azure. Maszyny wirtualne platformy Azure są umieszczane w tej sieci, gdy są tworzone po pracy awaryjnej.
- Usługi Site Recovery w portalu Azure hello mogą być używane w [Resource Manager](../resource-manager-deployment-model.md), lub w trybie klasycznym.
- Witaj sieć powinna znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello.
- Dowiedz się więcej o [cennik sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network/).
- Dowiedz się więcej o [łączności maszyny Wirtualnej Azure](physical-walkthrough-network.md) po pracy awaryjnej.


## <a name="set-up-an-azure-storage-account"></a>Konfigurowanie konta usługi Azure Storage

- Usługa Site Recovery replikacji lokalnych serwerów tooAzure magazynu. Maszyny wirtualne platformy Azure są tworzone na podstawie magazynu powitania po pracy awaryjnej.
- Konfigurowanie [konto magazynu Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) dla replikowanych danych.
- Odzyskiwanie lokacji w hello portalu Azure można używać kont magazynu w Menedżerze zasobów lub w trybie klasycznym.
- Konto magazynu Hello może być standardowe lub [premium](../storage/common/storage-premium-storage.md).
- Skonfigurowanie konta premium, należy również dodatkowe konta standardowego dla danych dziennika.


## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 6: Konfigurowanie magazynu](physical-walkthrough-create-vault.md)
