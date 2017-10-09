---
title: aaaBack maszyny wirtualne platformy Azure | Dokumentacja firmy Microsoft
description: "Odnajdowanie, rejestrowania i utworzyć kopię zapasową magazynu usług odzyskiwania tooa maszyn wirtualnych platformy Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: kopii zapasowej maszyny wirtualnej. Tworzenie kopii zapasowej maszyny wirtualnej; Kopia zapasowa i odzyskiwanie po awarii; ARM kopii zapasowej maszyny wirtualnej
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a>Magazyn usług odzyskiwania tooa i wykonywanie kopii zapasowych maszyn wirtualnych platformy Azure
> [!div class="op_single_selector"]
> * [Wykonaj kopię zapasową magazynu usług tooRecovery maszyny wirtualne](backup-azure-arm-vms.md)
> * [Wykonaj kopię zapasową magazynu tooBackup maszyny wirtualne](backup-azure-vms.md)
>
>

W tym artykule szczegółowo sposób magazynu tooback się tooa maszynach wirtualnych platformy Azure (wdrożone usługi Resource Manager i wdrożone w klasycznej) usług odzyskiwania. Większość pracy hello tworzenia kopii zapasowych maszyn wirtualnych jest przygotowanie hello. Zanim można utworzyć kopię zapasową lub ochrony maszyny Wirtualnej, należy wykonać hello [wymagania wstępne](backup-azure-arm-vms-prepare.md) tooprepare środowiska z ochroną maszyn wirtualnych. Po zakończeniu hello wymagań wstępnych, można zainicjować hello operacji tworzenia kopii zapasowej tootake migawki maszyny wirtualnej.


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

Aby uzyskać więcej informacji, zobacz artykuły hello na [planowania infrastruktury kopii zapasowych maszyn wirtualnych na platformie Azure](backup-azure-vms-introduction.md) i [maszyn wirtualnych platformy Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="triggering-hello-backup-job"></a>Wyzwolenie hello zadanie tworzenia kopii zapasowej
zasady tworzenia kopii zapasowej Hello skojarzone z powitalne magazyn usług odzyskiwania i definiuje kiedy i jak często jest uruchamiana hello operacji tworzenia kopii zapasowej. Domyślnie pierwszą zaplanowaną kopią zapasową hello jest hello początkowa kopia zapasowa. Dopóki nie wystąpi hello początkowa kopia zapasowa, hello stan ostatniej kopii zapasowej na powitania **zadania tworzenia kopii zapasowej** bloku jest pokazywana jako **ostrzeżenie (początkowa kopia zapasowa oczekujących)**.

![Oczekiwanie na kopię zapasową](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

O ile nie przypada tworzenia początkowej kopii zapasowej toobegin wkrótce, zalecane jest uruchomienie **wykonaj kopię zapasową teraz**. Po uruchomieniu procedury z pulpitem nawigacyjnym magazynu hello Hello. Ta procedura służy do uruchamiania hello początkowej zadanie tworzenia kopii zapasowej po zakończeniu wszystkie wymagania wstępne. Jeśli jest już uruchomione zadanie tworzenia kopii zapasowej początkowej hello, ta procedura nie jest dostępna. Witaj skojarzonych zasad tworzenia kopii zapasowej określa hello następne zadanie tworzenia kopii zapasowej.  

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

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami
Jeśli wystąpiły problemy podczas tworzenia kopii zapasowej maszyny wirtualnej, zobacz hello [maszyny Wirtualnej artykuł dotyczący rozwiązywania problemów](backup-azure-vms-troubleshoot.md) Aby uzyskać pomoc.

## <a name="next-steps"></a>Następne kroki
Teraz, ochrony maszyny Wirtualnej, zobacz hello następujące artykuły toolearn o zadaniach zarządzania maszyny Wirtualnej i w jaki sposób toorestore maszyn wirtualnych.

* [Monitorowanie maszyn wirtualnych i zarządzanie nimi](backup-azure-manage-vms.md)
* [Przywracanie maszyn wirtualnych](backup-azure-arm-restore-vms.md)
