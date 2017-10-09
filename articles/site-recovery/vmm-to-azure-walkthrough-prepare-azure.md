---
title: "aaaPrepare zasobów Azure tooreplicate tooAzure maszyn wirtualnych funkcji Hyper-V (w programie System Center VMM) przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, co jest potrzebne w miejscu na platformie Azure przed rozpoczęciem replikacji tooAzure maszyn wirtualnych funkcji Hyper-V (w programie VMM) przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a>Krok 5: Przygotowanie zasobów Azure dla funkcji Hyper-V tooAzure replikacji (w programie VMM)

Po zweryfikowaniu [wymagania sieciowego](vmm-to-azure-walkthrough-network.md), użyj instrukcji hello, w tym artykule tooprepare Azure zasobów, dzięki czemu można replikować maszyny wirtualne funkcji Hyper-V lokalnymi w tooAzure chmur programu System Center Virtual Machine Manager (VMM), za pomocą Witaj [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-an-azure-account"></a>Konfigurowanie konta platformy Azure

- Pobierz [konta Microsoft Azure](http://azure.microsoft.com/).
- Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
- Sprawdź, czy hello obsługiwane regiony usługi Site Recovery, w obszarze dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Dowiedz się więcej o [cenach usługi Site Recovery](site-recovery-faq.md#pricing)i uzyskać hello [szczegóły cennika](https://azure.microsoft.com/pricing/details/site-recovery/).
- Upewnij się, że konto Azure ma poprawne hello [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate maszynach wirtualnych platformy Azure. [Dowiedz się więcej](../active-directory/role-based-access-built-in-roles.md) o kontroli dostępu opartej na rolach na platformie Azure.


## <a name="set-up-an-azure-network"></a>Konfiguracja sieci platformy Azure

- Konfigurowanie [sieć platformy Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md). Maszyny wirtualne platformy Azure są umieszczane w tej sieci, gdy są tworzone po pracy awaryjnej.
- Witaj sieć powinna znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello
- Usługi Site Recovery w portalu Azure hello mogą być używane w [Resource Manager](../resource-manager-deployment-model.md), lub w trybie klasycznym.
- Zaleca się skonfigurowanie sieci przed rozpoczęciem dalszych działań. Jeśli nie, należy toodo go podczas wdrażania usługi Site Recovery.
- Dowiedz się więcej o [cennik sieci wirtualnej](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Konfigurowanie konta usługi Azure Storage

- Usługa Site Recovery replikuje magazynu tooAzure maszyny lokalnej. Maszyny wirtualne platformy Azure są tworzone na podstawie magazynu powitania po pracy awaryjnej.
- Konfigurowanie standard/premium [konto magazynu Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold dane replikowane tooAzure.
- [Magazyn w warstwie Premium](../storage/common/storage-premium-storage.md) jest zazwyczaj używana w przypadku maszyn wirtualnych, które wymagają wysoką wydajność We/Wy i intensywnych obciążeń we/wy toohost małe opóźnienia.
- Jeśli chcesz, aby toouse toostore konta premium zreplikowanych danych, należy również konta magazynu w warstwie standardowa toostore dzienników replikacji przechwytywania trwającą zmienia się tooon lokalne dane.
- W zależności od modelu zasobu hello ma toouse nie powiodła się na maszynach wirtualnych platformy Azure, należy skonfigurować konto w [tryb usługi Resource Manager](../storage/common/storage-create-storage-account.md), lub [trybu klasycznego](../storage/common/storage-create-storage-account.md).
- Zalecamy skonfigurowanie konta magazynu przed rozpoczęciem. Jeśli użytkownik nie należy toodo go podczas wdrażania usługi Site Recovery. Witaj konta muszą być w hello magazyn usług odzyskiwania i tym samym regionie co hello.
- Nie można przenieść magazynu konta używane przez usługę Site Recovery między grupami zasobów w ramach hello sam subskrypcji lub różnych subskrypcji.


## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 6: przygotowanie VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)
