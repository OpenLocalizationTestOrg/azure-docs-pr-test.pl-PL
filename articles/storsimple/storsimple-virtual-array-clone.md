---
title: aaaClone kopii zapasowej tablicy wirtualnego StorSimple | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooclone kopii zapasowej i odzyskiwanie pliku z macierzy wirtualne StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>Klonowanie z kopii zapasowej macierzy wirtualnego StorSimple

## <a name="overview"></a>Omówienie

W tym artykule opisano krok po kroku tooclone kopię zapasową konfiguracji udziały lub woluminy na tablica wirtualne Microsoft Azure StorSimple. Kopia zapasowa sklonowany Hello jest toorecover używanych plików usuniętych lub zostały utracone. Witaj w nim także tooperform szczegółowy opis kroków, które odzyskiwanie na poziomie elementu, na tablica wirtualnego StorSimple skonfigurowany jako serwer plików.

## <a name="clone-shares-from-a-backup-set"></a>Akcje w klonowania z zestawu kopii zapasowych

**Przed podjęciem próby tooclone udziałów, upewnij się, że masz wystarczającą ilość miejsca na powitania urządzenia toocomplete tej operacji.** tooclone z kopii zapasowej w hello [portalu Azure](https://portal.azure.com/), wykonaj następujące kroki hello.

#### <a name="tooclone-a-share"></a>tooclone udziału

1. Przeglądaj zbyt**urządzeń** bloku. Wybierz i kliknij urządzenie, a następnie kliknij przycisk **udziałów**. Wybierz udział hello, które mają tooclone, menu kontekstowe hello tooinvoke udziału powitania kliknij prawym przyciskiem myszy. Wybierz **klonowania**.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. W hello **klonowania** bloku, kliknij przycisk **kopii zapasowej > Wybierz** , a następnie hello następujące: 
   
   a.    Filtr kopii zapasowej na tym urządzeniu, na podstawie hello zakresu czasu. Możesz wybrać spośród **ostatnie 7 dni**, **w ciągu ostatnich 30 dni**, i **ciągu ostatniego roku**.
   
   b.    Zaznacz kopii zapasowej tooclone z liście hello filtrowane tworzenia kopii zapasowych, które są wyświetlane.
   
   c.    Kliknij przycisk **OK**.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. W hello **klonowania** bloku, kliknij przycisk **Target ustawienia** , a następnie hello następujące:
   
   a.    Podaj nazwę udziału. Nazwa udziału Hello musi zawierać 3-127 znaków.
   
   b.    Opcjonalnie wprowadź opis udziału sklonowany hello.
   
   c.    Nie można zmienić typu hello hello są przywracane do udziału. Udział warstwowych został sklonowany jako warstwowych a udziałem przypięty lokalnie, przypięty lokalnie.
   
   d.    pojemność Hello jest ustawiony jako rozmiar równy toohello udziału hello, które są klonowania z.
   
   e.    Przypisz administratorów powitania dla tego udziału. Po ukończeniu klonowania hello będzie właściwości udziału hello stanie toomodify za pomocą Eksploratora plików.
   
   f.    Kliknij przycisk **OK**.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Kliknij przycisk **klonowania** toostart zadania klonowania. Po zakończeniu zadania hello operacji klonowania hello rozpoczyna się i zostanie wyświetlone powiadomienie. postęp hello toomonitor w klonowania, przejdź toohello **zadania** bloku i kliknij przycisk hello tooview zadania szczegóły zadania.
5. Po pomyślnym utworzeniu hello klonowania, przejdź wstecz toohello **udziałów** bloku na urządzeniu.
6. Możesz teraz przeglądać nowego udziału sklonowany hello hello listy udziałów na urządzeniu. Udział warstwowych został sklonowany, ponieważ do warstwy a udziałem przypiętych lokalnie jako udział przypiętych lokalnie.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Klonowanie woluminów z zestawu kopii zapasowych

tooclone z kopii zapasowej w hello portalu Azure, masz tooperform kroki podobne toohello widocznych w przypadku klonowania udziału. Operacja klonowania Hello klonów hello kopii zapasowej tooa nowy wolumin na powitania tego samego urządzenia wirtualnego; Nie można sklonować tooa innego urządzenia.

#### <a name="tooclone-a-volume"></a>tooclone woluminu

1. Przeglądaj zbyt**urządzeń** bloku. Wybierz i kliknij urządzenie, a następnie kliknij przycisk **woluminów**. Wybier hello woluminów, które mają tooclone, kliknij prawym przyciskiem myszy menu kontekstowe hello hello woluminu tooinvoke. Wybierz **klonowania**.
   
   ![Klonowanie woluminu](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. W hello **klonowania** bloku, kliknij przycisk **kopii zapasowej** , a następnie hello następujące: 
   
   a.    Filtr kopii zapasowej na tym urządzeniu, na podstawie hello zakresu czasu. Możesz wybrać spośród **ostatnie 7 dni**, **w ciągu ostatnich 30 dni**, i **ciągu ostatniego roku**. 
   
   b.    Zaznacz kopii zapasowej tooclone z liście hello filtrowane tworzenia kopii zapasowych, które są wyświetlane.
   
   c.    Kliknij przycisk **OK**.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. W hello **klonowania** bloku, kliknij przycisk **docelowy wolumin ustawienia** , a następnie hello po::
   
   a. Nazwa urządzenia Hello jest wypełniane automatycznie.
   
   b. Podaj nazwę woluminu hello **sklonować woluminu**. Nazwa woluminu Hello musi zawierać znaki too127 3.
   
   c. Typ woluminu Hello jest automatycznie ustawiana toohello oryginalnego woluminu. Wolumin warstwowy został sklonowany, ponieważ do warstwy i przypięty lokalnie woluminu przypiętego lokalnie.
   
   d. Dla hello **połączone hosty**, kliknij przycisk **wybierz**.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. W hello **połączone hosty** bloku, wybierz z istniejących ACR lub Dodaj nowe ACR. tooadd ACR nowe, konieczne będzie tooprovide nazwa ACR i hosta hello IQN. Kliknij pozycję **Wybierz**.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Kliknij przycisk **klonowania** toolaunch zadania klonowania.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Po utworzeniu zadania sklonowany hello klonowania zostanie uruchomiony. Po utworzeniu klonowania hello jest wyświetlany w bloku woluminów hello na urządzeniu. Warto zauważyć, że wolumin warstwowy został sklonowany, ponieważ do warstwy woluminu przypiętego lokalnie został sklonowany jako woluminu przypiętego lokalnie.
   
   ![Klonowanie kopii zapasowej](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Gdy wolumin hello pojawi się w trybie online na powitania listę woluminów, hello wolumin jest dostępny do użycia. Na hoście inicjatora iSCSI hello Odśwież listę hello elementów docelowych w oknie właściwości inicjatora iSCSI. Nowy docelowy, który zawiera nazwę sklonowanego woluminu hello powinny być wyświetlane jako "nieaktywne" w kolumnie Stan hello.
8. Wybierz cel hello, a następnie kliknij przycisk **Connect**. Inicjatora powitania po docelowych połączonych toohello hello stan powinien zmienić się zbyt**połączony**.
9. W hello **Zarządzanie dyskami** , hello zainstalowanych woluminów wyświetlone okno pokazane na następującej ilustracji hello. Kliknij prawym przyciskiem myszy hello odnaleziony wolumin (kliknij nazwę dysku hello), a następnie kliknij przycisk **Online**.

> [!IMPORTANT]
> Podczas próby tooclone wolumin lub udział z zestawu kopii zapasowych, jeśli zadanie klonowania hello zakończy się niepowodzeniem, wolumin docelowy lub udziału nadal można tworzyć w portalu hello. Należy usunąć tego woluminu docelowego, lub udostępnianie w portalu toominimize hello wszystkie przyszłe problemy wynikające z tego elementu.
> 
> 

## <a name="item-level-recovery-ilr"></a>Odzyskiwanie na poziomie elementu (ILR)

Tej wersji wprowadzono hello odzyskiwania poziomie elementu (ILR) w macierzy wirtualnego StorSimple, skonfigurowany jako serwer plików. Funkcja Hello pozwala toodo szczegółowego odzyskiwania plików i folderów z kopii zapasowej chmury wszystkich udziałów hello na urządzeniu StorSimple hello. Ostatnie kopie zapasowe przy użyciu modelu samoobsługi może pobrać usuniętych plików.

Każdy udział ma *.backups* folder zawierający hello najnowszej kopii zapasowych. Można znaleźć żądanego kopii zapasowej toohello, skopiuj odpowiednie pliki i foldery z kopii zapasowej hello i przywrócić je. Ta funkcja eliminuje tooadministrators wywołania przywracania plików z kopii zapasowych.

1. Podczas wykonywania hello ILR, można wyświetlić hello tworzenia kopii zapasowych za pomocą Eksploratora plików. Kliknij przycisk hello określonego udziału interesujące toolook na powitania kopii zapasowej. Zobaczysz *.backups* folder utworzony w obszarze hello udziału, który przechowuje wszystkie hello kopie zapasowe. Rozwiń węzeł hello *.backups* folderu tooview hello tworzenia kopii zapasowych. Hello folder pokazuje hello widok hello całej hierarchii kopii zapasowej. Ten widok jest tworzony na żądanie i zazwyczaj trwa tylko kilka sekund toocreate.
   
   kopie zapasowe pięć ostatnich Hello są wyświetlane w ten sposób i mogą być używane tooperform poziomu elementu odzyskiwania. Witaj pięć najnowszych kopii zapasowych zawiera zarówno hello domyślny zaplanowany i hello ręcznego tworzenia kopii zapasowych.
   
   * **Zaplanowane tworzenie kopii zapasowych** jako &lt;nazwa urządzenia&gt;DailySchedule-RRRRMMDD-HHMMSS-UTC.
   * **Ręczne tworzenie kopii zapasowych** jako Ad-hoc — RRRRMMDD-HHMMSS-UTC.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Zidentyfikuj hello kopii zapasowej zawierającego hello najnowszej wersji pliku hello usunięte. Chociaż hello nazwa folderu zawiera sygnaturę czasową UTC w każdym hello poprzedzających przypadków, godzinę hello które hello utworzenia folderu jest hello rzeczywistego urządzenia uruchomieniu po hello kopii zapasowej. Użyj hello folderu sygnatury czasowej toolocate i zidentyfikować hello kopii zapasowych.

3. Zlokalizuj hello folder lub hello pliku toorestore hello kopii zapasowej, który został zidentyfikowany w poprzednim kroku hello. Należy pamiętać, że możesz jedynie wyświetlić hello pliki lub foldery, które mają uprawnienia. Jeśli nie masz dostępu do niektórych plików lub folderów, skontaktuj się z administratorem udziału. Hello administrator można użyć uprawnień udziału hello tooedit Eksplorator plików i umożliwiają dostęp toohello określonego pliku lub folderu. Jest to grupa użytkowników zamiast pojedynczego użytkownika jest zalecanym najlepszym rozwiązaniem, które hello udział administratora.

4. Skopiuj plik hello lub odpowiedni udział toohello hello folderu na serwerze plików StorSimple.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o tym, jak za[administrowania tablica wirtualnego StorSimple przy użyciu lokalne powitania interfejsu użytkownika sieci web](storsimple-ova-web-ui-admin.md).

