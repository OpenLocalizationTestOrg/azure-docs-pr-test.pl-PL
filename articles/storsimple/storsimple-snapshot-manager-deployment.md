---
title: aaaDeploy StorSimple Snapshot Manager | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodownload i zainstaluj hello StorSimple Snapshot Manager przystawki programu MMC do zarządzania funkcji ochrony i kopii zapasowej danych StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Wdrażanie hello przystawki MMC programu StorSimple Snapshot Manager

## <a name="overview"></a>Omówienie
Witaj StorSimple Snapshot Manager jest przystawki programu Microsoft Management Console (MMC), która ułatwia ochronę danych i zarządzania kopiami zapasowymi w środowisku Microsoft Azure StorSimple. StorSimple Snapshot Manager można zarządzać lokalnym Microsoft Azure StorSimple i magazynu w chmurze tak, jakby była systemu pełni zintegrowane magazynu, w związku z tym uproszczenie i przywracania kopii zapasowej i zmniejszenie kosztów. 

W tym samouczku opisano wymagania dotyczące konfiguracji, a także procedury instalowanie, usuwanie i uaktualnianie programu StorSimple Snapshot Manager.

> [!NOTE]
> * Nie można użyć toomanage StorSimple Snapshot Manager Microsoft Azure StorSimple wirtualnego tablic (znanej także jako StorSimple lokalnego urządzenia wirtualnego).
> * Jeśli planujesz tooinstall StorSimple Update 2 na urządzeniu StorSimple można się toodownload hello najnowszej wersji programu StorSimple Snapshot Manager i zainstalować ją **przed zainstalowaniem StorSimple Update 2**. Witaj najnowszej wersji programu StorSimple Snapshot Manager jest zgodne z poprzednimi wersjami i działa w przypadku wszystkich wersji wydanej programu Microsoft Azure StorSimple. Jeśli używasz hello poprzedniej wersji programu StorSimple Snapshot Manager, należy tooupdate it (nie trzeba toouninstall hello poprzedniej wersji przed zainstalowaniem nowej wersji hello).


## <a name="storsimple-snapshot-manager-installation"></a>Instalacja programu StorSimple Snapshot Manager
StorSimple Snapshot Manager można zainstalować na komputerach, na których jest uruchomiony system operacyjny Windows Server 2008 R2 z dodatkiem SP1, Windows Server 2012 lub Windows Server 2012 R2 hello. Na serwerach z systemem Windows 2008 R2 należy również zainstalować system Windows Server 2008 z dodatkiem SP1 i Windows Management Framework 3.0.

Przed zainstalowaniem lub uaktualnieniem hello StorSimple Snapshot Manager przystawkę dla hello Microsoft Management Console (MMC), upewnić się, że urządzenie Microsoft Azure StorSimple hello i serwer hosta są poprawnie skonfigurowane.

## <a name="configure-prerequisites"></a>Konfigurowanie wymagań wstępnych
Witaj następujące kroki stanowią ogólne omówienie zadań konfiguracji które należy wykonać przed zainstalowaniem hello StorSimple Snapshot Manager. Aby całe środowisko Microsoft Azure StorSimple i informacje o instalacji, w tym wymagania systemowe i instrukcje krok po kroku, zobacz [wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Przed rozpoczęciem należy przejrzeć hello [Lista kontrolna dotycząca konfiguracji wdrożenia](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) i i [wymagania wstępne dotyczące wdrażania](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) w [wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Przed zainstalowaniem programu StorSimple Snapshot Manager
1. Rozpakowywanie, zainstalować i podłącz urządzenie Microsoft Azure StorSimple hello, zgodnie z opisem w [zainstalować do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md) lub [zainstalować do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Upewnij się, że komputer-host działa jeden z następujących systemów operacyjnych hello:
   
   * Windows Server 2008 R2 (na serwery z systemem Windows 2008 R2, należy również zainstalować system Windows Server 2008 z dodatkiem SP1 i Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Urządzenie wirtualne StorSimple hello hosta musi być maszyny wirtualnej Microsoft Azure.
3. Upewnij się, czy zostały spełnione wszystkie wymagania dotyczące konfiguracji Microsoft Azure StorSimple hello. Aby uzyskać więcej informacji, przejdź zbyt[wymagania wstępne dotyczące wdrażania](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Połącz hosta toohello urządzenia hello i wykonaj konfigurację początkową hello. Aby uzyskać więcej informacji, przejdź zbyt[kroki wdrażania](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Utworzyć woluminy na urządzeniu hello, przypisz im toohello hosta i sprawdź, że host hello można zainstalować i używać ich. StorSimple Snapshot Manager obsługuje następujące typy woluminów hello:
   
   * Woluminy podstawowe
   * Woluminów prostych
   * Woluminy dynamiczne
   * Dynamiczne woluminy dublowane (RAID 1)
   * Udostępnione woluminy klastra
     
     Informacji o tworzeniu woluminów na urządzeniu StorSimple hello lub urządzenia wirtualnego StorSimple, przejdź zbyt[krok 6: Tworzenie woluminu](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)w [wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Zainstaluj nowy StorSimple Snapshot Manager
Przed zainstalowaniem programu StorSimple Snapshot Manager, upewnij się, że hello woluminy utworzone dla urządzenia StorSimple hello lub urządzenia wirtualnego StorSimple są zainstalowane, zainicjować i sformatowany zgodnie z opisem w [konfigurowanie wymagań wstępnych](#configure-prerequisites).

> [!IMPORTANT]
> * Urządzenie wirtualne StorSimple hello hosta musi być maszyny wirtualnej Microsoft Azure. 
> * Hello host musi działać system Windows 2008 R2, Windows Server 2012 lub Windows Server 2012 R2. Jeśli na serwerze jest uruchomiona w systemie Windows Server 2008 R2, należy również zainstalować system Windows Server 2008 z dodatkiem SP1 i Windows Management Framework 3.0.
> * Należy skonfigurować połączenia iSCSI z urządzenia StorSimple toohello hosta hello przed podłączeniem hello urządzenia tooStorSimple Snapshot Manager.

Wykonaj te kroki toocomplete nową instalację programu StorSimple Snapshot Manager. Jeśli instalujesz uaktualnienia Przejdź zbyt[uaktualnienia lub ponownego zainstalowania programu StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Krok 1: Instalowanie programu StorSimple Snapshot Manager 
* Krok 2: Łączenie urządzenia StorSimple Snapshot Manager tooa 
* Krok 3: Weryfikowanie hello połączenia toohello urządzenia 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Krok 1: Instalowanie programu StorSimple Snapshot Manager
Użyj hello następujące kroki tooinstall StorSimple Snapshot Manager.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall StorSimple Snapshot Manager
1. Pobierz oprogramowanie StorSimple Snapshot Manager hello (Przejdź zbyt[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) w hello Microsoft Download Center) i zapisz go lokalnie na powitania hosta.
2. W Eksploratorze plików kliknij prawym przyciskiem myszy hello skompresowanego folderu, a następnie kliknij przycisk **Wyodrębnij wszystkie**.
3. W hello **foldery Wyodrębnij skompresowane (Zipped)** okna na powitania **wybierz lokalizację docelową i wyodrębnianie plików** wpisz lub Przeglądaj toohello ścieżki, której chcesz wyodrębnić toobe toofile.
   
    > [!IMPORTANT]
    > StorSimple Snapshot Manager należy zainstalować na powitania dysku C:.
    
4. Wybierz hello **Pokaż wyodrębnione pliki po zakończeniu** pole wyboru, a następnie kliknij przycisk **wyodrębnić**.
   
    ![Wyodrębnij plikach — okno dialogowe](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Po zakończeniu operacji wyodrębniania hello otwiera hello folderu docelowego. Kliknij dwukrotnie ikonę Instalatora aplikacji hello, który pojawia się w folderze docelowym hello.
6. Gdy hello **Instalator pomyślnie** pojawi się komunikat, kliknij przycisk **Zamknij**. Ikona programu StorSimple Snapshot Manager hello powinny być widoczne na pulpicie.
   
    ![ikony pulpitu](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Krok 2: Łączenie urządzenia StorSimple Snapshot Manager tooa
Użyj hello następujące kroki tooconnect urządzenia StorSimple tooa StorSimple Snapshot Manager.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect urządzenia StorSimple Snapshot Manager tooa
1. Kliknij ikonę StorSimple Snapshot Manager hello na pulpicie. zostanie wyświetlone okno programu StorSimple Snapshot Manager Hello. Okno Hello zawiera **zakres** okienku **wyniki** okienku i **akcje** okienka. 
   
    ![Interfejs użytkownika programu StorSimple Snapshot Manager](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Witaj **zakres** okienko (w okienku po lewej stronie powitania) zawiera listę węzłów strukturę drzewa. Można rozwinąć niektóre węzły tooselect widoku lub węzeł pokrewne toothat określonych danych. Kliknij tooexpand ikonę strzałki hello lub zwinąć węzeł. Kliknij prawym przyciskiem myszy element hello **zakres** toosee okienko listę dostępnych akcji dla tego elementu.
   * Witaj **wyniki** okienko (hello w środkowym okienku) zawiera szczegółowe informacje o stanie dotyczące węzła hello, widoku lub dane, które wybrano w hello **zakres** okienka.
   * Hello **akcje** okienko zawiera hello operacje, które można wykonywać na powitania węzła, widoku lub dane, które wybrano w hello **zakres** okienka.
     
     Aby uzyskać pełny opis interfejsu użytkownika programu StorSimple Snapshot Manager hello, zobacz [interfejsu użytkownika programu StorSimple Snapshot Manager](storsimple-use-snapshot-manager.md).
2. W hello **zakres** okienku, kliknij prawym przyciskiem myszy hello **urządzeń** węzeł, a następnie kliknij przycisk **Skonfiguruj urządzenie**. Witaj **Skonfiguruj urządzenie** zostanie wyświetlone okno dialogowe.
   
    ![Konfigurowanie urządzenia](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. W hello **urządzenia** listy, pola, wybierz hello adres IP urządzenia Microsoft Azure StorSimple hello lub wirtualnych. W hello **hasło** polu tekstowym, wpisz hasło programu StorSimple Snapshot Manager hello, utworzonej dla hello urządzenia w portalu Azure hello. Kliknij przycisk **OK**.
4. StorSimple Snapshot Manager wyszukuje urządzenia hello, który został zidentyfikowany. Jeśli urządzenie hello jest dostępny, StorSimple Snapshot Manager dodaje połączenie. Możesz [Sprawdź urządzenie toohello połączenia hello](#to-verify-the-connection) tooconfirm, który hello połączenia został dodany pomyślnie.
   
    Jeśli urządzenie hello jest niedostępne w różnych przyczyn, StorSimple Snapshot Manager zwraca komunikat o błędzie. Kliknij przycisk **OK** tooclose hello komunikat o błędzie, a następnie kliknij przycisk **anulować** tooclose hello **Skonfiguruj urządzenie** okno dialogowe.
5. Podczas łączenia urządzeń tooa, StorSimple Snapshot Manager importuje każdej grupy woluminu skonfigurowane dla tego urządzenia, pod warunkiem, że hello grupy woluminu skojarzył kopii zapasowych. Wolumin grup, które nie mają skojarzonych kopii zapasowych nie zostaną zaimportowane. Ponadto zasady tworzenia kopii zapasowej, które zostały utworzone dla grupy woluminu nie zostały zaimportowane. toosee hello zaimportowane grupy, kliknij prawym przyciskiem myszy najwyższy hello **grup woluminu** węzła w hello **zakres** okienka, a następnie kliknij przycisk **Przełącz zaimportowane grupy**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Krok 3: Weryfikowanie hello połączenia toohello urządzenia
Użyj hello następujące kroki tooverify czy StorSimple Snapshot Manager jest toohello podłączonego urządzenia StorSimple.

#### <a name="tooverify-hello-connection"></a>tooverify hello połączenia
1. W hello **zakres** okienku, kliknij przycisk hello **urządzeń** węzła.
   
    ![Stan urządzenia StorSimple Snapshot Manager](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Sprawdź hello **wyniki** okienka: 
   
   * Na ikonę urządzenia hello pojawi się zielony wskaźnik i **dostępne** pojawia się w hello **stan** kolumny, a następnie urządzenia hello jest połączony. 
   * Jeśli czerwony wskaźnik pojawi się na ikonę urządzenia hello a niedostępne w hello **stan** kolumny, a następnie hello urządzenie nie jest połączona. 
   * Jeśli **odświeżanie** pojawia się w hello **stan** kolumny, a następnie StorSimple Snapshot Manager pobiera grup woluminu i skojarzonych kopii zapasowych dla podłączonego urządzenia.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Uaktualnij lub ponowne zainstalowanie programu StorSimple Snapshot Manager
Należy całkowicie odinstalować StorSimple Snapshot Manager przed uaktualnienia lub ponownej instalacji oprogramowania hello. 

Przed ponownym zainstalowaniem programu StorSimple Snapshot Manager, Utwórz kopię zapasową hello istniejącej StorSimple Snapshot Manager bazy danych na komputerze hosta hello. To zapisuje hello kopii zapasowej zasady i informacje o konfiguracji, dzięki czemu można łatwo przywrócić dane z kopii zapasowej.

Jeśli uaktualniasz lub ponowne zainstalowanie programu StorSimple Snapshot Manager, wykonaj następujące kroki:

* Krok 1: Odinstaluj StorSimple Snapshot Manager 
* Krok 2: Wykonaj kopię zapasową bazy danych programu StorSimple Snapshot Manager hello 
* Krok 3: Zainstaluj ponownie StorSimple Snapshot Manager i przywracanie bazy danych hello 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Krok 1: Odinstaluj StorSimple Snapshot Manager
Użyj hello następujące kroki toouninstall StorSimple Snapshot Manager.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall StorSimple Snapshot Manager
1. Na komputerze hosta hello Otwórz hello **Panelu sterowania**, kliknij przycisk **programy**, a następnie kliknij przycisk **programy i funkcje**.
2. W okienku po lewej stronie powitania kliknij **Odinstaluj lub zmień program**.
3. Kliknij prawym przyciskiem myszy **StorSimple Snapshot Manager**, a następnie kliknij przycisk **Odinstaluj**.
4. Spowoduje to uruchomienie hello program instalacyjny programu StorSimple Snapshot Manager. Kliknij przycisk **zmodyfikować ustawienia**, a następnie kliknij przycisk **Odinstaluj**.
   
   > [!NOTE]
   > Jeśli istnieją MMC procesów działających w tle hello, takich jak StorSimple Snapshot Manager lub przystawki Zarządzanie dyskami, odinstaluj hello zakończy się niepowodzeniem i tooclose komunikat zostanie wyświetlony wszystkich wystąpień programu MMC, aby spróbować toouninstall hello program. Wybierz **automatycznie Zamknij aplikacje i podejmij próbę toorestart zakończyć je po konfiguracji**, a następnie kliknij przycisk **OK**.
   > 
   > 
5. Podczas odinstalowywania hello proces jest zakończony, **Instalator pomyślnie** zostanie wyświetlony komunikat. Kliknij przycisk **Zamknij**.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Krok 2: Wykonaj kopię zapasową bazy danych programu StorSimple Snapshot Manager hello
Użyj hello następujące kroki toocreate i Zapisz kopię bazy danych programu StorSimple Snapshot Manager hello.

#### <a name="tooback-up-hello-database"></a>tooback hello bazy danych
1. Zatrzymaj usługi zarządzania StorSimple Microsoft hello:
   
   1. Uruchom Menedżera serwera.
   2. Na powitania nawigacyjnym Menedżera serwera na powitania **narzędzia** menu, wybierz opcję **usług**.
   3. Na powitania **usług** wybierz pozycję **usługi zarządzania StorSimple Microsoft**.
   4. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Zatrzymaj usługę hello**.
      
        ![Zatrzymaj usługę Menedżera urządzenia StorSimple hello](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Przeglądaj tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > Folder ProgramData jest folderem ukrytym.
  
3. Znajdź plik XML katalogu hello, kopiowania pliku hello i przechowywanie hello kopiowanie w bezpiecznym miejscu lub w chmurze hello.
   
    ![Plik kopii zapasowej katalogu StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Ponowne uruchamianie usługi zarządzania StorSimple Microsoft hello: 
   
   1. Na powitania nawigacyjnym Menedżera serwera na powitania **narzędzia** menu, wybierz opcję **usług**.
   2. Na powitania **usług** strona, wybierz hello **Microsoft StorSimple zarządzania Servic**e.
   3. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Uruchom ponownie usługę hello**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Krok 3: Zainstaluj ponownie StorSimple Snapshot Manager i przywracanie bazy danych hello
tooreinstall StorSimple Snapshot Manager, wykonaj kroki hello w [zainstalować nowy StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager). Następnie należy użyć hello następujące procedury toorestore hello StorSimple Snapshot Manager w bazie danych.

#### <a name="toorestore-hello-database"></a>toorestore hello w bazie danych
1. Zatrzymaj usługi zarządzania StorSimple Microsoft hello:
   
   1. Uruchom Menedżera serwera.
   2. Na powitania nawigacyjnym Menedżera serwera na powitania **narzędzia** menu, wybierz opcję **usług**.
   3. Na powitania **usług** wybierz pozycję **usługi zarządzania StorSimple Microsoft**.
   4. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Zatrzymaj usługę hello**.
2. Przeglądaj tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > Folder ProgramData jest folderem ukrytym.
   > 
   > 
3. Usuń plik XML katalogu hello i zastąp go hello wersji, który został wcześniej zapisany.
4. Ponowne uruchamianie usługi zarządzania StorSimple Microsoft hello: 
   
   1. Na powitania nawigacyjnym Menedżera serwera na powitania **narzędzia** menu, wybierz opcję **usług**.
   2. Na powitania **usług** wybierz pozycję **usługi zarządzania StorSimple Microsoft**.
   3. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Uruchom ponownie usługę hello**.

## <a name="next-steps"></a>Następne kroki
* toolearn więcej o StorSimple Snapshot Manager, przejdź zbyt[co to jest StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md).
* toolearn więcej informacji na temat interfejsu użytkownika programu StorSimple Snapshot Manager hello Przejdź zbyt[interfejsu użytkownika programu StorSimple Snapshot Manager](storsimple-use-snapshot-manager.md).
* toolearn więcej informacji na temat przy użyciu programu StorSimple Snapshot Manager Przejdź zbyt[tooadminister Użyj StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).

