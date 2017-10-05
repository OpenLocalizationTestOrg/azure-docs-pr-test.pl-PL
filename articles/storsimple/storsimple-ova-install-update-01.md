---
title: Instalowanie aktualizacji w macierzy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "Informacje dotyczące używania interfejsu użytkownika sieci web tablicy wirtualnego StorSimple do stosowania aktualizacji za pomocą portalu i poprawki — metoda"
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
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Instalowanie aktualizacji na tablica wirtualnego StorSimple
## <a name="overview"></a>Omówienie
W tym artykule opisano kroki wymagane do zainstalowania aktualizacji na tablica wirtualnego StorSimple za pośrednictwem lokalnego interfejsu użytkownika sieci web i za pośrednictwem klasycznego portalu Azure. Należy zastosować aktualizacje oprogramowania lub poprawek, aby zapewnić aktualność tablica wirtualne StorSimple. 

Należy pamiętać, polegające na zainstalowanie aktualizacji lub poprawki ponownym uruchomieniu urządzenia. Biorąc pod uwagę, że tablica wirtualne StorSimple jest urządzeniem jeden węzeł, wszystkie operacje We/Wy w toku jest zakłócona i urządzenia napotyka przestoju. 

Przed zainstalowaniem aktualizacji zalecamy wykonanie woluminy lub udziały w trybie offline na hoście pierwszy, a następnie urządzenia. Pozwala to zmniejszyć możliwości uszkodzenie danych.

> [!IMPORTANT]
> Jeśli używasz Update 0.1 lub GA wersje oprogramowania, należy użyć metody poprawek za pomocą lokalnego interfejsu użytkownika sieci web do zainstalowania update 0.3. Jeśli używasz wersji Update 0.2, zaleca się zainstalowanie aktualizacji za pośrednictwem klasycznego portalu Azure.
> 
> 

## <a name="use-the-local-web-ui"></a>Użyj lokalnego interfejsu użytkownika sieci web
Istnieją dwa kroki, korzystając z lokalnego interfejsu użytkownika sieci web:

* Pobieranie aktualizacji lub poprawek
* Zainstalowanie aktualizacji lub poprawek

### <a name="download-the-update-or-the-hotfix"></a>Pobieranie aktualizacji lub poprawek
Wykonaj następujące kroki, aby pobrać aktualizację oprogramowania z Wykazu usługi Microsoft Update.

#### <a name="to-download-the-update-or-the-hotfix"></a>Aby pobrać aktualizacji lub poprawek
1. Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Jeśli po raz pierwszy używasz Wykazu usługi Microsoft Update na danym komputerze, po wyświetleniu monitu o zainstalowanie dodatku Wykazu usługi Microsoft Update kliknij pozycję **Zainstaluj**.
3. W polu wyszukiwania z wykazu usługi Microsoft Update wprowadź numer bazy wiedzy Knowledge Base (KB) poprawki, którą chcesz pobrać. Wprowadź **3182061** aktualizacja 0.3, a następnie kliknij przycisk **wyszukiwania**.
   
    Poprawka zostanie wyświetlona na liście, na przykład **StorSimple wirtualnej tablicy Update 0.3**.
   
    ![Przeszukiwanie wykazu](./media/storsimple-ova-install-update-01/download1.png)
4. Kliknij pozycję **Dodaj**. Aktualizacja zostanie dodana do koszyka.
5. Kliknij pozycję **Wyświetl koszyk**.
6. Kliknij pozycję **Pobierz**. Określ lokalizację lokalną, do której mają trafiać pobrane pliki, albo **przejdź** do takiej lokalizacji. Aktualizacje zostaną pobrane do wskazanej lokalizacji i umieszczone w podfolderze o nazwie takiej samej jak aktualizacja. Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.
7. Otwórz skopiowany folder, plik pakietu autonomicznego aktualizacji firmy Microsoft powinna zostać wyświetlona `WindowsTH-KB3011067-x64`. Ten plik służy do instalowania aktualizacji lub poprawek.

### <a name="install-the-update-or-the-hotfix"></a>Zainstalowanie aktualizacji lub poprawek
Przed instalacją aktualizacji lub poprawki upewnij się, że aktualizacja lub poprawka pobierane lokalnie na hoście lub dostępny za pośrednictwem udziału sieciowego. 

Ta metoda umożliwia instalowanie aktualizacji na urządzeniu z systemem GA lub zaktualizuj 0,1 wersje oprogramowania. Ta procedura może zająć mniej niż 2 minut. Wykonaj poniższe kroki, aby zainstalować aktualizacja lub poprawka.

#### <a name="to-install-the-update-or-the-hotfix"></a>Do zainstalowania aktualizacji lub poprawek
1. W lokalnej sieci web interfejsu użytkownika, przejdź do **konserwacji** > **aktualizacji oprogramowania**.
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update1m.png)
2. W **ścieżka pliku aktualizacji**, wprowadź nazwę pliku dla aktualizacji lub poprawek. Możesz również przejść do lokalizacji pliku instalacyjnego aktualizacja lub poprawka umieszczony w udziale sieciowym. Kliknij przycisk **Zastosuj**.
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update2m.png)
3. Zostanie wyświetlone ostrzeżenie. Biorąc pod uwagę te to urządzenie jednego węzła, po zastosowaniu aktualizacji, ponownym uruchomieniu urządzenia i brak przestojów. Kliknij ikonę znacznika wyboru.
   
   ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update3m.png)
4. Aktualizacja zostanie uruchomiony. Po pomyślnym zaktualizowaniu urządzenia ponownego uruchomienia. Lokalnego interfejsu użytkownika nie jest dostępny w tym przedziale czasu.
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update5m.png)
5. Po ponownym uruchomieniu komputera, zostają przeniesieni do **Zaloguj** strony. Aby zweryfikować, że oprogramowanie urządzenia został zaktualizowany w lokalnej sieci web interfejsu użytkownika, przejdź do **konserwacji** > **aktualizacji oprogramowania**. Wersja oprogramowania wyświetlane **10.0.0.0.0.10288.0** for Update 0.3.
   
   > [!NOTE]
   > Firma Microsoft raport wersji oprogramowania w sposób nieco inne w lokalnym interfejsu użytkownika sieci web i klasycznego portalu Azure. Na przykład raporty lokalnego interfejsu użytkownika sieci web **10.0.0.0.0.10288** i Azure raporty portalu klasycznego **10.0.10288.0** dla tej samej wersji. 
   > 
   > 
   
    ![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a>Użyj klasycznego portalu Azure
Uruchomiona Update 0.2, zaleca się zainstalowanie aktualizacji za pośrednictwem klasycznego portalu Azure. Procedury portalu wymaga od użytkownika skanowania, Pobierz i zainstaluj aktualizacje. Ta procedura trwa około 7 minut do wykonania. Wykonaj poniższe kroki, aby zainstalować aktualizacja lub poprawka.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Po zakończeniu instalacji (co wskazuje stan zadania w skali 100%), przejdź do **urządzenia > konserwacja > aktualizacji oprogramowania**. Wersja oprogramowania wyświetlane powinna mieć 10.0.10288.0.

![aktualizowanie urządzenia](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

