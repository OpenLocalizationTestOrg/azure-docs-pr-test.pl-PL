---
title: "Pierwsze spojrzenie — tworzenie kopii zapasowej maszyn wirtualnych platformy Azure przy użyciu magazynu kopii zapasowych | Microsoft Docs"
description: "Użyj klasycznego portalu tooback hello zapasowej magazyn kopii zapasowych tooa maszynach wirtualnych platformy Azure. W tym samouczku opisano wszystkich faz, w tym tworzenie magazynu kopii zapasowych hello, rejestrowanie hello maszyn wirtualnych, tworzenia zasad tworzenia kopii zapasowej i uruchamianie hello początkowej zadanie tworzenia kopii zapasowej."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a>Pierwsze spojrzenie: tworzenie kopii zapasowych maszyn wirtualnych platformy Azure
> [!div class="op_single_selector"]
> * [Ochrona maszyn wirtualnych przy użyciu magazynu usługi Recovery Services](backup-azure-vms-first-look-arm.md)
> * [Ochrona maszyn wirtualnych platformy Azure przy użyciu magazynu usługi Backup](backup-azure-vms-first-look.md)
>
>

Ten samouczek przedstawia kroki hello tworzenia kopii zapasowej maszyny wirtualnej platformy Azure (VM) tooa magazynu kopii zapasowych na platformie Azure. W tym artykule opisano hello klasycznego modelu lub model wdrażania programu Service Manager, tworzenie kopii zapasowych maszyn wirtualnych. Witaj poniższe kroki mają zastosowanie tylko tooBackup magazynów utworzone w portalu klasycznym hello. Firma Microsoft zaleca używanie hello modelu Menedżera zasobów dla nowych wdrożeń.

Jeśli interesuje Cię w tworzeniu kopii zapasowych w magazynie usług odzyskiwania tooa maszyny Wirtualnej należy tooa grupy zasobów, zobacz [Pierwsze spojrzenie: ochrona maszyn wirtualnych z magazynu usług odzyskiwania](backup-azure-vms-first-look-arm.md).

toosuccessfully wykonaj następujące czynności hello samouczek, musi istnieć te wymagania wstępne:

* Utworzona została maszyna wirtualna w ramach subskrypcji platformy Azure.
* Hello maszyna wirtualna ma łączność tooAzure publicznych adresów IP. Aby uzyskać więcej informacji, zobacz [Network connectivity](backup-azure-vms-prepare.md#network-connectivity) (Łączność sieciowa).


> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym samouczku jest przeznaczona do użytku z maszyn wirtualnych utworzonych w portalu klasycznym hello.
>
>

## <a name="create-a-backup-vault"></a>Tworzenie magazynu kopii zapasowych
Magazyn kopii zapasowych to jednostka, która przechowuje wszystkie hello kopie zapasowe i punkty odzyskiwania, które zostały utworzone w czasie. Witaj magazynu kopii zapasowych zawiera również hello zasad tworzenia kopii zapasowej, które są toohello zastosowane maszyn wirtualnych, których powstaje kopia zapasowa.

> [!IMPORTANT]
> Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.
> Można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="discover-and-register-azure-virtual-machines"></a>Odnajdywanie i rejestrowanie maszyn wirtualnych platformy Azure
Przed zarejestrowaniem hello maszyny Wirtualnej w magazynie, uruchom tooidentify procesu odnajdywania hello wszelkie nowe maszyny wirtualne. Zwraca listę maszyn wirtualnych hello subskrypcji, wraz z dodatkowymi informacjami, takie jak nazwa usługi w chmurze hello i hello regionu.

1. Zaloguj się toohello [klasycznego portalu Azure](http://manage.windowsazure.com/)
2. W hello klasycznego portalu Azure, kliknij przycisk **usług odzyskiwania** tooopen hello listę magazynów usług odzyskiwania.
    ![Wybór obciążenia](./media/backup-azure-vms-first-look/recovery-services-icon.png)
3. Z listy hello magazynów wybierz tooback magazynu hello zapasowej maszyny Wirtualnej.

    Po wybraniu magazyn zostanie otwarty w hello **Szybki Start** strony
4. W menu magazynu powitania kliknij **zarejestrowane elementy**.

    ![Wybieranie obciążenia](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. Z hello **typu** menu, wybierz opcję **maszyny wirtualnej Azure**.

    ![Wybieranie obciążenia](./media/backup-azure-vms/discovery-select-workload.png)
6. Kliknij przycisk **ODNAJDOWANIA** u dołu hello hello strony.
    ![Przycisk Odnajdź](./media/backup-azure-vms/discover-button-only.png)

    Hello proces odnajdowania może zająć kilka minut hello maszyny wirtualne są wyszczególniane. Brak powiadomienie u dołu hello ekranu hello, który informuje o tym, że proces hello jest uruchomiony.

    ![Odnajdywanie maszyn wirtualnych](./media/backup-azure-vms/discovering-vms.png)

    Witaj powiadomienie ulega zmianie po zakończeniu procesu hello.

    ![Odnajdywanie zostało zakończone](./media/backup-azure-vms-first-look/discovery-complete.png)
7. Kliknij przycisk **ZAREJESTROWAĆ** u dołu hello hello strony.
    ![Przycisk Zarejestruj](./media/backup-azure-vms-first-look/register-icon.png)
8. W hello **Zarejestruj elementy** menu skrótów, wybierz hello maszyn wirtualnych, które mają tooregister.

   > [!TIP]
   > W tym samym czasie można zarejestrować wiele maszyn wirtualnych.
   >
   >

    Zadanie jest tworzone dla każdej maszyny wirtualnej, która zostanie wybrana.
9. Kliknij przycisk **zadania** w hello powiadomień toogo toohello **zadania** strony.

    ![Rejestrowanie zadania](./media/backup-azure-vms/register-create-job.png)

    Maszyna wirtualna Hello pojawia się również hello liście zarejestrowanych elementów wraz ze stanu hello hello rejestracji operacji.

    ![Rejestrowanie — stan 1](./media/backup-azure-vms/register-status01.png)

    Po zakończeniu operacji hello hello stan zmienia się tooreflect hello *zarejestrowany* stanu.

    ![Rejestrowanie — stan 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Zainstaluj hello agenta maszyny Wirtualnej na maszynie wirtualnej hello
Witaj Agent maszyny Wirtualnej musi być zainstalowany na powitania maszyny wirtualnej platformy Azure dla hello kopii zapasowej rozszerzenia toowork. Jeśli maszyna wirtualna została utworzona z hello galerii Azure, hello agenta maszyny Wirtualnej jest już obecny na powitania wirtualna; można pominąć zbyt[ochroną maszyn wirtualnych](backup-azure-vms-first-look.md#create-the-backup-policy).

Migracji maszyny Wirtualnej z lokalnego centrum danych, hello wirtualna prawdopodobnie nie ma hello zainstalowanego agenta maszyny Wirtualnej. Hello agenta maszyny Wirtualnej należy zainstalować na maszynie wirtualnej hello przed kontynuowaniem tooprotect hello maszyny Wirtualnej. Aby uzyskać szczegółowe instrukcje dotyczące instalowania hello agenta maszyny Wirtualnej, zobacz hello [sekcję VM Agent hello kopii zapasowych maszyn wirtualnych artykułu](backup-azure-vms-prepare.md#vm-agent).

## <a name="create-hello-backup-policy"></a>Tworzenie zasad tworzenia kopii zapasowej hello
Przed wyzwoleniem hello początkowej zadanie tworzenia kopii zapasowej Ustaw harmonogram hello, gdy migawek kopii zapasowych. Witaj Zaplanuj, kiedy migawek kopii zapasowych są pobierane i hello czas te migawki są przechowywane, jest hello zasad tworzenia kopii zapasowej. informacje dotyczące przechowywania Hello jest oparty na schemacie rotacji kopii zapasowej dziadek ojciec syn..

1. Przejdź toohello magazynu kopii zapasowych w obszarze **usług odzyskiwania** w hello klasycznego portalu Azure i kliknij przycisk **zarejestrowane elementy**.
2. Wybierz **maszyny wirtualnej Azure** z menu rozwijanego hello.

    ![Wybieranie obciążenia w portalu](./media/backup-azure-vms/select-workload.png)
3. Kliknij przycisk **Chroń** u dołu hello hello strony.
    ![Klikanie pozycji Chroń](./media/backup-azure-vms-first-look/protect-icon.png)

    Witaj **Kreator ochrony elementów** i zostanie wyświetlona lista *tylko* maszyn wirtualnych, które są zarejestrowane i nie są chronione.

    ![Konfigurowanie ochrony w dużej skali](./media/backup-azure-vms/protect-at-scale.png)
4. Wybierz hello maszyn wirtualnych, które mają tooprotect.

    Jeśli istnieją dwa lub więcej maszyn wirtualnych z hello takie same nazwy, użyj hello toodistinguish usługi w chmurze między maszynami wirtualnymi hello.
5. Na powitania **skonfiguruj ochronę** menu Wybierz istniejące zasady lub Utwórz nowy tooprotect zasad zidentyfikowanych maszyn wirtualnych hello.

    Nowe magazynami kopii zapasowych są skojarzone z magazynem hello zasady domyślne. Ta zasada ma dziennym określają tworzenie każdego wieczoru i hello dziennej migawki są przechowywane przez 30 dni. Z jednymi zasadami tworzenia kopii zapasowych może być skojarzonych wiele maszyn wirtualnych. Jednak hello maszyny wirtualnej można skojarzyć tylko z jednymi zasadami naraz.

    ![Ochrona za pomocą nowych zasad](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Zasady tworzenia kopii zapasowych obejmują schemat przechowywania hello zaplanowanych kopii zapasowych. W przypadku wybrania istniejących zasad tworzenia kopii zapasowej będzie opcje przechowywania hello toomodify w hello następnego kroku.
   >
   >
6. Na **zakres przechowywania** zdefiniuj hello codziennie, co tydzień, miesięcznych i rocznych zakres hello określonych punktów kopii zapasowych.

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/long-term-retention.png)

    Zasady przechowywania określa hello czas przechowywania kopii zapasowej. Można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej.
7. Kliknij przycisk **zadania** tooview hello lista **konfiguracji ochrony** zadania.

    ![Zadanie konfigurowania ochrony](./media/backup-azure-vms/protect-configureprotection.png)

    Po ustanowieniu zasad hello, przejdź do następnego kroku toohello i uruchom tworzenie początkowej kopii zapasowej hello.

## <a name="initial-backup"></a>Początkowa kopia zapasowa
Po chronionej maszyny wirtualnej za pomocą zasad można wyświetlić tę relację na powitania **chronione elementy** kartę. Dopóki hello utworzona początkowa kopia zapasowa, hello **stanu ochrony** jest pokazywana jako **chroniona — (oczekiwanie początkowa kopia zapasowa)**. Domyślnie pierwszą zaplanowaną kopią zapasową hello jest hello *początkowa kopia zapasowa*.

![Oczekiwanie na kopię zapasową](./media/backup-azure-vms-first-look/protection-pending-border.png)

toostart hello początkową kopię zapasową teraz:

1. Na powitania **chronione elementy** kliknij przycisk **Utwórz kopię zapasową teraz** u dołu hello hello strony.
    ![Ikona Utwórz kopię zapasową teraz](./media/backup-azure-vms-first-look/backup-now-icon.png)

    Hello usługi Azure Backup tworzy zadanie tworzenia kopii zapasowej hello początkowej operacji tworzenia kopii zapasowej.
2. Kliknij przycisk hello **zadania** kartę tooview hello listy zadań.

    ![Tworzenie kopii zapasowej w toku](./media/backup-azure-vms-first-look/protect-inprogress.png)

    Po zakończeniu tworzenia początkowej kopii zapasowej, stan hello hello maszyny wirtualnej w hello **chronione elementy** jest karta *chronione*.

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > Tworzenie kopii zapasowych maszyn wirtualnych jest procesem lokalnym. Nie można utworzyć kopii zapasowych maszyn wirtualnych z jednego regionu tooa magazynu kopii zapasowych w innym regionie. Tak dla każdego regionu Azure, który ma maszyn wirtualnych, które wymagają toobe kopii zapasowej, co najmniej jeden magazyn kopii zapasowych należy utworzyć w tym regionie.
   >
   >

## <a name="next-steps"></a>Następne kroki
Po pomyślnym utworzeniu kopii zapasowej maszyny wirtualnej można wykonać jeden z kilku kroków. najbardziej logicznym krokiem Hello jest toofamiliarize sobie z przywracaniem danych tooa maszyny Wirtualnej. Istnieją jednak zadań zarządzania, które ułatwią zrozumienie sposobu tookeep bezpiecznych danych i ograniczania kosztów.

* [Monitorowanie maszyn wirtualnych i zarządzanie nimi](backup-azure-manage-vms.md)
* [Przywracanie maszyn wirtualnych](backup-azure-restore-vms.md)
* [Wskazówki dotyczące rozwiązywania problemów](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a>Pytania?
Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).
