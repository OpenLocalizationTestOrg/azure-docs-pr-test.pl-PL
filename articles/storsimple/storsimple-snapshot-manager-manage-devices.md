---
title: "urządzenia aaaManage z StorSimple Snapshot Manager | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse hello tooconnect przystawki MMC programu StorSimple Snapshot Manager i zarządzanie urządzeniami StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>Użyj tooconnect StorSimple Snapshot Manager i zarządzanie urządzeniami StorSimple
## <a name="overview"></a>Omówienie
Możesz użyć węzłów w hello StorSimple Snapshot Manager **zakresu** tooverify okienko zaimportowane dane urządzenia StorSimple i Odśwież urządzeń połączonych magazynów. Ponadto po kliknięciu hello **urządzeń** węzła, można wyświetlić listę podłączonego urządzenia i odpowiednie informacje o stanie w hello **wyniki** okienka.

![Połączonych urządzeń](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Rysunek 1: Podłączonego urządzenia StorSimple Snapshot Manager** 

W zależności od Twojego **widoku** wybór, powitalne **wyniki** w okienku zostaną wyświetlone hello następujące informacje dotyczące każdego urządzenia. (Aby uzyskać więcej informacji o konfigurowaniu widok, przejdź zbyt[menu Widok](storsimple-use-snapshot-manager.md#view-menu).

| Kolumny wyników | Opis |
|:--- |:--- |
| Nazwa |Nazwa Hello hello urządzenia zgodnie z konfiguracją hello klasycznego portalu Azure |
| Model |numer modelu Hello hello urządzenia |
| Wersja |Wersja Hello hello oprogramowania zainstalowanego na urządzeniu hello |
| Stan |Określa, czy urządzenie hello jest dostępne |
| Od ostatniej synchronizacji upłynęła |Data i godzina, kiedy urządzenie hello ostatniej synchronizacji |
| Numer seryjny |numer seryjny Hello hello urządzenia |

Kliknięcie prawym przyciskiem myszy hello **urządzeń** węzła w hello **zakres** okienka, możesz wybrać z hello następujące akcje:

* Dodaj lub Zastąp urządzenia
* Podłącz urządzenie i sprawdź importów
* Odśwież połączonych urządzeń

Jeśli klikniesz przycisk hello **urządzeń** węzła, a następnie kliknij prawym przyciskiem myszy urządzenie nazwisko hello **wyniki** okienka, możesz wybrać z hello następujące akcje:

* Uwierzytelniania urządzenia
* Wyświetl szczegóły urządzenia
* Odśwież urządzenia
* Usuwanie konfiguracji urządzenia
* Zmień hasło urządzenia

> [!NOTE]
> Wszystkie te działania są także dostępne w hello **akcje** okienka.


Ten samouczek wyjaśnia sposób toouse tooconnect StorSimple Snapshot Manager i zarządzania urządzeniami i wykonywać następujące zadania hello:

* Dodaj lub Zastąp urządzenia
* Podłącz urządzenie i sprawdź importów
* Odśwież połączonych urządzeń
* Uwierzytelniania urządzenia
* Wyświetl szczegóły urządzenia
* Odśwież poszczególnych urządzeń
* Usuwanie konfiguracji urządzenia
* Zmień hasło urządzenia wygasły
* Zastąp urządzenia nie powiodło się

> [!NOTE]
> Aby uzyskać ogólne informacje o interfejsie StorSimple Snapshot Manager hello Przejdź zbyt[interfejsu użytkownika programu StorSimple Snapshot Manager](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Dodaj lub Zastąp urządzenia
Użyj następującej procedury tooadd hello lub zastąpić urządzenia StorSimple.

#### <a name="tooadd-or-replace-a-device"></a>tooadd lub Zastąp urządzenia
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij prawym przyciskiem myszy hello **urządzeń** węzeł, a następnie kliknij przycisk **Skonfiguruj urządzenie**. Witaj **Skonfiguruj urządzenie** zostanie wyświetlone okno dialogowe.
   
    ![Konfigurowanie urządzenia StorSimple](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. W hello **urządzenia** pole listy rozwijanej, wybierz hello adres IP urządzenia hello lub wirtualnych. 
4. W hello **hasło** polu tekstowym, wpisz hasło programu StorSimple Snapshot Manager hello, utworzonej dla urządzenia hello w hello klasycznego portalu Azure. Kliknij przycisk **OK**. StorSimple Snapshot Manager wyszukuje urządzenia hello, który został zidentyfikowany. 
   
   * Jeśli urządzenie hello jest dostępny, StorSimple Snapshot Manager dodaje połączenie.
   * Jeśli urządzenie hello jest niedostępne w różnych przyczyn, StorSimple Snapshot Manager zwraca komunikat o błędzie. Kliknij przycisk **OK** tooclose hello komunikat o błędzie, a następnie kliknij przycisk **anulować** tooclose hello **Skonfiguruj urządzenie** okno dialogowe.

## <a name="connect-a-device-and-verify-imports"></a>Podłącz urządzenie i sprawdź importów
Użyj hello następujące procedury tooconnect urządzenia StorSimple i sprawdź, czy jakichkolwiek istniejących grup woluminów, które administrator skojarzył kopie zapasowe są importowane.

#### <a name="tooconnect-a-device-and-verify-imports"></a>tooconnect urządzenie i sprawdź importów
1. tooconnect tooStorSimple urządzenia Snapshot Manager, wykonaj te instrukcje hello Dodaj lub zastąpić urządzenia. Podczas łączenia urządzeń tooa, StorSimple Snapshot Manager działa w następujący sposób:
   
   * Jeśli urządzenie hello jest niedostępne w różnych przyczyn, StorSimple Snapshot Manager zwraca komunikat o błędzie. 
   
   * Jeśli urządzenie hello jest dostępny, StorSimple Snapshot Manager dodaje połączenie. Po wybraniu urządzenia hello jest wyświetlana w hello **wyniki** okienku i pole stanu hello wskazuje, czy urządzenie hello jest **dostępne**. StorSimple Snapshot Manager importuje wszystkie grupy woluminu skonfigurowany dla urządzenia hello, pod warunkiem, że grupy woluminu hello mieć skojarzone kopii zapasowych. Zasady tworzenia kopii zapasowej nie zostały zaimportowane. Wolumin grup, które nie mają skojarzonych kopii zapasowych nie zostaną zaimportowane.
2. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
3. Kliknij prawym przyciskiem myszy górny węzeł hello w hello **zakres** okienka, a następnie kliknij przycisk **Przełącz importów wyświetlanie**.
   
    ![Wybierz opcję Przełącz wyświetlanie importów](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Witaj **Przełącz importów wyświetlanie** zostanie wyświetlone okno dialogowe, wyświetlanie stanu hello hello zaimportowane grupy woluminu i kopii zapasowych. Kliknij przycisk **OK**.

Po pomyślnie zaimportowano hello grup woluminu i kopii zapasowych, można użyć toomanage StorSimple Snapshot Manager ich, tylko będzie zarządzać grupami woluminu i kopii zapasowych, które zostały utworzone i skonfigurowane z StorSimple Snapshot Manager. 

## <a name="refresh-connected-devices"></a>Odśwież połączonych urządzeń
Witaj użyj następującej procedury toosynchronize hello połączone urządzenia StorSimple z StorSimple Snapshot Manager.

#### <a name="toorefresh-connected-devices"></a>toorefresh podłączone urządzenia
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku kliknij prawym przyciskiem myszy **urządzeń**, a następnie kliknij przycisk **Odśwież urządzeń**. Synchronizuje hello podłączone urządzenia, z StorSimple Snapshot Manager tak, aby wyświetlić hello grup woluminu i kopii zapasowych, w tym wszelkie ostatnio dodane. 
   
    ![Odśwież hello urządzenia StorSimple](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Witaj **Odśwież urządzeń** działanie powoduje pobranie wszystkich nowych grup wolumin i wszystkie skojarzone kopii zapasowych z połączonych urządzeń. W odróżnieniu od hello **ponownego skanowania woluminów** umożliwiające hello **woluminów** węzła, **Odśwież urządzenia** nie powoduje przywrócenia kopii zapasowej rejestru hello.

## <a name="authenticate-a-device"></a>Uwierzytelniania urządzenia
Użyj następującej procedury tooauthenticate urządzenia StorSimple z StorSimple Snapshot Manager hello.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate urządzenia
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij przycisk **urządzeń**.
3. W hello **wyniki** okienku kliknij prawym przyciskiem myszy nazwę hello hello urządzenia, a następnie kliknij przycisk **Uwierzytelnij**.
4. Witaj **Uwierzytelnij** zostanie wyświetlone okno dialogowe. Wpisz hasło urządzenia hello, a następnie kliknij przycisk **OK**.
   
    ![Uwierzytelnianie — okno dialogowe](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Wyświetl szczegóły urządzenia
Użyj hello poniższe procedury tooview hello informacje urządzenia StorSimple i, jeśli to konieczne, należy ponownie zsynchronizować urządzenie hello z StorSimple Snapshot Manager.

#### <a name="tooview-and-resynchronize-device-details"></a>tooview i ponownie synchronizować szczegóły urządzenia
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij przycisk **urządzeń**.
3. W hello **wyniki** okienku kliknij prawym przyciskiem myszy nazwę hello hello urządzenia, a następnie kliknij przycisk **szczegóły**.

4 Witaj **szczegóły urządzenia** zostanie wyświetlone okno dialogowe. To pole zawiera nazwę hello, modelu, wersji, numer seryjny, stan, obiektów docelowych iSCSI kwalifikowana nazwa (IQN) i ostatniej synchronizacji daty i godziny.

* Kliknij przycisk **ponownej synchronizacji** toosynchronize hello urządzenia.
* Kliknij przycisk **OK** lub **anulować** hello tooclose — okno dialogowe.
  
  ![Szczegóły urządzenia](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Odśwież poszczególnych urządzeń
Użyj następującej procedury tooresynchronize poszczególne urządzenia StorSimple z StorSimple Snapshot Manager hello.

#### <a name="toorefresh-a-device"></a>toorefresh urządzenia
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager. 
2. W hello **zakres** okienku, kliknij przycisk **urządzeń**. 
3. W hello **wyniki** okienku kliknij prawym przyciskiem myszy nazwę hello hello urządzenia, a następnie kliknij przycisk **Odśwież urządzenia**. Witaj urządzenia do synchronizacji z StorSimple Snapshot Manager.

## <a name="delete-a-device-configuration"></a>Usuwanie konfiguracji urządzenia
Użyj następującej procedury toodelete poszczególnych konfiguracji urządzenia StorSimple z StorSimple Snapshot Manager hello.

#### <a name="toodelete-a-device-configuration"></a>toodelete konfiguracji urządzenia
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij przycisk **urządzeń**. 
3. W hello **wyniki** okienku kliknij prawym przyciskiem myszy nazwę hello hello urządzenia, a następnie kliknij przycisk **usunąć**. 
4. zostanie wyświetlone następujące wiadomość Hello. Kliknij przycisk **tak** toodelete hello konfiguracji lub kliknij przycisk **nr** toocancel hello usunięcia.
   
    ![Usuwanie konfiguracji urządzenia](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Zmień hasło urządzenia wygasły
Należy wprowadzić tooauthenticate hasła urządzenia StorSimple z StorSimple Snapshot Manager. Skonfigurować takie hasło, korzystając z tooset interfejsu programu Windows PowerShell hello hello urządzenia. Jednak hello hasło można wygasa. W takim przypadku można użyć hello Azure classic portal toochange hello hasła. Następnie ponieważ urządzenie hello skonfigurowano programu StorSimple Snapshot Manager przed wygaśnięciem hasła hello, możesz ponownego uwierzytelnienia hello urządzenia StorSimple Snapshot Manager.

#### <a name="toochange-hello-expired-password"></a>Wygaśnięcie hasła hello toochange
1. W hello klasycznego portalu Azure należy uruchomić usługę Menedżer StorSimple hello.
2. Kliknij przycisk **urządzeń** > **Konfiguruj** hello urządzenia.
3. Przewiń w dół toohello sekcji StorSimple Snapshot Manager. Wprowadź hasło składające się z 14-15 znaków. Upewnij się, że to hasło hello zawiera wielkie litery, małe litery, liczbowego i znaki specjalne.
4. Wprowadź ponownie tooconfirm hasło hello go.
5. Kliknij przycisk **zapisać** u dołu hello hello strony.

#### <a name="toore-authenticate-hello-device"></a>toore-uwierzytelnienia hello urządzenia
1. Uruchom StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij przycisk **urządzeń**. Zostanie wyświetlona lista skonfigurowanych urządzeń w hello **wyniki** okienka.
3. Wybierz urządzenie hello, kliknij prawym przyciskiem myszy, a następnie kliknij **Uwierzytelnij**.
4. W hello **Uwierzytelnij** okna, wprowadź nowe hasło hello.
5. Wybierz urządzenie hello, kliknij prawym przyciskiem myszy i wybierz **urządzenia odświeżania**. Witaj urządzenia do synchronizacji z StorSimple Snapshot Manager.

## <a name="replace-a-failed-device"></a>Zastąp urządzenia nie powiodło się
Jeśli urządzenie StorSimple kończy się niepowodzeniem i jest zastąpione przez urządzenie stan wstrzymania (failover), użyj hello następujące kroki tooconnect toohello nowe urządzenie i widoku hello skojarzonych kopii zapasowych.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>nowe urządzenie tooa tooconnect po pracy awaryjnej
1. Skonfiguruj ponownie hello iSCSI połączenia toohello nowe urządzenie. Aby uzyskać instrukcje, przejdź zbyt "krok 7: instalacji, zainicjować i formatowanie woluminu" w [wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Jeśli nowe urządzenie StorSimple hello ma hello sam adres IP hello stare hasło, może być możliwe tooconnect hello starą konfigurację.


1. Zatrzymaj usługi zarządzania StorSimple Microsoft hello:
   
   1. Uruchom Menedżera serwera.
   2. Na powitania nawigacyjnym Menedżera serwera na powitania **narzędzia** menu, wybierz opcję **usług**.
   3. Na powitania **usług** okna, wybierz hello **usługi zarządzania StorSimple Microsoft**.
   4. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Zatrzymaj usługę hello**.
2. Usuń urządzenie stare informacje pokrewne toohello hello konfiguracji:
   
   1. W Eksploratorze plików Przejdź tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   2. Usuń hello pliki w folderze BACatalog hello.
3. Ponowne uruchamianie usługi zarządzania StorSimple Microsoft hello:
   
   1. Na powitania nawigacyjnym Menedżera serwera na powitania **narzędzia** menu, wybierz opcję **usług**.
   2. Na powitania **usług** okna, wybierz hello **usługi zarządzania StorSimple Microsoft**.
   3. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Uruchom ponownie usługę hello**.
4. Uruchom StorSimple Snapshot Manager.
5. tooconfigure hello nowego urządzenia StorSimple, pełną hello kroków w kroku 2: łączenie urządzenia StorSimple w [wdrażanie StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
6. Kliknij prawym przyciskiem myszy hello najwyższego poziomu w węźle hello **zakres** okienka (StorSimple Snapshot Manager w przykładzie hello), a następnie kliknij przycisk **Przełącz importów wyświetlanie**. 
7. Komunikat jest wyświetlany, gdy hello zaimportowane grupy woluminu i kopii zapasowych są widoczne w StorSimple Snapshot Manager. Kliknij przycisk **OK**.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Dowiedz się, jak za[Użyj tooview StorSimple Snapshot Manager i zarządzanie woluminami](storsimple-snapshot-manager-manage-volumes.md).

