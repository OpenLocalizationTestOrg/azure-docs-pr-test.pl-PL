---
title: "Pierwsze spojrzenie: ochrona maszyn wirtualnych platformy Azure przy użyciu magazynu usługi Recovery Services | Microsoft Docs"
description: "Ochrona maszyn wirtualnych platformy Azure przy użyciu magazynu usługi Recovery Services. Tworzenie kopii zapasowych maszyn wirtualnych wdrożonych przez usługę Resource Manager, maszyn wirtualnych wdrożonych klasycznie i maszyn wirtualnych usługi Premium Storage, szyfrowanych maszyn wirtualnych oraz maszyn wirtualnych na dyskach zarządzanych pozwala na ochronę danych. Utwórz i zarejestruj magazyn usługi Recovery Services. Rejestruj maszyny wirtualne, twórz zasady i chroń maszyny wirtualne na platformie Azure."
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
ms.date: 09/04/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 639f008eea61b973b9d32dc734d42d5c4e93e924
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="back-up-azure-virtual-machines-to-recovery-services-vaults"></a>Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure w magazynach usługi Recovery Services
> [!div class="op_single_selector"]
> * [Ochrona maszyn wirtualnych przy użyciu magazynu usługi Recovery Services](backup-azure-vms-first-look-arm.md)
> * [Ochrona maszyn wirtualnych przy użyciu magazynu kopii zapasowych](backup-azure-vms-first-look.md)
>
>

Ten samouczek zawiera kroki prowadzące do utworzenia magazynu usługi Recovery Services oraz utworzenia kopii zapasowej maszyny wirtualnej Azure. Magazyny usługi Recovery Services chronią:

* Maszyny wirtualne wdrożone przez program Resource Manager platformy Azure
* Klasyczne maszyny wirtualne
* Maszyny wirtualne magazynu w warstwie Standard
* Maszyny wirtualne magazynu w warstwie Premium
* Maszyny wirtualne uruchomione na dyskach zarządzanych
* Maszyny wirtualne szyfrowane przy użyciu usługi Azure Disk Encryption
* Spójna na poziomie aplikacji kopia zapasowa maszyn wirtualnych z systemem Windows wykonywana przy użyciu usługi VSS i kopia zapasowa maszyn wirtualnych z systemem Linux wykonywana przy użyciu niestandardowych skryptów uruchamianych przed utworzeniem i po utworzeniu migawki

Dodatkowe informacje na temat ochrony maszyn wirtualnych usługi Premium Storage można znaleźć w artykule [Tworzenie kopii zapasowej i przywracanie maszyn wirtualnych usługi Premium Storage](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Dodatkowe informacje na temat obsługi maszyn wirtualnych dysku zarządzanego można znaleźć w sekcji [Tworzenie kopii zapasowej i przywracanie maszyn wirtualnych na dyskach zarządzanych](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). Aby uzyskać więcej informacji dotyczących struktury skryptów wykonywanych przed utworzeniem kopii zapasowej maszyny wirtualnej z systemem Linux i po utworzeniu kopii zapasowej, zobacz [Application consistent Linux VM backup using pre-script and post-script (Spójna na poziomie aplikacji kopia zapasowa maszyn wirtualnych z systemem Linux wykonywana przy użyciu skryptów uruchamianych przed utworzeniem i po utworzeniu kopii zapasowej)] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

Więcej informacji na temat zasobów, których kopie zapasowe można wykonywać, możesz znaleźć [tutaj](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> W tym samouczku zakładamy, że masz już maszynę wirtualną w subskrypcji platformy Azure i zostały podjęte działania umożliwiające usłudze tworzenia kopii zapasowej dostęp do maszyny wirtualnej.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

W zależności od liczby maszyn wirtualnych, które chcesz chronić, możesz rozpocząć od różnych punktów początkowych. Jeśli chcesz utworzyć kopię zapasową wielu maszyn wirtualnych w ramach jednej operacji, przejdź do magazynu usługi Recovery Services i [zainicjuj zadanie tworzenia kopii zapasowej z poziomu pulpitu nawigacyjnego magazynu](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Jeśli chcesz utworzyć kopię zapasową jednej maszyny wirtualnej, możesz zainicjować zadanie tworzenia kopii zapasowej z bloku zarządzania maszyną wirtualną.

## <a name="configure-the-backup-job-from-the-vm-management-blade"></a>Konfigurowanie zadania tworzenia kopii zapasowej z bloku zarządzania maszyną wirtualną

Wykonaj poniższe kroki w celu skonfigurowania zadania tworzenia kopii zapasowej z bloku zarządzania maszyną wirtualną w witrynie Azure Portal. Te kroki nie dotyczą maszyn wirtualnych w portalu klasycznym.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).
2. W menu Centrum kliknij opcję **Więcej usług** i w oknie dialogowym filtrowania wpisz ciąg **Maszyny wirtualne**. Podczas pisania odbywa się filtrowanie listy zasobów. Po wyświetleniu ciągu „Maszyny wirtualne” wybierz go.

  ![W menu Centrum kliknij pozycję Więcej usług, aby otworzyć okno dialogowe tekstu, a następnie wpisz ciąg „Maszyny wirtualne”](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  Zostanie wyświetlona lista maszyn wirtualnych w subskrypcji.

  ![Zostanie wyświetlona lista maszyn wirtualnych w subskrypcji.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Z listy wybierz maszynę wirtualną do utworzenia kopii zapasowej.

  ![Zostanie wyświetlona lista maszyn wirtualnych w subskrypcji.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Wybranie maszyny wirtualnej spowoduje przesunięcie listy maszyn wirtualnych w lewo oraz otwarcie bloku zarządzania maszyną wirtualną i pulpitu nawigacyjnego. </br>
 ![Blok zarządzania maszyną wirtualną](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. W bloku zarządzania maszyną wirtualną w sekcji **Ustawienia** kliknij pozycję **Kopia zapasowa**. </br>

  ![Opcja Kopia zapasowa w bloku zarządzania maszyną wirtualną](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  Spowoduje to otwarcie bloku włączania kopii zapasowej.

  ![Opcja Kopia zapasowa w bloku zarządzania maszyną wirtualną](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. W magazynie usługi Recovery Services kliknij pozycję **Wybierz istniejący** i wybierz magazyn z listy rozwijanej.

  ![Kreator włączania kopii zapasowej](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Jeśli nie ma magazynów usługi Recovery Services lub chcesz użyć nowego magazynu, kliknij pozycję **Utwórz nowy** i podaj nazwę nowego magazynu. Nowy magazyn zostanie utworzony w tej samej lokalizacji i tej samej grupie zasobów, co maszyna wirtualna. Jeśli chcesz utworzyć magazyn usługi Recovery Services przy użyciu różnych wartości, zobacz sekcję dotyczącą [tworzenia magazynu usługi Recovery Services](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. Aby wyświetlić szczegóły zasad tworzenia kopii zapasowej, kliknij pozycję **Zasady tworzenia kopii zapasowej**.

  Zostanie otwarty blok **Zasady tworzenia kopii zapasowej** zawierający szczegóły wybranych zasad. Jeśli istnieją inne zasady, użyj menu rozwijanego, aby wybrać inne zasady tworzenia kopii zapasowej. Aby utworzyć zasady, wybierz opcję **Utwórz nowy** z menu rozwijanego. Instrukcje dotyczące definiowania zasad tworzenia kopii zapasowych można znaleźć w sekcji [Definiowanie zasad tworzenia kopii zapasowej](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). Aby zapisać zmiany zasad tworzenia kopii zapasowej i wrócić do bloku Włącz kopie zapasowe, kliknij przycisk **OK**.

  ![Wybór zasad tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. W bloku włączania kopii zapasowej kliknij przycisk **Włącz wykonywanie kopii zapasowej**, aby wdrożyć zasady. Wdrożenie zasad spowoduje skojarzenie ich z magazynem i maszynami wirtualnymi.

  ![Przycisk Włącz wykonywanie kopii zapasowej](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Możesz śledzić postęp konfiguracji za pośrednictwem powiadomień wyświetlanych w portalu. W poniższym przykładzie pokazano, że rozpoczęto wdrażanie.

  ![Powiadomienie dotyczące włączania kopii zapasowej](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Po zakończeniu konfiguracji w bloku zarządzania maszyną wirtualną kliknij pozycję **Kopia zapasowa**, aby otworzyć blok elementu kopii zapasowej i wyświetlić szczegóły.

  ![Widok elementu kopii zapasowej maszyny wirtualnej](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Do czasu zakończenia procesu tworzenia początkowej kopii zapasowej w polu **Stan ostatniej kopii zapasowej** wyświetlany jest komunikat **Ostrzeżenie (oczekiwanie na początkową kopię zapasową)**. Aby sprawdzić, na kiedy zaplanowano kolejne zadania tworzenia kopii zapasowej, w obszarze **Zasady tworzenia kopii zapasowej** kliknij nazwę zasad. Zostanie otwarty blok zasad tworzenia kopii zapasowej zawierający informacje o czasie zaplanowanego utworzenia kopii zapasowej.

10. Aby uruchomić zadanie tworzenia kopii zapasowej i utworzyć początkowy punkt odzyskiwania, w bloku magazynu kopii zapasowych kliknij pozycję **Utwórz teraz kopię zapasową**.

  ![kliknięcie pozycji Utwórz teraz kopię zapasową w celu uruchomienia tworzenia początkowej kopii zapasowej](./media/backup-azure-vms-first-look-arm/backup-now.png)

  Zostanie otwarty blok Utwórz teraz kopię zapasową.

  ![wyświetlanie bloku Utwórz teraz kopię zapasową](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. W bloku Utwórz teraz kopię zapasową kliknij ikonę kalendarza, wybierz ostatni dzień okresu zachowywania tego punktu odzyskiwania przy użyciu kontrolki kalendarza, a następnie kliknij pozycję **Kopia zapasowa**.

  ![ustawianie ostatniego dnia okresu zachowywania punktu odzyskiwania Utwórz teraz punkt odzyskiwania](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Powiadomienia dotyczące wdrożenia informują o wyzwoleniu zadania tworzenia kopii zapasowej, dzięki czemu możesz monitorować postęp zadania na stronie zadań tworzenia kopii zapasowych.

## <a name="configure-the-backup-job-from-the-recovery-services-vault"></a>Konfigurowanie zadania tworzenia kopii zapasowej z poziomu magazynu usługi Recovery Services
Aby skonfigurować zadanie tworzenia kopii zapasowej, wykonaj poniższe kroki.  

1. Utwórz magazyn usługi Recovery Services dla maszyny wirtualnej.
2. W witrynie Azure Portal wybierz scenariusz, ustaw zasady tworzenia kopii zapasowej i zidentyfikuj elementy do objęcia ochroną.
3. Uruchom proces tworzenia początkowej kopii zapasowej.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Tworzenie magazynu usługi Recovery Services dla maszyny wirtualnej
Magazyn Usług odzyskiwania jest jednostką, która przechowuje wszystkie utworzone dotychczas kopie zapasowe i punkty odzyskiwania. Magazyn Usług odzyskiwania zawiera także zasady tworzenia kopii zapasowej stosowane do chronionych maszyn wirtualnych.

> [!NOTE]
> Wykonywanie kopii zapasowych maszyn wirtualnych jest procesem lokalnym. Nie można utworzyć kopii maszyn wirtualnych z jednej lokalizacji w magazynie Usług odzyskiwania w innej lokalizacji. Z tego powodu w każdej lokalizacji platformy Azure zawierającej maszyny wirtualne, których kopie zapasowe mają być wykonywane, musi istnieć co najmniej jeden magazyn Usług odzyskiwania.
>
>

Aby utworzyć magazyn Usług odzyskiwania:

1. Jeśli nie zostało to jeszcze zrobione, zaloguj się do witryny [Azure Portal](https://portal.azure.com/) przy użyciu subskrypcji platformy Azure.
2. W menu Centrum kliknij opcję **Więcej usług** i w oknie dialogowym filtrowania wpisz ciąg **Recovery Services**. Podczas pisania odbywa się filtrowanie listy zasobów. Po wyświetleniu pozycji Magazyny usługi Recovery Services kliknij ją.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Jeśli w ramach subskrypcji istnieją magazyny usługi Recovery Services, zostaną one wyświetlone.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. W menu **Magazyny usługi Recovery Services** kliknij pozycję **Dodaj**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Zostanie otwarty blok magazynu Usług odzyskiwania i pojawi się monit o podanie wartości w polach **Nazwa**, **Subskrypcja**, **Grupa zasobów** i **Lokalizacja**.

    ![Tworzenie magazynu usługi Recovery Services — krok 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. W polu **Nazwa** wprowadź przyjazną nazwę identyfikującą magazyn. Nazwa musi być unikalna w tej subskrypcji platformy Azure. Wpisz nazwę o długości od 2 do 50 znaków. Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.

5. W sekcji **Subskrypcja** użyj menu rozwijanego, aby wybrać subskrypcję platformy Azure. Jeśli używasz tylko jednej subskrypcji, zostanie ona wyświetlona i możesz przejść do następnego kroku. Jeśli nie masz pewności, której subskrypcji użyć, wybierz domyślną (lub sugerowaną). Większa liczba opcji do wyboru jest dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.

6. W sekcji **Grupa zasobów**:

    * wybierz pozycję **Utwórz nową**, jeśli chcesz utworzyć grupę zasobów.
    Lub
    * wybierz pozycję **Użyj istniejącej** i kliknij menu rozwijane, aby wyświetlić listę dostępnych grup zasobów.

  Pełne informacje na temat grup zasobów można znaleźć w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Kliknij pozycję **Lokalizacja**, aby wybrać region geograficzny magazynu. Ten wybór określa region geograficzny, do którego wysyłane są dane kopii zapasowej.

  > [!IMPORTANT]
  > Jeśli nie wiesz, w jakiej lokalizacji znajdują się Twoje maszyny wirtualne, zamknij okno dialogowe tworzenia magazynu, a następnie przejdź do listy maszyn wirtualnych w portalu. Jeśli Twoje maszyny wirtualne znajdują się w wielu regionach, utwórz magazyn usługi Recovery Services w każdym regionie. Przed przejściem do następnej lokalizacji utwórz magazyn w pierwszej lokalizacji. Nie ma potrzeby określania kont magazynu do przechowywania danych kopii zapasowych — magazyn usługi Recovery Services i usługa Azure Backup automatycznie określają magazyn.
  >

8. W dolnej części bloku magazynu usług Recovery Services kliknij pozycję **Utwórz**.

    Utworzenie magazynu usług Recovery Services może potrwać kilka minut. Monitoruj powiadomienia o stanie wyświetlane w prawej górnej części obszaru portalu. Po utworzeniu magazynu pojawi się on na liście magazynów Usług odzyskiwania. Jeśli po kilku minutach nie widzisz swojego magazynu, kliknij pozycję **Odśwież**.

    ![Klikanie pozycji Odśwież](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Po wyświetleniu magazynu na liście magazynów usług Recovery Services możesz rozpocząć ustawianie nadmiarowości przechowywania.

Magazyn został już utworzony, więc teraz zajmiemy się skonfigurowaniem jego replikacji.

### <a name="set-storage-replication"></a>Konfigurowanie replikacji magazynu
Dla opcji replikacji magazynu można wybrać magazynowanie nadmiarowe geograficznie lub lokalnie. Domyślnie magazyn jest nadmiarowy geograficznie. Jeśli magazyn usługi Recovery Services jest podstawową kopią zapasową, pozostaw opcję replikacji magazynu ustawioną na magazyn geograficznie nadmiarowy. Wybierz magazyn lokalnie nadmiarowy, jeśli chcesz skorzystać z tańszej, ale mniej trwałej opcji. Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w temacie [Azure Storage replication overview](../storage/common/storage-redundancy.md) (Omówienie replikacji usługi Azure Storage).

Aby edytować ustawienia replikacji magazynu:

1. W bloku **Magazyny usługi Recovery Services** wybierz nowy magazyn.

  ![Wybieranie nowego magazynu z listy magazynów usług Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Wybranie magazynu spowoduje otwarcie bloków Ustawienia (*o nazwie magazynu wskazanego w górnej części*) i szczegółów magazynu.

  ![Wyświetlanie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. W bloku ustawień nowego magazynu użyj pionowego suwaka, aby przewinąć w dół do sekcji Zarządzanie, a następnie kliknij pozycję **Infrastruktura zapasowa**.
    Zostanie otwarty blok Infrastruktura zapasowa.
3. W bloku Infrastruktura zapasowa kliknij pozycję **Konfiguracja kopii zapasowej** w celu otwarcia bloku **Konfiguracja kopii zapasowej**.

    ![Ustawianie konfiguracji przechowywania dla nowego magazynu](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Wybierz odpowiednią opcję replikacji dla magazynu.

    ![Opcje konfiguracji usługi Storage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Domyślnie magazyn jest nadmiarowy geograficznie. Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, kontynuuj korzystanie z magazynu **geograficznie nadmiarowego**. Jeśli nie używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, wybierz pozycję **Lokalnie nadmiarowy**, co zmniejszy koszty magazynów platformy Azure. Więcej informacji o opcjach magazynu [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [lokalnie nadmiarowego](../storage/common/storage-redundancy.md#locally-redundant-storage) można znaleźć w tym [omówieniu nadmiarowości magazynu](../storage/common/storage-redundancy.md).


## <a name="select-a-backup-goal-set-policy-and-define-items-to-protect"></a>Wybieranie celu tworzenia kopii zapasowej, ustawianie zasad i definiowanie elementów podlegających ochronie
Przed zarejestrowaniem maszyny wirtualnej w magazynie uruchom proces wykrywania, aby mieć pewność, że zostały znalezione wszystkie nowe maszyny wirtualne dodane do subskrypcji. Proces wyszukuje na platformie Azure listę maszyn wirtualnych w ramach subskrypcji wraz z dodatkowymi informacjami, takimi jak nazwa usługi w chmurze i region. W portalu Azure scenariusz odnosi się do elementów, które mają zostać umieszczone w magazynie usług odzyskiwania. Zasady są harmonogramem określającym częstotliwość i czas tworzenia punktów odzyskiwania. Zasady zawierają także zakres przechowywania dla punktów odzyskiwania.

1. Jeśli Twój magazyn usługi Recovery Services jest już otwarty, przejdź do kroku 2. W przeciwnym razie w menu Centrum kliknij pozycję **Więcej usług**, na liście zasobów wpisz ciąg **Recovery Services**, a następnie kliknij pozycję **Magazyny usługi Recovery Services**.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Zostanie wyświetlona lista magazynów usługi Recovery Services.

    ![Widok listy magazynów usługi Recovery Services](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Wybierz magazyn z listy magazynów usługi Recovery Services, aby otworzyć jego pulpit nawigacyjny.

     ![Otwarcie bloku magazynu](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. W menu pulpitu nawigacyjnego magazynu kliknij pozycję **Kopia zapasowa**, aby otworzyć blok Kopia zapasowa.

    ![Otwarcie bloku Kopia zapasowa](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Zostaną otwarte bloki Kopia zapasowa i Cel kopii zapasowej.

    ![Otwarcie bloku scenariusza](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. W bloku Cel kopii zapasowej z menu rozwijanego **Gdzie jest uruchomione Twoje obciążenie?** wybierz platformę Azure. Z listy rozwijanej **Co ma zawierać kopia zapasowa** wybierz pozycję Maszyna wirtualna, a następnie kliknij przycisk **OK**.

    Te akcje spowodują zarejestrowanie rozszerzenia maszyny wirtualnej w magazynie. Blok Cel kopii zapasowej zostanie zamknięty, po czym zostanie otwarty blok **Zasady tworzenia kopii zapasowych**.

    ![Otwarcie bloku scenariusza](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. W bloku zasad tworzenia kopii zapasowych wybierz zasady tworzenia kopii zapasowej, które mają zostać zastosowane do magazynu.

    ![Wybór zasad tworzenia kopii zapasowej](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Szczegóły domyślnych zasad znajdują się w menu rozwijanym. Aby utworzyć zasady, wybierz opcję **Utwórz nowy** z menu rozwijanego. Instrukcje dotyczące definiowania zasad tworzenia kopii zapasowych można znaleźć w sekcji [Definiowanie zasad tworzenia kopii zapasowej](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Kliknij przycisk **OK**, aby skojarzyć zasady tworzenia kopii zapasowych z magazynem.

    Blok Zasady tworzenia kopii zapasowej zostanie zamknięty, po czym zostanie otwarty blok **Wybieranie maszyn wirtualnych**.
5. W bloku **Wybieranie maszyn wirtualnych** wybierz maszyny wirtualne do skojarzenia z określonymi zasadami i kliknij przycisk **OK**.

    ![Wybór obciążenia](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    Wybrana maszyna wirtualna jest weryfikowana. Jeśli nie widzisz oczekiwanych maszyn wirtualnych, sprawdź, czy istnieją one w tej samej lokalizacji platformy Azure, co magazyn usługi Recovery Services. Lokalizacja magazynu usługi Recovery Services jest wyświetlana na pulpicie nawigacyjnym magazynu.

6. Skoro zdefiniowano wszystkie ustawienia magazynu, w bloku Kopia zapasowa kliknij przycisk **Włącz wykonywanie kopii zapasowej**, aby wdrożyć zasady w magazynie i na maszynach wirtualnych. Wdrożenie zasad tworzenia kopii zapasowej nie powoduje utworzenia początkowego punktu odzyskiwania maszyny wirtualnej.

    ![Włączenie kopii zapasowej](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Po pomyślnym włączeniu kopii zapasowej zasady tworzenia kopii zapasowych zostaną wykonane zgodnie z harmonogramem. Należy jednak przejść do inicjowania pierwszego zadania tworzenia kopii zapasowej.

## <a name="initial-backup"></a>Początkowa kopia zapasowa
Wdrożenie zasad tworzenia kopii zapasowej na maszynie wirtualnej nie oznacza wykonania kopii zapasowej danych. Domyślnie pierwszą zaplanowaną kopią zapasową (zgodnie z definicją w zasadach tworzenia kopii zapasowej) jest początkowa kopia zapasowa. Do czasu uruchomienia procesu tworzenia początkowej kopii zapasowej w polu Stan ostatniej kopii zapasowej w bloku **Zadania tworzenia kopii zapasowej** wyświetlany jest komunikat **Ostrzeżenie (oczekiwanie na początkową kopię zapasową)**.

![Oczekiwanie na kopię zapasową](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

Jeśli tworzenie początkowej kopii zapasowej nie ma rozpocząć się wkrótce, zalecane jest wykonanie akcji **Wykonaj kopię zapasową teraz**.

Aby uruchomić zadanie tworzenia początkowej kopii zapasowej:

1. Na pulpicie nawigacyjnym magazynu kliknij liczbę w obszarze **Elementy kopii zapasowej** lub kliknij kafelek **Elementy kopii zapasowej**. <br/>
  ![Ikona Ustawienia](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Zostanie otwarty blok **Elementy kopii zapasowej**.

  ![Tworzenie kopii zapasowych elementów](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. W bloku **Elementy kopii zapasowej** wybierz element.

  ![Ikona Ustawienia](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Zostanie otwarta lista **Elementy kopii zapasowej**. <br/>

  ![Zadanie tworzenia kopii zapasowej zostało wyzwolone](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Na liście **Elementy kopii zapasowej** kliknij przycisk z wielokropkiem **...**, aby otworzyć menu Kontekst.

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu.png)

  Zostanie wyświetlone menu Kontekst.

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. W menu Kontekst kliknij pozycję **Utwórz teraz kopię zapasową**.

  ![Menu Kontekst](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  Zostanie otwarty blok Utwórz teraz kopię zapasową.

  ![wyświetlanie bloku Utwórz teraz kopię zapasową](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. W bloku Utwórz teraz kopię zapasową kliknij ikonę kalendarza, wybierz ostatni dzień okresu zachowywania tego punktu odzyskiwania przy użyciu kontrolki kalendarza, a następnie kliknij pozycję **Kopia zapasowa**.

  ![ustawianie ostatniego dnia okresu zachowywania punktu odzyskiwania Utwórz teraz punkt odzyskiwania](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Powiadomienia dotyczące wdrożenia informują o wyzwoleniu zadania tworzenia kopii zapasowej, dzięki czemu możesz monitorować postęp zadania na stronie zadań tworzenia kopii zapasowych. W zależności od rozmiaru maszyny wirtualnej tworzenie początkowej kopii zapasowej może potrwać pewien czas.

6. Aby wyświetlić lub śledzić stan początkowej kopii zapasowej, na pulpicie nawigacyjnym magazynu na kafelku **Zadania tworzenia kopii zapasowej** kliknij pozycję **W toku**.

  ![Kafelek Zadania tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Zostanie otwarty blok Zadania tworzenia kopii zapasowej.

  ![Kafelek Zadania tworzenia kopii zapasowej](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  W bloku **Zadania tworzenia kopii zapasowej** można sprawdzić stan wszystkich zadań. Sprawdź, czy zadanie tworzenia kopii zapasowej dla maszyny wirtualnej jest nadal w toku, czy zostało zakończone. Po zakończeniu zadania tworzenia kopii zapasowej stan przyjmuje wartość *Ukończono*.

  > [!NOTE]
  > W ramach operacji tworzenia kopii zapasowej usługa Azure Backup wydaje polecenie rozszerzeniu kopii zapasowej w każdej maszynie wirtualnej powodujące opróżnienie wszystkich zapisów i wykonanie spójnej migawki.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-the-vm-agent-on-the-virtual-machine"></a>Instalowanie agenta maszyny wirtualnej na maszynie wirtualnej
Te informacje są dostarczane w przypadku, gdy są wymagane. Aby rozszerzenie usługi Backup mogło działać, na maszynie wirtualnej Azure musi być zainstalowany agent maszyny wirtualnej. Jeśli jednak maszyna wirtualna została utworzona z poziomu galerii Azure, agent maszyny wirtualnej znajduje się już na maszynie wirtualnej. Maszyny wirtualne migrowane z lokalnych centrów danych nie będą miały zainstalowanego agenta maszyny wirtualnej. W takim przypadku konieczne jest zainstalowanie agenta maszyny wirtualnej. Jeśli masz problemy z tworzeniem kopii zapasowej maszyny wirtualnej Azure, sprawdź, czy agent maszyny wirtualnej Azure został poprawnie zainstalowany na maszynie wirtualnej (zobacz tabela poniżej). Jeśli tworzysz niestandardową maszynę wirtualną, przed jej udostępnieniem [upewnij się, że pole wyboru **Zainstaluj agenta maszyny wirtualnej** jest zaznaczone](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Dowiedz się więcej o [agencie maszyny wirtualnej](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) i [sposobie jego instalowania](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Poniższa tabela zawiera dodatkowe informacje na temat agenta maszyny wirtualnej dla maszyn wirtualnych systemów Windows i Linux.

| **Operacja** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalowanie agenta maszyny wirtualnej |<li>Pobierz i zainstaluj [plik MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Do ukończenia procesu instalacji niezbędne są uprawnienia administratora. <li>[Zaktualizuj właściwości maszyny wirtualnej](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx), aby wskazać, że agent jest zainstalowany. |<li> Zainstaluj najnowszą wersję [agenta systemu Linux](https://github.com/Azure/WALinuxAgent) z usługi GitHub. Do ukończenia procesu instalacji niezbędne są uprawnienia administratora. <li> [Zaktualizuj właściwości maszyny wirtualnej](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx), aby wskazać, że agent jest zainstalowany. |
| Aktualizowanie agenta maszyny wirtualnej |Aktualizowanie agenta maszyny wirtualnej jest równie proste, jak ponowne zainstalowanie [plików binarnych agenta maszyny wirtualnej](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Upewnij się, że żadna operacja tworzenia kopii zapasowej nie jest uruchomiona podczas aktualizowania agenta maszyny wirtualnej. |Postępuj zgodnie z instrukcjami dotyczącymi [aktualizowania agenta maszyny wirtualnej systemu Linux ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Upewnij się, że podczas aktualizowania agenta maszyny wirtualnej żadna operacja tworzenia kopii zapasowej nie jest uruchomiona. |
| Sprawdzanie poprawności instalacji agenta maszyny wirtualnej |<li>Przejdź do folderu *C:\WindowsAzure\Packages* w maszynie wirtualnej Azure. <li>Powinien znajdować się w nim plik WaAppAgent.exe.<li> Kliknij plik prawym przyciskiem myszy, przejdź do opcji **Właściwości**, a następnie wybierz kartę **Szczegóły**. W polu Wersja produktu powinna znajdować się wartość 2.6.1198.718 lub wyższa. |Nie dotyczy |

### <a name="backup-extension"></a>Rozszerzenie kopii zapasowej
Po zainstalowaniu agenta na maszynie wirtualnej usługa Azure Backup instaluje rozszerzenie kopii zapasowej do agenta maszyny wirtualnej. Usługa Azure Backup płynnie uaktualnia rozszerzenia kopii zapasowej i wprowadza do nich poprawki bez dodatkowej interwencji użytkownika.

Usługa Backup instaluje rozszerzenie kopii zapasowej, nawet jeśli maszyna wirtualna nie została uruchomiona. Uruchomiona maszyna wirtualna zapewnia największe prawdopodobieństwo uzyskania punktu odzyskiwania spójnego z aplikacją. Jednak usługa Azure Backup będzie kontynuować tworzenie kopii zapasowej maszyny wirtualnej nawet w sytuacji, gdy jest ona wyłączona i nie można zainstalować rozszerzenia. Ten typ kopii zapasowej jest określany jako maszyna wirtualna w trybie offline, a punkt odzyskiwania to *Spójne na poziomie awarii*.

## <a name="troubleshooting-information"></a>Informacje dotyczące rozwiązywania problemów
W przypadku wystąpienia problemów z wykonaniem którychkolwiek zadań z tego artykułu zapoznaj się z tematem [Troubleshooting guidance](backup-azure-vms-troubleshoot.md) (Wskazówki dotyczące rozwiązywania problemów).

## <a name="pricing"></a>Cennik
Koszt wykonywania kopii zapasowych maszyn wirtualnych platformy Azure jest określany na podstawie liczby chronionych wystąpień. Definicję chronionego wystąpienia można znaleźć w części [Co to jest chronione wystąpienie](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Przykład obliczania kosztu wykonania kopii zapasowej maszyny wirtualnej można znaleźć w części [How are protected instances calculated](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances) (Sposób przeprowadzania obliczeń dotyczących chronionych wystąpień). Informacje na temat [cennika usługi Backup](https://azure.microsoft.com/pricing/details/backup/) można znaleźć na stronie cennika usługi Azure Backup.

## <a name="questions"></a>Pytania?
Jeśli masz pytania lub jeśli brakuje Ci jakiejś funkcji, [prześlij nam opinię](http://aka.ms/azurebackup_feedback).
