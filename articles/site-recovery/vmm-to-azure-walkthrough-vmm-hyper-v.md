---
title: aaaPrepare programu System Center VMM dla funkcji Hyper-V replikacji tooAzure | Dokumentacja firmy Microsoft
description: "Opisuje sposób serwer programu System Center VMM tooprepare tooAzure replikacji funkcji Hyper-V, za pomocą usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Krok 6: Przygotowanie serwerów programu VMM i hosty funkcji Hyper-V do tooAzure replikacji funkcji Hyper-V

Po skonfigurowaniu [Azure składniki](vmm-to-azure-walkthrough-prepare-azure.md) hello wdrożenia, użyj instrukcji hello w tym serwerów VMM lokalnych tooprepare artykułu i toointeract hosty funkcji Hyper-V z usługą Azure Site Recovery.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>Przygotowanie serwerów programu VMM

- Należy co najmniej jeden serwer VMM spełniające wymagania dotyczące obsługi hello replikacji usługi Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Upewnij się, że zostały przygotowane powitania serwera VMM dla [mapowania sieci](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Upewnij się, że na tym serwerze programu VMM hello mogą uzyskiwać dostęp do tych adresów URL

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.
- Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).
- Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).

Podczas wdrażania usługi Site Recovery Pobierz hello dostawcy usługi Site Recovery i zainstalować ją na każdym serwerze programu VMM. Serwer VMM Hello jest zarejestrowany w powitalne magazyn usług odzyskiwania.




## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[kroku 7: Tworzenie magazynu](vmm-to-azure-walkthrough-create-vault.md)

