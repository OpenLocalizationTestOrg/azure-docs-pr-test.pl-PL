<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>poprawki toodownload
Wykonaj powitania po aktualizacji oprogramowania hello toodownload czynności.

1. Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.
    ![Zainstaluj katalogu](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello hello poprawki mają toodownload, na przykład **3063418**, a następnie kliknij przycisk **wyszukiwania**.
4. Zobaczysz hello **StorSimple aktualizacja 1.2 urządzenia aktualizacja** pakietu. Kliknij pozycję **Dodaj**. Aktualizacja Hello zostaną dodane toohello koszyka.
5. Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli hello (**3043005** i **3063416**) i Dodaj każdy koszyka hello.
6. Kliknij pozycję **Wyświetl koszyk**.
   
    ![Wyświetl koszyk](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. Kliknij pozycję **Pobierz**. Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear. Witaj aktualizacje zostaną pobrane toohello określonej lokalizacji i umieszczane w podfolderze o hello takie same nazwy co hello update. Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.

> [!NOTE]
> poprawki Hello musi być dostępny z obu toodetect kontrolerów wszelkie potencjalne błędy komunikaty z hello równorzędnej kontrolera.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall i sprawdź regularne poprawki
Wykonaj następujące kroki tooinstall hello i sprawdź poprawki hello regularne. Jeśli zainstalowano je przy użyciu hello portalu Azure przejdź za[zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).

1. Aktualizacja oprogramowania hello tooinstall, interfejsu programu Windows PowerShell hello dostępu na konsoli szeregowej urządzenia StorSimple. Wykonaj hello szczegółowe instrukcje w [konsoli szeregowej przy użyciu programu PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). W wierszu polecenia hello naciśnij **Enter**.
2. Wybierz **opcję 1** toolog toohello urządzenia z pełnym dostępem.
3. tooinstall hello pakiet aktualizacji, w wierszu polecenia wpisz hello:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Użyj adresu IP, a nie DNS w ścieżce udziału hello powyżej polecenia. Parametr credential Hello jest używany tylko wtedy, gdy uzyskujesz dostęp do udziału uwierzytelniony.
   
    Zalecamy użycie udziałów tooaccess parametr credential hello. Nawet udziałów, które są otwarte za "wszyscy" są zwykle nie otworzyć toounauthenticated użytkowników.
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Typ **Y** gdy zostanie wyświetlony monit o tooconfirm hello instalacji poprawki.
5. Monitoruj hello aktualizacji za pomocą hello `Get-HcsUpdateStatus` polecenia cmdlet.
   
    Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku. Witaj `RunInprogress` będzie `True` podczas aktualizacji hello jest w toku.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone. Witaj `RunInProgress` będzie `False` po zakończeniu aktualizacji hello.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > Czasami hello raporty polecenia cmdlet `False` podczas aktualizacji hello jest nadal w toku. tooensure, który hello poprawka została ukończona, poczekaj kilka minut, ponownie uruchomić to polecenie i sprawdź, że hello `RunInProgress` jest `False`. Jeśli tak jest, poprawki hello zostało zakończone.
   > 
   > 
6. Po zakończeniu aktualizacji oprogramowania hello Sprawdź wersje oprogramowania hello systemu. Wpisz następujące polecenie hello:
   
    `Get-HcsSystem`
   
    Powinny pojawić się hello następujące wersje:
   
   * HcsSoftwareVersion: 6.3.9600.17584
   * CisAgentVersion: 1.0.9049.0
   * MdsAgentVersion: 26.0.4696.1433
     
     Jeśli po zastosowaniu aktualizacji hello nie należy zmieniać numerów wersji hello, oznacza to, że ta poprawka hello nie powiodło się tooapply. Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.
7. Powtórz kroki 3 – 5 tooinstall hello pozostałych poprawki tryb zwykły (KB3043005).

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall i sprawdź poprawki trybu konserwacji
Użyj aktualizacji oprogramowania układowego dysku tooinstall KB3063416. Te aktualizacje zakłócenie i zająć około 30 do 45 minut toocomplete. Można wybrać tooinstall je w oknie obsługi planowanych przez łączącego konsoli szeregowej urządzenia toohello.

aktualizacje oprogramowania układowego tooinstall hello dysku, wykonaj poniższe instrukcje hello.

1. Ustaw hello urządzenia w trybie konserwacji. Należy pamiętać, że nie należy używać komunikacji zdalnej programu Windows PowerShell podczas łączenia tooa urządzenia w trybie konserwacji. Konieczne będzie toorun tego polecenia cmdlet na kontrolerze urządzenia hello podczas połączenia za pośrednictwem konsoli szeregowej urządzenia hello. Wpisz:
   
    `Enter-HcsMaintenanceMode`
   
    Poniżej pokazano przykładowe dane wyjściowe.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
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
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. Monitor hello Instaluj postępu przy użyciu `Get-HcsUpdateStatus` polecenia. Witaj aktualizacja została ukończona, gdy hello `RunInProgress` zmiany zbyt`False`.
4. Po zakończeniu instalacji hello hello kontrolera, na którym zainstalowano poprawkę trybu konserwacji hello zostanie uruchomiony ponownie. Zaloguj się jako opcja 1 z pełnym dostępem i sprawdź, wersja oprogramowania układowego hello dysku. Wpisz:
   
   `Get-HcsFirmwareVersion`
   
   Witaj oczekiwanych wersji oprogramowania układowego dysku:
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Uruchom hello `Get-HcsFirmwareVersion` polecenie hello drugi kontroler tooverify który hello wersji oprogramowania została zaktualizowana. Następnie można zakończyć tryb konserwacji hello. Wpisz następujące polecenie dla każdego kontrolera urządzenia hello:
   
   `Exit-HcsMaintenanceMode`
5. kontrolery Hello ponownie po wyjściu z trybu konserwacji. Po oprogramowania układowego dysku hello skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie hello opuścił tryb konserwacji, zwracany toohello klasycznego portalu Azure. Należy pamiętać, że tego portalu hello nie mogą być wyświetlane, czy zainstalowane aktualizacje w trybie konserwacji hello przez 24 godziny.

