---
title: aaaStorSimple administracji Snapshot Manager | Dokumentacja firmy Microsoft
description: "Zawiera omówienie i linki toomore informacji na temat zadań administracyjnych w rozwiązaniu StorSimple Snapshot Manager i przepływów pracy."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>Użyj programu StorSimple Snapshot Manager tooadminister rozwiązania StorSimple

## <a name="overview"></a>Omówienie
StorSimple Snapshot Manager jest przystawką Microsoft Management Console (MMC), która ułatwia ochronę danych i zarządzania kopiami zapasowymi w środowisku Microsoft Azure StorSimple. StorSimple Snapshot Manager można zarządzać danych Microsoft Azure StorSimple w centrum danych hello i w chmurze hello jako pojedynczy magazyn zintegrowanego rozwiązania, w związku z tym uproszczeniu procesów tworzenia kopii zapasowej i zmniejszenie kosztów.

Witaj StorSimple Snapshot Manager centralną konsolę zarządzania umożliwia toocreate spójny, w momencie tworzenia kopii zapasowej kopii lokalnej i danych w chmurze. Na przykład można użyć konsoli hello:

* Konfigurowanie, tworzenie kopii zapasowej i usuwanie woluminów.
* Skonfiguruj wolumin tooensure grupy, którego kopię zapasową danych jest spójne z aplikacjami.
* Zarządzanie zasad tworzenia kopii zapasowych, dzięki czemu jest wykonywana kopia zapasowa danych na uprzednio określonym harmonogramem.
* Tworzenie niezależnych kopii danych, który może być przechowywane w chmurze hello i używanych na potrzeby odzyskiwania po awarii.

Ten artykuł zawiera tootutorials łącza, które opisują StorSimple Snapshot Manager i w jaki sposób toouse on toocomplete zadań administracyjnych i przepływów pracy.

* Aby uzyskać więcej informacji o składnikach programu StorSimple Snapshot Manager i architektury, zobacz [co to jest StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md) 
* toodownload StorSimple Snapshot Manager Przejdź zbyt[strony pobierania programu StorSimple Snapshot Manager hello](https://www.microsoft.com/download/details.aspx?id=44220).
* Dotyczące procedur wdrażania StorSimple Snapshot Manager można przejść za[wdrażanie StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).

> [!NOTE]
> Nie można użyć toomanage StorSimple Snapshot Manager Microsoft Azure StorSimple wirtualnego tablic (znanej także jako StorSimple lokalnego urządzenia wirtualnego).


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>Zadania programu StorSimple Snapshot Manager i przepływów pracy
Można użyć hello toomonitor StorSimple Snapshot Manager i zarządzanie bieżących, zaplanowane i zakończonych zadań tworzenia kopii zapasowej. Ponadto StorSimple Snapshot Manager udostępnia katalog się too64 ukończyć tworzenia kopii zapasowych. Można użyć toofind katalogu hello i Przywracanie woluminów lub poszczególnych plików. 

| Jeśli chcesz tooDO ta... | UŻYJ TEGO SAMOUCZKA... |
|:--- |:--- |
| Dowiedz się więcej o StorSimple Snapshot Manager |[Co to jest StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md) |
| Instalowanie programu StorSimple Snapshot Manager<br>Ponowne zainstalowanie programu StorSimple Snapshot Manager<br>Usuń StorSimple Snapshot Manager |[Wdrażanie programu StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md) |
| Użyj StorSimple Snapshot Manager menu i funkcje:<ul><li>Pasek menu</li><li>Pasek narzędzi</li><li>Okienko zakresu</li><li>W okienku wyników</li><li>W okienku Akcje</li><li>Skróty i nawigacji klawiatury</li></ul> |[Interfejs użytkownika programu StorSimple Snapshot Manager](storsimple-use-snapshot-manager.md) |
| Użyj hello uwzględnione programu StorSimple Snapshot Manager wspólne funkcje programu MMC:<ul><li>Widok</li><li>Nowe okno w tym miejscu</li><li>Odśwież</li><li>Wyeksportuj listę</li><li>Pomoc</li></ul> |[Użyj hello MMC menu Akcje programu StorSimple Snapshot Manager](storsimple-snapshot-manager-mmc-menu.md) |
| Dodaj lub Zastąp urządzenia<br>Podłącz urządzenie<br>Sprawdź importowany woluminu grup<br>Odśwież połączonych urządzeń<br>Uwierzytelniania urządzenia<br>Wyświetl szczegóły urządzenia<br>Usuwanie konfiguracji urządzenia<br>Zmień hasło urządzenia<br>Zastąp urządzenia nie powiodło się<br> |[Użyj tooconnect StorSimple Snapshot Manager i zarządzanie urządzeniami StorSimple](storsimple-snapshot-manager-manage-devices.md) |
| Zainstalować woluminów<br>Wyświetlanie informacji o woluminach<br>Usuwanie woluminu<br>Skanuj woluminów<br>Konfigurowanie i tworzenie kopii zapasowej woluminu podstawowego<br>Konfigurowanie i kopii zapasowej woluminu dublowanego dynamiczne |[Użyj tooview StorSimple Snapshot Manager i zarządzanie woluminami](storsimple-snapshot-manager-manage-volumes.md) |
| Wyświetlanie grup woluminu<br>Utwórz grupę woluminu<br>Tworzenie kopii zapasowej grupy woluminu<br>Edytowanie grupy woluminu<br>Usuwanie grupy woluminu |[Użyj toocreate StorSimple Snapshot Manager i Zarządzaj grupami woluminu](storsimple-snapshot-manager-manage-volume-groups.md) |
| Tworzenie zasad tworzenia kopii zapasowej <br>Edytowanie zasad tworzenia kopii zapasowej<br>Usuń zasady tworzenia kopii zapasowej |[Użyj toocreate StorSimple Snapshot Manager i zarządzanie zasadami tworzenia kopii zapasowej](storsimple-snapshot-manager-manage-backup-policies.md) |
| Wyświetl i zarządzaj nimi zaplanowanych zadań kopii zapasowej<br>Wyświetl i zarządzaj nimi ostatnich zadań tworzenia kopii zapasowej<br>Wyświetl i zarządzaj nimi uruchomionych obecnie zadań tworzenia kopii zapasowej |[Użyj tooview StorSimple Snapshot Manager i zarządzanie nimi zadania tworzenia kopii zapasowej](storsimple-snapshot-manager-manage-backup-jobs.md) |
| Przywracanie woluminu<br>Klonowanie woluminu lub grupy woluminu<br>Usuwanie kopii zapasowej<br>Odzyskiwanie pliku<br>Przywracanie bazy danych programu StorSimple Snapshot Manager hello |[Katalog kopii zapasowej hello toomanage Użyj StorSimple Snapshot Manager](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>Następne kroki
[Pobieranie programu StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220).

