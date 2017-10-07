---
title: "aaaView tablicy wirtualnego StorSimple zadania i zarządzać nimi | Dokumentacja firmy Microsoft"
description: "Zawiera opis strony zadania usługi Menedżer StorSimple urządzenia hello i w jaki sposób toouse go tootrack ostatnie i bieżącego zadania dla hello tablicy wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>Zadania tooview usługi Menedżer StorSimple urządzenia hello na użytek hello tablicy wirtualnego StorSimple
## <a name="overview"></a>Omówienie
Witaj **zadania** bloku udostępnia pojedynczy portal centralnej do przeglądania i zarządzania zadaniami, które są uruchamiane w tablicach wirtualnych, które są połączone tooyour usługi Menedżer StorSimple urządzenia. Możesz wyświetlić zadania uruchomione, została zakończona i nie powiodło się dla wielu urządzeń wirtualnych. Wyniki są prezentowane w formie tabeli.

![Bloku zadań](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

Można szybko znaleźć hello zadania, które są zainteresowani przez filtrowanie w polach, takich jak:

* **Zakres czasu** — zadania mogą być filtrowane na podstawie hello zakres dat i godzin.
* **Urządzenia** — zadań są inicjowane w usłudze tooyour określonego urządzenia połączone. Witaj odfiltrowanych zadań następnie wyszczególniono w oparciu hello następujące atrybuty:
  
  * **Nazwa** — Nazwa zadania hello może być **wszystkie**, **kopii zapasowej**, **klonowania**, **awaryjnie**, **pobierania aktualizacji** , lub **instalowania aktualizacji**.
  * **Stan** — zadania mogą być **wszystkie**, **w toku**, **zakończyło się pomyślnie**, lub ****, lub **anulowane**.
  * **Jednostka** — Witaj zadań można skojarzyć z woluminu, udziału lub urządzenia.
  * **Urządzenie** — Witaj nazwa hello urządzenia, na którym hello zadanie zostało uruchomione.
  * **Rozpoczęto w** — Witaj czas uruchomienia zadania hello.
  * **Czas trwania** — Witaj czas trwania na zadanie (job) hello zostało uruchomione.
* **Stan** — możesz wyszukać wszystkie zadania uruchomione, zakończone lub nie powiodło się.
* **Typ zadania** — typ zadania hello mogą być wszystkie, tworzenia kopii zapasowych, przywracania, trybu failover, Pobierz aktualizacje lub instalowania aktualizacji.

Witaj listy zadań są odświeżane co 30 sekund.

## <a name="view-job-details"></a>Wyświetlanie szczegółów zadania
Wykonaj hello poniższe kroki tooview hello informacje wszystkie zadania.

#### <a name="tooview-job-details"></a>Szczegóły zadania tooview
1. Na powitania **zadania** bloku, wyświetlania zadań hello są zainteresowani, uruchamiając zapytanie o odpowiednie filtry. Można wyszukiwać zadania zakończone lub nie działają.
2. Wybierz zadanie z hello tabelarycznej listę zadań.
   
    ![Blok zadania](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. U dołu hello hello strony, kliknij przycisk **szczegóły**.
4. W hello **szczegóły** okno dialogowe, można wyświetlić stan, szczegóły i statystyk czasu. Witaj poniższej ilustracji przedstawiono przykład hello **szczegóły zadania tworzenia kopii zapasowej** okno dialogowe.
   
    ![Szczegóły zadania](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>Wykonanie zadań po hello maszyna wirtualna jest wstrzymana w funkcji hypervisor hello
Gdy zadanie jest w postęp na tablicy wirtualnego StorSimple i hello urządzenia (udostępniane w ramach funkcji hypervisor maszyny wirtualnej) jest wstrzymana na więcej niż 15 minut, zadanie hello zakończy się niepowodzeniem. To jest powodu tooyour tablicy wirtualnego StorSimple czasu są zsynchronizowane z czasem Microsoft Azure hello. 

Zobaczysz hello następujący błąd: "Godzina na urządzeniu jest zsynchronizowany z czasem Microsoft Azure hello przez ponad 15 minut. Upewnij się, że hello funkcji hypervisor i hello godzin urządzenia są synchronizowane z serwer NTP. Sprawdź, czy nie ma żadnych problemów łączności. problemy z łącznością tootroubleshoot, uruchamiania testów diagnostycznych z lokalne powitania interfejsu użytkownika urządzenia wirtualnego sieci web."

Te błędy się zadania toobackup, przywracania, aktualizacji i pracy awaryjnej. Maszyny wirtualnej jest obsługiwana w funkcji Hyper-V, maszyny hello ostatecznie synchronizuje czas z Twojej funkcji hypervisor. Gdy tak się stanie, można ponownie uruchomić zadanie.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się, jak toouse hello tooadminister interfejsu użytkownika sieci web lokalnego tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

