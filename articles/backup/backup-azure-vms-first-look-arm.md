---
title: "Pierwsze spojrzenie: ochrona maszyn wirtualnych platformy Azure przy użyciu magazynu usługi Recovery Services | Microsoft Docs"
description: "Ochrona maszyn wirtualnych platformy Azure przy użyciu magazynu usługi Recovery Services. Użyj danych kopii zapasowych wdrożonych przez Menedżera zasobów maszyn wirtualnych, wdrożone w klasycznej maszyny wirtualne i Premium magazynu maszyn wirtualnych, szyfrowane maszyn wirtualnych, maszyny wirtualne na tooprotect dysków zarządzanych. Utwórz i zarejestruj magazyn usługi Recovery Services. Rejestruj maszyny wirtualne, twórz zasady i chroń maszyny wirtualne na platformie Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Wykonaj kopię zapasową Magazyny usług tooRecovery maszyn wirtualnych platformy Azure
> [!div class="op_single_selector"]
> * [Ochrona maszyn wirtualnych przy użyciu magazynu usługi Recovery Services](backup-azure-vms-first-look-arm.md)
> * [Ochrona maszyn wirtualnych przy użyciu magazynu kopii zapasowych](backup-azure-vms-first-look.md)
>
>

Ten samouczek przedstawia kroki hello tworzenia magazynu usług odzyskiwania i wykonywania kopii zapasowych maszyny wirtualnej platformy Azure (VM). Magazyny usługi Recovery Services chronią:

* Maszyny wirtualne wdrożone przez program Resource Manager platformy Azure
* Klasyczne maszyny wirtualne
* Maszyny wirtualne magazynu w warstwie Standard
* Maszyny wirtualne magazynu w warstwie Premium
* Maszyny wirtualne uruchomione na dyskach zarządzanych
* Maszyny wirtualne szyfrowane przy użyciu usługi Azure Disk Encryption (BEK i KEK)
* Spójna na poziomie aplikacji kopia zapasowa maszyn wirtualnych z systemem Windows wykonywana przy użyciu usługi VSS i kopia zapasowa maszyn wirtualnych z systemem Linux wykonywana przy użyciu niestandardowych skryptów uruchamianych przed utworzeniem i po utworzeniu migawki

Aby uzyskać więcej informacji o ochronie magazyn w warstwie Premium maszyn wirtualnych, zobacz artykuł hello [kopie zapasowe i przywracanie maszyn wirtualnych magazyn w warstwie Premium](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Dodatkowe informacje na temat obsługi maszyn wirtualnych dysku zarządzanego można znaleźć w sekcji [Tworzenie kopii zapasowej i przywracanie maszyn wirtualnych na dyskach zarządzanych](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). Aby uzyskać więcej informacji dotyczących struktury skryptów wykonywanych przed utworzeniem kopii zapasowej maszyny wirtualnej z systemem Linux i po utworzeniu kopii zapasowej, zobacz [Application consistent Linux VM backup using pre-script and post-script (Spójna na poziomie aplikacji kopia zapasowa maszyn wirtualnych z systemem Linux wykonywana przy użyciu skryptów uruchamianych przed utworzeniem i po utworzeniu kopii zapasowej)] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

toofind się więcej o tym, co może kopii zapasowej możesz i co nie można znaleźć [tutaj](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> Ten samouczek zakłada już maszyny Wirtualnej w Twojej subskrypcji platformy Azure i wykonano środki tooallow hello usługi tworzenia kopii zapasowej tooaccess hello maszyny Wirtualnej.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

W zależności od liczby hello maszyn wirtualnych ma tooprotect, możesz rozpocząć od różnych punktów początkowych. Tooback zapasową wielu maszyn wirtualnych w ramach jednej operacji, przejdź magazyn usług odzyskiwania toohello i [inicjować hello zadanie tworzenia kopii zapasowej z pulpitem nawigacyjnym magazynu hello](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Jeśli chcesz tooback jednej maszyny wirtualnej, można zainicjować hello zadanie tworzenia kopii zapasowej z bloku zarządzania maszyny Wirtualnej.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Konfigurowanie zadania tworzenia kopii zapasowej hello z bloku zarządzania maszyny Wirtualnej hello

Użyj poniższych kroków zadanie tworzenia kopii zapasowej hello tooconfigure z hello bloku zarządzania maszyny wirtualnej w portalu Azure hello hello. Te kroki należy stosować toohello maszyn wirtualnych w portalu klasycznym hello.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu Centrum powitania kliknij **więcej usług** i w oknie dialogowym hello filtru wpisz **maszyn wirtualnych**. Podczas wpisywania hello lista filtrów zasobów. Po wyświetleniu ciągu „Maszyny wirtualne” wybierz go.

  ![W menu Centrum kliknij okna dialogowego tekstu tooopen więcej usług, a następnie wpisz maszyny wirtualne](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  zostanie wyświetlona lista Hello maszyn wirtualnych (VM) w subskrypcji hello.

  ![zostanie wyświetlona lista Hello maszyn wirtualnych w hello subskrypcji.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Wybierz tooback maszyny Wirtualnej z listy hello się.

  ![zostanie wyświetlona lista Hello maszyn wirtualnych w hello subskrypcji.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Po wybraniu hello wirtualna hello listę maszyn wirtualnych przewiduje toohello po lewej stronie i blok zarządzania hello maszyny wirtualnej i hello maszyny wirtualnej z pulpitu nawigacyjnego, Otwórz. </br>
 ![Blok zarządzania maszyną wirtualną](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. Na powitania bloku zarządzania maszyny Wirtualnej, w hello **ustawienia** kliknij **kopii zapasowej**. </br>

  ![Opcja Kopia zapasowa w bloku zarządzania maszyną wirtualną](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  zostanie otwarty blok tworzenia kopii zapasowej Włącz Hello.

  ![Opcja Kopia zapasowa w bloku zarządzania maszyną wirtualną](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Witaj magazynu usług odzyskiwania, kliknij przycisk **wybierz istniejącą** i wybierz z listy rozwijanej hello hello magazynu.

  ![Kreator włączania kopii zapasowej](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Jeśli nie ma żadnego magazynu usług odzyskiwania lub ma toouse nowy magazyn, kliknij przycisk **Utwórz nowy** i podaj nazwę hello hello nowego magazynu. Nowy magazyn jest tworzony w hello same grupy zasobów i tej samej lokalizacji co hello maszyny wirtualnej. Jeśli chcesz toocreate magazynu usług odzyskiwania o różnych wartościach sekcji hello na temat zbyt[Tworzenie magazynu usług odzyskiwania](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. Szczegóły hello tooview hello zasad tworzenia kopii zapasowej, kliknij przycisk **kopii zapasowej zasad**.

  Witaj **kopii zapasowej zasad** bloku otwiera i zawiera szczegóły hello hello wybrane zasady. Jeśli istnieją inne zasady, użyj toochoose menu rozwijanego hello różnych zasad tworzenia kopii zapasowej. Jeśli chcesz toocreate zasady, wybierz opcję **Utwórz nowy** z menu rozwijanego hello. Instrukcje dotyczące definiowania zasad tworzenia kopii zapasowych można znaleźć w sekcji [Definiowanie zasad tworzenia kopii zapasowej](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). zasady tworzenia kopii zapasowej toohello toosave hello zmian i zwracany toohello Włącz bloku kopii zapasowej, kliknij przycisk **OK**.

  ![Wybór zasad tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. W bloku kopia zapasowa Włącz hello, kliknij **Włącz kopię zapasową** toodeploy hello zasad. Wdrażanie zasad hello kojarzy ją z hello magazynu i maszyn wirtualnych hello.

  ![Przycisk Włącz wykonywanie kopii zapasowej](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Możesz śledzić postępy konfiguracji hello za pośrednictwem hello powiadomienia, które są wyświetlane w portalu hello. Hello poniższy przykład pokazuje, że wdrożenie jest uruchomione.

  ![Powiadomienie dotyczące włączania kopii zapasowej](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Po zakończeniu postęp konfiguracji hello na powitania bloku zarządzania maszyny Wirtualnej, kliknij przycisk **kopii zapasowej** tooopen hello kopii zapasowej elementu bloku i widoku hello szczegóły.

  ![Widok elementu kopii zapasowej maszyny wirtualnej](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Dopiero po ukończeniu tworzenia początkowej kopii zapasowej hello, **ostatniej kopii zapasowej stanu** jest pokazywana jako **ostrzeżenie (początkowa kopia zapasowa oczekujących)**. występuje toosee gdy hello Następne zaplanowane zadanie tworzenia kopii zapasowej, w obszarze **kopii zapasowej zasad** kliknij nazwę hello hello zasad. Blok zasady tworzenia kopii zapasowej Hello otwiera i pokazuje czas hello hello zaplanowanego tworzenia kopii zapasowej.

10. toorun kopii zapasowej zadania i utworzyć hello początkowego punktu odzyskiwania, na powitania kopii zapasowej magazynu kliknij bloku **wykonaj kopię zapasową teraz**.

  ![kliknij kopię zapasową teraz toorun hello początkowa kopia zapasowa](./media/backup-azure-vms-first-look-arm/backup-now.png)

  zostanie otwarty blok Utwórz kopię zapasową teraz Hello.

  ![Pokazuje hello Utwórz kopię zapasową teraz bloku](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Na powitania Utwórz kopię zapasową teraz bloku, kliknij ikonę kalendarza hello, użyj hello kalendarza kontroli tooselect hello ostatni dzień tego punktu odzyskiwania jest zachowywana, a następnie kliknij przycisk **kopii zapasowej**.

  ![Ustaw hello ostatni dzień hello Utwórz kopię zapasową teraz punktu odzyskiwania są przechowywane.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Wdrożenie powiadomień informujący zostało wyzwolone zadanie tworzenia kopii zapasowej hello i monitorować postęp hello hello zadania na stronie zadań tworzenia kopii zapasowej hello.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Konfigurowanie zadania tworzenia kopii zapasowej hello z powitalne magazyn usług odzyskiwania
zadanie tworzenia kopii zapasowej hello tooconfigure, wykonaj hello następujące kroki.  

1. Utwórz magazyn usługi Recovery Services dla maszyny wirtualnej.
2. Użyj hello Azure tooselect portalu scenariusza, ustawić zasady tworzenia kopii zapasowej i zidentyfikuj tooprotect elementów.
3. Uruchom hello początkowa kopia zapasowa.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Tworzenie magazynu usługi Recovery Services dla maszyny wirtualnej
Magazyn usług odzyskiwania jest jednostka, która przechowuje wszystkie hello kopie zapasowe i punkty odzyskiwania, które zostały utworzone w czasie. Hello magazyn usług odzyskiwania zawiera również zasady tworzenia kopii zapasowej hello stosowane toohello chronionych maszyn wirtualnych.

> [!NOTE]
> Wykonywanie kopii zapasowych maszyn wirtualnych jest procesem lokalnym. Nie można utworzyć kopii zapasowych maszyn wirtualnych z jednej lokalizacji magazynu usług odzyskiwania tooa w innej lokalizacji. Tak dla każdej platformy Azure lokalizacji, która zawiera kopię zapasową toobe maszyn wirtualnych, co najmniej jeden magazyn usług odzyskiwania musi istnieć w tej lokalizacji.
>
>

toocreate magazynu usług odzyskiwania:

1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.
2. W menu Centrum powitania kliknij **więcej usług** w hello typu okna dialogowego filtru **usług odzyskiwania**. Podczas wpisywania hello lista filtrów zasobów. Gdy pojawi się magazyny usług odzyskiwania na liście hello, kliknij go.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Jeśli występują Magazyny usług odzyskiwania w ramach subskrypcji hello, magazynów hello są wyświetlane.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu. Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure. Wpisz nazwę o długości od 2 do 50 znaków. Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.

5. W hello **subskrypcji** Użyj hello menu rozwijanego toochoose hello subskrypcji platformy Azure. Jeśli używasz tylko jedną subskrypcję, wyświetlonym subskrypcji i toohello następny krok można pominąć. Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji. Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.

6. W hello **grupy zasobów** sekcji:

    * Wybierz **Utwórz nowy** Jeśli toocreate grupę zasobów.
    Lub
    * Wybierz **Użyj istniejącego** i kliknij przycisk hello menu rozwijanego toosee hello listę dostępnych grup zasobów.

  Aby uzyskać pełne informacje na temat grup zasobów, zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello. Ten wybór Określa region geograficzny hello wysyłania danych kopii zapasowych.

  > [!IMPORTANT]
  > Jeśli nie wiesz hello lokalizacji, w której istnieje maszyna wirtualna, Zamknij z okna dialogowego Tworzenie magazynu hello i przejdź toohello listę maszyn wirtualnych w portalu hello. Jeśli Twoje maszyny wirtualne znajdują się w wielu regionach, utwórz magazyn usługi Recovery Services w każdym regionie. Utwórz magazyn hello w miejscu pierwszego hello przed przejściem do następnej lokalizacji toohello. Brak kont magazynu nie konieczności toospecify hello używane dane kopii zapasowej hello toostore — Witaj magazyn usług odzyskiwania i hello usługi Kopia zapasowa Azure automatycznie obsługiwać hello magazynu.
  >

8. U dołu hello blok magazyn usług odzyskiwania hello, kliknij przycisk **Utwórz**.

    Może upłynąć kilka minut hello toobe utworzony magazyn usług odzyskiwania. Monitor stanu hello powiadomienia w górnym obszarze po prawej stronie powitania hello portalu. Po utworzeniu magazynu zostanie wyświetlony hello listę magazynów usług odzyskiwania. Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.

    ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Przeanalizowanie magazynu na liście hello magazynów usług odzyskiwania jest nadmiarowość magazynu hello tooset gotowe.

Po utworzeniu magazynu, Dowiedz się, jak tooset hello replikacji magazynu.

### <a name="set-storage-replication"></a>Konfigurowanie replikacji magazynu
opcji replikacji magazynu Hello umożliwia toochoose między magazynu geograficznie nadmiarowego i lokalnie nadmiarowego magazynu. Domyślnie magazyn jest nadmiarowy geograficznie. Jeśli powitalne magazyn usług odzyskiwania jest Twoja podstawowa kopia zapasowa, należy pozostawić hello magazynu replikacji opcji set toogeo nadmiarowego magazynu. Wybierz magazyn lokalnie nadmiarowy, jeśli chcesz skorzystać z tańszej, ale mniej trwałej opcji. Przeczytaj więcej na temat [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [magazyn lokalnie nadmiarowy](../storage/common/storage-redundancy.md#locally-redundant-storage) opcje magazynu w hello [Omówienie replikacji usługi Azure Storage](../storage/common/storage-redundancy.md).

ustawienia replikacji magazynu hello tooedit:

1. Z hello **Magazyny usług odzyskiwania** bloku, wybierz hello nowy magazyn.

  ![Wybierz nowy magazyn hello z listy hello magazynu usług odzyskiwania](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Po wybraniu magazynu hello hello blok ustawień (*mającego nazwę magazynu hello u góry hello*) i hello magazynu szczegóły blok otwarte.

  ![Widok konfiguracji magazynu hello nowy magazyn](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. W bloku ustawienia hello nowy magazyn, użyj tooscroll pionowy slajdów hello dół toohello sekcji Zarządzaj, a następnie kliknij przycisk **infrastruktura kopii zapasowej**.
    zostanie otwarty blok infrastruktura kopii zapasowej Hello.
3. W bloku infrastruktura kopii zapasowej powitania kliknij **konfiguracji kopii zapasowej** tooopen hello **konfiguracji kopii zapasowej** bloku.

    ![Ustaw hello konfigurację magazynu dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Wybierz hello odpowiednią opcję replikacji dla magazynu.

    ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Domyślnie magazyn jest nadmiarowy geograficznie. Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych nadal toouse **geograficznie nadmiarowego**. Jeśli nie używasz Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, należy wybrać **magazyn lokalnie nadmiarowy**, co zmniejsza koszty usługi Azure storage hello. Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Wybierz cel kopii zapasowej, ustawienie zasad i zdefiniowanie tooprotect elementów
Przed zarejestrowaniem maszyny Wirtualnej w magazynie, uruchom tooensure procesu odnajdywania hello rozpoznaniem żadnych nowych maszyn wirtualnych, które zostały dodane toohello subskrypcji. kwerendy procesu Hello Azure hello listę maszyn wirtualnych w subskrypcji hello, wraz z dodatkowymi informacjami, takie jak nazwa usługi w chmurze hello i hello regionu. W hello portalu Azure scenariusz odnosi się do magazynu usług odzyskiwania hello ma tooput toowhat. Zasady są harmonogram hello kiedy i jak często są pobierane punktów odzyskiwania. Zasady obejmują również zakres przechowywania hello hello punktów odzyskiwania.

1. Jeśli masz już otworzyć magazyn usług odzyskiwania, należy kontynuować toostep 2. W przeciwnym razie w menu Centrum powitania kliknij **więcej usług** i hello listy zasobów, wpisz **usług odzyskiwania** i kliknij przycisk **Magazyny usług odzyskiwania**.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    zostanie wyświetlona lista Hello Magazyny usług odzyskiwania.

    ![Lista magazynów widoku hello usług odzyskiwania](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Z listy hello Magazyny usług odzyskiwania wybierz tooopen magazynu jego pulpitu nawigacyjnego.

     ![Otwarcie bloku magazynu](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. W menu nawigacyjnym magazynu hello, kliknij polecenie **kopii zapasowej** tooopen hello kopii zapasowej bloku.

    ![Otwarcie bloku Kopia zapasowa](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Otwórz Hello tworzenia kopii zapasowej i cel kopii zapasowej blokach.

    ![Otwarcie bloku scenariusza](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. W bloku celu kopii zapasowej hello z hello **gdzie działa Twoje obciążenie** menu rozwijanego wybierz pozycję Azure. Z hello **co chcesz toobackup** listy rozwijanej, wybierz maszynę wirtualną, a następnie kliknij przycisk **OK**.

    Te akcje Zarejestruj magazynie hello hello rozszerzenia maszyny Wirtualnej. Hello zamyka bloku celu kopii zapasowej i hello **kopii zapasowej zasad** zostanie otwarty blok.

    ![Otwarcie bloku scenariusza](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. W bloku zasad tworzenia kopii zapasowej hello wybierz zasady tworzenia kopii zapasowej hello ma tooapply toohello magazynu.

    ![Wybór zasad tworzenia kopii zapasowej](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Szczegóły Hello hello domyślne zasady są wyświetlane w menu rozwijanym hello. Jeśli chcesz toocreate zasady, wybierz opcję **Utwórz nowy** z menu rozwijanego hello. Instrukcje dotyczące definiowania zasad tworzenia kopii zapasowych można znaleźć w sekcji [Definiowanie zasad tworzenia kopii zapasowej](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Kliknij przycisk **OK** tooassociate hello zasad tworzenia kopii zapasowej w magazynie hello.

    Witaj zamknięciu bloku zasady tworzenia kopii zapasowej i hello **wybierz maszyny wirtualne** zostanie otwarty blok.
5. W hello **wybierz maszyny wirtualne** bloku, wybierz hello tooassociate maszyn wirtualnych z hello określone zasady i kliknij przycisk **OK**.

    ![Wybieranie obciążenia](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    maszyny wirtualnej wybrany Hello jest weryfikowana. Jeśli nie widzisz hello wirtualnej maszyny, które powinny toosee, sprawdź, czy istnieją one w hello tej samej lokalizacji platformy Azure, jako magazyn usług odzyskiwania hello. na pulpicie nawigacyjnym magazynu hello wyświetlana jest lokalizacja Hello powitalne magazyn usług odzyskiwania.

6. Teraz, gdy wszystkie ustawienia magazynu hello został zdefiniowany w bloku kopia zapasowa hello, kliknij przycisk **włączenia kopii zapasowej** toodeploy hello magazynu toohello zasad i hello maszyn wirtualnych. Wdrażanie zasad tworzenia kopii zapasowej hello nie tworzy hello początkowego punktu odzyskiwania dla maszyny wirtualnej hello.

    ![Włączenie kopii zapasowej](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Po pomyślnym włączeniu kopii zapasowej hello zasad tworzenia kopii zapasowej będą wykonywane zgodnie z harmonogramem. Jednak kontynuować tooinitiate hello pierwszego zadania tworzenia kopii zapasowej.

## <a name="initial-backup"></a>Początkowa kopia zapasowa
Po wdrożeniu zasad tworzenia kopii zapasowej na maszynie wirtualnej hello, który nie oznacza to, hello danych wykonano kopię zapasową. Domyślnie pierwszą zaplanowaną kopią zapasową hello (zgodnie z definicją w zasadach tworzenia kopii zapasowej hello) jest hello początkowa kopia zapasowa. Dopóki nie wystąpi hello początkowa kopia zapasowa, hello stan ostatniej kopii zapasowej na powitania **zadania tworzenia kopii zapasowej** bloku jest pokazywana jako **ostrzeżenie (początkowa kopia zapasowa oczekujących)**.

![Oczekiwanie na kopię zapasową](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

O ile nie przypada tworzenia początkowej kopii zapasowej toobegin wkrótce, zalecane jest uruchomienie **wykonaj kopię zapasową teraz**.

toorun hello początkowej zadanie tworzenia kopii zapasowej:

1. Na pulpicie nawigacyjnym magazynu hello, kliknij przycisk numer hello pod **kopii zapasowej elementów**, lub kliknij przycisk hello **kopii zapasowej elementów** kafelka. <br/>
  ![Ikona Ustawienia](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Witaj **kopii zapasowej elementów** zostanie otwarty blok.

  ![Tworzenie kopii zapasowych elementów](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Na powitania **kopii zapasowej elementów** bloku, wybierz hello elementu.

  ![Ikona Ustawienia](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Witaj **kopii zapasowej elementów** listy zostanie otwarta. <br/>

  ![Zadanie tworzenia kopii zapasowej zostało wyzwolone](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Na powitania **kopii zapasowej elementów** kliknij wielokropek hello **...**  menu kontekstowe hello tooopen.

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu.png)

  zostanie wyświetlone menu kontekstowe Hello.

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. W menu kontekstowym hello, kliknij przycisk **wykonaj kopię zapasową teraz**.

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  zostanie otwarty blok Utwórz kopię zapasową teraz Hello.

  ![Pokazuje hello Utwórz kopię zapasową teraz bloku](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Na powitania Utwórz kopię zapasową teraz bloku, kliknij ikonę kalendarza hello, użyj hello kalendarza kontroli tooselect hello ostatni dzień tego punktu odzyskiwania jest zachowywana, a następnie kliknij przycisk **kopii zapasowej**.

  ![Ustaw hello ostatni dzień hello Utwórz kopię zapasową teraz punktu odzyskiwania są przechowywane.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Wdrożenie powiadomień informujący zostało wyzwolone zadanie tworzenia kopii zapasowej hello i monitorować postęp hello hello zadania na stronie zadań tworzenia kopii zapasowej hello. W zależności od rozmiaru hello maszyny Wirtualnej tworzenie początkowej kopii zapasowej hello może chwilę potrwać.

6. tooview lub Śledź stan hello hello tworzenia początkowej kopii zapasowej, na pulpicie nawigacyjnym magazynu hello, na powitania **zadania tworzenia kopii zapasowej** kliknij Kafelek **w toku**.

  ![Kafelek Zadania tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  zostanie otwarty blok zadania tworzenia kopii zapasowej Hello.

  ![Kafelek Zadania tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  W hello **kopii zapasowej zadania** bloku widać hello stan wszystkich zadań. Sprawdź, czy hello kopii zapasowej dla maszyny Wirtualnej jest nadal w toku, czy zakończyło się. Po zakończeniu zadania tworzenia kopii zapasowej stanu hello jest *Ukończono*.

  > [!NOTE]
  > W ramach operacji tworzenia kopii zapasowej hello hello usługi Kopia zapasowa Azure problemy z rozszerzeniem kopii zapasowej polecenia toohello w każdej tooflush maszyna wirtualna, wszystkie zapisuje i migawki spójne.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Zainstaluj hello agenta maszyny Wirtualnej na maszynie wirtualnej hello
Te informacje są dostarczane w przypadku, gdy są wymagane. Witaj Agent maszyny Wirtualnej musi być zainstalowany na powitania maszyny wirtualnej platformy Azure dla hello kopii zapasowej rozszerzenia toowork. Jednak jeśli maszyna wirtualna została utworzona z hello galerii Azure, następnie hello agenta maszyny Wirtualnej jest już obecny w maszynie wirtualnej hello. Maszyny wirtualne, które są migrowane z lokalnymi centrami danych, czy nie hello agenta maszyny Wirtualnej zainstalowano. W takim przypadku hello agenta maszyny Wirtualnej musi toobe zainstalowane. Jeśli masz problemy z tworzenia kopii zapasowej hello maszyny Wirtualnej platformy Azure, sprawdź, czy Agent maszyny Wirtualnej hello jest poprawnie zainstalowany na maszynie wirtualnej hello (zobacz hello w poniższej tabeli). W przypadku utworzenia niestandardowego maszyny Wirtualnej, [zapewnienia hello **hello Zainstaluj agenta maszyny Wirtualnej** zaznaczone jest pole wyboru](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) przed udostępnieniu hello maszyny wirtualnej.

Dowiedz się więcej o hello [agenta maszyny Wirtualnej](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) i [jak tooinstall go](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

w poniższej tabeli Hello udostępnia dodatkowe informacje o hello VM Agent dla systemu Windows i maszyn wirtualnych systemu Linux.

| **Operacja** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalowanie hello agenta maszyny Wirtualnej |<li>Pobierz i zainstaluj hello [pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Potrzebujesz instalacji hello toocomplete uprawnienia administratora. <li>[Aktualizuj właściwości maszyny Wirtualnej hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, który hello agent jest zainstalowany. |<li> Zainstaluj najnowsze hello [agenta systemu Linux](https://github.com/Azure/WALinuxAgent) z usługi GitHub. Potrzebujesz instalacji hello toocomplete uprawnienia administratora. <li> [Aktualizuj właściwości maszyny Wirtualnej hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate, który hello agent jest zainstalowany. |
| Aktualizowanie hello agenta maszyny Wirtualnej |Aktualizowanie hello agenta maszyny Wirtualnej jest tak proste, jak ponowne zainstalowanie hello [plików binarnych agenta maszyny Wirtualnej](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Upewnij się, że żadna operacja tworzenia kopii zapasowej działa podczas aktualizowania hello agenta maszyny Wirtualnej. |Wykonaj instrukcje hello [aktualizowanie hello agenta maszyny Wirtualnej systemu Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Upewnij się, że podczas powitalne agenta maszyny Wirtualnej jest aktualizowana działa żadna operacja tworzenia kopii zapasowej. |
| Sprawdzanie poprawności instalacji agenta maszyny Wirtualnej hello |<li>Przejdź toohello *C:\WindowsAzure\Packages* folderu w hello maszyny Wirtualnej platformy Azure. <li>Powinien znajdować się plik WaAppAgent.exe hello jest obecny.<li> Kliknij prawym przyciskiem myszy plik hello znajduje się zbyt**właściwości**, a następnie wybierz hello **szczegóły** kartę hello wersji produktu pole powinno być 2.6.1198.718 lub nowszej. |Nie dotyczy |

### <a name="backup-extension"></a>Rozszerzenie kopii zapasowej
Raz powitalne Agent maszyny Wirtualnej jest zainstalowany na maszynie wirtualnej hello hello usługi Kopia zapasowa Azure instaluje hello zapasowy numer wewnętrzny toohello agenta maszyny Wirtualnej. Witaj usługi Kopia zapasowa Azure bezproblemowo uaktualniania i poprawek hello zapasowy numer wewnętrzny bez interwencji użytkownika dodatkowe.

Usługa Kopia zapasowa Hello instaluje hello zapasowy numer wewnętrzny, nawet wtedy, gdy hello maszyna wirtualna nie jest uruchomiona. Uruchomionych maszynach wirtualnych zapewnia największe prawdopodobieństwo hello pobieranie punktów odzyskiwania zapewniających spójność aplikacji. Jednak hello usługi Kopia zapasowa Azure nadal tooback się hello maszyny Wirtualnej, nawet jeśli jest wyłączony i nie można zainstalować rozszerzenia hello. Ten typ kopii zapasowej nosi nazwę trybu Offline maszyny Wirtualnej, a punkt odzyskiwania hello jest *awaria spójne*.

## <a name="troubleshooting-information"></a>Informacje dotyczące rozwiązywania problemów
Jeśli masz problemy z wykonywanie niektórych zadań hello w tym artykule, należy skontaktować się [wskazówki rozwiązywania problemów](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Cennik
Hello koszt tworzenia kopii zapasowych maszyn wirtualnych platformy Azure jest oparta na powitania liczbę wystąpień chronionych. Definicję chronionego wystąpienia można znaleźć w części [Co to jest chronione wystąpienie](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Przykład obliczanie kosztu hello wykonywanie kopii zapasowej maszyny wirtualnej, zobacz [jak wystąpienia chronione są obliczane](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Zobacz hello cennikiem usługi Kopia zapasowa Azure strony informacji o [cennikiem usługi Kopia zapasowa](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>Pytania?
Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).
