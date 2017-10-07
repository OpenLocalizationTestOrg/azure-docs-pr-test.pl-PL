---
title: "aaaPrerequisites dla tooAzure replikacji przy użyciu usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera podsumowanie wymagań wstępnych dotyczących replikowanie maszyn wirtualnych i maszyn fizycznych tooAzure za pomocą usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Wymagania wstępne dotyczące replikacji region tooanother maszyn wirtualnych platformy Azure przy użyciu usługi Azure Site Recovery

> [!div class="op_single_selector"]
> * [Replikacja między Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Replikacja między lokalnymi tooAzure](site-recovery-prereq.md)

Witaj usługi Azure Site Recovery przyczynia się tooyour ciągłość oraz strategia odzyskiwania (BCDR) poprzez organizowanie:
* Replikacja maszyn wirtualnych platformy Azure tooanother region platformy Azure.
* Replikacja lokalnymi fizycznych serwerów i maszyn wirtualnych tooAzure lub tooa dodatkowego centrum danych. 

W przypadku wystąpienia awarii w lokalizacji głównej, można przełączyć tooa dodatkowej lokalizacji tookeep aplikacji i obciążeń dostępne. Zwrócona operacji toonormal może zakończyć się niepowodzeniem wstecz tooyour lokalizacji głównej. Aby uzyskać więcej informacji na temat odzyskiwania lokacji, zobacz [co to jest usługa Site Recovery?](site-recovery-overview.md).

Ten artykuł zawiera podsumowanie hello wymagania wstępne wymagane toobegin replikacji usługi Site Recovery z lokalnymi tooAzure.

Opublikuj wszelkie komentarze u dołu hello hello artykułu lub zadawaj pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Wymagania systemu Azure

**Wymaganie** | **Szczegóły**
--- | ---
**Konto platformy Azure** | A [Microsoft Azure](http://azure.microsoft.com/) konta.<br/><br/> Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
**Usługa Site Recovery** | Aby uzyskać więcej informacji o cenach usługi Site Recovery, zobacz [cenach usługi Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). Zaleca się tworzenie magazynu usług odzyskiwania w celu hello region platformy Azure, które mają toouse jako lokalizację odzyskiwania po awarii. Na przykład jeśli źródłowe maszyny wirtualne są uruchomione w wschodnie stany USA, a chcesz tooreplicate tooCentral, zaleca się tworzenie magazynu hello w środkowe stany USA.|
**Pojemność Azure** | Dla celu hello region platformy Azure, które ma być toouse jako lokalizacja odzyskiwania po awarii należy toohave subskrypcji z wystarczającą pojemność dla maszyn wirtualnych, kont magazynu i składników sieciowych. Możesz skontaktować się tooadd obsługę większej pojemności.
**Wskazówki dotyczące magazynu** | Upewnij się, że stosujesz hello [wskazówki magazynu](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) źródła wirtualnej Azure maszynami tooavoid wszelkie problemy z wydajnością. Jeśli wykonujesz hello domyślne ustawienia Site Recovery tworzy na podstawie konfiguracji źródła hello kont magazynu hello wymagane. Jeśli należy dostosować i wybrać własne ustawienia, upewnij się, należy wykonać hello [wartości docelowe skalowalności dysków maszyny wirtualnej](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Wskazówki dotyczące sieci** | Należy łączność wychodząca hello toowhitelist z maszyny Wirtualnej platformy Azure dla określonych adresów URL lub adres IP zakresu. Aby uzyskać więcej informacji, zobacz toohello [wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure networking](site-recovery-azure-to-azure-networking-guidance.md) artykułu.
**Maszyna wirtualna platformy Azure** | Upewnij się, że wszystkie certyfikaty główne najnowsze hello występują na hello Windows lub maszyny Wirtualnej systemu Linux. Jeśli nie podano hello najnowsze certyfikaty główne, hello maszyny Wirtualnej nie może być zarejestrowany tooSite odzyskiwania ze względu na ograniczenia toosecurity.

>[!NOTE]
>Aby uzyskać więcej informacji na temat obsługi dla określonej konfiguracji odczytu hello [macierz obsługi](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure networking](site-recovery-azure-to-azure-networking-guidance.md).
- Włączyć ochronę obciążeń przez [replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure.md).
