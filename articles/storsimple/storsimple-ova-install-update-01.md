---
title: Aktualizacje aaaInstall w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toouse hello tablicy wirtualnego StorSimple web UI tooapply aktualizacji przy użyciu metody hello portalu i poprawki"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Instalowanie aktualizacji na tablica wirtualnego StorSimple
## <a name="overview"></a>Omówienie
W tym artykule opisano hello kroki tooinstall wymagane aktualizacje na tablica wirtualnego StorSimple za pośrednictwem lokalne powitania interfejsu użytkownika sieci web i za pośrednictwem hello klasycznego portalu Azure. Należy tookeep aktualizacji lub poprawek oprogramowania tooapply tablica wirtualnego StorSimple aktualne. 

Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia. Podane czy hello tablicy wirtualne StorSimple jest urządzeniem jednego węzła, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju. 

Przed zastosowaniem aktualizacji, zaleca się zająć hello woluminy lub udziały w tryb offline na powitania najpierw hosta i następnie hello urządzenia. Pozwala to zmniejszyć możliwości uszkodzenie danych.

> [!IMPORTANT]
> Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawki hello za pośrednictwem hello lokalnej sieci web UI tooinstall update 0.3. Jeśli używasz wersji Update 0.2, zaleca się zainstalowanie aktualizacji hello za pośrednictwem hello klasycznego portalu Azure.
> 
> 

## <a name="use-hello-local-web-ui"></a>Użyj lokalne powitania interfejsu użytkownika sieci web
Istnieją dwa kroki, korzystając z lokalne powitania interfejsu użytkownika sieci web:

* Pobierz hello aktualizacja lub poprawka hello
* Zainstaluj hello aktualizacja lub poprawka hello

### <a name="download-hello-update-or-hello-hotfix"></a>Pobierz hello aktualizacja lub poprawka hello
Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>poprawki lub aktualizacji hello hello toodownload
1. Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.
3. W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello poprawki hello ma toodownload. Wprowadź **3182061** aktualizacja 0.3, a następnie kliknij przycisk **wyszukiwania**.
   
    Witaj poprawka zostanie wyświetlona na liście, na przykład **StorSimple wirtualnej tablicy Update 0.3**.
   
    ![Przeszukiwanie wykazu](./media/storsimple-ova-install-update-01/download1.png)
4. Kliknij pozycję **Dodaj**. Witaj aktualizacja została dodana toohello koszyka.
5. Kliknij pozycję **Wyświetl koszyk**.
6. Kliknij pozycję **Pobierz**. Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear. Witaj aktualizacje zostaną pobrane toohello określonej lokalizacji i umieszczane w podfolderze o hello takie same nazwy co hello update. Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.
7. Otwórz hello skopiować folder, plik pakietu autonomicznego aktualizacji firmy Microsoft powinna zostać wyświetlona `WindowsTH-KB3011067-x64`. Ten plik jest używany tooinstall hello aktualizacja lub poprawka.

### <a name="install-hello-update-or-hello-hotfix"></a>Zainstaluj hello aktualizacja lub poprawka hello
Toohello poprzednich instalacji aktualizacji lub poprawki, upewnij się, że masz hello aktualizacji lub poprawek hello pobierane lokalnie na hoście lub jest dostępny za pośrednictwem udziału sieciowego. 

Użyj tej metody tooinstall aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania. Ta procedura ma mniej niż 2 minuty toocomplete. Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>poprawki lub aktualizacji hello hello tooinstall
1. W hello lokalnego interfejsu użytkownika sieci web, przejdź do pozycji zbyt**konserwacji** > **aktualizacji oprogramowania**.
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update1m.png)
2. W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku hello hello aktualizacji lub poprawek hello. Można również przeglądać plik instalacyjny aktualizacji lub poprawki toohello umieszczony w udziale sieciowym. Kliknij przycisk **Zastosuj**.
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update2m.png)
3. Zostanie wyświetlone ostrzeżenie. Biorąc pod uwagę te to urządzenie jednego węzła, po zastosowaniu aktualizacji hello, ponownego uruchomienia urządzenia hello i brak przestojów. Kliknij ikonę znacznika wyboru hello.
   
   ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update3m.png)
4. Uruchamia Hello aktualizacji. Po pomyślnym zaktualizowaniu urządzenia hello ponownego uruchomienia. Witaj lokalnego interfejsu użytkownika nie jest dostępny w tym czasie trwania.
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update5m.png)
5. Po zakończeniu ponownego uruchomienia hello są pobierane toohello **Zaloguj** strony. tooverify oprogramowanie urządzenia hello zaktualizowana w sieci web lokalne powitania interfejsu użytkownika, przejdź zbyt**konserwacji** > **aktualizacji oprogramowania**. Wersja oprogramowania Hello wyświetlane powinna mieć **10.0.0.0.0.10288.0** for Update 0.3.
   
   > [!NOTE]
   > Firma Microsoft raportu hello wersji oprogramowania w sposób nieco inne w lokalne powitania interfejsu użytkownika sieci web i hello klasycznego portalu Azure. Na przykład Witaj raporty interfejsu użytkownika sieci web lokalnego **10.0.0.0.0.10288** i hello Azure raporty portalu klasycznego **10.0.10288.0** dla hello tej samej wersji. 
   > 
   > 
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a>Witaj Użyj klasycznego portalu Azure
Uruchomiona Update 0.2, zaleca się zainstalowanie aktualizacji za pomocą hello klasycznego portalu Azure. Procedura portalu Hello wymaga tooscan użytkownika hello, pobieranie i instalowanie aktualizacji hello. Ta procedura ma toocomplete około 7 minut. Wykonaj następujące hello kroki tooinstall hello aktualizacja lub poprawka.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Po hello instalacja została zakończona, (określone przez stan zadania w skali 100%), przejdź zbyt**urządzenia > konserwacja > aktualizacji oprogramowania**. Wersja oprogramowania Hello wyświetlane powinna mieć 10.0.10288.0.

![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

