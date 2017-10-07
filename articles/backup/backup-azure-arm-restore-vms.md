---
title: "Kopia zapasowa Azure: Przywracanie maszyn wirtualnych przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Przywracanie maszyny wirtualnej platformy Azure z punktu odzyskiwania za pomocą portalu Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: Przywracanie kopii zapasowej. jak toorestore; punkt odzyskiwania;
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Użyj maszyn wirtualnych Azure toorestore portalu
> [!div class="op_single_selector"]
> * [Przywracanie maszyn wirtualnych w portalu klasycznym](backup-azure-restore-vms.md)
> * [Przywracanie maszyn wirtualnych w portalu Azure](backup-azure-arm-restore-vms.md)
>
>

Ochrona danych za tworzenie migawek danych w określonych odstępach czasu. Te migawki są określane jako punkty odzyskiwania, i są przechowywane w Magazyny usług odzyskiwania. Jeśli lub jeśli jest konieczne toorepair lub skompiluj ponownie Maszynę wirtualną, można przywrócić hello maszyny Wirtualnej za pomocą dowolnego hello zapisane punkty odzyskiwania. Po przywróceniu punkt odzyskiwania, można utworzyć nowej maszyny Wirtualnej, która odzwierciedla w momencie kopii zapasowej maszyny Wirtualnej, lub przywrócić dysków i szablon hello dołączonym do jego toocustomize hello przywrócić maszyny Wirtualnej lub wykonaj odzyskiwanie poszczególnych plików. W tym artykule opisano sposób toorestore tooa wirtualna nowej maszyny Wirtualnej lub dysków przywrócenia wszystkich kopii zapasowej. Odzyskiwanie poszczególnych plików, można znaleźć zbyt[odzyskać pliki z kopii zapasowej maszyny Wirtualnej Azure](backup-azure-restore-files-from-vm.md)

![3-Ways-Restore-from-VM-Backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem i pracą z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Ten artykuł zawiera hello informacje i procedury dotyczące przywracania maszyn wirtualnych wdrożonych przy użyciu hello modelu Resource Manager.
>
>

Przywrócenie maszyny Wirtualnej lub wszystkich dysków z maszyny Wirtualnej kopii zapasowej obejmuje dwa kroki:

1. Wybierz punkt przywracania dla przywracania
2. Wybór hello przywrócenia typu — Tworzenie nowej maszyny Wirtualnej lub przywrócenia dysków i określ wymagane parametry. 

## <a name="select-restore-point-for-restore"></a>Wybierz punkt przywracania do przywrócenia
1. Zaloguj się toohello [portalu Azure](http://portal.azure.com/)
2. Na hello Azure menu, kliknij przycisk **Przeglądaj** i liście hello usług, wpisz **usług odzyskiwania**. Lista Hello usług dopasowuje toowhat wpisywane. Po wyświetleniu **Magazyny usług odzyskiwania**, zaznacz go.

    ![Otwórz magazyn usług odzyskiwania](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    zostanie wyświetlona lista Hello magazynów w hello subskrypcji.

    ![Lista usług odzyskiwania magazynów](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Z listy hello wybierz hello magazynu skojarzone z hello ma toorestore maszyny Wirtualnej. Po kliknięciu magazynu hello otwiera jego pulpitu nawigacyjnego.

    ![Lista usług odzyskiwania magazynów](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Teraz, możesz hello magazynu w pulpicie nawigacyjnym. Na powitania **kopii zapasowej elementów** Kafelek, kliknij przycisk **maszyny wirtualne Azure** hello toodisplay maszyn wirtualnych skojarzony z magazynem hello.

    ![pulpitem nawigacyjnym magazynu](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Witaj **kopii zapasowej elementów** bloku otwiera i wyświetla hello listę maszyn wirtualnych platformy Azure.

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Z listy hello wybierz pulpit nawigacyjny hello tooopen maszyny Wirtualnej. pulpit nawigacyjny wirtualna Hello otwiera toohello obszarze monitorowania, zawierającą kafelka punktów przywracania hello.

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Polecenie menu pulpitu nawigacyjnego wirtualna hello **przywracania**

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    zostanie otwarty blok przywracania Hello.

    ![Blok przywracania](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Na powitania **przywrócić** bloku, kliknij przycisk **punkt przywracania** tooopen hello **przywracania wybierz punkt** bloku.

    ![Blok przywracania](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Domyślnie okno dialogowe hello Wyświetla wszystkie punkty przywracania z hello ostatnich 30 dni. Użyj hello **filtru** przedział czasu hello tooalter hello przywrócić punkty wyświetlane. Domyślnie są wyświetlane punkty przywracania na wszystkich spójności. Modyfikowanie **przywrócić wszystkie punkty** filtrować tooselect spójności określonych punktów przywracania. Aby uzyskać więcej informacji na temat poszczególnych typów punktu przywracania, zobacz opis hello [spójność danych](backup-azure-vms-introduction.md#data-consistency).  

   * **Przywróć spójności punktu** z tej listy wybierz:
     * Punkty przywracania na poziomie awarii
     * Punkty przywracania na poziomie aplikacji,
     * Punkty przywracania na poziomie systemu plików
     * Wszystkie punkty przywracania.  
8. Wybierz punkt przywracania, a następnie kliknij przycisk **OK**.

    ![Wybierz punkt przywracania](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Witaj **przywrócić** bloku pokazuje ustawiono hello punktu przywracania.

    ![punkt przywracania jest ustawiona.](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Na powitania **przywrócić** bloku **przywracania** otwierany automatycznie po ustawieniu punktu przywracania.

## <a name="choosing-a-vm-restore-configuration"></a>Wybieranie konfiguracji przywracania maszyny Wirtualnej
Teraz, gdy wybrano hello punkt przywracania, wybierz konfigurację przywracania maszyny Wirtualnej. Opcje dotyczące konfigurowania hello przywrócić maszyny Wirtualnej są toouse: Azure portal lub programu PowerShell.

1. Jeśli użytkownik nie są już istnieje, przejdź toohello **przywrócić** bloku. Upewnij się, [został wybrany punkt przywracania](#select-restore-point-for-restore)i kliknij przycisk **przywracania** tooopen hello **konfiguracji odzyskiwania** bloku.

    ![Kreator konfiguracji odzyskiwania jest ustawiona.](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Na powitania **przywracania** bloku dostępne są dwie opcje:
   * Przywróć pełną maszyny wirtualnej
   * Przywracanie kopii zapasowych dysków

Portal zapewnia szybkie tworzenie opcję przywróconej maszyny wirtualnej. Jeśli konfiguracja maszyny Wirtualnej hello toocustomize lub nazwy zasobów hello utworzone jako część utworzyć nową opcję maszyny Wirtualnej, użyj programu PowerShell lub portalu toorestore kopie zapasowe dysków i użyj tooattach poleceń programu PowerShell ich toochoice konfiguracji lub użyj szablonu maszyny Wirtualnej który pochodzi z przywracania hello toocustomize dysków przywrócić maszyny Wirtualnej. Zobacz [przywracanie maszyny Wirtualnej z konfiguracjami sieci specjalne](#restoring-vms-with-special-network-configurations) szczegółowe informacje na temat toorestore maszyny Wirtualnej, który ma wiele kart sieciowych lub w obszarze usługi równoważenia obciążenia. Jeśli maszyna wirtualna systemu Windows używa [Centrum licencjonowania](../virtual-machines/windows/hybrid-use-benefit-licensing.md), potrzebne są dyski toorestore i szablon programu PowerShell/zgodnie z poniższymi hello toocreate maszyny Wirtualnej i upewnij się, określ LicenseType jako "Windows_Server" podczas tworzenia maszyny Wirtualnej tooavail Centrum korzyści na przywróconą maszyną Wirtualną. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Utwórz nową maszynę Wirtualną z punktu przywracania
Jeśli nie masz już istnieje, [wybierz punkt przywracania](#restoring-vms-with-special-network-configurations) przed kontynuowaniem toocreating nowej maszyny Wirtualnej z przywracania punktu. Po wybraniu punktu przywracania na powitania **przywracania** bloku, wprowadź lub wybierz wartości dla każdego hello następujące pola:

* **Przywróć typu** — tworzenie maszyny wirtualnej.
* **Nazwa maszyny wirtualnej** — Podaj nazwę dla hello maszyny Wirtualnej. Nazwa Hello musi być unikatowy toohello grupy zasobów (dla VM wdrożone usługi Resource Manager) lub usługi w chmurze (w przypadku klasycznych maszyn wirtualnych). Nie można zamienić hello maszyny wirtualnej, jeśli już istnieje w subskrypcji hello.
* **Grupa zasobów** — Użyj istniejącej grupy zasobów lub Utwórz nową. Jeśli przywracasz klasyczne maszyny Wirtualnej, należy użyć tej nazwy hello toospecify pola w nowej usługi w chmurze. Jeśli tworzysz nową usługę chmury/grupy zasobów, nazwa hello musi być globalnie unikatowe. Zazwyczaj nazwa usługi w chmurze hello jest skojarzony z adresem URL publicznych — na przykład: [cloudservice]. cloudapp.net. Jeśli toouse nazwę hello zasobów chmury/grupy usługi w chmurze została już użyta, usługi chmury/grupy zasobów hello Azure przypisuje hello tej samej nazwy jak hello maszyny Wirtualnej. Azure Wyświetla usług chmury/grupy zasobów i maszyny wirtualne nie są skojarzone z grup koligacji. Aby uzyskać więcej informacji, zobacz [jak toomigrate z grup koligacji tooa regionalną sieć wirtualną (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Sieć wirtualna** — wybierz tę opcję hello sieć wirtualną (VNET), podczas tworzenia hello maszyny Wirtualnej. pole Hello zawiera wszystkie sieci wirtualne skojarzone z subskrypcją hello. Grupa zasobów hello maszyny Wirtualnej jest wyświetlany w nawiasach.
* **Podsieci** — Jeśli hello sieci Wirtualnej ma podsieci, hello pierwszej podsieci jest domyślnie zaznaczona. Jeśli istnieją dodatkowe podsieci, wybierz podsieć hello potrzebne.
* **Konto magazynu** — w tym menu znajdują hello kont magazynu w hello tej samej lokalizacji co hello magazyn usług odzyskiwania. Konta magazynu, które są obszar strefowo nadmiarowy nie są obsługiwane. Jeśli nie ma żadnych kont magazynu z hello tej samej lokalizacji co hello magazyn usług odzyskiwania, należy utworzyć przed rozpoczęciem powitalne operacji przywracania. typ replikacji konta magazynu Hello jest wymieniony w nawiasach.

![Kreator konfiguracji przywracania jest ustawiona.](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Jeśli przywracasz maszyn wirtualnych wdrożonych przez Menedżera zasobów należy zidentyfikować sieć wirtualną (VNET). Sieć wirtualną (VNET) jest opcjonalny w przypadku klasycznych maszyn wirtualnych.
> 2. Jeśli przywracasz maszyny wirtualne z dyskami zarządzanych, upewnij się, że wybrane konto magazynu nie jest włączona dla magazynu usługi Encryption(SSE) w jego okres istnienia.
> 3. Oparte na typ magazynu hello wybrane konto magazynu (premium lub standard), wszystkie dyski przywrócić będzie premium lub dyski standardowe. Obecnie nie obsługujemy trybu mieszanego dysków podczas przywracania.  
>
>

Na powitania **przywracania** bloku, kliknij przycisk **OK** toofinalize hello przywracania. Na powitania **przywrócić** bloku, kliknij przycisk **przywrócić** hello tootrigger podczas operacji przywracania.

## <a name="restore-backed-up-disks"></a>Przywracanie kopii zapasowych dysków
Jeśli chcesz maszyny wirtualnej hello toocustomize chcesz toocreate z kopii zapasowej dysków niż co znajduje się w bloku konfiguracji przywracania, wybierz opcję **przywrócenia dysków** wartości dla **przywrócić typu**. Ten wybór poprosi o podanie konta magazynu, w którym dyski zapasowe są kopiowane do. Wybierając konto magazynu, należy wybrać konto akcji hello tej samej lokalizacji, ponieważ magazyn usług odzyskiwania hello. Konta magazynu, które są obszar strefowo nadmiarowy nie są obsługiwane. Jeśli nie ma żadnych kont magazynu z hello tej samej lokalizacji co hello magazyn usług odzyskiwania, należy utworzyć przed rozpoczęciem powitalne operacji przywracania. typ replikacji konta magazynu Hello jest wymieniony w nawiasach.

Po zakończeniu operacji przywracania, można:
* [Użyj szablonu toocustomize hello przywrócić maszyny Wirtualnej](#use-templates-to-customize-restore-vm)
* [Użyj hello przywrócić dysków tooattach tooan istniejącej maszyny wirtualnej](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Utwórz nową maszynę wirtualną przy użyciu programu PowerShell z przywróconą dysków.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Na powitania **przywracania** bloku, kliknij przycisk **OK** toofinalize hello przywracania. Na powitania **przywrócić** bloku, kliknij przycisk **przywrócić** hello tootrigger podczas operacji przywracania.

![Konfiguracja odzyskiwania została zakończona](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Śledzenie hello operacji przywracania
Gdy użytkownik zainicjuje hello operacji przywracania, hello usługi Kopia zapasowa tworzy zadanie śledzenia hello operacji przywracania. Hello usługi Kopia zapasowa tworzy także i tymczasowo wyświetla hello powiadomień w obszarze powiadomień z portalu. Jeśli nie ma hello powiadomień, zawsze kliknięcie tooview ikonę powiadomienia hello powiadomienia.

![Przywracanie wyzwalane](./media/backup-azure-arm-restore-vms/restore-notification.png)

Operacja hello tooview podczas przetwarzania lub tooview po jej zakończeniu Otwórz listę zadań tworzenia kopii zapasowej hello.

1. Na hello Azure menu, kliknij przycisk **Przeglądaj** i liście hello usług, wpisz **usług odzyskiwania**. Lista Hello usług dopasowuje toowhat wpisywane. Po wyświetleniu **Magazyny usług odzyskiwania**, zaznacz go.

    ![Otwórz magazyn usług odzyskiwania](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    zostanie wyświetlona lista Hello magazynów w hello subskrypcji.

    ![Lista usług odzyskiwania magazynów](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Z listy hello wybierz hello magazynu skojarzone z hello przywróconej maszyny Wirtualnej. Po kliknięciu magazynu hello otwiera jego pulpitu nawigacyjnego.
3. Na pulpicie nawigacyjnym magazynu hello na powitania **zadania tworzenia kopii zapasowej** Kafelek, kliknij przycisk **maszyny wirtualne Azure** toodisplay hello zadania skojarzony z magazynem hello.

    ![pulpitem nawigacyjnym magazynu](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Witaj **zadania tworzenia kopii zapasowej** bloku otwiera i wyświetla hello listy zadań.

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Użyj szablonów maszyny wirtualnej z przywracania toocustomize
Raz [zakończeniu operacji przywracania dysków](#Track-the-restore-operation), można użyć szablonu hello, wygenerowane jako część toocreate operacji przywracania nowej maszyny Wirtualnej z konfiguracją inne niż kopii zapasowej konfiguracji lub toocustomize nazwy zasobów utworzone podczas tworzenia nowej maszyny wirtualnej z punktu przywracania. 

> [!NOTE]
> Szablony zostaną dodane jako część przywrócenia dysków dla punktów odzyskiwania po 1 marca 2017 r. Są one odpowiednie dla dysku niezaszyfrowane i niezarządzanych maszyn wirtualnych. Obsługa zaszyfrowane maszyn wirtualnych i zarządzania maszynami wirtualnymi dysku będzie dostępna w kolejnych wersjach. 
>
>

Szablon hello tooget wygenerowane jako część opcji dysków przywracania

1. Przejdź szczegóły zadania toorestore odpowiadającego toohello zadania. 
2. Na ekran szczegółów zadania przywracania powitania kliknij *wdrażanie szablonu* przycisk tooinitiate szablonu wdrożenia. 

     ![Przywróć przechodzenia zadania](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Na powitania bloku szablonu wdrażania niestandardowe wdrożenie, przy użyciu szablonu wdrażania zbyt[edytować i wdrażanie szablonu hello](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) lub dołączyć więcej dostosowań przez [tworzenia szablonu](../azure-resource-manager/resource-group-authoring-templates.md) przed wdrożeniem. 

   ![Trwa ładowanie szablonu wdrożenia](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Po wprowadzeniu hello wymagane wartości, należy zaakceptować hello *warunków i postanowień* i wybierz polecenie **zakupu**.

   ![Przesyłanie szablonu wdrożenia](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Wykonywane po przywróceniu kroki
* Korzystania z dystrybucji systemu Linux chmury inicjowania na podstawie takich jak Ubuntu, ze względów bezpieczeństwa hasła jest zablokowana post przywracania. Sprawdź użycie rozszerzenia VMAccess na powitania przywrócić maszyny Wirtualnej za[resetowania hasła hello](../virtual-machines/linux/classic/reset-access.md). Zalecamy używanie kluczy SSH w tych tooavoid dystrybucje Resetowanie hasła post przywracania.
* Podczas tworzenia kopii zapasowej konfiguracji hello rozszerzenia zostanie zainstalowany, jednak nie jest włączony. Jeśli widzisz jakikolwiek problem, zainstaluj ponownie rozszerzenia. 
* Jeśli hello kopii zapasowej maszyna wirtualna ma statyczny adres IP, przywracania post, przywróconą maszyną Wirtualną zostanie występuje konflikt tooavoid IP dynamiczny, podczas tworzenia przywracania maszyny Wirtualnej. Dowiedz się więcej na temat [dodać statycznych toorestored IP maszyny Wirtualnej](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* Przywróconą maszyną Wirtualną nie będzie miał wartość dostępności. Zaleca się użycie opcji dysków przywracania i [Dodawanie zestawu dostępności](../virtual-machines/windows/tutorial-availability-sets.md) tworzenia maszyny Wirtualnej za pomocą programu PowerShell lub szablonów przy użyciu przywrócenie dysków. 


## <a name="backup-for-restored-vms"></a>Tworzenie kopii zapasowej dla przywróconej maszyny wirtualne
Jeśli maszyna wirtualna toosame grupy zasobów z hello tej samej nazwy pierwotnie kopii zapasowej maszyny Wirtualnej została przywrócona, kopia zapasowa nadal na powitania przywracania post maszyny Wirtualnej. Jeśli masz przywrócić tooa maszyny Wirtualnej innej grupie zasobów lub określić inną nazwę dla przywróconej maszyny Wirtualnej, jest ona traktowana jako nowej maszyny Wirtualnej i potrzebujesz kopii zapasowej toosetup przywróconej maszyny wirtualnej.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Przywracanie maszyny Wirtualnej podczas awarii centrum danych Azure
Kopia zapasowa Azure umożliwia przywracanie z kopii zapasowych centrum danych sparowanego toohello maszyn wirtualnych w przypadku, gdy centrum danych podstawowych hello którym maszyny wirtualne są uruchomione po awarii środowiska i skonfigurować geograficznie nadmiarowego toobe magazynu kopii zapasowej. W takich scenariuszach należy tooselect konta magazynu, który znajduje się w centrum danych sparowanego i resztę procesu przywracania hello pozostaje w tym samym. Kopia zapasowa Azure używa usługi obliczeniowe z maszyny wirtualnej hello przywrócić toocreate sparowanego geo. Dowiedz się więcej o [odporności centrum danych Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Przywracanie maszyn wirtualnych z kontrolera domeny
Kopia zapasowa maszyn wirtualnych kontrolera domeny (DC) jest obsługiwany scenariusz w usłudze Kopia zapasowa Azure. Jednak należy uważać podczas procesu przywracania hello. proces przywracania poprawne Hello zależy od struktury hello hello domeny. W przypadku najprostszym hello pojedynczy kontroler domeny znajduje się w jednej domenie. Najczęściej w przypadku obciążeń produkcyjnych, będziesz mieć pojedynczą domenę z wielu kontrolerów domeny, prawdopodobnie z kilka kontrolerów domeny lokalnie. Ponadto może być lesie z wieloma domenami. 

Z usługi Active Directory perspektywy hello maszyny Wirtualnej platformy Azure jest podobnie jak inne maszyny Wirtualnej w nowoczesnych obsługiwanej funkcji hypervisor. Witaj główne różnice w funkcji hypervisor lokalnej jest dostępnej na platformie Azure jest konsoli maszyny Wirtualnej. Konsola jest wymagana dla niektórych scenariuszy, takich jak odzyskiwanie przy użyciu kopii zapasowej typu odzyskiwania systemu operacyjnego systemu od zera (BMR). Jednak przywrócenie maszyny Wirtualnej z magazynu kopii zapasowych hello nie zastępuje pełnego odzyskiwania systemu od ZERA. Active Directory przywracania trybu (DSRM) jest również dostępna, więc działało wszystkie scenariusze odzyskiwania usługi Active Directory. Aby uzyskać więcej informacji w tle, sprawdź, czy [kopia zapasowa i przywracanie zagadnienia dotyczące zwirtualizowanych kontrolerów domeny](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) i [planowanie odzyskiwanie lasu usługi Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Pojedynczy kontroler domeny w jednej domenie
Witaj maszyny Wirtualnej można przywrócić (na przykład innych maszyn wirtualnych) z hello Azure portalu lub przy użyciu programu PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Wiele kontrolerów domeny w jednej domenie
Jeśli inne kontrolery domeny z tej samej domeny można połączyć się za pośrednictwem powitalne hello sieci, takich jak żadnej maszyny Wirtualnej można przywrócić hello kontrolera domeny. Jeśli jest hello ostatniego pozostałego kontrolera domeny w domenie hello lub przeprowadzane jest Odzyskiwanie w sieci izolowanej musi występować procedury odzyskiwania lasu.

### <a name="multiple-domains-in-one-forest"></a>Wiele domen w jednym lesie
Jeśli inne kontrolery domeny z tej samej domeny można połączyć się za pośrednictwem powitalne hello sieci, takich jak żadnej maszyny Wirtualnej można przywrócić hello kontrolera domeny. Jednak w innych przypadkach zaleca się przywrócenie lasu.

## <a name="restoring-vms-with-special-network-configurations"></a>Przywracanie maszyn wirtualnych z konfiguracjami sieci specjalne
Jest możliwe tooback zapasowej i przywracania maszyn wirtualnych z hello następujące konfiguracje sieciowe specjalnych. Jednak te konfiguracje wymagają niektórych szczególną uwagę podczas przechodzenia przez proces przywracania hello.

* Maszyn wirtualnych w usłudze równoważenia obciążenia (wewnętrznych i zewnętrznych)
* Maszyny wirtualne z wielu zastrzeżonych adresów IP
* Maszyny wirtualne z wieloma kartami sieciowymi

> [!IMPORTANT]
> Podczas tworzenia hello konfiguracji specjalnych sieci dla maszyn wirtualnych, należy użyć maszyn wirtualnych toocreate programu PowerShell z dysków hello przywrócona.
>
>

maszyny wirtualne hello Utwórz toofully po przywróceniu toodisk, wykonaj następujące kroki:

1. Przywróć hello dysków z używania magazynu usług odzyskiwania [środowiska PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Utwórz konfigurację maszyny Wirtualnej hello wymagane dla usługi równoważenia obciążenia / wielu kart/wiele zastrzeżonego adresu IP za pomocą hello poleceń cmdlet programu PowerShell i korzystać z niego toocreate hello wirtualna wymaganą konfiguracją.

   * Tworzenie maszyny Wirtualnej w usłudze w chmurze z [wewnętrznego modułu równoważenia obciążenia](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Tworzenie maszyny Wirtualnej tooconnect zbyt[internetowy modułu równoważenia obciążenia](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Tworzenie maszyny Wirtualnej z [wiele kart sieciowych](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Tworzenie maszyny Wirtualnej z [wielu zastrzeżone adresy IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Następne kroki
Teraz, można przywrócić maszyn wirtualnych, zobacz hello Rozwiązywanie problemów z artykułu, aby uzyskać informacje dotyczące typowych problemów z maszynami wirtualnymi. Również zapoznaj się z artykułem hello na zarządzanie zadaniami maszyn wirtualnych.

* [Rozwiązywanie problemów z błędami](backup-azure-vms-troubleshoot.md#restore)
* [Zarządzanie maszynami wirtualnymi](backup-azure-manage-vms.md)
