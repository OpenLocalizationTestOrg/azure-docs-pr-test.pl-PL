---
title: " Usuwanie magazynu usług odzyskiwania na platformie Azure | Dokumentacja firmy Microsoft "
description: "Jak toodelete kopia zapasowa Azure i usługi odzyskiwania magazynu. Magazyn kopii zapasowych można wywołać chmury Azure magazyn lub magazyn Azure recovery. Rozwiązywanie problemów, gdy nie można usunąć magazynu kopii zapasowych w portalu klasycznym hello lub portalu Azure."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Usuwanie magazynu usługi Recovery Services
Witaj usługi Kopia zapasowa Azure ma dwa typy magazynów - hello magazyn kopii zapasowych i hello magazyn usług odzyskiwania. Magazyn kopii zapasowych Hello pochodzi pierwszy. Następnie powitalne magazyn usług odzyskiwania i pochodzi wzdłuż wdrożenia usługi Resource Manager toosupport hello rozwinięty. Ze względu na powitania rozszerzone możliwości i hello informacji zależności, które muszą być przechowywane w magazynie hello, usuwanie magazynu usług odzyskiwania lub kopii zapasowej może być trudne. W tym artykule opisano, jak magazyny toodelete hello w portalu klasycznym hello i hello portalu Azure.  

| **Typ wdrożenia** | **Portal** | **Nazwa magazynu** |
| --- | --- | --- |
| Wdrożenie klasyczne |Wdrożenie klasyczne |Magazyn kopii zapasowych |
| Resource Manager |Azure |Magazyn usługi Recovery Services |

> [!NOTE]
> Magazyny kopii zapasowych nie mogą chronić rozwiązań wdrożonych przy użyciu usługi Resource Manager. Można jednak użyć magazynu usług odzyskiwania tooprotect wdrożone w klasycznym serwerów i maszyn wirtualnych.  
>

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> **15 października 2017**, użytkownik nie będzie już magazyny kopii zapasowych toocreate PowerShell toouse stanie. <br/> **Od 1 listopada 2017 roku**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

W tym artykule używamy hello termin, magazynu, formularz ogólny toohello toorefer magazyn kopii zapasowych hello lub magazyn usług odzyskiwania. Używamy nazwy posiadanie hello, Magazyn kopii zapasowych lub magazyn usług odzyskiwania, gdy jest konieczne toodistinguish między magazynami hello.

## <a name="deleting-a-recovery-services-vault"></a>Usuwanie magazynu usług Recovery Services
Usuwanie magazynu usług odzyskiwania jest jednoetapowy proces - *pod warunkiem hello magazynu nie zawiera żadnych zasobów*. Przed usunięciem magazynu usług odzyskiwania, należy usunąć lub usunąć wszystkie zasoby w magazynie hello. Jeśli próba toodelete magazynu, który zawiera zasoby, wystąpi błąd jak powitania po obrazu:

![Błąd usuwania magazynu](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Dopóki hello zasobów z magazynu hello zostały wyczyszczone, klikając pozycję **ponów** tworzy hello sam błąd. Jeśli użytkownik pozostaje zablokowany na ten komunikat o błędzie, kliknij przycisk **anulować** i użyj hello następujące czynności toodelete hello zasobów w magazynie hello.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>Usuwanie elementów hello z magazynu ochrony maszyn wirtualnych
Jeśli masz już otworzyć magazyn usług odzyskiwania hello, pomiń krok drugi toohello.

1. Otwórz hello portalu Azure, a z hello pulpitu nawigacyjnego magazynu hello ma toodelete.

   Jeśli nie masz hello magazyn usług odzyskiwania przypięty toohello pulpitu nawigacyjnego, w menu centralnym hello, kliknij przycisk **więcej usług** i hello listy zasobów, wpisz **usług odzyskiwania**. Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe. Kliknij przycisk **Magazyny usług odzyskiwania**.

   ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   zostanie wyświetlona lista Hello Magazyny usług odzyskiwania. Z listy hello wybierz magazyn hello ma toodelete.

   ![Wybierz magazyn z listy](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. W hello magazynu widoku poszukać w hello **Essentials** okienka. toodelete magazynu, nie może być dowolnym chronione elementy. Jeśli jest wyświetlana liczba różne od zera, w obszarze albo **kopii zapasowej elementów** lub **kopii zapasowej serwerów zarządzania**, przed usunięciem magazynu hello, musisz usunąć te elementy.

    ![Szukaj w okienku Essentials elementy chronione](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    Maszyny wirtualne i pliki i foldery są traktowane jako elementy kopii zapasowej i znajduje się w hello **kopii zapasowej elementów** obszar hello Essentials okienka. Serwer DPM znajduje się na powitania **kopii zapasowej serwera zarządzania** obszar hello Essentials okienka. **Elementy replikowane** odnoszą się toohello usługi Azure Site Recovery.
3. Usuwanie hello toobegin chronione elementy z magazynu hello, Znajdź hello elementów w magazynie hello. Na pulpicie nawigacyjnym magazynu powitania kliknij **ustawienia**, a następnie kliknij przycisk **kopii zapasowej elementów** tooopen tego bloku.

    ![Wybierz magazyn z listy](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    Witaj **kopii zapasowej elementów** blok zawiera osobne listy, oparte na powitania typu elementu: maszynach wirtualnych platformy Azure lub folderów plików (zobacz obraz). Hello domyślnej typu elementu listy, wyświetlany jest maszynach wirtualnych platformy Azure. tooview hello listę elementów folderów plików w magazynie hello, wybierz opcję **folderów plików** z menu rozwijanego hello.
4. Przed usunięciem elementu z magazynu hello ochrony maszyn wirtualnych, należy zatrzymać zadanie tworzenia kopii zapasowej hello element i usunąć hello odzyskiwania punktu danych. Dla każdego elementu w magazynie hello wykonaj następujące kroki:

    a. Na powitania **elementów kopii zapasowych** bloku powitania kliknij prawym przyciskiem myszy element i z menu kontekstowego hello, wybierz **kopii zapasowej Zatrzymaj**.

    ![Zatrzymaj zadanie tworzenia kopii zapasowej hello](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    zostanie otwarty blok tworzenia kopii zapasowej Zatrzymaj Hello.

    b. Na powitania **zatrzymać kopii zapasowej** bloku z hello **wybierz opcję** menu, wybierz opcję **usunąć dane z kopii zapasowej** > Nazwa hello typu elementu hello > i kliknij przycisk **zatrzymać Kopia zapasowa**.

    Nazwa typu hello elementu hello tooverify ma toodelete go. Witaj **zatrzymać kopii zapasowej** aktywuje przycisk po Sprawdź hello elementu. Jeśli nie ma hello okna dialogowego pole tootype hello nazwę elementu kopii zapasowej hello, wybrano hello **Zachowaj dane kopii zapasowej** opcji.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    Opcjonalnie możesz podać przyczyny, dlaczego usuwasz hello danych i Dodaj komentarze. Po kliknięciu **zatrzymać kopii zapasowej**, Zezwalaj toocomplete zadania usuwania hello przed podjęciem próby wykonania toodelete hello magazynu. tooverify, który hello zadanie zostało zakończone, sprawdź wiadomości powitania Azure ![usunąć danych kopii zapasowej](./media/backup-azure-delete-vault/messages.png). <br/>
    Po zakończeniu zadania hello pojawi się komunikat z informacją o hello procesu tworzenia kopii zapasowej zostało zatrzymane i hello dane kopii zapasowej dla tego elementu, został usunięty.

    c. Po usunięciu elementu z listy hello na powitania **kopii zapasowej elementów** menu, kliknij przycisk **Odśwież** hello toosee pozostałych elementów w magazynie hello.

      ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/empty-items-list.png)

      Jeśli nie ma żadnych elementów na liście hello, przewiń toohello **Essentials** okienka w bloku magazynu kopii zapasowej hello. Nie powinny istnieć żadnego **kopii zapasowej elementów**, **kopii zapasowej serwerów zarządzania**, lub **elementy replikowane** na liście. Jeśli elementy nadal wyświetlana w magazynie hello, zwracać toostep trzech, a następnie wybierz pozycję listy Typ innego elementu.  
5. Jeśli nie ma więcej elementów hello magazynu w pasku narzędzi, kliknij przycisk **usunąć**.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/delete-vault.png)
6. tooverify, które mają toodelete hello magazynu, kliknij przycisk **tak**.

    Hello magazynu zostanie usunięte, a hello portal zwraca toohello **nowy** menu usługi.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>Co zrobić, jeśli zatrzymano proces tworzenia kopii zapasowej hello, ale przechowywane dane hello?
Jeśli jednak przypadkowo zatrzymano proces tworzenia kopii zapasowej hello *zachowane* hello danych, należy usunąć dane kopii zapasowej hello przed usunięciem hello magazynu. dane kopii zapasowej hello toodelete:

1. Na powitania **elementów kopii zapasowych** bloku powitania kliknij prawym przyciskiem myszy element i w menu kontekstowym powitania kliknij **usunąć danych kopii zapasowej**.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    Witaj **usunąć dane z kopii zapasowej** zostanie otwarty blok.
2. Na powitania **usunąć dane z kopii zapasowej** bloku, nazwa typu hello hello elementu, a następnie kliknij przycisk **usunąć**.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Po usunięciu danych hello zwracać toostep 4c i kontynuować hello procesu.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>Usuń tooprotect Magazyn używany serwer programu DPM
Przed usunięciem tooprotect Magazyn używany serwer DPM musi wyczyść punktów odzyskiwania, które zostały utworzone, a następnie wyrejestrowanie powitania serwera z magazynu hello.

dane hello toodelete skojarzone z grupy ochrony:

1. W konsoli administratora programu DPM hello, kliknij przycisk **ochrony** > Wybierz grupę ochrony > Wybierz hello członka grupy ochrony > i hello wstążce narzędzia, kliknij przycisk **Usuń**.

  Witaj Wybierz członka grupy ochrony tooactivate Witaj **Usuń** przycisku na powitania Wstążka narzędzi. Przykład Witaj hello jest **dummyvm9**. tooselect wielu członków w grupie ochrony hello, przytrzymaj klawisz Ctrl hello podczas klikania w elementach członkowskich hello.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    Witaj **Zatrzymaj ochronę** zostanie otwarte okno dialogowe.
2. W hello **Zatrzymaj ochronę** okno dialogowe, wybierz opcję **Usuń chronione dane**i kliknij przycisk **Zatrzymaj ochronę**.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete magazynu, należy wyczyścić, lub usunąć, hello magazynu z chronionych danych. W zależności od hello liczbę punktów odzyskiwania i danych w grupie ochrony hello go może zająć od kilku sekund tooseveral minut toodelete hello danych. Witaj **Zatrzymaj ochronę** okna dialogowego pokazuje stan powitania po ukończeniu zadania hello.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. Kontynuować ten proces dla wszystkich członków we wszystkich grupach ochrony.

    Usuń wszystkie chronione dane i ochronę grupy.
4. Po usunięciu wszystkich członków z grupy ochrony hello, Przełącz toohello portalu Azure. Otwórz pulpit nawigacyjny magazynu hello i upewnij się, że istnieją nie **kopii zapasowej elementów**, **kopii zapasowej serwerów zarządzania**, lub **elementy replikowane**. Na pasku narzędzi magazynu hello, kliknij przycisk **usunąć**.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/delete-vault.png)

    W przypadku magazynu toohello zarejestrowanych serwerów zarządzania kopii zapasowych, nawet jeśli nie ma żadnych danych w magazynie hello nie można usunąć magazynu hello. Jeśli usunięto serwerów zarządzania kopiami zapasowymi hello skojarzony z magazynem hello, ale istnieją serwery wymienione w hello **Essentials** okienku, zobacz [magazynu toohello zarejestrowanych serwerów zarządzania w kopii zapasowej hello Znajdź](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. tooverify, które mają toodelete hello magazynu, kliknij przycisk **tak**.

    Hello magazynu zostanie usunięte, a hello portal zwraca toohello **nowy** menu usługi.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>Usuń magazyn używany tooprotect serwera produkcyjnego
Przed usunięciem tooprotect Magazyn używany serwer produkcyjny, musisz usunąć lub Wyrejestruj serwer hello z magazynu hello.

serwer produkcyjny hello toodelete skojarzony z magazynem hello:

1. W portalu Azure hello, otwarcia pulpitu nawigacyjnego magazynu hello, a następnie kliknij przycisk **ustawienia** > **infrastruktura kopii zapasowej** > **serwerów produkcyjnych**.

    ![Otwiera blok serwerów produkcyjnych.](./media/backup-azure-delete-vault/delete-production-server.png)

    Witaj **serwerów produkcyjnych** bloku otwiera i wyświetla listę wszystkich serwerów produkcyjnych w magazynie hello.

    ![Lista serwerów produkcyjnych.](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. Na powitania **serwerów produkcyjnych** bloku, kliknij prawym przyciskiem myszy na powitania serwera, a następnie kliknij przycisk **usunąć**.

    ![Usuwanie serwera produkcyjnego ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    Witaj **usunąć** zostanie otwarty blok.

    ![Usuwanie serwera produkcyjnego ](./media/backup-azure-delete-vault/delete-blade.png)
3. Na powitania **usunąć** bloku, potwierdź hello nazwę serwera, a następnie kliknij przycisk **usunąć**. Powitania serwera, tooactivate hello musi poprawnie nazw **usunąć** przycisku.

    Po usunięciu magazynu hello pojawi się komunikat z informacją o magazynie hello została usunięta. Po usunięciu wszystkich serwerów w magazynie hello przewiń okienku Essentials toohello wstecz na pulpicie nawigacyjnym magazynu hello.
4. Na pulpicie nawigacyjnym magazynu hello, upewnij się, brak nie **kopii zapasowej elementów**, **kopii zapasowej serwerów zarządzania**, lub **elementy replikowane**. Na pasku narzędzi magazynu hello, kliknij przycisk **usunąć**.
5. tooverify, które mają toodelete hello magazynu, kliknij przycisk **tak**.

    Hello magazynu zostanie usunięte, a hello portal zwraca toohello **nowy** menu usługi.

## <a name="delete-a-backup-vault-in-classic-portal"></a>Usuń magazyn kopii zapasowych w portalu klasycznym
Witaj poniższe instrukcje dotyczą usuwania magazynu kopii zapasowych w portalu klasycznym hello. Przed usunięciem hello magazyn kopii zapasowych, należy usunąć punktów odzyskiwania hello, lub kopii zapasowej elementów i Usuń hello zarejestrowane serwery. Witaj zarejestrowane serwery są hello systemu Windows Server, stacji roboczej lub maszyn wirtualnych, które zostały zarejestrowane toohello magazynu.

1. Otwórz hello [klasyczny portal](https://manage.windowsazure.com).

2. Z listy hello magazynów kopii zapasowych wybierz magazyn hello ma toodelete.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    Otwiera Hello pulpitem nawigacyjnym magazynu. Spójrz na powitania liczby serwerów z systemem Windows i/lub Azure maszyny wirtualne skojarzony z magazynem hello. Ponadto przyjrzeć się całkowita ilość miejsca hello zużyte na platformie Azure. Zatrzymaj wszystkie zadania tworzenia kopii zapasowej i usunięcie wszystkich danych przed usunięciem magazynu hello.

3. Kliknij przycisk hello **chronione elementy** , a następnie kliknij pozycję **Zatrzymaj ochronę**

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    Witaj **Zatrzymaj ochronę Twojego magazynu** zostanie wyświetlone okno dialogowe.
4. W hello **Zatrzymaj ochronę Twojego magazynu** dialogowym wyboru **Usuń skojarzone dane kopii zapasowej** i kliknij przycisk ![znacznikiem wyboru](./media/backup-azure-delete-vault/checkmark.png). <br/>
    Można opcjonalnie wybierz przyczynę zatrzymywanie ochrony i podaj komentarz.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Po usunięciu elementów hello w magazynie hello, magazynie hello jest pusta.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. Kliknij na liście hello kart **zarejestrowane elementy**. Witaj **typu** menu rozwijanego, umożliwia toochoose hello typu magazynu toohello zarejestrowanie serwera. Typ Hello może być systemu Windows Server lub maszynie wirtualnej platformy Azure. W hello poniższy przykład, wybierz magazyn zarejestrowanych toohello maszyny wirtualnej hello, a następnie kliknij przycisk **Unregister**.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Jeśli chcesz toodelete hello rejestracji w systemie Windows Server z hello **typu** menu rozwijanego wybierz **systemu Windows Server**, kliknij przycisk ![znacznikiem wyboru](./media/backup-azure-delete-vault/checkmark.png) ekranie powitania toorefresh a następnie kliknij przycisk **usunąć**. <br/>

  ![Wybierz serwer z systemem Windows](./media/backup-azure-delete-vault/select-windows-server.png)

6. Kliknij na liście hello kart **pulpitu nawigacyjnego** tooopen, który karcie. Sprawdź, czy nie ma żadnych zarejestrowanych serwerów lub chroniona w chmurze hello maszyn wirtualnych platformy Azure. Sprawdź także, że nie ma w magazynie danych. Kliknij przycisk **usunąć** toodelete hello magazynu.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    zostanie otwarty ekran potwierdzenia magazynu usuwanie kopii zapasowej Hello. Wybierz opcję Dlaczego usuwana hello magazynu, a następnie kliknij przycisk ![Znacznik wyboru](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    Hello magazyn zostanie usunięty, a zwracany toohello pulpitu nawigacyjnego portalu klasycznego.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>Znajdź hello zarządzania kopii zapasowej serwerów zarejestrowanych toohello magazynu
Jeśli masz wiele serwerów zarejestrowanych tooa magazynu, może być trudne tooremember je. serwery hello toosee zarejestrowanych toohello magazynu i usunąć je:

1. Otwórz hello pulpitem nawigacyjnym magazynu.
2. W hello **Essentials** okienku, kliknij przycisk **ustawienia** tooopen tego bloku.

    ![Otwórz blok ustawień](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. Na powitania **bloku ustawienia**, kliknij przycisk **infrastruktura kopii zapasowej**.
4. Na powitania **infrastruktura kopii zapasowej** bloku, kliknij przycisk **serwerów zarządzania kopiami zapasowymi**. zostanie otwarty blok serwerów zarządzania kopiami zapasowymi Hello.

    ![Lista serwerów zarządzania kopiami zapasowymi](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete serwer z listy hello, kliknij prawym przyciskiem myszy nazwę hello powitania serwera, a następnie kliknij przycisk **usunąć**.
    Witaj **usunąć** zostanie otwarty blok.
6. Na powitania **usunąć** bloku, podaj nazwę hello powitania serwera. Jeśli jest długa nazwa, można skopiować i wkleić go z listy serwerów zarządzania kopiami zapasowymi hello. Następnie kliknij przycisk **usunąć**.  
