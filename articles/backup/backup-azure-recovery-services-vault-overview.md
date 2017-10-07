---
title: "aaaOverview Magazyny usług odzyskiwania | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie i porównanie Magazyny usług odzyskiwania i magazyny kopii zapasowych platformy Azure."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.assetid: 38d4078b-ebc8-41ff-9bc8-47acf256dc80
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/15/2017
ms.author: markgal;arunak
ms.openlocfilehash: 77dd9ece7fe86429cc6f9a47a68b5150a1f4af71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="recovery-services-vaults-overview"></a>Omówienie Magazyny usług odzyskiwania

W tym artykule opisano funkcje hello magazynu usług odzyskiwania. Magazyn usług odzyskiwania jest jednostką magazynu na platformie Azure, która przechowuje dane. dane Hello jest zwykle kopii danych lub informacje o konfiguracji dla maszyn wirtualnych (VM), obciążenia, serwerach lub stacjach roboczych. Magazyn usług odzyskiwania jest wersją Resource Manager hello magazynu kopii zapasowych. Firma Microsoft zaleca toouse Magazyny usług odzyskiwania i tooconvert Magazyny usług tooRecovery magazynami żadnych kopii zapasowych.

## <a name="what-is-a-recovery-services-vault"></a>Co to jest magazyn usługi Recovery Services?

Magazyn usług odzyskiwania ma wartość jednostki magazynu online na platformie Azure używać toohold dane, takie jak kopii zapasowych, punkty odzyskiwania, a zasady tworzenia kopii zapasowej. Dane kopii zapasowej toohold Magazyny usług odzyskiwania służy do różnych usług Azure, takich jak maszyny wirtualne IaaS (Linux lub Windows) oraz baz danych Azure SQL. System obsługi magazynów usług odzyskiwania Centrum programu DPM, Windows Server, serwer kopii zapasowej Azure i więcej. Magazyny usług odzyskiwania był łatwy tooorganize danych kopii zapasowych, przy jednoczesnym zmniejszeniu obciążenia administracyjnego.

W ramach subskrypcji platformy Azure można utworzyć dowolną liczbę Magazyny usług odzyskiwania według uznania.

## <a name="comparing-recovery-services-vaults-and-backup-vaults"></a>Magazyny usług odzyskiwania porównaniem i magazynami kopii zapasowych

Magazyny usług odzyskiwania są oparte na modelu usługi Azure Resource Manager hello Azure, magazyny kopii zapasowych są oparte na powitania modelu Azure Service Manager. Po uaktualnieniu magazynu usług odzyskiwania tooa magazynu kopii zapasowych danych kopii zapasowej hello podczas i po zakończeniu procesu uaktualniania hello pozostanie niezmieniona. Magazyny usług odzyskiwania zapewniają funkcje nie są dostępne dla magazyny kopii zapasowych, takich jak:

- **Rozszerzone dane kopii zapasowej bezpiecznego toohelp możliwości**: magazynów z usług odzyskiwania, kopia zapasowa Azure zapewnia bezpieczeństwo możliwości tooprotect kopii zapasowych w chmurze. Te funkcje zabezpieczeń sprawdź secure kopii zapasowych i bezpiecznie odzyskać dane z kopii zapasowych w chmurze, nawet jeśli serwerów produkcyjnych i tworzenia kopii zapasowej są uszkodzone. [Dowiedz się więcej](backup-azure-security-feature.md)

- **Centralne monitorowanie sieci hybrydowe środowiska IT**: magazynów z usług odzyskiwania, można monitorować nie tylko z [maszyn wirtualnych IaaS platformy Azure](backup-azure-manage-vms.md) , ale także z [zasoby lokalne](backup-azure-manage-windows-server.md#manage-backup-items) z centralnej portalu. [Dowiedz się więcej](http://azure.microsoft.com/blog/alerting-and-monitoring-for-azure-backup)

- **Kontrola dostępu oparta na rolach (RBAC)**: RBAC zapewnia szczegółowej zarządzania kontroli dostępu na platformie Azure. [Platforma Azure oferuje różne role wbudowane](../active-directory/role-based-access-built-in-roles.md), a kopia zapasowa Azure ma trzy [punktów odzyskiwania toomanage wbudowane role](backup-rbac-rs-vault.md). Magazyny usług odzyskiwania są zgodne z RBAC, który ogranicza możliwość użycia kopii zapasowej i przywracanie dostępu toohello zdefiniowany zestaw ról użytkownika. [Dowiedz się więcej](backup-rbac-rs-vault.md)

- **Chroń wszystkie konfiguracje maszyn wirtualnych Azure**: Magazyny usług odzyskiwania chronić maszyny wirtualne oparte na Menedżera zasobów, w tym dyski Premium, dysków zarządzanych i szyfrowane maszyn wirtualnych. Uaktualnianie tooa magazynu kopii zapasowej magazyn usług odzyskiwania i zapewnia hello tooupgrade możliwości tooResource Twojego programu Service Manager na podstawie maszyn wirtualnych maszyn wirtualnych w Menedżerze. Podczas uaktualniania magazynu hello, można zachować punktów odzyskiwania maszyny Wirtualnej opartej na programu Service Manager i skonfigurować ochronę dla hello uaktualnione VMs (włączone Resource Manager). [Dowiedz się więcej](http://azure.microsoft.com/blog/azure-backup-recovery-services-vault-ga)

- **Natychmiastowego przywracania dla maszyn wirtualnych IaaS**: Magazyny usług odzyskiwania przy użyciu, można przywrócić pliki i foldery z maszyn wirtualnych IaaS bez przywracania hello całą maszynę Wirtualną, która umożliwia szybsze przywracania. Natychmiastowego przywracania dla maszyn wirtualnych IaaS jest dostępna dla systemów Windows i maszyn wirtualnych systemu Linux. [Dowiedz się więcej](http://azure.microsoft.com/blog/instant-file-recovery-from-azure-linux-vm-backup-using-azure-backup-preview)

## <a name="managing-your-recovery-services-vaults-in-hello-portal"></a>Zarządzanie z Magazyny usług odzyskiwania w portalu hello
Tworzenie i zarządzanie Magazyny usług odzyskiwania w portalu Azure hello jest łatwe, ponieważ hello usługi Kopia zapasowa jest zintegrowany z hello blok ustawień platformy Azure. Integracja ta oznacza, że można tworzyć ani nimi zarządzać Magazyn usług odzyskiwania *w kontekście hello usługi docelowej hello*. Na przykład punkty odzyskiwania hello tooview dla maszyny Wirtualnej, zaznacz go i kliknij przycisk **kopii zapasowej** w bloku ustawienia hello. pojawi się toothat określone informacje o kopii zapasowej Hello maszyny Wirtualnej. W hello poniższy przykład **ContosoVM** jest nazwą hello hello maszyny wirtualnej. **ContosoVM demovault** jest nazwą hello hello magazyn usług odzyskiwania. Nie ma potrzeby tooremember hello nazwa magazynu usług odzyskiwania hello przechowujący hello punktów odzyskiwania, dostęp do tych informacji z hello maszyny wirtualnej.  

![Szczegóły magazynu usług odzyskiwania maszyny Wirtualnej](./media/backup-azure-recovery-services-vault-overview/rs-vault-in-context.png)

Jeśli wiele serwerów są chronione przy użyciu hello usług odzyskiwania tego samego magazynu, może być bardziej logiczne toolook na powitalne magazyn usług odzyskiwania. Wyszukaj wszystkie magazyny usług odzyskiwania w ramach subskrypcji hello i wybierz z listy hello.

Witaj poniższe sekcje zawierają tooarticles łącza, który objaśnia, jak toouse usług odzyskiwania magazynu w każdym typem działania.

### <a name="back-up-data"></a>Tworzenie kopii zapasowej danych
- [Tworzenie kopii zapasowej maszyny Wirtualnej platformy Azure](backup-azure-vms-first-look-arm.md)
- [Tworzenie kopii zapasowej systemu Windows Server lub stacji roboczej systemu Windows](backup-try-azure-backup-in-10-mins.md)
- [Wykonaj kopię zapasową tooAzure obciążeń programu DPM](backup-azure-dpm-introduction.md)
- [Przygotowanie tooback dużych obciążeń, za pomocą serwera usługi Kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md)

### <a name="manage-recovery-points"></a>Zarządzanie punktami odzyskiwania
- [Zarządzanie kopiami zapasowymi maszyny Wirtualnej Azure](backup-azure-manage-vms.md)
- [Zarządzanie plikami i folderami](backup-azure-manage-windows-server.md)

### <a name="restore-data-from-hello-vault"></a>Przywróć dane z magazynu hello
- [Odzyskanie poszczególnych plików maszyny Wirtualnej platformy Azure](backup-azure-restore-files-from-vm.md)
- [Przywracanie maszyny Wirtualnej platformy Azure](backup-azure-arm-restore-vms.md)

### <a name="secure-hello-vault"></a>Witaj bezpiecznego magazynu
- [Zabezpieczanie danych kopii zapasowej w chmurze w Magazyny usług odzyskiwania](backup-azure-security-feature.md)



## <a name="next-steps"></a>Następne kroki
Użyj poniższego artykułu dla hello:</br>
[Tworzenie kopii zapasowej maszyn wirtualnych IaaS](backup-azure-arm-vms-prepare.md)</br>
[Utwórz kopię zapasową serwera kopia zapasowa Azure](backup-azure-microsoft-azure-backup.md)</br>
[Tworzenie kopii zapasowej systemu Windows Server](backup-configure-vault.md)
