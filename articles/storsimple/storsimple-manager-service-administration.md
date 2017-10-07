---
title: aaaStorSimple Administracja service Manager | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak urządzenia StorSimple przy użyciu hello usługi Menedżer StorSimple w toomanage hello klasycznego portalu Azure."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2586582e-d85c-42e1-afb3-be734c1c0461
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 695ebbb785590a0e3d6de4c73125f65b16dcb776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooadminister-your-storsimple-device"></a>Użyj tooadminister usługi Menedżer StorSimple hello urządzenia StorSimple
## <a name="overview"></a>Omówienie
W tym artykule opisano hello interfejsie usługi Menedżer StorSimple, takich jak tooconnect tooit hello różne opcje dostępne i łączy się toohello konkretnych przepływów pracy, które mogą być wykonywane za pośrednictwem tego interfejsu użytkownika. W tych wskazówkach jest zastosowanie tooboth; Hello fizycznego StorSimple i hello urządzenia wirtualnego.

Po przeczytaniu tego artykułu, dowiesz się:

* Usługa Menedżera tooStorSimple Connect
* Przejdź hello interfejsu użytkownika Menedżera StorSimple
* Administrowanie urządzenia StorSimple za pośrednictwem hello usługi Menedżer StorSimple

## <a name="connect-toostorsimple-manager-service"></a>Usługa Menedżera tooStorSimple Connect
Witaj usługi Menedżer StorSimple działa na platformie Microsoft Azure i łączy toomultiple urządzenia StorSimple. Za pomocą centralnej portalu klasycznego Microsoft Azure działa w toomanage przeglądarki tych urządzeń. toohello tooconnect usługi Menedżer StorSimple hello następujące.

#### <a name="tooconnect-toohello-service"></a>Usługa toohello tooconnect
1. Przejdź za[https://manage.windowsazure.com/](https://manage.windowsazure.com/).
2. Przy użyciu poświadczeń konta Microsoft, zaloguj się na toohello Microsoft klasycznego portalu Azure (znajdujący się na powitania prawym górnym rogu okienka hello).
3. Przewiń w dół hello usługi Menedżer StorSimple hello tooaccess okienko nawigacji w lewo.

## <a name="navigate-storsimple-manager-service-ui"></a>Przejdź do usługi Menedżer StorSimple interfejsu użytkownika
Witaj hierarchii nawigacji dla usługi Menedżer StorSimple hello wyświetlone w poniższej tabeli hello interfejsu użytkownika.

* **Menedżer StorSimple** strona docelowa ma toohello interfejsu użytkownika strony poziomu usługi tooall dotyczy urządzeń w ramach usługi.
* **Urządzenia** strony przyjmuje toohello urządzenia — poziom interfejsu użytkownika strony tooa dotyczy określonego urządzenia.
* **Kontenery woluminów** strony przyjmuje toohello woluminu strony, która zawiera wszystkie woluminy hello skojarzonych z urządzeniem.

#### <a name="storsimple-manager-service-navigational-hierarchy"></a>Hierarchia nawigacji usługi Menedżer StorSimple
| Strona początkowa | Strony poziomu usługi | Stron na poziomie urządzenia | Stron na poziomie urządzenia |
| --- | --- | --- | --- |
| Usługa StorSimple Manager |Pulpit nawigacyjny usług |Pulpit nawigacyjny urządzenia | |
| Urządzenia → |Monitorowanie | | |
| Katalog kopii zapasowej |Containers→ woluminu |Woluminy | |
| Konfigurowanie (usługi) |Zasady tworzenia kopii zapasowej | | |
| Zadania |Skonfiguruj (na urządzenie) | | |
| Alerty |Konserwacji | | |

![Zobacz film](./media/storsimple-manager-service-administration/Video_icon.png) **Zobacz film**

toowatch wideo, który przeprowadzi Cię przez kolejne hello interfejsu użytkownika usługi Menedżer StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-manager-service-overview/).

## <a name="administer-storsimple-device-using-storsimple-manager-service"></a>Administrowanie urządzenia StorSimple przy użyciu usługi Menedżer StorSimple
Witaj Poniższa tabela zawiera podsumowanie wszystkich hello typowych zadań zarządzania i złożonych przepływów pracy, które mogą być wykonywane w ramach hello usługi Menedżer StorSimple interfejsu użytkownika. Te zadania są zorganizowane w oparciu hello interfejsu użytkownika strony, na których jest inicjowana.

Aby uzyskać więcej informacji na temat każdego przepływu pracy kliknij przycisk hello odpowiedniej procedury hello tabeli.

#### <a name="storsimple-manager-workflows"></a>Menedżer StorSimple przepływy pracy
| Jeśli chcesz toodo, to... | Przejdź toothis interfejsu użytkownika strony... | Użyj tej procedury. |
| --- | --- | --- |
| Tworzenie usługi</br>Usuwanie usługi</br>Pobierz klucz rejestracji usługi</br>Wygeneruj ponownie klucz rejestracji usługi |Usługa StorSimple Manager |[Wdrażanie usługi Menedżer StorSimple](storsimple-manage-service.md) |
| Klucz szyfrowania danych usługi hello zmiany</br>Wyświetl dzienniki operacji hello |Pulpit nawigacyjny → usługi Menedżer StorSimple |[Pulpit nawigacyjny usługi Menedżer StorSimple hello](storsimple-service-dashboard.md) |
| Dezaktywować urządzenie</br>Usuwanie urządzenia |Menedżer StorSimple, urządzenia usługi → |[Dezaktywuj lub usuń urządzenie](storsimple-deactivate-and-delete-device.md) |
| Dowiedz się więcej o pracy awaryjnej odzyskiwania i urządzenia po awarii</br>Urządzenie fizyczne tooa trybu failover</br>Urządzenie wirtualne tooa trybu failover</br>Odzyskiwanie po awarii ciągłości biznesowej (BCDR) |Menedżer StorSimple, urządzenia usługi → |[Tryb failover i odzyskiwania po awarii dla urządzenia StorSimple](storsimple-device-failover-disaster-recovery.md) |
| Kopie zapasowe woluminu z listy</br>Wybierz zestaw kopii zapasowych</br>Usuń zestaw kopii zapasowych |Katalog kopii zapasowej → usługi Menedżer StorSimple |[Zarządzanie kopiami zapasowymi](storsimple-manage-backup-catalog.md) |
| Klonowanie woluminu |Katalog kopii zapasowej → usługi Menedżer StorSimple |[Klonowanie woluminu](storsimple-clone-volume.md) |
| Przywróć zestaw kopii zapasowych |Katalog kopii zapasowej → usługi Menedżer StorSimple |[Przywróć zestaw kopii zapasowych](storsimple-restore-from-backup-set.md) |
| Dotyczących kont magazynu</br>Dodawanie konta magazynu</br>Edytuj konto magazynu</br>Usuwanie konta magazynu</br>Rotacją kluczy kont magazynu |Skonfiguruj → usługi Menedżer StorSimple |[Zarządzanie kontami magazynu](storsimple-manage-storage-accounts.md) |
| Informacje o szablonach przepustowości</br>Dodaj szablon przepustowości</br>Edytuj szablon przepustowości</br>Usuń szablon przepustowości</br>Użyj domyślnego szablonu przepustowości</br>Tworzenie szablonu przepustowości całodzienne, która rozpoczyna się od określonego czasu |Skonfiguruj → usługi Menedżer StorSimple |[Zarządzanie szablonami przepustowości](storsimple-manage-bandwidth-templates.md) |
| Informacje o rekordach kontroli dostępu</br>Utwórz rekord kontroli dostępu</br>Edytuj rekord kontroli dostępu</br>Usuń rekord kontroli dostępu |Skonfiguruj → usługi Menedżer StorSimple |[Zarządzanie rekordami kontroli dostępu](storsimple-manage-acrs.md) |
| Wyświetlanie szczegółów zadania</br>Anulowanie zadania |Zadania usługi → Menedżer StorSimple |[Zarządzanie zadaniami](storsimple-manage-jobs.md) |
| Otrzymywanie powiadomień o alertach</br>Zarządzanie alertami</br>Alerty dotyczące weryfikacji |Alerty usługi → Menedżer StorSimple |[Wyświetl alerty i zarządzaj nimi StorSimple](storsimple-manage-alerts.md) |
| Wyświetl połączone inicjatorów</br>Znaleźć numer seryjny urządzenia hello</br>Znajdź element docelowy hello IQN |Menedżer StorSimple usługi → urządzeń → pulpitu nawigacyjnego |[Pulpit nawigacyjny urządzenia StorSimple hello](storsimple-device-dashboard.md) |
| Tworzenie wykresów monitorowania |Menedżer StorSimple usługi → urządzeń monitorowanie → |[Monitorowanie urządzenia StorSimple](storsimple-monitor-device.md) |
| Dodaj kontener woluminów</br>Modyfikowanie kontenera woluminów</br>Usunięcie kontenera woluminów |Kontenery woluminów → urządzenia StorSimple Manager service → |[Zarządzanie kontenerami woluminów](storsimple-manage-volume-containers.md) |
| Dodawanie woluminu</br>Modyfikowanie woluminu</br>Przełącz do trybu offline woluminu</br>Usuwanie woluminu</br>Monitor woluminu |Woluminy StorSimple Menedżera usługi → urządzeń → kontenery woluminów → |[Zarządzanie woluminami](storsimple-manage-volumes.md) |
| Zmodyfikuj ustawienia urządzenia</br>Zmodyfikuj ustawienia czasu</br>Zmodyfikuj ustawienia DNS.md</br>Skonfiguruj interfejsy sieciowe |Menedżer StorSimple usługi → urządzeń skonfigurować → |[Modyfikowanie konfiguracji urządzenia dla urządzenia StorSimple](storsimple-modify-device-config.md) |
| Wyświetl ustawienia serwera proxy sieci web |Menedżer StorSimple usługi → urządzeń skonfigurować → |[Skonfiguruj serwer proxy sieci web dla urządzenia](storsimple-configure-web-proxy.md) |
| Zmodyfikuj hasło administratora urządzenia</br>Zmodyfikuj hasło programu StorSimple Snapshot Manager |Menedżer StorSimple usługi → urządzeń skonfigurować → |[Zmienianie haseł usługi StorSimple](storsimple-change-passwords.md) |
| Konfigurowanie zdalnego zarządzania |Menedżer StorSimple usługi → urządzeń skonfigurować → |[Połączyć się zdalnie tooyour urządzenia StorSimple](storsimple-remote-connect.md) |
| Konfigurowanie ustawień alertów |Menedżer StorSimple usługi → urządzeń skonfigurować → |[Wyświetl alerty i zarządzaj nimi StorSimple](storsimple-manage-alerts.md) |
| Konfigurowanie protokołu CHAP dla urządzenia StorSimple |Menedżer StorSimple usługi → urządzeń skonfigurować → |[Konfigurowanie protokołu CHAP dla urządzenia StorSimple](storsimple-configure-chap.md) |
| Dodawanie zasad kopii zapasowych</br>Dodaj lub zmodyfikuj harmonogram</br>Usuń zasady tworzenia kopii zapasowej</br>Wykonaj kopię zapasową ręczne</br>Tworzenie niestandardowych zasad tworzenia kopii zapasowej z wieloma woluminami i harmonogramów |Zasady tworzenia kopii zapasowej → urządzeń → usługi Menedżer StorSimple |[Zarządzanie zasadami tworzenia kopii zapasowych](storsimple-manage-backup-policies.md) |
| Zatrzymaj kontrolery urządzeń</br>Uruchom ponownie kontrolery urządzeń</br>Zamknij kontrolery urządzeń</br>Resetuj domyślne toofactory urządzenia</br>(Powyżej są do lokalnego urządzenia) |Menedżer StorSimple usługi → urządzeń → konserwacji |[Zarządzanie kontrolera urządzenia StorSimple](storsimple-manage-device-controller.md) |
| Dowiedz się więcej o składniki sprzętowe StorSimple</br>Monitor stanu sprzętu</br>(Powyżej są do lokalnego urządzenia) |Menedżer StorSimple usługi → urządzeń → konserwacji |[Monitor składników sprzętowych](storsimple-monitor-hardware-status.md) |
| Utwórz pakiet pomocy technicznej |Menedżer StorSimple usługi → urządzeń → konserwacji |[Tworzenie i zarządzanie nimi pakietu obsługi](storsimple-create-manage-support-package.md) |
| Instalacja aktualizacji oprogramowania |Menedżer StorSimple usługi → urządzeń → konserwacji |[Aktualizowanie urządzenia](storsimple-update-device.md) |

## <a name="next-steps"></a>Następne kroki
Jeśli występują problemy z codziennych operacji hello urządzenia StorSimple lub za pomocą dowolnego z jego składniki sprzętowe, zobacz:

* [Rozwiązywanie problemów z urządzeniem operacyjne](storsimple-troubleshoot-operational-device.md)
* [Użyj StorSimple monitorowania wskaźników](storsimple-monitoring-indicators.md)

Nie można rozwiązać problemy hello i trzeba toocreate żądania obsługi, zapoznaj się zbyt[skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-contact-microsoft-support.md).

