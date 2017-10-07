---
title: "aaaView StorSimple zadania i zarządzać nimi | Dokumentacja firmy Microsoft"
description: "Zawiera opis strony zadania usługi Menedżer StorSimple hello i w jaki sposób toouse on tootrack ostatnie, bieżących i zaplanowanych zadań tworzenia kopii zapasowej."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a>Użyj tooview usługi Menedżer StorSimple hello zadania i zarządzać nimi StorSimple
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Omówienie
Witaj **zadania** strona zawiera pojedynczy portalu centralnej do przeglądania i zarządzania zadaniami, które zostały uruchomione na urządzeniach podłączony tooyour usługi Menedżer StorSimple. Można wyświetlić zadań zaplanowanych, uruchomionych, została zakończona i nie powiodło się dla wielu urządzeń. Wyniki są prezentowane w formie tabeli. 

![Strona zadania](./media/storsimple-manage-jobs/HCS_JobsPage.png)

Można szybko znaleźć hello zadania, które są zainteresowani przez filtrowanie w polach, takich jak:

* **Stan** — zadania może być uruchomiony, zaplanowane, nie powiodło się, ukończonych, anulowanie lub anulowane.
* **Typ** — zadania mogą być tworzone w wyniku zaplanowanego lub kopii zapasowej na żądanie (**wykonać kopii zapasowej**), klonowanie, przywracania urządzenia lub operacji aktualizacji.
* **Urządzenia** — zadań są inicjowane na niektórych usługi tooyour podłączonych urządzeń.
* **Od i do** — zadania mogą być filtrowane na podstawie hello zakres dat i godzin.

Witaj odfiltrowanych zadań następnie wyszczególniono na podstawie hello hello następujące atrybuty:

* **Typ** — kopii zapasowej, sklonowany, przywracania, pracy awaryjnej lub aktualizacji.
* **Stan** — uruchomiona, zaplanowane, nie powiodło się, ukończone, anulowanie lub anulowane.
* **Jednostka** — hello zadań można skojarzyć z woluminu, zasad tworzenia kopii zapasowej lub urządzeniu. Zadanie klonowania jest skojarzony z woluminem, zaplanowane zadanie tworzenia kopii zapasowej jest skojarzone z zasadami tworzenia kopii zapasowej. Zadania urządzenia jest tworzony w wyniku odzyskiwania awaryjnego (DR) lub operacji przywracania.
* **Urządzenie** — Witaj nazwa hello urządzenia, na którym hello zadanie zostało uruchomione.
* **Rozpoczęto na** — Witaj czas uruchomienia zadania hello.
* **Postęp** — Witaj procentu ukończenia uruchomionego zadania. Zadanie zostało ukończone, aby uzyskać to zawsze być 100%.

Witaj listy zadań są odświeżane co 30 sekund.

Można wykonywać następujące zadania związane z akcji na tej stronie powitania:

* Wyświetlanie szczegółów zadania
* Anulowanie zadania

## <a name="view-job-details"></a>Wyświetlanie szczegółów zadania
Wykonaj hello poniższe kroki tooview hello informacje wszystkie zadania.

#### <a name="tooview-job-details"></a>Szczegóły zadania tooview
1. Na powitania **zadania** strony, wyświetlania zadań hello są zainteresowani, uruchamiając zapytanie o odpowiednie filtry. Można wyszukiwać ukończone, uruchomiona lub anulowane zadania.
2. Wybierz zadanie.
3. U dołu hello hello strony, kliknij przycisk **szczegóły**.
4. W hello **szczegóły zadania tworzenia kopii zapasowej** okno dialogowe, można wyświetlić stan hello, szczegóły statystyk czasu i statystyki danych.

## <a name="cancel-a-job"></a>Anulowanie zadania
Wykonaj następujące kroki toocancel wykonywanym zadaniem hello.

### <a name="toocancel-a-job"></a>toocancel zadania
1. Na powitania **zadania** strony, wyświetlania zadań uruchomionych hello mają toocancel, uruchamiając zapytanie o odpowiednie filtry.
2. Wybierz zadanie hello.
3. U dołu hello hello strony, kliknij przycisk **anulować**.
4. Po wyświetleniu monitu o potwierdzenie kliknij przycisk **Tak**.

To zadanie jest teraz anulowane.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Zarządzanie zasadami tworzenia kopii zapasowej StorSimple](storsimple-manage-backup-policies.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

