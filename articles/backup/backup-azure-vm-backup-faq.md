---
title: "aaaAzure kopii zapasowej maszyny Wirtualnej — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na pytania toocommon o: w jaki sposób działa kopii zapasowej maszyny Wirtualnej platformy Azure, ograniczenia i co się stanie po toopolicy zmiany wystąpić"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: azure vm backup, azure vm restore, backup policy
ms.assetid: c4cd7ff6-8206-45a3-adf5-787f64dbd7e1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: a1ad2cb3a379577a8c4258c8207ce75809e11a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-vm-backup-service"></a>Pytania dotyczące hello usługi Kopia zapasowa maszyny Wirtualnej Azure
Ten artykuł zawiera toohelp pytania toocommon odpowiedzi szybko poznać hello składników kopii zapasowej maszyny Wirtualnej Azure. W niektórych hello odpowiedzi są artykuły toohello łącza, zawierające szczegółowe informacje. Można również zadawać pytania dotyczące usługi Azure Backup hello w hello [forum dyskusyjne](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Konfigurowanie kopii zapasowych
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Czy magazyny usługi Recovery Services obsługują klasyczne maszyny wirtualne, czy maszyny wirtualne oparte na usłudze Resource Manager? <br/>
Magazyny usługi Recovery Services obsługują oba modele.  Można tworzyć kopie zapasowe klasyczne maszyny Wirtualnej (utworzonej w portalu klasycznym hello) lub tooa Menedżera zasobów maszyny Wirtualnej (utworzonej w portalu Azure hello), który magazyn usług odzyskiwania.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup-"></a>Jakie konfiguracje nie są obsługiwane przez funkcję tworzenia kopii zapasowej maszyny wirtualnej platformy Azure?
Zapoznaj się z informacjami w tematach [Obsługiwane systemy operacyjne](backup-azure-arm-vms-prepare.md#supported-operating-system-for-backup) i [Limitations of VM backup (Ograniczenia tworzenia kopii zapasowej maszyny wirtualnej)](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>Dlaczego nie widzę swojej maszyny wirtualnej w kreatorze konfigurowania kopii zapasowych?
W kreatorze konfigurowania kopii zapasowych usługi Azure Backup na liście są wyświetlane tylko maszyny wirtualne spełniające następujące warunki:
* Nie jest jeszcze chroniona — można sprawdzić hello stanu kopii zapasowej maszyny wirtualnej, przechodząc bloku tooVM i sprawdzanie stanu kopii zapasowej z Menu ustawień hello bloku. Dowiedz się więcej na temat zbyt[sprawdzanie stanu kopii zapasowej maszyny wirtualnej](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-management-blade)
* Należy toosame region jako maszyna wirtualna

## <a name="backup"></a>Tworzenie kopii zapasowych
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>Czy dla zadań tworzenia kopii zapasowej na żądanie będzie stosowany ten sam harmonogram przechowywania co dla zaplanowanych zadań tworzenia kopii zapasowej?
Nie. Zakres przechowywania hello toospecify potrzebę zadanie tworzenia kopii zapasowej na żądanie. Domyślnie dane będą przechowywane przez 30 dni po wyzwoleniu z portalu. 

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-toowork"></a>Ostatnio na niektórych maszynach wirtualnych została włączona usługa Azure Disk Encryption. Moje kopie zapasowe będą nadal toowork?
Musisz mieć uprawnienia toogive dla tooaccess usługi Kopia zapasowa Azure Key Vault. Te uprawnienia możesz podać w programie PowerShell przy użyciu czynności wymienionych w sekcji *Włączenie kopii zapasowej* dokumentacji programu [PowerShell](backup-azure-vms-automation.md).

### <a name="i-migrated-disks-of-a-vm-toomanaged-disks-will-my-backups-continue-toowork"></a>Po migracji dysków dysków toomanaged maszyny Wirtualnej. Moje kopie zapasowe będą nadal toowork?
Tak, kopie zapasowe działają bezproblemowo i toore nie potrzeby — skonfigurowanie usługi Kopia zapasowa. 

## <a name="restore"></a>Przywracanie
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>Jak wybrać między przywróceniem dysków a pełnym przywróceniem maszyny wirtualnej?
Pełne przywracanie maszyny wirtualnej na platformie Azure można traktować jak opcję szybkiego utworzenia przywracanej maszyny wirtualnej. Przywracanie maszyny Wirtualnej opcja zmienia nazwy hello dysków, kontenery używane przez dyski, publiczne adresy IP interfejsu sieciowego nazwy unikatowość zasobów pobierania utworzona w ramach tworzenia maszyny Wirtualnej. On również nie doda hello wirtualna tooavailability zestawu. 

Opcji przywracania dysków można używać w następujących celach:
* Dostosowywanie hello maszynę Wirtualną, która pobiera utworzone na podstawie punktu w czasie konfiguracji jak zmiana rozmiaru hello z konfiguracji kopii zapasowej
* Dodawanie konfiguracji, które nie są obecne w momencie hello kopii zapasowej 
* Kontrolować konwencję nazewnictwa hello dla uzyskiwania tworzenia zasobów
* Dodaj zestaw tooavailability maszyny Wirtualnej
* Korzystasz z konfiguracji, którą można uzyskać jedynie przy użyciu programu PowerShell lub definicji deklaracyjnego szablonu

## <a name="manage-vm-backups"></a>Zarządzanie kopiami zapasowymi maszyn wirtualnych
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>Co się stanie po zmianie zasad kopii zapasowych na maszynach wirtualnych?
Podczas stosowania nowej zasady na wirtualne, harmonogram i przechowywania nowych zasad hello nastąpią. Jeśli przechowywania zostanie rozszerzony, istniejące punkty odzyskiwania zostaną oznaczone jako tookeep je zgodnie z harmonogramem nowych zasad. W przypadku przechowywania, są oznaczone do oczyszczania w hello następne zadanie oczyszczania i zostaną usunięte. 
