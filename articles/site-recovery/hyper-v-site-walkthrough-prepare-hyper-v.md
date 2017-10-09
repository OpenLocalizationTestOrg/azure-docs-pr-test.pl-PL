---
title: "aaaPrepare funkcji Hyper-V obsługuje (bez programu System Center VMM) dla replikacji tooAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooprepare funkcji Hyper-V obsługuje dla tooAzure replikacji przy użyciu usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>Krok 6: Przygotowanie hosty funkcji Hyper-V do tooAzure replikacji

Użyj hello instrukcje w tym artykule tooprepare lokalnymi toointeract hosty funkcji Hyper-V z usługą Azure Site Recovery.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Przygotowywanie hostów

- Upewnij się, że hello funkcji Hyper-V, hosty spełniają hello [wymagania wstępne](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Upewnij się, że hosty hello dostęp hello wymagane adresów URL:

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Jeśli masz reguły zapory oparte na adresie IP, sprawdź, czy umożliwiają one tooAzure komunikacji.
- Zezwalaj na powitania [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)i hello port HTTPS (port 443).
- Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).

Podczas wdrażania usługi Site Recovery możesz dodać hostów funkcji Hyper-V, zawierających maszyny wirtualne mają tooreplicate lokacji tooa funkcji Hyper-V. Witaj dostawcy usługi Site Recovery i agenta usług odzyskiwania są instalowane na każdym hoście. Witryna Hello funkcji Hyper-V jest zarejestrowana w powitalne magazyn usług odzyskiwania.

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[kroku 7: Tworzenie magazynu](hyper-v-site-walkthrough-create-vault.md)

