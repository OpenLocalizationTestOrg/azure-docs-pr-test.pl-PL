---
title: "tooAzure aaaMigrate z usługą Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie migracji maszyn wirtualnych i serwerów fizycznych tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Migrowanie tooAzure z usługą Site Recovery

Przeczytaj ten artykuł Omówienie używania usługi Azure Site Recovery hello do migracji maszyn wirtualnych i serwerów fizycznych.

Usługa Site Recovery jest usługą platformy Azure, która wspiera strategię BCDR tooyour, poprzez organizowanie replikacji lokalnych serwerów fizycznych i maszyn wirtualnych toohello chmury (Azure) lub tooa dodatkowego centrum danych. Po awarii w lokacji głównej, należy przełączyć toohello dodatkowej lokalizacji tookeep aplikacji i obciążeń dostępne. Lokalizacją główną tooyour Wstecz nie zostanie zwrócona toonormal operacji. Dowiedz się więcej w temacie [Co to jest usługa Site Recovery?](site-recovery-overview.md) Umożliwia także toomigrate usługi Site Recovery z istniejącymi lokalnymi tooexpedite tooAzure obciążeń do chmury podróży i rezultatów hello tablicy funkcje, które platforma Azure oferuje.

Aby szybko zapoznać się jak tooperform migracji, można znaleźć toothis wideo.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

W tym artykule opisano wdrażanie w hello [portalu Azure](https://portal.azure.com). Witaj [klasycznego portalu Azure](https://manage.windowsazure.com/) może być toomaintain używane istniejące magazynów usługi Site Recovery, ale nie można utworzyć nowego magazynu.

Po wszelkie komentarze u dołu hello w tym artykule. Zadawaj pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>Co mamy na myśli przez migrację?

Usługa Site Recovery można wdrożyć replikacji lokalnych maszyn wirtualnych i serwerów fizycznych, tooAzure lub tooa lokacji dodatkowej. Replikowanie maszyn, przełączyć je z lokacji głównej powitania po awarii wystąpić i niepowodzenie ich lokacji głównej toohello Wstecz, gdy odzyskuje. W toothis dodanie można użyć maszyny wirtualne toomigrate usługi Site Recovery i tooAzure serwerów fizycznych, dzięki czemu użytkownicy mogą uzyskiwać do nich dostęp jako maszynach wirtualnych platformy Azure. Migracja wymaga replikacji i trybu failover z hello tooAzure lokacji głównej i gestu przeprowadzenia migracji.

## <a name="what-can-site-recovery-migrate"></a>Co może migrować usługa Site Recovery?

Możesz:

- Przeprowadź migrację obciążeń uruchomionych na lokalnej toorun maszyn wirtualnych funkcji Hyper-V, maszyn wirtualnych VMware i serwerów fizycznych na maszynach wirtualnych Azure. W ramach tego scenariusza możesz również wykonać pełną replikację i powrót po awarii.
- Przeprowadzić migrację [maszyn wirtualnych IaaS platformy Azure](site-recovery-migrate-azure-to-azure.md) między regionami platformy Azure. W tym scenariuszu aktualnie jest obsługiwana tylko migracja, co oznacza, że powrót po awarii nie jest obsługiwany.
- Migrowanie [wystąpień systemu Windows usług AWS](site-recovery-migrate-aws-to-azure.md) tooAzure maszyn wirtualnych IaaS. W tym scenariuszu aktualnie jest obsługiwana tylko migracja, co oznacza, że powrót po awarii nie jest obsługiwany.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Migracja lokalnych maszyn wirtualnych i serwerów fizycznych

toomigrate lokalnych maszyn wirtualnych funkcji Hyper-V, maszyn wirtualnych VMware i serwery fizyczne, wykonaj prawie hello kroki takie same jak te używane w przypadku zwykłej replikacji.

1. Konfigurowanie magazynu usługi Recovery Services
2. Konfigurowanie serwerów zarządzania hello wymagane (VMware, program VMM, funkcji Hyper-V — w zależności od tego, co ma toomigrate), dodaj je w magazynie toohello i określ ustawienia replikacji.
3. Włącz replikację dla hello maszyny, które mają toomigrate
4. Po zakończeniu migracji początkowej hello Uruchom szybkie testu tooensure trybu failover, czy wszystko działa jak powinno.
5. Po zweryfikowaniu, że środowisko replikacji działa, należy użyć planowanego lub nieplanowanego przejścia do trybu failover w zależności od tego, [co obsługuje](site-recovery-failover.md) scenariusz. Zaleca się przeprowadzenie planowanego przejścia do trybu failover, jeśli jest to możliwe.
6. W przypadku migracji nie potrzebujesz toocommit trybu failover lub usuń go. Zamiast tego należy wybrać hello **przeprowadzenia migracji** opcji dla każdego komputera ma toomigrate.
     - W **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny Wirtualnej i kliknij przycisk **przeprowadzenia migracji**. Kliknij przycisk **OK** toocomplete. Możesz śledzić postępy hello właściwości maszyny Wirtualnej, w monitorując hello zadanie przeprowadzenia migracji w **zadania usługi Site Recovery**.
     - Witaj **przeprowadzenia migracji** akcji kończy proces migracji hello, spowoduje usunięcie replikacji dla maszyny hello i zatrzymuje rozliczeń usługi Site Recovery dla maszyny hello.

![pełna_migracja](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Migracja między regionami platformy Azure

Maszyny wirtualne platformy Azure można migrować między regionami przy użyciu usługi Site Recovery. W tym scenariuszu jest obsługiwana tylko migracja. Innymi słowy można replikować maszyny wirtualne Azure hello i awaryjnie tooanother region, ale nie można przerwać ponownie. W tym scenariuszu należy skonfigurować magazyn usług odzyskiwania wdrażanie lokalnej konfiguracji serwera toomanage replikacji, dodać magazyn toohello i określ ustawienia replikacji. Można włączyć replikacji dla maszyny hello toomigrate, a następnie uruchom szybkiego testowanie trybu failover. A następnie uruchom nieplanowanego trybu failover z hello **przeprowadzenia migracji** opcji.

## <a name="migrate-aws-tooazure"></a>Migrowanie usług AWS tooAzure

Można przeprowadzić migrację usług AWS tooAzure wystąpień maszyn wirtualnych. W tym scenariuszu jest obsługiwana tylko migracja. Innymi słowy można replikować hello wystąpień usług AWS i awaryjnie tooAzure, ale nie można przerwać ponownie. Wystąpień usług AWS są obsługiwane w hello sam sposób jak serwerów fizycznych, dla celów migracji. Konfigurowanie magazynu usług odzyskiwania, wdrażanie replikacji toomanage lokalnej konfiguracji serwera, dodaj ją toohello magazynu i określ ustawienia replikacji. Można włączyć replikacji dla maszyny hello toomigrate, a następnie uruchom szybkiego testowanie trybu failover. A następnie uruchom nieplanowanego trybu failover z hello **przeprowadzenia migracji** opcji.




## <a name="next-steps"></a>Następne kroki

- [Migrowanie maszyn wirtualnych VMware tooAzure](site-recovery-vmware-to-azure.md)
- [Migrowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmury VMM](site-recovery-vmm-to-azure.md)
- [Migrowanie maszyn wirtualnych funkcji Hyper-V bez VMM tooAzure](site-recovery-hyper-v-site-to-azure.md)
- [Migrowanie maszyn wirtualnych platformy Azure między regionami platformy Azure](site-recovery-migrate-azure-to-azure.md)
- [Migrowanie usług AWS tooAzure wystąpień](site-recovery-migrate-aws-to-azure.md)
- [Przygotowanie replikacji tooenable zmigrowane maszyny](site-recovery-azure-to-azure-after-migration.md) tooanother region na potrzeby odzyskiwania po awarii.
- Zacznij chronić obciążenia, [replikując maszyny wirtualne platformy Azure.](site-recovery-azure-to-azure.md)
