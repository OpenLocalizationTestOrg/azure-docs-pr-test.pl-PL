---
title: Przygotowanie docelowego (fizycznych do platformy Azure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób przygotowania środowiska Azure, aby uruchomić replikowania serwerów fizycznych z systemem Windows lub Linux na platformie Azure."
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
ms.date: 11/23/2017
ms.author: bsiva
ms.openlocfilehash: 2c5377f7193f8357a7e99ed1ef1a61b066b8ce5f
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="prepare-target-vmware-to-azure"></a>Przygotowanie docelowego (VMware do platformy Azure)
> [!div class="op_single_selector"]
> * [Z programu VMware do platformy Azure](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Fizycznych do platformy Azure](./site-recovery-prepare-target-physical-to-azure.md)

W tym artykule opisano sposób przygotowania środowiska Azure do rozpoczęcia replikacji serwery fizyczne (x 64) z systemu Windows lub Linux na platformie Azure.

## <a name="prerequisites"></a>Wymagania wstępne

Założono artykułu:
- Utworzono magazyn usług odzyskiwania, aby chronić serwery fizyczne. Można utworzyć magazyn usług odzyskiwania z [portalu Azure](http://portal.azure.com "portalu Azure").
- Masz [konfiguracji środowiska lokalnego](./site-recovery-set-up-physical-to-azure.md) do replikowania serwerów fizycznych do platformy Azure.

## <a name="prepare-target"></a>Przygotowanie docelowego

Po zakończeniu **cel ochrony krok 1** i **krok 2: przygotowanie źródła**, zostają przeniesieni do **krok 3: docelowy**

![Przygotowanie docelowego](./media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.png)

1. **Subskrypcja:** z menu rozwijanego Wybierz subskrypcję, która ma zostać zreplikowana na serwerach fizycznych.
2. **Model wdrażania:** wybierz model wdrażania (Classic lub Resource Manager)

Oparte na modelu wdrażania wybranego, uruchomieniu aby upewnić się, że użytkownik ma co najmniej jedno konto magazynu zgodny i sieć wirtualną w docelowej subskrypcji replikacji i trybu failover serwerów fizycznych do weryfikacji.

Po operacji sprawdzania poprawności zakończy się pomyślnie, kliknij przycisk OK, aby przejść do następnego kroku.

Jeśli nie masz konta magazynu usługi Resource Manager zgodny lub sieci wirtualnej, można utworzyć klikając **+ konto magazynu** lub **+ sieć** przycisków w górnej części strony.

## <a name="next-steps"></a>Kolejne kroki
[Konfigurowanie ustawień replikacji](./site-recovery-setup-replication-settings-vmware.md).
