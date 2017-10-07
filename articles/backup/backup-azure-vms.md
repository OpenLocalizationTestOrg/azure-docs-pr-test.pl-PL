---
title: "aaaBack się magazynu kopii zapasowych tooa wdrożone w klasycznej maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Odnajdowanie, rejestrowania i utworzyć kopię zapasową maszyn wirtualnych z tych procedur do utworzenia kopii zapasowej maszyny wirtualnej platformy Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: kopii zapasowej maszyny wirtualnej. Tworzenie kopii zapasowej maszyny wirtualnej; Kopia zapasowa i odzyskiwanie po awarii; kopii zapasowej maszyny wirtualnej
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a>Tworzenie kopii zapasowej maszyn wirtualnych platformy Azure (klasyczny portal)
> [!div class="op_single_selector"]
> * [Wykonaj kopię zapasową magazynu usług tooRecovery maszyny wirtualne](backup-azure-arm-vms.md)
> * [Wykonaj kopię zapasową magazynu tooBackup maszyny wirtualne](backup-azure-vms.md)
>
>

Ten artykuł zawiera hello procedur tworzenia kopii zapasowych w magazynie kopii zapasowej tooa wdrożone w klasycznej maszyny wirtualnej platformy Azure (VM). Istnieje kilka zadań, które należy tootake care z przed utworzeniem kopii zapasowej maszyny wirtualnej platformy Azure. Jeśli jeszcze tak, pełną hello [wymagania wstępne](backup-azure-vms-prepare.md) tooprepare środowiska do tworzenia kopii zapasowych maszyn wirtualnych.

Aby uzyskać dodatkowe informacje, zobacz artykuły hello na [planowania infrastruktury kopii zapasowych maszyn wirtualnych na platformie Azure](backup-azure-vms-introduction.md) i [maszyn wirtualnych platformy Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Magazyn kopii zapasowych może chronić tylko wdrożone w klasycznej maszyn wirtualnych. Nie można chronić wdrożonych przez Menedżera zasobów maszyn wirtualnych w magazynie kopii zapasowej. Zobacz [kopii zapasowych maszyn wirtualnych tooRecovery usług magazynu](backup-azure-arm-vms.md) szczegółowe informacje na temat pracy z usług odzyskiwania magazynów.
>
>

Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure obejmuje trzy kroki klucza:

![Trzy kroki tooback zapasowej maszyny Wirtualnej platformy Azure IaaS](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> Tworzenie kopii zapasowych maszyn wirtualnych jest procesem lokalnym. Nie można utworzyć kopii zapasowych maszyn wirtualnych w jeden region tooa magazyn kopii zapasowych w innym regionie. Dlatego należy utworzyć magazyn kopii zapasowych w każdym regionie Azure, gdy istnieją maszyny wirtualne, które zostaną umieszczone w kopii zapasowej.
>
> [!IMPORTANT]
> Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

## <a name="step-1---discover-azure-virtual-machines"></a>Krok 1 — odnajdywanie maszyn wirtualnych platformy Azure
tooensure wszelkie nową subskrypcję dodano toohello maszynach wirtualnych (VM) są identyfikowane przed zarejestrowaniem, uruchom proces wykrywania hello. kwerendy procesu Hello Azure hello listę maszyn wirtualnych w subskrypcji hello, wraz z dodatkowymi informacjami, takie jak nazwa usługi w chmurze hello i hello regionu.

1. Zaloguj się toohello [klasyczny portal](http://manage.windowsazure.com/)
2. Na liście hello usług platformy Azure, kliknij **usług odzyskiwania** tooopen hello lista magazynów kopii zapasowych i odzyskiwania lokacji.
    ![Otwórz magazyn listy](./media/backup-azure-vms/choose-vault-list.png)
3. Na liście hello magazyny kopii zapasowych wybierz tooback magazynu hello zapasowej maszyny Wirtualnej.

    Jeśli jest to nowy portal hello magazynu otwiera toohello **Szybki Start** strony.

    ![Otwórz zarejestrowane elementy menu](./media/backup-azure-vms/vault-quick-start.png)

    Jeśli wcześniej skonfigurowano Magazyn hello, hello portal otwiera menu toohello ostatnio używane.
4. W menu magazynu hello (u góry hello hello strony), kliknij **zarejestrowane elementy**.

    ![Otwórz zarejestrowane elementy menu](./media/backup-azure-vms/vault-menu.png)
5. Z hello **typu** menu, wybierz opcję **maszyny wirtualnej Azure**.

    ![Wybieranie obciążenia](./media/backup-azure-vms/discovery-select-workload.png)
6. Kliknij przycisk **ODNAJDOWANIA** u dołu hello hello strony.
    ![Przycisk Odnajdź](./media/backup-azure-vms/discover-button-only.png)

    Hello proces odnajdowania może zająć kilka minut hello maszyny wirtualne są wyszczególniane. Brak powiadomienie u dołu hello ekranu hello, który informuje o tym, że proces hello jest uruchomiony.

    ![Odnajdywanie maszyn wirtualnych](./media/backup-azure-vms/discovering-vms.png)

    Witaj powiadomienie ulega zmianie po zakończeniu procesu hello. Jeśli proces odnajdywania hello nie znaleziono maszyn wirtualnych hello, najpierw upewnij się, że istnieje hello maszyn wirtualnych. Jeśli istnieje hello maszyn wirtualnych, upewnij się, hello maszyny wirtualne są w hello sam region jako hello magazynu kopii zapasowych. Jeśli hello maszyn wirtualnych istnieją i są w tym samym regionie Witaj, upewnij się, że hello maszyny wirtualne nie są już zarejestrowane tooa magazynu kopii zapasowych. Jeśli maszyna wirtualna jest przypisany tooa magazynu kopii zapasowych nie jest magazynów kopii zapasowych tooother dostępne toobe przypisane.

    ![Odnajdywanie zostało zakończone](./media/backup-azure-vms/discovery-complete.png)

    Po hello nowe elementy zostały odnalezione, przejdź tooStep 2 i zarejestruj maszyny wirtualne.

## <a name="step-2---register-azure-virtual-machines"></a>Krok 2 — rejestrowanie maszyn wirtualnych platformy Azure
Zarejestruj tooassociate maszyny wirtualnej platformy Azure za pomocą hello usługi Kopia zapasowa Azure. Jest to zazwyczaj jednorazowe działania.

1. Przejdź toohello magazynu kopii zapasowych w obszarze **usług odzyskiwania** w hello portalu Azure, a następnie kliknij przycisk **zarejestrowane elementy**.
2. Wybierz **maszyny wirtualnej Azure** z menu rozwijanego hello.

    ![Wybieranie obciążenia](./media/backup-azure-vms/discovery-select-workload.png)
3. Kliknij przycisk **ZAREJESTROWAĆ** u dołu hello hello strony.
    ![Przycisk Zarejestruj](./media/backup-azure-vms/register-button-only.png)
4. W hello **Zarejestruj elementy** menu skrótów, wybierz hello maszyn wirtualnych, które mają tooregister. Jeśli istnieje co najmniej dwie maszyny wirtualne z hello takie same nazwy, użyj toodistinguish usługi chmury hello między nimi.

   > [!TIP]
   > W tym samym czasie można zarejestrować wiele maszyn wirtualnych.
   >
   >

    Zadanie jest tworzone dla każdej maszyny wirtualnej, która zostanie wybrana.
5. Kliknij przycisk **zadania** w hello powiadomień toogo toohello **zadania** strony.

    ![Rejestrowanie zadania](./media/backup-azure-vms/register-create-job.png)

    Maszyna wirtualna Hello pojawia się również hello liście zarejestrowanych elementów wraz ze stanu hello hello rejestracji operacji.

    ![Rejestrowanie — stan 1](./media/backup-azure-vms/register-status01.png)

    Po zakończeniu operacji hello hello stan zmienia się tooreflect hello *zarejestrowany* stanu.

    ![Rejestrowanie — stan 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a>Krok 3 — ochrona maszyn wirtualnych platformy Azure
Teraz można skonfigurować zasady tworzenia kopii zapasowej i przechowywania hello maszyny wirtualnej. Wiele maszyn wirtualnych mogą być chronione przy użyciu pojedynczej chronić akcji.

Azure magazyny kopii zapasowych utworzonych po 2015 może pochodzić z domyślnych zasad wbudowany w magazynie hello. Ta zasada domyślna zawiera zachowanie domyślne, 30 dni i harmonogram tworzenia kopii zapasowych raz dziennie.

1. Przejdź toohello magazynu kopii zapasowych w obszarze **usług odzyskiwania** w hello portalu Azure, a następnie kliknij przycisk **zarejestrowane elementy**.
2. Wybierz **maszyny wirtualnej Azure** z menu rozwijanego hello.

    ![Wybieranie obciążenia w portalu](./media/backup-azure-vms/select-workload.png)
3. Kliknij przycisk **Chroń** u dołu hello hello strony.

    Witaj **Kreator ochrony elementów** pojawi się. Kreator Hello wyświetla tylko maszyny wirtualne, które są zarejestrowane i nie są chronione. Wybierz hello maszyn wirtualnych, które mają tooprotect.

    Jeśli istnieje co najmniej dwie maszyny wirtualne z hello takie same nazwy, użyj toodistinguish usługi chmury hello między maszynami wirtualnymi hello.

   > [!TIP]
   > Można chronić wiele maszyn wirtualnych w tym samym czasie.
   >
   >

    ![Konfigurowanie ochrony w dużej skali](./media/backup-azure-vms/protect-at-scale.png)

4. Wybierz **harmonogram tworzenia kopii zapasowych** tooback zapasowych hello maszyn wirtualnych, które zostały wybrane. Można wybierać z istniejącego zestawu zasad lub zdefiniuj nowy.

    Z jednymi zasadami tworzenia kopii zapasowych może być skojarzonych wiele maszyn wirtualnych. Jednak hello maszyny wirtualnej może być skojarzony tylko z jedną zasadę na dowolnym etapie w czasie.

    ![Ochrona za pomocą nowych zasad](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > Zasady tworzenia kopii zapasowych obejmują schemat przechowywania hello zaplanowanych kopii zapasowych. W przypadku wybrania istniejących zasad tworzenia kopii zapasowej nie można zmodyfikować opcje przechowywania hello w hello następnego kroku.
   >
   >

5. Wybierz **zakres przechowywania** tooassociate z hello kopii zapasowych.

    ![Chroń za pomocą elastycznych przechowywania](./media/backup-azure-vms/policy-retention.png)

    Zasady przechowywania określa hello czas przechowywania kopii zapasowej. Można określić różne zasady przechowywania na podstawie hello tworzenia kopii zapasowej. Na przykład punktu kopii zapasowej pobierane raz dziennie (która służy jako punkt odzyskiwania operacyjne) mogą zostać zachowane przez 90 dni. Z kolei toobe przechowywane przez wiele miesięcy lub lat. może być konieczne punktu kopii zapasowej wykonywaną na końcu hello co kwartał (na potrzeby inspekcji).

    ![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/long-term-retention.png)

    W tym obrazie przykładzie:

   * **Zasady przechowywania codziennych**: kopii zapasowych wykonanych codziennie są przechowywane przez 30 dni.
   * **Co tydzień zasady przechowywania**: kopii zapasowych wykonanych co tydzień w niedzielę zostaną zachowane w celu 104 tygodni.
   * **Miesięczne zasady przechowywania**: kopie zapasowe wykonane w hello niedziela ostatniego dnia każdego miesiąca są zachowywane przez 120 miesięcy.
   * **Zasady przechowywania corocznych**: kopie zapasowe wykonane w hello Pierwsza niedziela co stycznia zostaną zachowane w celu 99 lat.

     Zadanie tworzenia zasad ochrony hello tooconfigure i skojarz hello maszyn wirtualnych toothat zasad dla każdej maszyny wirtualnej, która zostanie wybrana.
6. Lista hello tooview **konfiguracji ochrony** zadań, z menu magazynów hello, kliknij przycisk **zadania** i wybierz **konfiguracji ochrony** z hello **operacji**  filtru.

    ![Zadanie konfigurowania ochrony](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a>Początkowa kopia zapasowa
Gdy maszyna wirtualna hello jest chroniona za pomocą zasad, jest wyświetlane w obszarze hello **chronione elementy** kartę ze stanem hello *chroniona — (oczekiwanie początkowa kopia zapasowa)*. Domyślnie pierwszą zaplanowaną kopią zapasową hello jest hello *początkowa kopia zapasowa*.

tootrigger hello tworzenia początkowej kopii zapasowej natychmiast po skonfigurowaniu ochrony:

1. U dołu hello hello **chronione elementy** kliknij przycisk **Utwórz kopię zapasową teraz**.

    Hello usługi Azure Backup tworzy zadanie tworzenia kopii zapasowej hello początkowej operacji tworzenia kopii zapasowej.
2. Kliknij przycisk hello **zadania** kartę tooview hello listy zadań.

    ![Tworzenie kopii zapasowej w toku](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> Podczas operacji tworzenia kopii zapasowej hello hello usługi Kopia zapasowa Azure problemy z rozszerzeniem kopii zapasowej polecenia toohello w każdej tooflush maszyny wirtualnej, wszystkie zadania zapisu i migawki spójne.
>
>

Po zakończeniu tworzenia początkowej kopii zapasowej hello, stan hello hello maszyny wirtualnej w hello **chronione elementy** jest karta *chronione*.

![Kopia zapasowa maszyny wirtualnej jest tworzona z punktem odzyskiwania](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a>Wyświetlanie stanu kopii zapasowej i szczegóły
Gdy chroniony, liczba maszyn wirtualnych hello również wzrost hello **pulpitu nawigacyjnego** strony podsumowania. Hello **pulpitu nawigacyjnego** strona zawiera również hello numer zadania z ostatnich 24 godzin, które były hello *pomyślnie*, ma *nie powiodło się*i są *w toku*. Na powitania **zadania** Użyj hello **stan**, **operacji**, lub **z** i **do** toofilter menu Witaj zadania.

![Stan tworzenia kopii zapasowej na stronie pulpitu nawigacyjnego](./media/backup-azure-vms/dashboard-protectedvms.png)

Wartości na pulpicie nawigacyjnym hello są odświeżane co 24 godziny.

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami
Jeśli wystąpiły problemy podczas tworzenia kopii zapasowej maszyny wirtualnej przyjrzeć się hello [maszyny Wirtualnej artykuł dotyczący rozwiązywania problemów](backup-azure-vms-troubleshoot.md) Aby uzyskać pomoc.

## <a name="next-steps"></a>Następne kroki
* [Monitorowanie maszyn wirtualnych i zarządzanie nimi](backup-azure-manage-vms.md)
* [Przywracanie maszyn wirtualnych](backup-azure-restore-vms.md)
