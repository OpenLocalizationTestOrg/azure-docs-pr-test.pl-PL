<!--author=alkohli last changed: 08/21/17-->

#### <a name="to-download-hotfixes"></a>Aby pobrać poprawki

Wykonaj następujące kroki, aby pobrać aktualizację oprogramowania z Wykazu usługi Microsoft Update.

1. Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Jeśli po raz pierwszy używasz Wykazu usługi Microsoft Update na danym komputerze, po wyświetleniu monitu o zainstalowanie dodatku Wykazu usługi Microsoft Update kliknij pozycję **Zainstaluj**.

    ![Instalowanie wykazu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. W polu wyszukiwania z wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) poprawki do pobrania, na przykład **4037264**, a następnie kliknij przycisk **wyszukiwania**.
   
    Poprawka zostanie wyświetlona na liście, na przykład **zbiorczą 5.0 aktualizacji pakietu oprogramowania dla z serii StorSimple 8000**.
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. Kliknij pozycję **Pobierz**. Określ lokalizację lokalną, do której mają trafiać pobrane pliki, albo **przejdź** do takiej lokalizacji. Kliknij przycisk pliki do pobrania do określonej lokalizacji i folderu. Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.
5. Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli (**4037266**) i pobierz odpowiednie pliki do określonych folderów wymienione w powyższej tabeli.

> [!NOTE]
> Poprawki musi być dostępny z obu kontrolerów, aby wykryć potencjalne komunikaty o błędach z kontrolera elementu równorzędnego.
>
> Poprawki muszą zostać skopiowane do 3 oddzielnych folderów. Na przykład aktualizacja oprogramowania/Cis/MDS agenta urządzenia mogą być kopiowane w _FirstOrderUpdate_ folderu, mógł zostać skopiowany wszystkich innych Brak aktualizacji w _SecondOrderUpdate_ folderu, i aktualizacje trybu konserwacji skopiowany w _ThirdOrderUpdate_ folderu.

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a>Aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego

Wykonaj następujące kroki, aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego. Jeśli została już zainstalowana ich przy użyciu portalu Azure, przejdź do [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).

1. Aby zainstalować poprawki, przejdź do interfejsu programu Windows PowerShell na konsoli szeregowej Twojego urządzenia StorSimple. Postępuj zgodnie ze szczegółowymi instrukcjami w części [Nawiązywanie połączenia z konsolą szeregową urządzenia przy użyciu programu PuTTY](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console). W wierszy polecenia naciśnij klawisz **Enter**.
2. Wybierz **opcję 1**, aby zalogować się do urządzenia z pełnym dostępem. Zalecamy, aby najpierw zainstalować poprawkę na kontrolerze pasywnym.
3. Aby zainstalować poprawkę, w wierszu polecenia wpisz:
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    W powyższym poleceniu użyj adresu IP zamiast nazwy DNS w ścieżce udziału. Parametr Credential jest używany tylko wtedy, gdy uzyskuje się dostęp do uwierzytelnionego udziału.
   
    Użycie parametru Credential jest zalecane przy uzyskiwaniu dostępu do udziałów. Nawet udziały otwarte dla wszystkich nie są zwykle otwarte dla użytkowników nieuwierzytelnionych.
   
4. Po wyświetleniu monitu podaj hasło. Przykładowe dane wyjściowe dotyczące instalacji aktualizacji stosowanych w pierwszej kolejności są pokazane poniżej. Pierwszą aktualizacją kolejności należy wskazać określonego pliku.

    >[!NOTE] 
    > Należy zainstalować _HcsSoftwareUpdate.exe_ pierwszy. Po zakończeniu tej instalacji, następnie zainstalować _CisMdsAgentUpdate.exe_.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. Wpisz **Y**, gdy zostanie wyświetlony monit o potwierdzenie instalacji poprawki.
6. Monitoruj aktualizację za pomocą polecenia cmdlet `Get-HcsUpdateStatus`. Aktualizacja zakończy się najpierw na kontrolerze pasywnym. Gdy kontroler pasywny zostanie zaktualizowany, nastąpi przejście do trybu failover i aktualizacja zostanie zastosowana na drugim kontrolerze. Aktualizacja zostanie zakończona po zaktualizowaniu obu kontrolerów.
   
    Następujące przykładowe dane wyjściowe pokazują aktualizację w toku. `RunInprogress` Jest `True` gdy aktualizacja jest w toku.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Następujące przykładowe dane wyjściowe wskazują, że aktualizacja została zakończona. `RunInProgress` Jest `False` po ukończeniu aktualizacji.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > Czasem polecenie cmdlet zgłasza wartość `False`, gdy aktualizacja jest ciągle w toku. Aby upewnić się, że instalacja poprawki została zakończona, zaczekaj kilka minut, uruchom ponownie to polecenie i sprawdź, czy parametr `RunInProgress` ma wartość `False`. Jeśli tak jest, instalowanie poprawki zostało zakończone.

7. Po zakończeniu aktualizowania oprogramowania sprawdź wersje oprogramowania systemu. Wpisz:
   
    `Get-HcsSystem`
   
    Powinny zostać wyświetlone następujące wersje:
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    Jeśli numer wersji nie zmieni się po zastosowaniu aktualizacji, wskazuje to, że stosowanie poprawki nie powiodło się. Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.
     
    > [!IMPORTANT]
    > Należy ponownie uruchomić aktywnym kontrolerze za pośrednictwem `Restart-HcsController` polecenia cmdlet przed zastosowaniem na następną aktualizację.
     
8. Powtórz kroki od 3 do 6, aby zainstalować _CisMDSAgentupdate.exe_ agenta pobrane do Twojej _FirstOrderUpdate_ folderu.
8. Powtórz kroki od 3 do 6, aby zainstalować drugie aktualizacje kolejności. 

    > [!NOTE] 
    > Drugi kolejność aktualizacji, można zainstalować wiele aktualizacji, uruchamiając tylko `Start-HcsHotfix cmdlet` i wskazujący folder zawierający drugi kolejność aktualizacji. Polecenie cmdlet uruchomi wszystkie aktualizacje dostępne w tym folderze. Jeśli aktualizacja jest już zainstalowana, logika aktualizacji wykryje to i nie zastosuje tej aktualizacji.

    Po zainstalowaniu wszystkich poprawek użyj polecenia cmdlet `Get-HcsSystem`. Wersje powinny być następujące:
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a>Aby zainstalować i zweryfikować poprawki przeznaczone do trybu konserwacji

Użyj KB4037263 do instalowania aktualizacji oprogramowania układowego dysku. Te aktualizacje wymagają zatrzymania pracy i zajmują około 30 minut. Można zdecydować się na zainstalowanie ich w zaplanowanym oknie obsługi, łącząc się z konsolą szeregową urządzenia.

> [!NOTE] 
> Jeśli oprogramowanie układowe dysku jest już aktualne, nie będzie trzeba instalować te aktualizacje. Uruchom polecenie cmdlet `Get-HcsUpdateAvailability` z konsoli szeregowej urządzenia, aby sprawdzić, czy aktualizacje są dostępne i czy wymagają przerwania pracy (są przeznaczone do trybu konserwacji), czy nie (są przeznaczone do trybu normalnego).

Aby zainstalować aktualizacje oprogramowania układowego dysku, postępuj zgodnie z instrukcjami poniżej.

1. Przełącz urządzenie do trybu konserwacji. 

    > [!NOTE] 
    > Nie należy używać komunikacji zdalnej programu Windows PowerShell, łącząc się z urządzeniem w trybie konserwacji. Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia podczas połączenia za pośrednictwem konsoli szeregowej urządzenia.

    Ustaw kontroler w trybie konserwacji, wpisz:
   
    `Enter-HcsMaintenanceMode`
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Oba kontrolery są następnie uruchamiane ponownie w trybie konserwacji.
2. Aby zainstalować aktualizację oprogramowania układowego dysku, wpisz:
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. Monitoruj postęp instalacji za pomocą polecenia `Get-HcsUpdateStatus`. Aktualizacja będzie zakończona, gdy parametr `RunInProgress` zmieni wartość na `False`.
4. Po zakończeniu instalacji kontroler, na którym została zainstalowana poprawka przeznaczona do trybu konserwacji, zostanie uruchomiony ponownie. Zaloguj się za pomocą opcji 1 (z pełnym dostępem) i sprawdź wersję oprogramowania układowego dysku. Wpisz:
   
   `Get-HcsFirmwareVersion`
   
   Oczekiwane wersje oprogramowania układowego dysku to:
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   Poniżej pokazano przykładowe dane wyjściowe.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    Uruchom polecenie `Get-HcsFirmwareVersion` na drugim kontrolerze, aby sprawdzić, czy wersja oprogramowania została zaktualizowana. Następnie możesz wyjść z trybu konserwacji. W tym celu wpisz następujące polecenie dla każdego kontrolera urządzenia:
   
   `Exit-HcsMaintenanceMode`

5. Po wyjściu z trybu konserwacji kontrolery zostaną ponownie uruchomione. Po oprogramowania układowego dysku skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie opuścił tryb konserwacji, wróć do portalu Azure. Pamiętaj, że fakt zainstalowania aktualizacji przeznaczonych do trybu konserwacji może nie być widoczny w portalu nawet przez 24 godziny.

