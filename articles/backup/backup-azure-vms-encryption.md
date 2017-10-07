---
title: "maszyny wirtualne przy użyciu usługi Kopia zapasowa Azure szyfrowane aaaBackup i przywracania"
description: "Ten artykuł zawiera informacje o kopii zapasowej hello i Przywróć środowisko dla maszyn wirtualnych szyfrowane przy użyciu szyfrowania dysków Azure."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Jak tooback zapasowej i przywracania szyfrowane maszyn wirtualnych w usłudze Kopia zapasowa Azure
Ten artykuł zawiera informacje o krokach toobackup i przywracania maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure. Zapewnia także szczegółowe informacje o obsługiwanych scenariuszach wymagania wstępne i kroki rozwiązywania problemów w przypadku wystąpienia błędów.

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
> [!NOTE]
> * Kopia zapasowa i przywracanie zaszyfrowanych maszyn wirtualnych jest obsługiwana tylko dla maszyn wirtualnych wdrożonych Menedżera zasobów. Nie jest obsługiwana dla maszyn wirtualnych klasycznego. <br>
> * Jest obsługiwane w systemach Windows i Linux maszyn wirtualnych, za pomocą szyfrowania dysków Azure, która wykorzystuje hello branżowy standard funkcji BitLocker funkcje systemu Windows i DM-Crypt Linux tooprovide szyfrowania dysków. <br>
> * Jest obsługiwane tylko w maszynach wirtualnych szyfrowana przy użyciu klucza szyfrowania funkcją BitLocker i klucza szyfrowania kluczy. Nie jest obsługiwana dla maszyn wirtualnych szyfrowane tylko przy użyciu klucza szyfrowania funkcją BitLocker. <br>
>
>

## <a name="prerequisites"></a>Wymagania wstępne
1. Maszyna wirtualna została zaszyfrowana przy użyciu [szyfrowania dysków Azure](../security/azure-security-disk-encryption.md). Powinny być szyfrowane przy użyciu klucza szyfrowania funkcją BitLocker i klucza szyfrowania kluczy.
2. Magazyn usług odzyskiwania został utworzony i ustawić za pomocą replikacji magazynu kroki wymienione w artykule hello [przygotować swoje środowisko do tworzenia kopii zapasowej](backup-azure-arm-vms-prepare.md).
3. Kopia zapasowa Azure została podana [magazynu kluczy tooaccess uprawnienia](#provide-permissions-to-azure-backup) zawierający klucze, szyfrowane klucze tajne dla maszyn wirtualnych.

## <a name="backup-encrypted-vm"></a>Kopia zapasowa szyfrowane maszyny Wirtualnej
Użyj powitania po celem tworzenia kopii zapasowej tooset kroki, zdefiniowania zasad, skonfigurować elementy i wyzwalanie tworzenia kopii zapasowej.

### <a name="configure-backup"></a>Konfigurowanie kopii zapasowych
1. Jeśli masz już magazyn usług odzyskiwania, Otwórz, przejdź toonext kroku. Jeśli nie masz otwarte magazyn usług odzyskiwania, ale znajdują się w portalu Azure, w menu centralnym hello hello kliknij **Przeglądaj**.

   * Na liście hello zasobów, wpisz **usług odzyskiwania**.
   * Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe. Po wyświetleniu pozycji **Magazyny Usług odzyskiwania** kliknij ją.

      ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     zostanie wyświetlona lista Hello Magazyny usług odzyskiwania. Z listy hello Magazyny usług odzyskiwania wybierz magazyn.

     Otwiera Hello wybranego magazynu z pulpitu nawigacyjnego.
2. Z listy hello elementów, który pojawia się w magazynie, kliknij przycisk **kopii zapasowej** tooopen hello kopii zapasowej bloku.

      ![Otwarcie bloku Kopia zapasowa](./media/backup-azure-vms-encryption/select-backup.png)
3. W bloku kopia zapasowa hello, kliknij **cel kopii zapasowej** bloku celu kopii zapasowej hello tooopen.

      ![Otwarcie bloku scenariusza](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Na powitania bloku celu kopii zapasowej, należy ustawić **gdzie działa Twoje obciążenie** tooAzure i **co chcesz toobackup** tooVirtual komputera, a następnie kliknij przycisk **OK**.

   Zamyka Hello bloku celu kopii zapasowej i zostanie otwarty blok zasady tworzenia kopii zapasowej hello.

   ![Otwarcie bloku scenariusza](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. W bloku zasad tworzenia kopii zapasowej hello, wybierz zasady tworzenia kopii zapasowej hello tooapply toohello magazynu i kliknij **OK**.

      ![Wybór zasad tworzenia kopii zapasowej](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    Szczegóły Hello hello domyślne zasady są wyświetlane w hello szczegóły. Jeśli chcesz toocreate zasady, wybierz opcję **Utwórz nowy** z menu rozwijanego hello. Po kliknięciu **OK**, hello zasad tworzenia kopii zapasowej jest skojarzony z magazynem hello.

    Następnie wybierz hello tooassociate maszyn wirtualnych z magazynem hello.
6. Wybierz hello szyfrowane maszyn wirtualnych tooassociate z hello określone zasady i kliknij przycisk **OK**.

      ![Wybierz zaszyfrowanych maszyny wirtualne](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Ta strona zawiera komunikat o magazynie kluczy, wybranych maszyn wirtualnych skojarzone toohello szyfrowane. Usługa tworzenia kopii zapasowej wymaga dostęp tylko do odczytu toohello kluczy i kluczy tajnych w magazynie kluczy hello. Używa klucza toobackup tych uprawnień i klucz tajny, wraz z hello skojarzone maszyn wirtualnych. **Musi nadać uprawnienia toobackup usługi tooaccess klucza magazynu dla kopii zapasowych toowork**. Możesz podać te uprawnienia za pomocą [czynności wymienionych w poniższej sekcji hello](#provide-permissions-to-azure-backup).

      ![Zaszyfrowanego komunikatu maszyny wirtualne](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Teraz, gdy zdefiniowano wszystkich ustawień dla magazynu hello, w bloku kopia zapasowa powitania kliknij włączenia kopii zapasowej u dołu strony hello hello. Włącz kopii zapasowej wdraża hello zasad toohello magazynu i maszyn wirtualnych hello.
8. Hello kolejną fazą przygotowania instaluje hello agenta maszyny Wirtualnej lub wprowadzania hello się, że Agent maszyny Wirtualnej jest zainstalowany. toodo hello sam, wykonaj kroki hello wymienione w artykule hello [przygotować swoje środowisko do tworzenia kopii zapasowej](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Wyzwolenie zadanie tworzenia kopii zapasowej
Wykonaj kroki hello wymienione w artykule hello [toorecovery kopii zapasowych maszyn wirtualnych platformy Azure z usług magazynu](backup-azure-arm-vms.md) tootrigger zadanie tworzenia kopii zapasowej.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Kontynuować kopie zapasowe utworzono już kopie zapasowe maszyn wirtualnych z włączone szyfrowanie  
Masz już w trakcie tworzenia kopii zapasowej się w magazynie usług odzyskiwania maszyn wirtualnych i włączono szyfrowania w późniejszym czasie, należy nadać uprawnienia toobackup usługi tooaccess klucza magazynu dla toocontinue kopii zapasowych. Możesz podać te uprawnienia za pomocą [kroki opisane w poniższej sekcji hello](#provide-permissions-to-azure-backup) lub przy użyciu programu PowerShell czynności wymienionych w **włączenia kopii zapasowej** sekcji [dokumentacji programu PowerShell](backup-azure-vms-automation.md). 

## <a name="provide-permissions-tooazure-backup"></a>Podaj tooAzure uprawnienia kopii zapasowej
Wykonanie kopii zapasowej zaszyfrowanego maszyn wirtualnych i używać hello następujące kroki tooprovide odpowiednie uprawnienia tooAzure kopii zapasowej tooaccess magazynu kluczy:
1. Wybierz **więcej usług** i wyszukaj **klucza magazynów**.

    ![Magazyn kluczy wyszukiwania](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. Z listy hello magazynów kluczy wybierz magazyn kluczy hello skojarzone z zaszyfrowanych maszynę Wirtualną, którą należy toobe kopii zapasowej.

     ![Wybierz magazyn kluczy](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Kliknij przycisk **zasady dostępu** , a następnie **Dodaj nowe**.

    ![Dodawanie zasad dostępu](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Kliknij przycisk **Wybierz podmiot zabezpieczeń** i typ **usługi zarządzania kopii zapasowej** hello pasku wyszukiwania. 

    ![Wyszukiwania usługi tworzenia kopii zapasowej](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Wybierz **usługi zarządzania kopii zapasowej** i kliknij przycisk Wybierz.

    ![Wybierz usługi tworzenia kopii zapasowej](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Wybierz **kopia zapasowa Azure** w konfiguracji z szablonu listy rozwijanej. Wstępnie wypełnia hello wymagane uprawnienia w uprawnieniach klucz i tajny uprawnień listy rozwijanej. 

    ![Wybierz kopia zapasowa Azure](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. Kliknij przycisk **OK**. Zwróć uwagę, że usługa zarządzania kopii zapasowej pobiera dodane w bloku zasad dostępu. 

    ![Zasady dostępu usługi tworzenia kopii zapasowej](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. Kliknij pozycję **Zapisz**. Zapewni to hello wymagane uprawnienia tooAzure kopii zapasowej.

    ![Zasady dostępu usługi tworzenia kopii zapasowej](./media/backup-azure-vms-encryption/save-access-policy.png)

Po pomyślnie zostały podane uprawnienia, może kontynuować włączenie kopii zapasowej zaszyfrowanego maszyn wirtualnych.

## <a name="restore-encrypted-vm"></a>Przywracanie zaszyfrowanych maszyny Wirtualnej
toorestore szyfrowane maszyny Wirtualnej, pierwszy przy użyciu dysków przywrócić kroki opisane powyżej w sekcji **przywracania kopii zapasowej dysków** w [Wybieranie konfiguracji maszyny Wirtualnej przywracania](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Po tym można użyć jednej z hello następujące opcje:
* Wykonaj kroki PowerShell hello wymienionych w [utworzyć Maszynę wirtualną z dysków przywróconej](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate pełne maszyny Wirtualnej z przywróconą dysków.
* OR [Użyj szablonu wygenerowane jako część przywrócenia dysków](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate maszyn wirtualnych z przywróconą dysków. Szablony może służyć tylko dla punktów odzyskiwania utworzonych po 26 kwietnia 2017 r.

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami
| Operacja | Szczegóły błędu | Rozwiązanie |
| --- | --- | --- |
| Tworzenie kopii zapasowych |Sprawdzanie poprawności nie powiodła się, ponieważ maszyna wirtualna jest zaszyfrowana z BEK samodzielnie. Kopie zapasowe można włączyć tylko dla zaszyfrowanych za pomocą zarówno BEK i KEK maszyn wirtualnych. |Maszyna wirtualna powinna być szyfrowana przy użyciu BEK i KEK. Najpierw odszyfrować hello maszyny Wirtualnej i szyfrowania za pomocą zarówno BEK i KEK. Włączenia kopii zapasowej, gdy maszyna wirtualna jest szyfrowana przy użyciu zarówno BEK i KEK. Dowiedz się więcej na temat [odszyfrowywania i szyfrowania hello maszyny Wirtualnej](../security/azure-security-disk-encryption.md)  |
| Przywracanie |Nie można przywrócić tej zaszyfrowanej maszyny Wirtualnej, ponieważ nie istnieje magazyn kluczy skojarzone z tej maszyny Wirtualnej. |Tworzenie przy użyciu magazynu kluczy [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md). Zobacz artykuł hello [Przywracanie klucza magazynu kluczy i klucz tajny przy użyciu usługi Kopia zapasowa Azure](backup-azure-restore-key-secret.md) toorestore klucza i klucz tajny, jeśli są nieobecne. |
| Przywracanie |Nie można przywrócić tej zaszyfrowanej maszyny Wirtualnej, ponieważ nie istnieją klucza i klucz tajny skojarzony z tej maszyny Wirtualnej. |Zobacz artykuł hello [Przywracanie klucza magazynu kluczy i klucz tajny przy użyciu usługi Kopia zapasowa Azure](backup-azure-restore-key-secret.md) toorestore klucza i klucz tajny, jeśli są nieobecne. |
| Przywracanie |Usługa tworzenia kopii zapasowej nie ma autoryzacji tooaccess zasobów w ramach subskrypcji. |Jak wspomniano powyżej, przywrócenia dysków, wykonując kroki wymienione w sekcji **przywracania kopii zapasowej dysków** w [Wybieranie konfiguracji maszyny Wirtualnej przywracania](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Po, użytkownik programu PowerShell za[utworzyć Maszynę wirtualną z dysków przywróconej](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Tworzenie kopii zapasowych | Usługa Kopia zapasowa Azure nie ma wystarczających uprawnień tooKey magazynu dla kopii zapasowej z zaszyfrowanych maszyny wirtualne | Maszyna wirtualna powinna być szyfrowana przy użyciu zarówno klucz szyfrowania funkcją BitLocker, jak i klucz szyfrowania klucza. Po wykonaniu tej kopii zapasowej powinno być włączone.  Usługi tworzenia kopii zapasowej należy podawać te uprawnienia za pomocą [czynności wymienionych w powyższej sekcji hello](#provide-permissions-to-azure-backup) lub za pomocą programu PowerShell czynności wymienionych w hello **Włącz ochronę** sekcji hello programu PowerShell Dokumentacja w [AzureRM.RecoveryServices.Backup użyj polecenia cmdlet tooback zapasowe](backup-azure-vms-automation.md#back-up-azure-vms). |  
