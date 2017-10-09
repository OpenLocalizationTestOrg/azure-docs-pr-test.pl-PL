---
title: zasady tworzenia kopii zapasowej Snapshot Manager aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje sposób toouse hello toocreate przystawki MMC programu StorSimple Snapshot Manager i zarządzanie nimi hello zasad tworzenia kopii zapasowych, które kontrolują zaplanowanych kopii zapasowych."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a>Użyj toocreate StorSimple Snapshot Manager i zarządzanie zasadami tworzenia kopii zapasowej
## <a name="overview"></a>Omówienie
Zasady tworzenia kopii zapasowej tworzy harmonogram tworzenia kopii zapasowych danych woluminu lokalnie lub w chmurze hello. Podczas tworzenia zasad tworzenia kopii zapasowej, można także określić zasady przechowywania. (Można zachować maksymalnie 64 migawki). Aby uzyskać więcej informacji na temat zasad tworzenia kopii zapasowych, zobacz [kopii zapasowej typy](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) w [z serii StorSimple 8000: rozwiązanie chmury hybrydowej](storsimple-overview.md).

Ten samouczek wyjaśnia, jak:

* Tworzenie zasad tworzenia kopii zapasowej
* Edytowanie zasad tworzenia kopii zapasowej
* Usuń zasady tworzenia kopii zapasowej

## <a name="create-a-backup-policy"></a>Tworzenie zasad tworzenia kopii zapasowej
Użyj hello następujące procedury toocreate nowych zasad tworzenia kopii zapasowej.

#### <a name="toocreate-a-backup-policy"></a>toocreate zasad tworzenia kopii zapasowej
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku kliknij prawym przyciskiem myszy **zasady tworzenia kopii zapasowej**i kliknij przycisk **zasad tworzenia kopii zapasowej**.

    ![Tworzenie zasad tworzenia kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    Witaj **utworzyć zasadę** zostanie wyświetlone okno dialogowe.

    ![Utwórz zasadę — karta Ogólne](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. Na powitania **ogólne** kartę, pełną hello następujących informacji:

   1. W hello **nazwa** polu tekstowym, wpisz nazwę zasady hello.
   2. W hello **grupy woluminu** pole tekstowe, nazwa typu hello hello woluminu grupy skojarzone z zasadą hello.
   3. Wybierz opcję **migawka lokalna** lub **migawki w chmurze**.
   4. Wybierz liczbę hello tooretain migawki. W przypadku wybrania **wszystkie**, zostaną zachowane 64 migawek (hello maksymalnej).
4. Kliknij przycisk hello **harmonogram** kartę.

    ![Utwórz zasadę — karta harmonogram](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. Na powitania **harmonogram** kartę, pełną hello następujących informacji:

   1. Kliknij przycisk hello **włączyć** pole wyboru tooschedule hello następnej kopii zapasowej.
   2. W obszarze **ustawienia**, wybierz pozycję **jeden raz**, **codzienne**, **co tydzień**, lub **miesięczne**.
   3. W hello **Start** pola tekstowego, kliknij ikonę kalendarza hello i wybierz datę rozpoczęcia.
   4. W obszarze **Zaawansowane ustawienia**, można ustawić opcjonalny powtarzania harmonogramów oraz datę zakończenia.
   5. Kliknij przycisk **OK**.

Po utworzeniu zasad tworzenia kopii zapasowej hello następujących informacji jest wyświetlana w hello **wyniki** okienka:

* **Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej.
* **Typ** — migawka lokalna i migawka w chmurze.
* **Grupy woluminu** — Witaj skojarzonych z zasadami hello grupy woluminu.
* **Przechowywania** — Witaj zachowane liczby migawek; hello maksymalna 64.
* **Utworzony** — Data hello zasada została utworzona.
* **Włączone** — czy zasada hello jest obecnie efekt: **True** wskazuje, że jest włączona; **False** wskazuje, że nie będzie obowiązywać.

## <a name="edit-a-backup-policy"></a>Edytowanie zasad tworzenia kopii zapasowej
Użyj hello następujące procedury tooedit istniejących zasad tworzenia kopii zapasowej.

#### <a name="tooedit-a-backup-policy"></a>tooedit zasad tworzenia kopii zapasowej
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij przycisk hello **zasady tworzenia kopii zapasowej** węzła. Wszystkie zasady tworzenia kopii zapasowej hello są wyświetlane w hello **wyniki** okienka.
3. Kliknij prawym przyciskiem myszy zasady hello mają tooedit, a następnie kliknij przycisk **Edytuj**.

    ![Edytowanie zasad tworzenia kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. Gdy hello **utworzyć zasadę** zostanie wyświetlone okno, wprowadź zmiany, a następnie kliknij przycisk **OK**.

## <a name="delete-a-backup-policy"></a>Usuń zasady tworzenia kopii zapasowej
Użyj hello następujące procedury toodelete zasad tworzenia kopii zapasowej.

#### <a name="toodelete-a-backup-policy"></a>toodelete zasad tworzenia kopii zapasowej
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij przycisk hello **zasady tworzenia kopii zapasowej** węzła. Wszystkie zasady tworzenia kopii zapasowej hello są wyświetlane w hello **wyniki** okienka.
3. Kliknij prawym przyciskiem myszy zasady tworzenia kopii zapasowej hello mają toodelete, a następnie kliknij przycisk **usunąć**.
4. Po wyświetleniu komunikatu potwierdzenia powitania kliknij **tak**.

    ![Zasady tworzenia kopii zapasowej potwierdzenie usunięcia](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Dowiedz się, jak za[Użyj tooview StorSimple Snapshot Manager i zarządzanie nimi zadania tworzenia kopii zapasowej](storsimple-snapshot-manager-manage-backup-jobs.md).
