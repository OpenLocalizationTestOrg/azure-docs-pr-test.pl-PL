<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a>poprawki toodownload

Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.

1. Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.

    ![Instalowanie wykazu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello hello poprawki mają toodownload, na przykład **4037264**, a następnie kliknij przycisk **wyszukiwania**.
   
    Witaj poprawka zostanie wyświetlona na liście, na przykład **zbiorczą 5.0 aktualizacji pakietu oprogramowania dla z serii StorSimple 8000**.
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. Kliknij pozycję **Pobierz**. Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear. Kliknij przycisk pliki hello toodownload toohello określić lokalizację i folderu. Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.
5. Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli hello (**4037266**), i wymienione w powyższej tabeli hello odpowiadającego hello pobierania plików toohello określonych folderów.

> [!NOTE]
> poprawki Hello musi być dostępny z obu toodetect kontrolerów wszelkie potencjalne błędy komunikaty z hello równorzędnej kontrolera.
>
> Witaj poprawek należy skopiować w oddzielnych folderach 3. Na przykład aktualizacja oprogramowania/Cis/MDS agenta urządzenia hello mogą zostać skopiowane w _FirstOrderUpdate_ folderu, hello wszystkie inne aktualizacje Brak mógł zostać skopiowany w hello _SecondOrderUpdate_ folderu, i aktualizacje trybu konserwacji skopiowany w _ThirdOrderUpdate_ folderu.

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall i sprawdź regularne poprawki

Wykonaj następujące kroki tooinstall hello i sprawdź regular poprawki. Jeśli zainstalowano je przy użyciu hello portalu Azure przejdź za[zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall hello poprawki interfejsu programu Windows PowerShell hello dostępu na konsoli szeregowej urządzenia StorSimple. Wykonaj hello szczegółowe instrukcje w [konsoli szeregowej przy użyciu programu PuTTy tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console). W wierszu polecenia hello naciśnij **Enter**.
2. Wybierz **opcję 1** toolog toohello urządzenia z pełnym dostępem. Zalecamy zainstalowanie poprawki hello na kontrolerze pasywnym hello najpierw.
3. poprawka hello tooinstall hello wiersza polecenia, wpisz:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Użyj adresu IP, a nie DNS w ścieżce udziału hello powyżej polecenia. Parametr credential Hello jest używany tylko wtedy, gdy uzyskujesz dostęp do udziału uwierzytelniony.
   
    Zalecamy użycie udziałów tooaccess parametr credential hello. Nawet udziałów, które są otwarte za "wszyscy" są zwykle nie otworzyć toounauthenticated użytkowników.
   
4. Podaj hasło powitania po wyświetleniu monitu. Poniżej przedstawiono przykładowe dane wyjściowe instalowania hello pierwszy kolejność aktualizacji. Hello pierwszej kolejności aktualizacji należy toopoint toohello określonego pliku.

    >[!NOTE] 
    > Należy zainstalować hello _HcsSoftwareUpdate.exe_ pierwszy. Po zakończeniu tej instalacji, następnie zainstalować _CisMdsAgentUpdate.exe_.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. Typ **Y** gdy zostanie wyświetlony monit o tooconfirm hello instalacji poprawki.
6. Monitoruj hello aktualizacji za pomocą hello `Get-HcsUpdateStatus` polecenia cmdlet. Hello aktualizacji zakończy się najpierw na powitania pasywnym kontrolera. Po kontrolera pasywnym hello jest aktualizowany, będą trybu failover i aktualizacji hello następnie zostaną zastosowane na hello inny kontroler. Witaj aktualizacja została ukończona, gdy obu kontrolerów hello są aktualizowane.
   
    Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku. Witaj `RunInprogress` jest `True` po aktualizacji hello jest w toku.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone. Witaj `RunInProgress` jest `False` po zakończeniu aktualizacji hello.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > Czasami hello raporty polecenia cmdlet `False` podczas aktualizacji hello jest nadal w toku. tooensure, który hello poprawka została ukończona, poczekaj kilka minut, ponownie uruchomić to polecenie i sprawdź, że hello `RunInProgress` jest `False`. Jeśli tak jest, poprawki hello zostało zakończone.

7. Po zakończeniu aktualizacji oprogramowania hello Sprawdź wersje oprogramowania hello systemu. Wpisz:
   
    `Get-HcsSystem`
   
    Powinny pojawić się hello następujące wersje:
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    Jeśli numer wersji hello nie zmienia się po zastosowaniu aktualizacji hello, oznacza to, że ta poprawka hello nie powiodło się tooapply. Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.
     
    > [!IMPORTANT]
    > Należy ponownie uruchomić hello na aktywnym kontrolerze za pośrednictwem hello `Restart-HcsController` polecenia cmdlet przed zastosowaniem hello następną aktualizację.
     
8. Powtórz kroki od 3 do 6 tooinstall hello _CisMDSAgentupdate.exe_ agent pobierany tooyour _FirstOrderUpdate_ folderu.
8. Powtórz kroki od 3 do 6 tooinstall hello drugi kolejność aktualizacji. 

    > [!NOTE] 
    > Drugi kolejność aktualizacji, można zainstalować wiele aktualizacji tylko uruchamiając hello `Start-HcsHotfix cmdlet` i wskazujący toohello folder zawierający drugi aktualizacje kolejności. polecenia cmdlet Hello wykona wszystkie dostępne aktualizacje hello w folderze hello. Jeśli aktualizacja jest już zainstalowana, logika aktualizacji hello wykryje, że i nie zastosować tę aktualizację.

    Po zainstalowaniu wszystkich hello poprawek, użyj hello `Get-HcsSystem` polecenia cmdlet. wersje Hello powinny być:
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall i sprawdź poprawki trybu konserwacji

Użyj aktualizacji oprogramowania układowego dysku tooinstall KB4037263. Te aktualizacje zakłócenie i podejmij toocomplete około 30 minut. Można wybrać tooinstall je w oknie obsługi planowanych przez łączącego konsoli szeregowej urządzenia toohello.

> [!NOTE] 
> Jeśli oprogramowanie układowe dysku jest już aktualne, nie ma potrzeby tooinstall te aktualizacje. Uruchom hello `Get-HcsUpdateAvailability` polecenia cmdlet z hello toocheck konsoli szeregowej urządzenia, jeśli aktualizacje są dostępne i czy hello aktualizacji są destrukcyjne (trybu konserwacji) lub Brak (tryb regularne) aktualizacji.

aktualizacje oprogramowania układowego tooinstall hello dysku, wykonaj poniższe instrukcje hello.

1. Ustaw hello urządzenia w trybie konserwacji hello. 

    > [!NOTE] 
    > Nie należy używać komunikacji zdalnej programu Windows PowerShell, łącząc tooa urządzenia w trybie konserwacji. Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia hello podczas połączenia za pośrednictwem konsoli szeregowej urządzenia hello.

    Kontroler hello tooplace w trybie konserwacji, wpisz:
   
    `Enter-HcsMaintenanceMode`
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Zarówno kontrolery hello następnie uruchom ponownie w trybie konserwacji.
2. tooinstall hello dysku aktualizacji oprogramowania układowego, wpisz:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Monitor hello Instaluj postępu przy użyciu `Get-HcsUpdateStatus` polecenia. Witaj aktualizacja została ukończona, gdy hello `RunInProgress` zmiany zbyt`False`.
4. Po zakończeniu instalacji hello hello kontrolera, na które hello zainstalowano poprawkę trybu konserwacji zostanie uruchomiony ponownie. Zaloguj się jako opcja 1 z pełnym dostępem i sprawdź, wersja oprogramowania układowego hello dysku. Wpisz:
   
   `Get-HcsFirmwareVersion`
   
   Witaj oczekiwanych wersji oprogramowania układowego dysku:
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   Poniżej pokazano przykładowe dane wyjściowe.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    Uruchom hello `Get-HcsFirmwareVersion` polecenie hello drugi kontroler tooverify który hello wersji oprogramowania została zaktualizowana. Następnie można zakończyć tryb konserwacji hello. toodo tak, wpisz następujące polecenie dla każdego kontrolera urządzenia hello:
   
   `Exit-HcsMaintenanceMode`

5. kontrolery Hello ponownie po wyjściu z trybu konserwacji. Po oprogramowania układowego dysku hello skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie hello opuścił tryb konserwacji, zwracany toohello portalu Azure. Należy pamiętać, że tego portalu hello nie mogą być wyświetlane, czy zainstalowane aktualizacje w trybie konserwacji hello przez 24 godziny.

