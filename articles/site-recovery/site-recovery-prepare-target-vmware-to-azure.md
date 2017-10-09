---
title: Przygotowanie docelowego (VMware tooAzure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób tooprepare Twojego toostart środowiska platformy Azure replikowanie tooAzure maszyny wirtualne VMware."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a>Przygotowanie docelowego (VMware tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [TooAzure fizycznych](./site-recovery-prepare-target-physical-to-azure.md)

W tym artykule opisano sposób tooprepare Twojego toostart środowiska platformy Azure replikowanie tooAzure maszyny wirtualne VMware.

## <a name="prerequisites"></a>Wymagania wstępne

Artykuł Hello założono hello poniżej:
- Utworzono tooprotect magazynu usług odzyskiwania maszyn wirtualnych VMware. Można utworzyć magazyn usług odzyskiwania na podstawie hello [portalu Azure](http://portal.azure.com "portalu Azure").
- Masz [konfiguracji środowiska lokalnego](./site-recovery-set-up-vmware-to-azure.md) tooAzure maszyny wirtualne VMware tooreplicate.

## <a name="prepare-target"></a>Przygotowanie docelowego

Po zakończeniu hello **cel ochrony krok 1** i **krok 2: przygotowanie źródła**, nastąpi za**krok 3: docelowy**

![Przygotowanie docelowego](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. **Subskrypcja:** z hello menu rozwijane, wybierz hello subskrypcji, które mają tooreplicate do maszyn wirtualnych.
2. **Model wdrażania:** hello wybierz model wdrażania (Classic lub Resource Manager)

Oparte na powitania wybrany model wdrażania, sprawdzanie poprawności jest uruchamiane tooensure, który ma co najmniej jedno konto magazynu zgodny i siecią wirtualną tooreplicate subskrypcji docelowej hello i trybu failover maszyny wirtualnej do.

Po hello operacji sprawdzania poprawności zakończy się pomyślnie, kliknij przycisk OK toogo toohello następnego kroku.

Jeśli nie masz zgodne konto magazynu Resource Manager lub sieci wirtualnej lub chcesz tooadd więcej, możesz to zrobić, klikając hello **+ konto magazynu** lub **+ sieć** przyciski na początku hello hello blok.

## <a name="next-steps"></a>Następne kroki
[Konfigurowanie ustawień replikacji](./site-recovery-setup-replication-settings-vmware.md).
