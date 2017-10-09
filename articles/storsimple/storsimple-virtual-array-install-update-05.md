---
title: aaaInstall aktualizacji 0,5 w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toouse hello tablicy wirtualnego StorSimple web UI tooapply aktualizacji za pomocą hello Azure portal i poprawki — metoda"
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a>Zainstaluj aktualizację 0,5 na tablica wirtualnego StorSimple

## <a name="overview"></a>Omówienie

W tym artykule opisano hello kroki wymagane tooinstall aktualizacji 0,5 na tablica wirtualnego StorSimple za pośrednictwem lokalne powitania interfejsu użytkownika sieci web i za pośrednictwem hello portalu Azure. Należy tookeep aktualizacji lub poprawek oprogramowania tooapply tablica wirtualnego StorSimple aktualne.

Przed zastosowaniem aktualizacji, zaleca się zająć hello woluminy lub udziały w tryb offline na powitania najpierw hosta i następnie hello urządzenia. Pozwala to zmniejszyć możliwości uszkodzenie danych. Po hello woluminy lub udziały są w trybie offline, należy również wziąć ręcznego tworzenia kopii zapasowej hello urządzenia.

> [!IMPORTANT]
> - Aktualizacja 0,5 odpowiada za**10.0.10290.0** wersji oprogramowania na urządzeniu. Dla informacji na temat nowości w ramach tej aktualizacji, przejdź zbyt[informacje o wersji dla aktualizacji 0,5](storsimple-virtual-array-update-05-release-notes.md).
>
> - Jeśli używasz wersji Update 0.2 lub później, zaleca się, że należy zainstalować aktualizacje hello za pomocą hello portalu Azure. Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawki hello za pośrednictwem tooinstall interfejsu użytkownika sieci web lokalnego hello aktualizacji 0,5.
>
> - Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia. Podane czy hello tablicy wirtualne StorSimple jest urządzeniem jednego węzła, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju.

## <a name="use-hello-azure-portal"></a>Użyj hello portalu Azure

Z aktualizacji, 0,2 i nowszymi wersjami, zaleca się zainstalowanie aktualizacji za pomocą hello portalu Azure. Procedura portalu Hello wymaga tooscan użytkownika hello, pobieranie i instalowanie aktualizacji hello. Ta procedura ma toocomplete około 7 minut. Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Po hello instalacja jest pełny, przejdź do pozycji tooyour usługi Menedżer StorSimple urządzenia. Wybierz **urządzeń** a następnie wybierz opcję i kliknij urządzenie powitania po zaktualizowaniu. Przejdź za**Ustawienia > Zarządzaj > aktualizacji urządzenia**. Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.10290.0**.

## <a name="use-hello-local-web-ui"></a>Użyj lokalne powitania interfejsu użytkownika sieci web

Istnieją dwa kroki, korzystając z lokalne powitania interfejsu użytkownika sieci web:

* Pobierz hello aktualizacja lub poprawka hello
* Zainstaluj hello aktualizacja lub poprawka hello

### <a name="download-hello-update-or-hello-hotfix"></a>Pobierz hello aktualizacja lub poprawka hello

Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>poprawki lub aktualizacji hello hello toodownload

1. Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.

3. W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello poprawki hello ma toodownload. Wprowadź **4021576** aktualizacja 0,5, a następnie kliknij przycisk **wyszukiwania**.
   
    Witaj poprawka zostanie wyświetlona na liście, na przykład **aktualizacji tablicy wirtualne StorSimple 0,5**.
   
    ![Przeszukiwanie wykazu](./media/storsimple-virtual-array-install-update-05/download1.png)

4. Kliknij pozycję **Pobierz**. 

5. Powinny pojawić się dwa pliki toodownload, *msu* i *cab* pliku. Pobierz każdego folderu tooa tych plików. Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.

6. Otwórz folder hello, w którym znajdują się pliki hello.
    ![Pliki w pakiecie hello](./media/storsimple-virtual-array-install-update-05/update05folder.png)

    Zobacz:
    -  Plik pakietu autonomicznego aktualizacji firmy Microsoft `WindowsTH-KB3011067-x64`. Ten plik jest używane tooupdate hello urządzenia oprogramowania.
    - Plik pakietu agenta monitorowania serwera Geneva `GenevaMonitoringAgentPackageInstaller`. Ten plik jest używany tooupdate hello monitorowania i diagnostyki usługi (MDS) agenta. Kliknij dwukrotnie plik cab hello. Msi jest wyświetlany. Wybierz hello pliku, kliknij prawym przyciskiem myszy, a następnie **wyodrębnić** hello pliku. Użyje hello _.msi_ pliku tooupdate hello agenta.

        ![Wyodrębnij plik aktualizacji agenta usług MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a>Zainstaluj hello aktualizacja lub poprawka hello

Toohello poprzednich instalacji aktualizacji lub poprawki, upewnij się, że masz hello aktualizacji lub poprawek hello pobierane lokalnie na hoście lub jest dostępny za pośrednictwem udziału sieciowego.

Użyj tej metody tooinstall aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania. Ta procedura ma mniej niż 2 minuty toocomplete. Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>poprawki lub aktualizacji hello hello tooinstall

1. W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **aktualizacji oprogramowania**.
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku hello hello aktualizacji lub poprawek hello. Można również przeglądać plik instalacyjny aktualizacji lub poprawki toohello umieszczony w udziale sieciowym. Kliknij przycisk **Zastosuj**.
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. Zostanie wyświetlone ostrzeżenie. Biorąc pod uwagę te to urządzenie jednego węzła, po zastosowaniu aktualizacji hello, ponownego uruchomienia urządzenia hello i brak przestojów. Kliknij ikonę znacznika wyboru hello.
   
   ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. Uruchamia Hello aktualizacji. Po pomyślnym zaktualizowaniu urządzenia hello ponownego uruchomienia. Witaj lokalnego interfejsu użytkownika nie jest dostępny w tym czasie trwania.
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Po zakończeniu ponownego uruchomienia hello są pobierane toohello **Zaloguj** strony. tooverify oprogramowanie urządzenia hello zaktualizowana w sieci web lokalne powitania interfejsu użytkownika, przejdź zbyt**konserwacji** > **aktualizacji oprogramowania**. Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.0.0.0.10290.0** aktualizacji 0,5.
   
   > [!NOTE]
   > Firma Microsoft raportu hello wersji oprogramowania w sposób nieco inne w lokalne powitania interfejsu użytkownika sieci web i hello portalu Azure. Na przykład Witaj raporty interfejsu użytkownika sieci web lokalnego **10.0.0.0.0.10290** i hello Azure raporty portalu **10.0.10290.0** dla hello tej samej wersji.
   
    ![aktualizowanie urządzenia](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. Witaj następnym krokiem jest tooupdate hello MDS agenta. W hello **aktualizacji oprogramowania** pozycję Przejdź toohello **ścieżka pliku aktualizacji** i Przeglądaj toohello `GenevaMonitoringAgentPackageInstaller.msi` pliku. Powtórz kroki od 2 do 4. Po ponownym uruchomieniu hello wirtualnego tablicy, zaloguj się do lokalne powitania interfejsu użytkownika sieci web.

Aktualizacja Hello jest teraz ukończona.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

