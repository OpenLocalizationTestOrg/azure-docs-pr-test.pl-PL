---
title: "aaaView i zarządzać zadaniami serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano bloku zadania usługi Menedżer StorSimple urządzenia hello i w jaki sposób toouse on tootrack ostatnie, bieżących i zaplanowanych zadań tworzenia kopii zapasowej."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>Użyj tooview usługi Menedżer StorSimple urządzenia hello zadania i zarządzać nimi (Update 3 i nowsze)

## <a name="overview"></a>Omówienie
Witaj **zadania** bloku zapewnia jednym portalu centralnej do wyświetlenia i zarządzanie zadaniami, które zostały uruchomione na urządzeniach połączone usługi Menedżer StorSimple urządzenia tooyour. Można wyświetlić zadań zaplanowanych, uruchomionych, zakończone, anulowane i nie powiodło się dla wielu urządzeń. Wyniki są prezentowane w formie tabeli.

![Bloku zadań](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

Można szybko znaleźć hello zadania, które są zainteresowani przez filtrowanie w polach, takich jak:

* **Stan** — zadania mogą być w toku, zakończyło się pomyślnie, anulowane, nie powiodło się, anulowanie lub zakończyło się pomyślnie z błędów.
* **Zakres czasu** — zadania mogą być filtrowane na podstawie hello zakres dat i godzin. zakresy Hello, dla których minął godzinę po 24 godzinach, ostatnie 7 dni, ostatnie 30 dni, ostatni rok lub Niestandardowa data.
* **Typ** — typ zadania hello można zaplanowanego tworzenia kopii zapasowej, ręcznego tworzenia kopii zapasowej i przywracania kopii zapasowej, Klonowanie woluminów, awaryjnie kontenery woluminów, utworzyć wolumin przypięty lokalnie, zmodyfikować woluminu, instalowania aktualizacji, zbierz dzienniki pomocy technicznej i utworzyć urządzenia chmury.
* **Urządzenia** — zadań są inicjowane na niektórych usługi tooyour podłączonych urządzeń.
  
Witaj odfiltrowanych zadań następnie wyszczególniono na podstawie hello hello następujące atrybuty:
  
* **Nazwa** — zaplanowanego tworzenia kopii zapasowej, ręcznego tworzenia kopii zapasowych, przywracania kopii zapasowej woluminu w klonowania, tryb failover kontenery woluminów tworzenia woluminu przypiętego lokalnie, zmodyfikować woluminu, instalowania aktualizacji, zbierz dzienniki pomocy technicznej lub utworzyć urządzenia chmury.
* **Stan** — uruchomiona, zakończone, anulowane, nie powiodło się, anulowanie lub ukończone z błędami.
* **Jednostka** — hello zadań można skojarzyć z woluminu, zasad tworzenia kopii zapasowej lub urządzeniu. Na przykład zadanie klonowania jest skojarzony z woluminem, zaplanowane zadanie tworzenia kopii zapasowej jest skojarzone z zasadami tworzenia kopii zapasowej. Zadania urządzenia jest tworzony w wyniku odzyskiwania awaryjnego (DR) lub operacji przywracania.
* **Urządzenie** — Witaj nazwa hello urządzenia, na którym hello zadanie zostało uruchomione.
* **Rozpoczęto w** — Witaj czas uruchomienia zadania hello.
* **Czas trwania** — hello czasu wymaganego toocomplete hello zadania.

Witaj listy zadań są odświeżane co 30 sekund.

Można wykonywać następujące zadania związane z akcji na tej stronie powitania:

* Wyświetlanie szczegółów zadania
* Anulowanie zadania

## <a name="view-job-details"></a>Wyświetlanie szczegółów zadania
Wykonaj hello poniższe kroki tooview hello informacje wszystkie zadania.

#### <a name="tooview-job-details"></a>Szczegóły zadania tooview
1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **zadania**.

2. W hello **zadania** bloku, wyświetlania zadań hello są zainteresowani, uruchamiając zapytanie o odpowiednie filtry. Można wyszukiwać ukończone, uruchomiona lub anulowane zadania.

    ![Blok zadania](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. Wybierz, a następnie kliknij zadanie.

    ![Blok zadania](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. W bloku szczegóły zadania hello można wyświetlić stan hello, szczegóły statystyk czasu i statystyki danych.
   
    ![Szczegóły zadania](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>Anulowanie zadania
Wykonaj następujące kroki toocancel wykonywanym zadaniem hello.

> [!NOTE]
> Niektóre zadania, takie jak modyfikowanie woluminu toochange hello woluminie, którego typ lub rozszerzenie woluminu, nie można anulować.


### <a name="toocancel-a-job"></a>toocancel zadania
1. Na powitania **zadania** strony, wyświetlania zadań uruchomionych hello mają toocancel, uruchamiając zapytanie o odpowiednie filtry. Wybierz zadanie hello.

2. Kliknij prawym przyciskiem myszy, w menu kontekstowym hello hello wybranego zadania tooinvoke, a następnie kliknij przycisk **anulować**.

    ![Szczegóły zadania](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**. To zadanie jest teraz anulowane.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Zarządzanie zasadami tworzenia kopii zapasowej StorSimple](storsimple-8000-manage-backup-policies-u2.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

