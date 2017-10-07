---
title: "Magazyn usług aaaRecovery — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ta wersja hello — często zadawane pytania obsługuje hello publicznej wersji zapoznawczej hello usługi Kopia zapasowa Azure. Toofrequently odpowiedzi zadawane pytania dotyczące agenta kopii zapasowej hello, tworzenia kopii zapasowej i przechowywania, odzyskiwania, zabezpieczeń i inne typowe pytania dotyczące hello rozwiązania Azure Backup."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "rozwiązanie kopii zapasowych; usługa kopii zapasowych"
ms.assetid: 5f55b500-1ee9-4f64-9306-02d6f7a8eded
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/21/2016
ms.author: markgal;trinadhk;
ms.openlocfilehash: 882b2e67ed424dc9f3681a8870e6b4c7b4cdcaec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vault---faq"></a>Magazyn usług Recovery Services — często zadawane pytania
Ten artykuł zawiera informacje tooRecovery określonych usług magazynu i uzupełnia go hello [kopia zapasowa Azure — często zadawane pytania](backup-azure-backup-faq.md). Hello Azure Backup — często zadawane pytania zapewnia hello pełny zestaw pytań i odpowiedzi dotyczących hello usługi Kopia zapasowa Azure.  

W sekcji Disqus tego artykułu lub powiązanego artykułu hello można zadawać pytania dotyczące usługi Azure Backup. Można również zadawać pytania dotyczące usługi Azure Backup hello w hello [forum dyskusyjne](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Magazyny usług Recovery Services są oparte na usłudze Resource Manager. Czy magazyny usługi Backup (tryb klasyczny) są nadal obsługiwane? <br/>
Tak. Magazyny usługi Backup nadal są obsługiwane. Magazyny kopii zapasowych w hello [klasyczny portal](https://manage.windowsazure.com). Magazyny usług odzyskiwania w hello [portalu Azure](https://portal.azure.com). Jednak zaleca się możesz toocreate magazynu usług odzyskiwania jako wszystkie przyszłe ulepszenia będą dostępne tylko w magazynie usług odzyskiwania.

## <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Czy można migrować magazynu usług odzyskiwania tooa magazynu kopii zapasowej? <br/>
Niestety nie, w tym momencie nie można migrować zawartość hello tooa magazynu kopii zapasowej, które Magazyn usług odzyskiwania. Pracujemy nad dodaniem tej funkcji, ale nie jest ona dostępna w ramach publicznej wersji zapoznawczej.

## <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Czy magazyny usługi Recovery Services obsługują klasyczne maszyny wirtualne, czy maszyny wirtualne oparte na usłudze Resource Manager? <br/>
Magazyny usługi Recovery Services obsługują oba modele.  Można tworzyć kopie zapasowe maszyny Wirtualnej utworzonej w portalu klasycznym hello (które są maszyn wirtualnych w trybie klasycznym) lub maszyny Wirtualnej utworzonej w hello portalu Azure (które są Menedżera zasobów na podstawie) Magazyn usług odzyskiwania tooa.

## <a name="i-have-backed-up-my-classic-vms-in-backup-vault-now-i-want-toomigrate-my-vms-from-classic-mode-tooresource-manager-mode--how-can-i-backup-them-in-recovery-services-vault"></a>Mam utworzone kopie zapasowe moich klasycznych maszyn wirtualnych w magazynie usługi Backup. Chcę toomigrate maszyn wirtualnych z trybu Menedżera tooResource trybu klasycznego.  Jak mogę utworzyć ich kopię zapasową w magazynie usługi Recovery Services?
Kopie zapasowe klasycznych maszyn wirtualnych w magazynie kopii zapasowych nie migracji automatycznie toorecovery usług magazynu podczas migracji hello maszyn wirtualnych z tooResource klasycznym trybie menedżera. Wykonaj poniższe działania, aby przeprowadzić migrację kopii zapasowych maszyn wirtualnych:

1. W magazynie kopii zapasowych Przejdź zbyt**chronione elementy** i wybierz hello maszyny Wirtualnej. Kliknij pozycję [Zatrzymaj ochronę](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Pozostaw opcję *Usuń powiązane dane kopii zapasowych* **niezaznaczoną**.
2. W hello [portalu Azure](https://portal.azure.com), przejdź toohello **rozszerzenia** menu hello maszyny Wirtualnej, a następnie odinstaluj hello **VMSnapshot/VMSnapshotLinux** rozszerzenia.
3. Migruj maszynę wirtualną hello z trybu Menedżera tooResource trybu klasycznego. Upewnij się, że magazynu i sieci odpowiadającego toovirtual maszyny również są migrowanych tooResource menedżera trybu.
4. Tworzenie magazynu usług odzyskiwania i konfigurowanie tworzenia kopii zapasowej na powitania migracji maszyny wirtualnej przy użyciu **kopii zapasowej** akcji na pulpicie nawigacyjnym magazynu. Dowiedz się więcej na temat zbyt[włączenia kopii zapasowej w magazynie usług odzyskiwania](backup-azure-vms-first-look-arm.md)
