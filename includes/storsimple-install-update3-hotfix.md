<!--author=alkohli last changed: 09/01/16-->

#### <a name="toodownload-hotfixes"></a>poprawki toodownload
Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.

1. Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.
    ![Zainstaluj katalogu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello hello poprawki mają toodownload, na przykład **3186843**, a następnie kliknij przycisk **wyszukiwania**.
   
    Witaj poprawka zostanie wyświetlona na liście, na przykład **zbiorczą 3.0 aktualizacji pakietu oprogramowania dla z serii StorSimple 8000**.
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. Kliknij pozycję **Dodaj**. Witaj aktualizacja została dodana toohello koszyka.
5. Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli hello (**3186859**) i Dodaj każdy koszyka toohello.
6. Kliknij pozycję **Wyświetl koszyk**.
7. Kliknij pozycję **Pobierz**. Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear. Witaj aktualizacje zostaną pobrane toohello określonej lokalizacji i umieścić w podfolderze o hello takie same nazwy co hello update. Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.

> [!NOTE]
> poprawki Hello musi być dostępny z obu toodetect kontrolerów wszelkie potencjalne błędy komunikaty z hello równorzędnej kontrolera.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall i sprawdź regularne poprawki
Wykonaj następujące kroki tooinstall hello i sprawdź regular poprawki. Jeśli zainstalowano je przy użyciu hello portalu Azure przejdź za[zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall hello poprawki interfejsu programu Windows PowerShell hello dostępu na konsoli szeregowej urządzenia StorSimple. Wykonaj hello szczegółowe instrukcje w [konsoli szeregowej przy użyciu programu PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). W wierszu polecenia hello naciśnij **Enter**.
2. Wybierz **opcję 1** toolog toohello urządzenia z pełnym dostępem. Zalecamy zainstalowanie poprawki hello na kontrolerze pasywnym hello najpierw.
3. poprawka hello tooinstall hello wiersza polecenia, wpisz:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Użyj adresu IP, a nie DNS w ścieżce udziału hello powyżej polecenia. Parametr credential Hello jest używany tylko wtedy, gdy uzyskujesz dostęp do udziału uwierzytelniony.
   
    Zalecamy użycie udziałów tooaccess parametr credential hello. Nawet udziałów, które są otwarte za "wszyscy" są zwykle nie otworzyć toounauthenticated użytkowników.
   
    Podaj hasło powitania po wyświetleniu monitu.
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. Typ **Y** gdy zostanie wyświetlony monit o tooconfirm hello instalacji poprawki.
5. Monitoruj hello aktualizacji za pomocą hello `Get-HcsUpdateStatus` polecenia cmdlet. Hello aktualizacji zakończy się najpierw na powitania pasywnym kontrolera. Po kontrolera pasywnym hello jest aktualizowany, będą trybu failover i aktualizacji hello następnie zostaną zastosowane na hello inny kontroler. Witaj aktualizacja została ukończona, gdy obu kontrolerów hello są aktualizowane.
   
    Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku. Witaj `RunInprogress` będzie `True` podczas aktualizacji hello jest w toku.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone. Witaj `RunInProgress` będzie `False` po zakończeniu aktualizacji hello.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > Czasami hello raporty polecenia cmdlet `False` podczas aktualizacji hello jest nadal w toku. tooensure, który hello poprawka została ukończona, poczekaj kilka minut, ponownie uruchomić to polecenie i sprawdź, że hello `RunInProgress` jest `False`. Jeśli tak jest, poprawki hello zostało zakończone.

1. Po zakończeniu aktualizacji oprogramowania hello Sprawdź wersje oprogramowania hello systemu. Wpisz:
   
    `Get-HcsSystem`
   
    Powinny pojawić się hello następujące wersje:
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     Jeśli po zastosowaniu aktualizacji hello nie należy zmieniać numerów wersji hello, oznacza to, że ta poprawka hello nie powiodło się tooapply. Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.
     
     > [!IMPORTANT]
     > Należy ponownie uruchomić hello na aktywnym kontrolerze za pośrednictwem hello `Restart-HcsController` polecenia cmdlet przed zastosowaniem hello pozostałych aktualizacji. 
     > 
     > 
2. Powtórz kroki 3 – 5 tooinstall hello LSI sterowników i oprogramowania układowego poprawkę **KB3186859**. Po zainstalowaniu poprawki hello użyć hello `Get-HcsSystem` polecenia cmdlet. Wersja Hello LSI powinny być:
   
   * `Lsisas2Version: 2.0.78.00`
3. Powtórz kroki 3 – 5 tooinstall hello Storport i aktualizacji Spaceport **KB3121261**.
4. Jeśli aktualizacja Update 2 lub starszej wersji, konieczne będzie również toodownload:
   
   * poprawka iSCSI przy użyciu KB3146621
   * Poprawka WMI za pomocą KB3103616

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall i sprawdź poprawki trybu konserwacji
Użyj aktualizacji oprogramowania układowego dysku tooinstall KB3121899. Te aktualizacje zakłócenie i podejmij toocomplete około 30 minut. Można wybrać tooinstall je w oknie obsługi planowanych przez łączącego konsoli szeregowej urządzenia toohello.

Uwaga: Jeśli oprogramowanie układowe dysku jest już aktualne, nie należy tooinstall te aktualizacje. Uruchom hello `Get-HcsUpdateAvailability` polecenia cmdlet z hello toocheck konsoli szeregowej urządzenia, jeśli aktualizacje są dostępne i czy hello aktualizacji są destrukcyjne (trybu konserwacji) lub Brak (tryb regularne) aktualizacji.

aktualizacje oprogramowania układowego tooinstall hello dysku, wykonaj poniższe instrukcje hello.

1. Ustaw hello urządzenia w trybie konserwacji hello. Należy pamiętać, że nie należy używać komunikacji zdalnej programu Windows PowerShell podczas łączenia tooa urządzenia w trybie konserwacji. Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia hello podczas połączenia za pośrednictwem konsoli szeregowej urządzenia hello. Wpisz:
   
    `Enter-HcsMaintenanceMode`
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
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
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
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
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   Poniżej pokazano przykładowe dane wyjściowe.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    Uruchom hello `Get-HcsFirmwareVersion` polecenie hello drugi kontroler tooverify który hello wersji oprogramowania została zaktualizowana. Następnie można zakończyć tryb konserwacji hello. toodo tak, wpisz następujące polecenie dla każdego kontrolera urządzenia hello:
   
   `Exit-HcsMaintenanceMode`
5. kontrolery Hello ponownie po wyjściu z trybu konserwacji. Po oprogramowania układowego dysku hello skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie hello opuścił tryb konserwacji, zwracany toohello klasycznego portalu Azure. Należy pamiętać, że tego portalu hello nie mogą być wyświetlane, czy zainstalowane aktualizacje w trybie konserwacji hello przez 24 godziny.

