---
title: "Kopia zapasowa Azure: Przywracanie maszyn wirtualnych przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Przywracanie maszyny wirtualnej platformy Azure z punktu odzyskiwania za pomocą portalu Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "Przywracanie kopii zapasowej. jak przywrócić; punkt odzyskiwania;"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1fe2b94d462a30f09cb23ab905542aa121ba46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-portal-to-restore-virtual-machines"></a>Używanie witryny Azure Portal w celu przywrócenia maszyn wirtualnych
> [!div class="op_single_selector"]
> * [Przywracanie maszyn wirtualnych w portalu klasycznym](backup-azure-restore-vms.md)
> * [Przywracanie maszyn wirtualnych w portalu Azure](backup-azure-arm-restore-vms.md)
>
>

Ochrona danych za tworzenie migawek danych w określonych odstępach czasu. Te migawki są określane jako punkty odzyskiwania, i są przechowywane w Magazyny usług odzyskiwania. Jeśli lub gdy jest to niezbędne naprawić lub skompiluj ponownie Maszynę wirtualną, można przywrócić maszyny Wirtualnej z żadnym z punktów odzyskiwania zapisane. Podczas przywracania punkt odzyskiwania, można utworzyć nową maszynę Wirtualną, która odzwierciedla w momencie kopii zapasowej maszyny Wirtualnej, lub przywrócić dysków i szablon dołączonym dostosować przywróconą maszyną Wirtualną lub wykonaj odzyskiwanie poszczególnych plików. W tym artykule wyjaśniono, jak przywrócić Maszynę wirtualną do nowej maszyny Wirtualnej lub przywrócić wszystkie dyski kopii zapasowej. Odzyskiwanie poszczególnych plików, można znaleźć w temacie [odzyskać pliki z kopii zapasowej maszyny Wirtualnej Azure](backup-azure-restore-files-from-vm.md)

![3-Ways-Restore-from-VM-Backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem i pracą z zasobami: [Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Ten artykuł zawiera informacje i procedury dotyczące przywracania maszyn wirtualnych wdrożonych przy użyciu modelu Resource Manager.
>
>

Przywrócenie maszyny Wirtualnej lub wszystkich dysków z maszyny Wirtualnej kopii zapasowej obejmuje dwa kroki:

1. Wybierz punkt przywracania dla przywracania
2. Wybór przywracania wpisz — Tworzenie nowej maszyny Wirtualnej lub przywrócenia dysków i określ wymagane parametry. 

## <a name="select-restore-point-for-restore"></a>Wybierz punkt przywracania do przywrócenia
1. Zaloguj się do [portalu Azure](http://portal.azure.com/)
2. Polecenie Azure menu **Przeglądaj** i na liście usług, wpisz **usług odzyskiwania**. Na liście usług można dostosować do wpisany. Po wyświetleniu **Magazyny usług odzyskiwania**, zaznacz go.

    ![Otwórz magazyn usług odzyskiwania](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Zostanie wyświetlona lista magazynów w subskrypcji.

    ![Lista usług odzyskiwania magazynów](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. Z listy wybierz magazyn skojarzonych z maszyną Wirtualną, aby przywrócić. Po kliknięciu magazyn zostanie otwarty jego pulpitu nawigacyjnego.

    ![Lista usług odzyskiwania magazynów](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Teraz, gdy jesteś na pulpicie nawigacyjnym magazynu. Na **kopii zapasowej elementów** Kafelek, kliknij przycisk **maszyny wirtualne Azure** do wyświetlenia skojarzonego z magazynem maszyn wirtualnych.

    ![pulpitem nawigacyjnym magazynu](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    **Kopii zapasowej elementów** bloku otwiera i wyświetla listę maszyn wirtualnych platformy Azure.

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Z listy wybierz maszyny Wirtualnej, aby otworzyć pulpit nawigacyjny. Pulpit nawigacyjny maszyny Wirtualnej zostanie otwarty obszar monitorowanie, który zawiera kafelka punktów przywracania.

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. W menu nawigacyjnym maszyny Wirtualnej, kliknij **przywracania**

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    Zostanie otwarty blok przywracania.

    ![Blok przywracania](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Na **przywrócić** bloku, kliknij przycisk **punkt przywracania** otworzyć **przywracania wybierz punkt** bloku.

    ![Blok przywracania](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Domyślnie okno dialogowe wyświetla wszystkie punkty przywracania z ostatnich 30 dni. Użyj **filtru** zmienić zakres czasu punktów przywracania wyświetlane. Domyślnie są wyświetlane punkty przywracania na wszystkich spójności. Modyfikowanie **przywrócić wszystkie punkty** filtr, aby wybrać określone spójności punktów przywracania. Aby uzyskać więcej informacji na temat poszczególnych typów punktu przywracania, patrz wyjaśnienia [spójność danych](backup-azure-vms-introduction.md#data-consistency).  

   * **Przywróć spójności punktu** z tej listy wybierz:
     * Punkty przywracania na poziomie awarii
     * Punkty przywracania na poziomie aplikacji,
     * Punkty przywracania na poziomie systemu plików
     * Wszystkie punkty przywracania.  
8. Wybierz punkt przywracania, a następnie kliknij przycisk **OK**.

    ![Wybierz punkt przywracania](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    **Przywrócić** bloku pokazuje ustawiono punktu przywracania.

    ![punkt przywracania jest ustawiona.](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Na **przywrócić** bloku **przywracania** otwierany automatycznie po ustawieniu punktu przywracania.

## <a name="choosing-a-vm-restore-configuration"></a>Wybieranie konfiguracji przywracania maszyny Wirtualnej
Teraz, gdy wybrano punkt przywracania, wybierz konfigurację przywracania maszyny Wirtualnej. Opcje dotyczące konfigurowania przywróconą maszyną Wirtualną są do użycia: Azure portal lub programu PowerShell.

1. Jeśli użytkownik jest nie już istnieje, przejść do **przywrócić** bloku. Upewnij się, [został wybrany punkt przywracania](#select-restore-point-for-restore)i kliknij przycisk **przywracania** otworzyć **konfiguracji odzyskiwania** bloku.

    ![Kreator konfiguracji odzyskiwania jest ustawiona.](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Na **przywracania** bloku dostępne są dwie opcje:
   * Przywróć pełną maszyny wirtualnej
   * Przywracanie kopii zapasowych dysków

Portal zapewnia szybkie tworzenie opcję przywróconej maszyny wirtualnej. Jeśli chcesz dostosować konfigurację maszyny Wirtualnej lub nazwy zasobów utworzone jako część utworzyć nową opcję maszyny Wirtualnej, użyj programu PowerShell lub portalu do przywrócenia kopii zapasowej, dysków i dołącz je do wybranej konfiguracji maszyn wirtualnych, lub użyj szablonu, który jest dostarczany z za pomocą poleceń programu PowerShell re przechowywanie dysków, aby dostosować przywróconą maszyną Wirtualną. Zobacz [przywracanie maszyny Wirtualnej z konfiguracjami sieci specjalne](#restoring-vms-with-special-network-configurations) szczegółowe informacje dotyczące przywracania maszyny Wirtualnej, który ma wiele kart sieciowych lub w obszarze usługi równoważenia obciążenia. Jeśli maszyna wirtualna systemu Windows używa [Centrum licencjonowania](../virtual-machines/windows/hybrid-use-benefit-licensing.md), musisz przywrócić dysków i szablon programu PowerShell/określonych poniżej do tworzenia maszyny Wirtualnej i upewnij się, że podczas tworzenia maszyny Wirtualnej, aby wykorzystać zalety Centrum na Określ LicenseType jako "Windows_Server" Przywrócenie maszyny Wirtualnej. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Utwórz nową maszynę Wirtualną z punktu przywracania
Jeśli nie masz już istnieje, [wybierz punkt przywracania](#restoring-vms-with-special-network-configurations) przed przystąpieniem do tworzenia nowej maszyny Wirtualnej z punktu przywracania. Gdy punkt przywracania jest zaznaczone, na **przywracania** bloku, wprowadź lub wybierz wartości dla każdego z następujących pól:

* **Przywróć typu** — tworzenie maszyny wirtualnej.
* **Nazwa maszyny wirtualnej** — Podaj nazwę dla maszyny Wirtualnej. Nazwa musi być unikatowa dla grupy zasobów (na Maszynę wirtualną wdrożone usługi Resource Manager) lub usługi w chmurze (w przypadku klasycznych maszyn wirtualnych). Nie można zamienić maszyny wirtualnej, jeśli już istnieje w subskrypcji.
* **Grupa zasobów** — Użyj istniejącej grupy zasobów lub Utwórz nową. Jeśli przywracasz klasyczne maszyny Wirtualnej to pole służy do określania nazwy nowej usługi w chmurze. Jeśli tworzysz nową usługę chmury/grupy zasobów musi być globalnie unikatowe nazwy. Zazwyczaj nazwa usługi w chmurze jest skojarzone z adresem URL publicznych — na przykład: [cloudservice]. cloudapp.net. Jeśli spróbujesz użyć nazwy dla usługi chmury/grupy zasobów w chmurze, który został już użyty Azure przypisuje usługi chmury/grupy zasobów taką samą nazwę jak maszyny Wirtualnej. Azure Wyświetla usług chmury/grupy zasobów i maszyny wirtualne nie są skojarzone z grup koligacji. Aby uzyskać więcej informacji, zobacz [jak przeprowadzić migrację z grup koligacji do regionalną sieć wirtualną (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Sieć wirtualna** — wybierz sieć wirtualną (VNET), podczas tworzenia maszyny Wirtualnej. Pole zawiera wszystkie sieci wirtualne skojarzone z subskrypcją. Grupa zasobów maszyny wirtualnej jest wyświetlany w nawiasach.
* **Podsieci** — Jeśli sieć wirtualna ma podsieci, pierwszej podsieci jest domyślnie zaznaczona. Jeśli istnieją dodatkowe podsieci, wybierz odpowiednie podsieci.
* **Konto magazynu** — w tym menu znajdują się konta magazynu w tej samej lokalizacji co magazyn usług odzyskiwania. Konta magazynu, które są obszar strefowo nadmiarowy nie są obsługiwane. Jeśli nie ma żadnych kont magazynu z tej samej lokalizacji co magazyn usług odzyskiwania, należy go utworzyć przed uruchomieniem operacji przywracania. Typ replikacji konta magazynu jest wymieniony w nawiasach.

![Kreator konfiguracji przywracania jest ustawiona.](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Jeśli przywracasz maszyn wirtualnych wdrożonych przez Menedżera zasobów należy zidentyfikować sieć wirtualną (VNET). Sieć wirtualną (VNET) jest opcjonalny w przypadku klasycznych maszyn wirtualnych.
> 2. Jeśli przywracasz maszyny wirtualne z dyskami zarządzanych, upewnij się, że wybrane konto magazynu nie jest włączona dla magazynu usługi Encryption(SSE) w jego okres istnienia.
> 3. Oparte na typ magazynu wybrane konto magazynu (premium lub standard), wszystkie dyski przywrócić będzie premium lub dyski standardowe. Obecnie nie obsługujemy trybu mieszanego dysków podczas przywracania.  
>
>

Na **przywracania** bloku, kliknij przycisk **OK** aby ukończyć konfigurację przywracania. Na **przywrócić** bloku, kliknij przycisk **przywrócić** wyzwalanie operacji przywracania.

## <a name="restore-backed-up-disks"></a>Przywracanie kopii zapasowych dysków
Jeśli chcesz dostosować maszyny wirtualnej chcesz utworzyć z dysków niż co znajduje się w bloku konfiguracji przywracania, wybierz kopię zapasową **przywrócenia dysków** wartości dla **przywrócić typu**. Ten wybór poprosi o podanie konta magazynu, w którym dyski zapasowe są kopiowane do. Wybierając konto magazynu, wybierz konto, które współużytkują tej samej lokalizacji co magazyn usług odzyskiwania. Konta magazynu, które są obszar strefowo nadmiarowy nie są obsługiwane. Jeśli nie ma żadnych kont magazynu z tej samej lokalizacji co magazyn usług odzyskiwania, należy go utworzyć przed uruchomieniem operacji przywracania. Typ replikacji konta magazynu jest wymieniony w nawiasach.

Po zakończeniu operacji przywracania, można:
* [Użyj szablonu w celu dostosowania przywróconą maszyną Wirtualną.](#use-templates-to-customize-restore-vm)
* [Użyj dysków przywróconej do dołączenia do istniejącej maszyny wirtualnej](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Utwórz nową maszynę wirtualną przy użyciu programu PowerShell z przywróconą dysków.](./backup-azure-vms-automation.md#restore-an-azure-vm)

Na **przywracania** bloku, kliknij przycisk **OK** aby ukończyć konfigurację przywracania. Na **przywrócić** bloku, kliknij przycisk **przywrócić** wyzwalanie operacji przywracania.

![Konfiguracja odzyskiwania została zakończona](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-the-restore-operation"></a>Śledź operacji przywracania
Gdy użytkownik zainicjuje operacji przywracania, usługa Kopia zapasowa tworzy zadanie śledzenia operacji przywracania. Usługa kopii zapasowej tworzy także i tymczasowe wyświetlanie powiadomień w obszarze powiadomień z portalu. Jeśli powiadomienia nie są wyświetlane, należy zawsze kliknij ikonę powiadomienia, aby wyświetlić powiadomienia.

![Przywracanie wyzwalane](./media/backup-azure-arm-restore-vms/restore-notification.png)

Aby wyświetlić operacji podczas przetwarzania lub wyświetlić po jej zakończeniu, Otwórz listę zadań tworzenia kopii zapasowej.

1. Polecenie Azure menu **Przeglądaj** i na liście usług, wpisz **usług odzyskiwania**. Na liście usług można dostosować do wpisany. Po wyświetleniu **Magazyny usług odzyskiwania**, zaznacz go.

    ![Otwórz magazyn usług odzyskiwania](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    Zostanie wyświetlona lista magazynów w subskrypcji.

    ![Lista usług odzyskiwania magazynów](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. Z listy wybierz magazyn skojarzonych z maszyną Wirtualną można przywrócić. Po kliknięciu magazyn zostanie otwarty jego pulpitu nawigacyjnego.
3. Na pulpicie nawigacyjnym magazynu na **zadania tworzenia kopii zapasowej** Kafelek, kliknij przycisk **maszyny wirtualne Azure** Aby wyświetlić zadania związane z magazynem.

    ![pulpitem nawigacyjnym magazynu](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    **Zadania tworzenia kopii zapasowej** bloku otwiera i wyświetla listę zadań.

    ![Lista maszyn wirtualnych w magazynie](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-to-customize-restore-vm"></a>Dostosuj przywracanie maszyny wirtualnej za pomocą szablonów
Raz [zakończeniu operacji przywracania dysków](#Track-the-restore-operation), można użyć szablonu, który jest generowany w ramach operacji przywracania do tworzenia nowej maszyny Wirtualnej z konfiguracją inny niż konfiguracji kopii zapasowej lub dostosować nazwy zasobów utworzone jak utworzyć nową maszynę wirtualną z punktu przywracania. 

> [!NOTE]
> Szablony zostaną dodane jako część przywrócenia dysków dla punktów odzyskiwania po 1 marca 2017 r. Są one odpowiednie dla dysku niezaszyfrowane i niezarządzanych maszyn wirtualnych. Obsługa zaszyfrowane maszyn wirtualnych i zarządzania maszynami wirtualnymi dysku będzie dostępna w kolejnych wersjach. 
>
>

Aby uzyskać szablon wygenerowane jako część opcji dysków przywracania

1. Przejdź do przywrócenia odpowiadający zadania szczegóły zadania. 
2. Na ekranie szczegóły zadania przywracania, kliknij na *wdrażanie szablonu* przycisku do inicjowania wdrożenia szablonu. 

     ![Przywróć przechodzenia zadania](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
W bloku szablonu wdrażania niestandardowe wdrożenie przy użyciu szablonu wdrażania do [edytować i wdrożyć szablon](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) lub dołączyć więcej dostosowań przez [tworzenia szablonu](../azure-resource-manager/resource-group-authoring-templates.md) przed wdrożeniem. 

   ![Trwa ładowanie szablonu wdrożenia](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Po wprowadzeniu wymaganych wartości, należy zaakceptować *warunków i postanowień* i wybierz polecenie **zakupu**.

   ![Przesyłanie szablonu wdrożenia](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Wykonywane po przywróceniu kroki
* Korzystania z dystrybucji systemu Linux chmury inicjowania na podstawie takich jak Ubuntu, ze względów bezpieczeństwa hasła jest zablokowana post przywracania. Użyj rozszerzenia VMAccess przywróconej maszynę wirtualną i [resetowania hasła](../virtual-machines/linux/classic/reset-access.md). Zalecamy używanie kluczy SSH w tych dystrybucji w celu uniknięcia Resetowanie hasła post przywracania.
* Podczas tworzenia kopii zapasowej konfiguracji rozszerzenia zostanie zainstalowany, jednak nie jest włączony. Jeśli widzisz jakikolwiek problem, zainstaluj ponownie rozszerzenia. 
* Jeśli kopie zapasowe maszyna wirtualna ma statyczny adres IP, przywracania post przywróconą maszyną Wirtualną ma dynamicznego adresu IP, aby uniknąć konfliktów, podczas tworzenia przywracania maszyny Wirtualnej. Dowiedz się więcej na temat [dodać statycznego adresu IP do przywróconą maszyną Wirtualną.](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* Przywróconą maszyną Wirtualną nie będzie miał wartość dostępności. Zaleca się użycie opcji dysków przywracania i [Dodawanie zestawu dostępności](../virtual-machines/windows/tutorial-availability-sets.md) tworzenia maszyny Wirtualnej za pomocą programu PowerShell lub szablonów przy użyciu przywrócenie dysków. 


## <a name="backup-for-restored-vms"></a>Tworzenie kopii zapasowej dla przywróconej maszyny wirtualne
Jeśli maszyna wirtualna została przywrócona do tej samej grupie zasobów o takiej samej nazwie pierwotnie kopii zapasowej maszyny Wirtualnej, kopii zapasowych jest kontynuowane od przywracania post maszyny Wirtualnej. Jeśli masz przywrócić maszyny Wirtualnej do innej grupy zasobów lub określić inną nazwę dla przywróconej maszyny Wirtualnej, jest ona traktowana jako nowej maszyny Wirtualnej i potrzebne do konfiguracji kopii zapasowej dla przywróconą maszyną Wirtualną.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Przywracanie maszyny Wirtualnej podczas awarii centrum danych Azure
Kopia zapasowa Azure umożliwia przywracanie kopii zapasowej maszyn wirtualnych centrum danych sparowanego w przypadku danych podstawowych Centrum, gdy maszyny wirtualne są uruchomione po awarii środowiska i skonfigurować Magazyn kopii zapasowych się geograficznie nadmiarowego. W takich scenariuszach należy wybrać konto magazynu, który znajduje się w centrum danych sparowanego i resztę procesu przywracania pozostaje w tym samym. Kopia zapasowa Azure używa usługi obliczeniowe z geograficznie sparowanego do utworzenia przywróconej maszyny wirtualnej. Dowiedz się więcej o [odporności centrum danych Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Przywracanie maszyn wirtualnych z kontrolera domeny
Kopia zapasowa maszyn wirtualnych kontrolera domeny (DC) jest obsługiwany scenariusz w usłudze Kopia zapasowa Azure. Jednak należy uważać podczas procesu przywracania. Proces przywracania poprawne zależy od struktura domeny. W przypadku najprostszym pojedynczy kontroler domeny znajduje się w jednej domenie. Najczęściej w przypadku obciążeń produkcyjnych, będziesz mieć pojedynczą domenę z wielu kontrolerów domeny, prawdopodobnie z kilka kontrolerów domeny lokalnie. Ponadto może być lesie z wieloma domenami. 

Z perspektywy usługi Active Directory maszyny Wirtualnej Azure jest podobne do innych maszyn wirtualnych w nowoczesnych obsługiwanej funkcji hypervisor. Główna różnica z lokalnymi funkcji hypervisor jest dostępnej na platformie Azure jest konsoli maszyny Wirtualnej. Konsola jest wymagana dla niektórych scenariuszy, takich jak odzyskiwanie przy użyciu kopii zapasowej typu odzyskiwania systemu operacyjnego systemu od zera (BMR). Jednak przywrócenie maszyny Wirtualnej z magazynu kopii zapasowych nie zastępuje pełnego odzyskiwania systemu od ZERA. Active Directory przywracania trybu (DSRM) jest również dostępna, więc działało wszystkie scenariusze odzyskiwania usługi Active Directory. Aby uzyskać więcej informacji w tle, sprawdź, czy [kopia zapasowa i przywracanie zagadnienia dotyczące zwirtualizowanych kontrolerów domeny](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) i [planowanie odzyskiwanie lasu usługi Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Pojedynczy kontroler domeny w jednej domenie
Można przywrócić maszyny Wirtualnej (na przykład innych maszyn wirtualnych) z platformy Azure portalu lub przy użyciu programu PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Wiele kontrolerów domeny w jednej domenie
Jeśli inne kontrolery domeny w tej samej domeny, można połączyć się za pośrednictwem sieci, takich jak żadnej maszyny Wirtualnej można przywrócić kontrolera domeny. Jeśli jest ostatniego pozostałego kontrolera domeny w domenie lub odzyskiwania w sieci izolowanej jest wykonywane, musi następować procedury odzyskiwania lasu.

### <a name="multiple-domains-in-one-forest"></a>Wiele domen w jednym lesie
Jeśli inne kontrolery domeny w tej samej domeny, można połączyć się za pośrednictwem sieci, takich jak żadnej maszyny Wirtualnej można przywrócić kontrolera domeny. Jednak w innych przypadkach zaleca się przywrócenie lasu.

## <a name="restoring-vms-with-special-network-configurations"></a>Przywracanie maszyn wirtualnych z konfiguracjami sieci specjalne
Istnieje możliwość kopie zapasowe i przywracanie maszyn wirtualnych z następujących konfiguracji sieciowych. Jednak te konfiguracje wymagają niektórych szczególną uwagę podczas przechodzenia przez proces przywracania.

* Maszyn wirtualnych w usłudze równoważenia obciążenia (wewnętrznych i zewnętrznych)
* Maszyny wirtualne z wielu zastrzeżonych adresów IP
* Maszyny wirtualne z wieloma kartami sieciowymi

> [!IMPORTANT]
> Podczas tworzenia konfiguracji specjalnych sieci dla maszyn wirtualnych, należy tworzyć maszyny wirtualne z dysków przywrócić za pomocą programu PowerShell.
>
>

Po przywróceniu do dysku pełni odtworzyć maszyny wirtualnej, wykonaj następujące kroki:

1. Przywracanie dysków z używania magazynu usług odzyskiwania [środowiska PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Utwórz konfigurację maszyny Wirtualnej wymagana dla usługi równoważenia obciążenia / wielu kart interfejsu Sieciowego/wiele zastrzeżonego adresu IP za pomocą poleceń cmdlet programu PowerShell i użyj go w celu utworzenia maszyny Wirtualnej z wymaganą konfiguracji.

   * Tworzenie maszyny Wirtualnej w usłudze w chmurze z [wewnętrznego modułu równoważenia obciążenia](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Tworzenie maszyny Wirtualnej, aby nawiązać połączenie [internetowy modułu równoważenia obciążenia](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Tworzenie maszyny Wirtualnej z [wiele kart sieciowych](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Tworzenie maszyny Wirtualnej z [wielu zastrzeżone adresy IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Następne kroki
Teraz, można przywrócić maszyn wirtualnych, zobacz artykuł dotyczący rozwiązywania problemów, aby uzyskać informacje o typowych problemów z maszynami wirtualnymi. Ponadto zapoznaj się z artykułu na temat zarządzania zadania związane z maszyn wirtualnych.

* [Rozwiązywanie problemów z błędami](backup-azure-vms-troubleshoot.md#restore)
* [Zarządzanie maszynami wirtualnymi](backup-azure-manage-vms.md)
