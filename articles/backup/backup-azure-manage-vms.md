---
title: "kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage i monitorowanie kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Zarządzanie kopiami zapasowymi maszyny wirtualnej platformy Azure
> [!div class="op_single_selector"]
> * [Zarządzanie kopiami zapasowymi maszyny Wirtualnej Azure](backup-azure-manage-vms.md)
> * [Zarządzanie kopiami zapasowymi klasyczne maszyny Wirtualnej](backup-azure-manage-vms-classic.md)
>
>

Ten artykuł zawiera wskazówki dotyczące zarządzania kopii zapasowych maszyn wirtualnych i wyjaśniono, hello alerty kopii zapasowej informacji dostępnych na pulpicie nawigacyjnym portalu hello. wskazówki Hello w tym artykule dotyczą maszyn wirtualnych toousing o Magazyny usług odzyskiwania. W tym artykule nie opisano hello tworzenia maszyn wirtualnych ani jest wyjaśniają sposób tooprotect maszyn wirtualnych. Aby Elementarz o ochronie usługi Azure Resource Manager wdrożone maszyny wirtualne na platformie Azure w magazynie usług odzyskiwania, zobacz [Pierwsze spojrzenie: Utwórz kopię zapasową maszyn wirtualnych tooa magazyn usług odzyskiwania i](backup-azure-vms-first-look-arm.md).

## <a name="manage-vaults-and-protected-virtual-machines"></a>Zarządzanie magazynami i chronione maszyny wirtualne
W portalu Azure hello pulpitem nawigacyjnym magazynu usług odzyskiwania hello zapewnia tooinformation dostępu o tym magazynie hello:

* Hello najnowszej kopii zapasowej migawki, która jest również najnowszy punkt przywracania hello < br\>
* Witaj zasad tworzenia kopii zapasowej < br\>
* Całkowity rozmiar wszystkich migawek kopii zapasowych < br\>
* Liczba maszyn wirtualnych, które są chronione przy użyciu magazynu hello < br\>

Wiele zadań zarządzania z kopii zapasowej maszyny wirtualnej zaczynać otwierania magazynu hello hello w pulpicie nawigacyjnym. Jednak ponieważ magazynów, mogą być używane tooprotect wielu elementów (lub wiele maszyn wirtualnych), tooview szczegółowych informacji o określonej maszyny Wirtualnej, Otwórz pulpit nawigacyjny elementu magazynu hello. Witaj poniższej procedurze wyjaśniono, jak tooopen hello *pulpitem nawigacyjnym magazynu* , a następnie kontynuuj toohello *pulpitem nawigacyjnym magazynu elementu*. W obu tych procedur, które wskazują sposób tooadd hello magazynu i magazynu toohello elementu pulpitu nawigacyjnego Azure za pomocą polecenia toodashboard numeru Pin hello są "porady". Toodashboard numer PIN jest sposób tworzenia skrótów toohello magazynu lub elementów. Można również wykonywać typowe polecenia ze skrótu hello.

> [!TIP]
> Jeśli masz wiele pulpitów nawigacyjnych i otworzyć bloków, za pomocą suwaka dark blue hello u dołu hello hello okna tooslide hello Azure pulpitu nawigacyjnego i z powrotem.
>
>

![Pełny widok z suwaka](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>Otwórz pulpit nawigacyjny hello magazynu usług odzyskiwania:
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu Centrum powitania kliknij **Przeglądaj** i hello listy zasobów, wpisz **usług odzyskiwania**. Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe. Kliknij opcję **Magazyn Usług odzyskiwania**.

    ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    wyświetli się lista Hello Magazyny usług odzyskiwania.

    ![Lista usług odzyskiwania magazynów ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > Jeśli przypniesz toohello magazyn Azure pulpitu nawigacyjnego tego magazynu jest natychmiast dostępna po otwarciu hello portalu Azure. toopin magazynu toohello pulpitu nawigacyjnego, na liście hello magazynu, kliknij prawym przyciskiem myszy hello magazynu, a następnie wybierz **toodashboard numeru Pin**.
   >
   >
3. Witaj wybierz z listy magazynów hello magazynu tooopen jego pulpitu nawigacyjnego. Po wybraniu magazynu hello, hello pulpitem nawigacyjnym magazynu i hello **ustawienia** Otwórz blok. W hello po obrazu, hello **magazynu Contoso** zostanie wyróżniona pulpitu nawigacyjnego.

    ![Otwórz pulpit nawigacyjny magazynu i blok ustawień](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>Otwórz pulpit nawigacyjny elementu magazynu
W poprzedniej procedurze hello możesz otworzyć hello pulpitem nawigacyjnym magazynu. tooopen hello elementu pulpitem nawigacyjnym magazynu:

1. Na pulpicie nawigacyjnym magazynu hello, na powitania **kopii zapasowej elementów** Kafelek, kliknij przycisk **maszyny wirtualne Azure**.

    ![Kafelek otwarte elementy kopii zapasowej](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    Witaj **elementów kopii zapasowych** hello ostatnie zadanie tworzenia kopii zapasowej dla każdego elementu listy bloku. W tym przykładzie Brak jednej maszyny wirtualnej, demovm-markgal chronione przez ten magazyn.  

    ![Kafelek elementów kopii zapasowych](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > W celu ułatwienia dostępu można przypiąć toohello elementu magazynu Azure pulpitu nawigacyjnego. toopin elementu magazynu w hello magazyn elementu listy, element powitania kliknij prawym przyciskiem myszy i wybierz **toodashboard numeru Pin**.
   >
   >
2. W hello **kopii zapasowej elementów** bloku, kliknij element hello tooopen magazynu hello elementów pulpitu nawigacyjnego.

    ![Kafelek elementów kopii zapasowych](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    pulpit nawigacyjny elementu magazynu Hello i jego **ustawienia** Otwórz blok.

    ![Pulpit nawigacyjny elementów kopii zapasowych z bloku ustawień](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    Z hello magazyn elementów pulpitu nawigacyjnego można wykonywać wiele zadań zarządzania kluczami, takich jak:

   * Zmiana zasad lub utworzyć nowe zasady tworzenia kopii zapasowej < br\>
   * Wyświetl punkty przywracania i wyświetlić ich stan spójności < br\>
   * na żądanie kopii zapasowej maszyny wirtualnej < br\>
   * Zatrzymaj ochronę maszyn wirtualnych < br\>
   * wznowić ochronę maszyny wirtualnej < br\>
   * Usuwanie danych kopii zapasowej (lub punktu odzyskiwania) < br\>
   * [Przywracanie kopii zapasowych dysków](backup-azure-arm-restore-vms.md#restore-backed-up-disks) < br\>

W przypadku hello zgodnie z procedurami hello punkt początkowy jest pulpit nawigacyjny elementu magazynu hello.

## <a name="manage-backup-policies"></a>Zarządzanie zasadami tworzenia kopii zapasowych
1. Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **wszystkie ustawienia** tooopen hello **ustawienia** bloku.

    ![Blok zasady tworzenia kopii zapasowej](./media/backup-azure-manage-vms/all-settings-button.png)
2. Na powitania **ustawienia** bloku, kliknij przycisk **kopii zapasowej zasad** tooopen tego bloku.

    W bloku hello hello kopii zapasowej częstotliwości i przechowywania zakresu są wyświetlane szczegóły.

    ![Blok zasady tworzenia kopii zapasowej](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. Z hello **wybierz zasady tworzenia kopii zapasowej** menu:

   * toochange zasady, wybierz inne zasady i kliknij przycisk **zapisać**. nowe zasady Hello jest natychmiast zastosowane toohello magazynu. < br\>
   * Wybierz zasady, toocreate **Utwórz nowy**.

     ![Kopia zapasowa maszyny wirtualnej](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     Aby uzyskać instrukcje na temat tworzenia zasad tworzenia kopii zapasowej, zobacz [Definiowanie zasad tworzenia kopii zapasowej](backup-azure-manage-vms.md#defining-a-backup-policy).

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> Zasady tworzenia kopii zapasowej i zarządzania nimi, upewnij się, że hello toofollow [najlepsze rozwiązania](backup-azure-vms-introduction.md#best-practices) do uzyskania optymalnej wydajności tworzenia kopii zapasowej
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>Na żądanie kopii zapasowej maszyny wirtualnej
Skonfigurowane dla ochrony na żądanie można wykonać kopii zapasowej maszyny wirtualnej. Jeśli oczekuje początkowa kopia zapasowa hello kopii zapasowej na żądanie tworzy pełną kopię hello maszyny wirtualnej w powitalne magazyn usług odzyskiwania. Jeśli hello początkowa kopia zapasowa została wykonana, na żądanie kopii zapasowej tylko wysłać zmiany z hello poprzednią migawkę toohello magazyn usług odzyskiwania. Oznacza to, że kolejne kopie zapasowe są zawsze przyrostowe.

> [!NOTE]
> zakres przechowywania kopii zapasowych na żądanie Hello jest hello wartość przechowywania określona dla hello codziennego punktu kopii zapasowej w zasadach hello. Jeśli wybrano opcję nie codziennego punktu kopii zapasowej, tygodniowego punktu kopii zapasowej hello jest używany.
>
>

tootrigger na żądanie kopii zapasowej maszyny wirtualnej:

* Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **wykonaj kopię zapasową teraz**.

    ![Kopię zapasową teraz przycisku.](./media/backup-azure-manage-vms/backup-now-button.png)

    Hello portal upewnia się, że chcesz toostart zadanie tworzenia kopii zapasowej na żądanie. Kliknij przycisk **tak** toostart hello — zadanie tworzenia kopii zapasowej.

    ![Kopię zapasową teraz przycisku.](./media/backup-azure-manage-vms/backup-now-check.png)

    zadanie tworzenia kopii zapasowej Hello tworzy punkt odzyskiwania. zakres przechowywania Hello hello punkt odzyskiwania jest hello taki sam jak zakres przechowywania określonym w zasadach hello skojarzonych z maszyną wirtualną hello. postęp hello tootrack hello zadania, na pulpicie nawigacyjnym magazynu hello, kliknij przycisk hello **zadania tworzenia kopii zapasowej** kafelka.  

## <a name="stop-protecting-virtual-machines"></a>Zatrzymaj ochronę maszyn wirtualnych
Jeśli wybierzesz toostop ochrony maszyny wirtualnej, są pytanie, czy punkty odzyskiwania hello tooretain. Istnieją dwa sposoby toostop ochrona maszyn wirtualnych:

* zatrzymanie wszystkich przyszłych zadań kopii zapasowej i usunięcie wszystkich punktów odzyskiwania lub
* zatrzymanie wszystkich przyszłych zadań kopii zapasowej, ale pozostawić hello punktów odzyskiwania <br/>

Brak kosztów związanych z pozostawienie hello punktów odzyskiwania w magazynie. Jednak zaletą hello pozostawienie hello punktów odzyskiwania jest hello maszyny wirtualnej można przywrócić później, w razie potrzeby. Aby dowiedzieć koszt hello opuszczania hello punktów odzyskiwania, zobacz hello [szczegóły cennika](https://azure.microsoft.com/pricing/details/backup/). Jeśli wybierzesz toodelete wszystkich punktów odzyskiwania, nie można przywrócić hello maszyny wirtualnej.

toostop ochrony dla maszyny wirtualnej:

1. Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **kopii zapasowej Zatrzymaj**.

    ![Zatrzymaj przycisku tworzenia kopii zapasowej](./media/backup-azure-manage-vms/stop-backup-button.png)

    zostanie otwarty blok tworzenia kopii zapasowej Zatrzymaj Hello.

    ![Zatrzymywanie tworzenia kopii zapasowej bloku](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. Na powitania **zatrzymać kopii zapasowej** bloku, wybierz, czy tooretain lub usuń hello dane kopii zapasowej. pole informacje Hello zawiera szczegółowe informacje o wybranym.

    ![Zatrzymaj ochronę](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. W przypadku wybrania dane kopii zapasowej hello tooretain Pomiń toostep 4. W przypadku wybrania toodelete dane kopii zapasowej potwierdzić, że mają zadania tworzenia kopii zapasowej hello toostop i usunąć punktów odzyskiwania hello — Nazwa typu hello hello elementu.

    ![Zatrzymaj weryfikacji](./media/backup-azure-manage-vms/item-verification-box.png)

    Jeśli nie masz pewności co nazwa elementu hello, umieść kursor nad hello wykrzyknik tooview hello nazwy. Nazwa hello elementu hello jest również w obszarze **zatrzymać kopii zapasowej** u góry bloku hello hello.
4. Opcjonalnie wprowadź **Przyczyna** lub **komentarz**.
5. Kliknij zadanie tworzenia kopii zapasowej hello toostop dla bieżącego elementu hello, ![Zatrzymaj przycisku tworzenia kopii zapasowej](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    Komunikat z powiadomieniem informuje o tym, że zadania tworzenia kopii zapasowej hello zostały zatrzymane.

    ![Upewnij się, Zatrzymaj ochronę](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>Wznów ochronę maszyny wirtualnej
Jeśli hello **Zachowaj dane kopii zapasowej** została wybrana opcja podczas ochrony dla maszyny wirtualnej hello została zatrzymana, wówczas jest możliwe tooresume ochrony. Jeśli hello **usunąć dane z kopii zapasowej** została wybrana opcja, a następnie nie można wznowić ochronę hello maszyny wirtualnej.

ochronę tooresume hello maszyny wirtualnej

1. Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **Wznów wykonywanie kopii zapasowej**.

    ![Wznów ochronę](./media/backup-azure-manage-vms/resume-backup-button.png)

    zostanie otwarty blok zasad tworzenia kopii zapasowej Hello.

   > [!NOTE]
   > Podczas ponownie ochrona powitalnych maszyny wirtualnej, można wybrać inne zasady niż zasady hello, z którą maszyny wirtualnej został początkowo chronić.
   >
   >
2. Wykonaj kroki hello w [Zarządzanie zasadami tworzenia kopii zapasowej](backup-azure-manage-vms.md#manage-backup-policies) zasad hello tooassign hello maszyny wirtualnej.

    Po hello zasad tworzenia kopii zapasowej jest stosowane toohello maszyny wirtualnej, zapoznaj się hello następującą wiadomości.

    ![Pomyślnie chronionej maszyny Wirtualnej](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>Usuwanie danych kopii zapasowej
Można usunąć danych kopii zapasowej hello skojarzonych z maszyną wirtualną podczas hello **kopii zapasowej Zatrzymaj** zadania, albo w dowolnym momencie po hello zadanie tworzenia kopii zapasowej została ukończona. Alternatywą może być korzystne toowait dni lub tygodnie przed usunięciem hello punktów odzyskiwania. W odróżnieniu od przywracanie punktów odzyskiwania, podczas usuwania danych kopii zapasowej, nie można wybrać określonego odzyskiwania toodelete punktów. Jeśli wybierzesz toodelete danych kopii zapasowych, należy usunąć wszystkie punkty odzyskiwania skojarzone z elementem hello.

Witaj poniższej procedurze przyjęto hello zadanie tworzenia kopii zapasowej dla maszyny wirtualnej hello została zatrzymana lub wyłączona. Po wyłączeniu zadanie tworzenia kopii zapasowej hello hello **Wznów wykonywanie kopii zapasowej** i **kopii zapasowej Delete** opcje są dostępne na pulpicie nawigacyjnym elementu magazynu hello.

![Wznów i usuń przyciski](./media/backup-azure-manage-vms/resume-delete-buttons.png)

toodelete dane kopii zapasowej na maszynie wirtualnej z hello *kopii zapasowej wyłączone*:

1. Na powitania [pulpitem nawigacyjnym magazynu elementu](backup-azure-manage-vms.md#open-a-vault-item-dashboard), kliknij przycisk **usunięcia kopii zapasowej**.

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    Witaj **usunąć dane z kopii zapasowej** zostanie otwarty blok.

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. Nazwa typu hello hello elementu tooconfirm ma punktów odzyskiwania hello toodelete.

    ![Zatrzymaj weryfikacji](./media/backup-azure-manage-vms/item-verification-box.png)

    Jeśli nie masz pewności co nazwa elementu hello, umieść kursor nad hello wykrzyknik tooview hello nazwy. Nazwa hello elementu hello jest również w obszarze **usunąć dane z kopii zapasowej** u góry bloku hello hello.
3. Opcjonalnie wprowadź **Przyczyna** lub **komentarz**.
4. dane kopii zapasowej hello toodelete dla bieżącego elementu hello, kliknij przycisk ![Zatrzymaj przycisku tworzenia kopii zapasowej](./media/backup-azure-manage-vms/delete-button.png)

    Komunikat z powiadomieniem informuje hello danych kopii zapasowych została usunięta.

## <a name="next-steps"></a>Następne kroki
Informacje dotyczące ponownego tworzenia maszyny wirtualnej z punktu odzyskiwania, zapoznaj się z [przywracanie maszyn wirtualnych Azure](backup-azure-restore-vms.md). Jeśli potrzebujesz informacji na temat ochrony maszyn wirtualnych, zobacz [Pierwsze spojrzenie: Utwórz kopię zapasową maszyn wirtualnych tooa magazyn usług odzyskiwania i](backup-azure-vms-first-look-arm.md). Aby uzyskać informacje dotyczące monitorowania zdarzeń, zobacz [monitorowania alertów dla kopii zapasowych maszyn wirtualnych Azure](backup-azure-monitor-vms.md).
