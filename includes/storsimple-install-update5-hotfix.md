<!--author=alkohli last changed: 08/21/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="0d0e0-101">Aby pobrać poprawki</span><span class="sxs-lookup"><span data-stu-id="0d0e0-101">To download hotfixes</span></span>

<span data-ttu-id="0d0e0-102">Wykonaj następujące kroki, aby pobrać aktualizację oprogramowania z Wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="0d0e0-103">Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0d0e0-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="0d0e0-104">Jeśli po raz pierwszy używasz Wykazu usługi Microsoft Update na danym komputerze, po wyświetleniu monitu o zainstalowanie dodatku Wykazu usługi Microsoft Update kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Instalowanie wykazu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="0d0e0-106">W polu wyszukiwania z wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) poprawki do pobrania, na przykład **4037264**, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="0d0e0-107">Poprawka zostanie wyświetlona na liście, na przykład **zbiorczą 5.0 aktualizacji pakietu oprogramowania dla z serii StorSimple 8000**.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="0d0e0-109">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-109">Click **Download**.</span></span> <span data-ttu-id="0d0e0-110">Określ lokalizację lokalną, do której mają trafiać pobrane pliki, albo **przejdź** do takiej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="0d0e0-111">Kliknij przycisk pliki do pobrania do określonej lokalizacji i folderu.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="0d0e0-112">Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="0d0e0-113">Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli (**4037266**) i pobierz odpowiednie pliki do określonych folderów wymienione w powyższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-113">Search for any additional hotfixes listed in the table above (**4037266**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="0d0e0-114">Poprawki musi być dostępny z obu kontrolerów, aby wykryć potencjalne komunikaty o błędach z kontrolera elementu równorzędnego.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="0d0e0-115">Poprawki muszą zostać skopiowane do 3 oddzielnych folderów.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="0d0e0-116">Na przykład aktualizacja oprogramowania/Cis/MDS agenta urządzenia mogą być kopiowane w _FirstOrderUpdate_ folderu, mógł zostać skopiowany wszystkich innych Brak aktualizacji w _SecondOrderUpdate_ folderu, i aktualizacje trybu konserwacji skopiowany w _ThirdOrderUpdate_ folderu.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="0d0e0-117">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego</span><span class="sxs-lookup"><span data-stu-id="0d0e0-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="0d0e0-118">Wykonaj następujące kroki, aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="0d0e0-119">Jeśli została już zainstalowana ich przy użyciu portalu Azure, przejdź do [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="0d0e0-119">If you already installed them using the Azure portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="0d0e0-120">Aby zainstalować poprawki, przejdź do interfejsu programu Windows PowerShell na konsoli szeregowej Twojego urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="0d0e0-121">Postępuj zgodnie ze szczegółowymi instrukcjami w części [Nawiązywanie połączenia z konsolą szeregową urządzenia przy użyciu programu PuTTY](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="0d0e0-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="0d0e0-122">W wierszy polecenia naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="0d0e0-123">Wybierz **opcję 1**, aby zalogować się do urządzenia z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="0d0e0-124">Zalecamy, aby najpierw zainstalować poprawkę na kontrolerze pasywnym.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="0d0e0-125">Aby zainstalować poprawkę, w wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="0d0e0-126">W powyższym poleceniu użyj adresu IP zamiast nazwy DNS w ścieżce udziału.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="0d0e0-127">Parametr Credential jest używany tylko wtedy, gdy uzyskuje się dostęp do uwierzytelnionego udziału.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="0d0e0-128">Użycie parametru Credential jest zalecane przy uzyskiwaniu dostępu do udziałów.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="0d0e0-129">Nawet udziały otwarte dla wszystkich nie są zwykle otwarte dla użytkowników nieuwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
4. <span data-ttu-id="0d0e0-130">Po wyświetleniu monitu podaj hasło.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-130">Supply the password when prompted.</span></span> <span data-ttu-id="0d0e0-131">Przykładowe dane wyjściowe dotyczące instalacji aktualizacji stosowanych w pierwszej kolejności są pokazane poniżej.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="0d0e0-132">Pierwszą aktualizacją kolejności należy wskazać określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-132">For the first order update, you need to point to the specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="0d0e0-133">Należy zainstalować _HcsSoftwareUpdate.exe_ pierwszy.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-133">You should install the _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="0d0e0-134">Po zakończeniu tej instalacji, następnie zainstalować _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="0d0e0-135">Wpisz **Y**, gdy zostanie wyświetlony monit o potwierdzenie instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-135">Type **Y** when prompted to confirm the hotfix installation.</span></span>
6. <span data-ttu-id="0d0e0-136">Monitoruj aktualizację za pomocą polecenia cmdlet `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-136">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="0d0e0-137">Aktualizacja zakończy się najpierw na kontrolerze pasywnym.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-137">The update will first complete on the passive controller.</span></span> <span data-ttu-id="0d0e0-138">Gdy kontroler pasywny zostanie zaktualizowany, nastąpi przejście do trybu failover i aktualizacja zostanie zastosowana na drugim kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-138">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="0d0e0-139">Aktualizacja zostanie zakończona po zaktualizowaniu obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-139">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="0d0e0-140">Następujące przykładowe dane wyjściowe pokazują aktualizację w toku.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-140">The following sample output shows the update in progress.</span></span> <span data-ttu-id="0d0e0-141">`RunInprogress` Jest `True` gdy aktualizacja jest w toku.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-141">The `RunInprogress` is `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="0d0e0-142">Następujące przykładowe dane wyjściowe wskazują, że aktualizacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-142">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="0d0e0-143">`RunInProgress` Jest `False` po ukończeniu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-143">The `RunInProgress` is `False` when the update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="0d0e0-144">Czasem polecenie cmdlet zgłasza wartość `False`, gdy aktualizacja jest ciągle w toku.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-144">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="0d0e0-145">Aby upewnić się, że instalacja poprawki została zakończona, zaczekaj kilka minut, uruchom ponownie to polecenie i sprawdź, czy parametr `RunInProgress` ma wartość `False`.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-145">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="0d0e0-146">Jeśli tak jest, instalowanie poprawki zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-146">If it is, then the hotfix has completed.</span></span>

7. <span data-ttu-id="0d0e0-147">Po zakończeniu aktualizowania oprogramowania sprawdź wersje oprogramowania systemu.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-147">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="0d0e0-148">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="0d0e0-149">Powinny zostać wyświetlone następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-149">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="0d0e0-150">Jeśli numer wersji nie zmieni się po zastosowaniu aktualizacji, wskazuje to, że stosowanie poprawki nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-150">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="0d0e0-151">Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="0d0e0-152">Należy ponownie uruchomić aktywnym kontrolerze za pośrednictwem `Restart-HcsController` polecenia cmdlet przed zastosowaniem na następną aktualizację.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-152">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
8. <span data-ttu-id="0d0e0-153">Powtórz kroki od 3 do 6, aby zainstalować _CisMDSAgentupdate.exe_ agenta pobrane do Twojej _FirstOrderUpdate_ folderu.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-153">Repeat steps 3-6 to install the _CisMDSAgentupdate.exe_ agent downloaded to your _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="0d0e0-154">Powtórz kroki od 3 do 6, aby zainstalować drugie aktualizacje kolejności.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-154">Repeat steps 3-6 to install the second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="0d0e0-155">Drugi kolejność aktualizacji, można zainstalować wiele aktualizacji, uruchamiając tylko `Start-HcsHotfix cmdlet` i wskazujący folder zawierający drugi kolejność aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-155">For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located.</span></span> <span data-ttu-id="0d0e0-156">Polecenie cmdlet uruchomi wszystkie aktualizacje dostępne w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-156">The cmdlet will execute all the updates available in the folder.</span></span> <span data-ttu-id="0d0e0-157">Jeśli aktualizacja jest już zainstalowana, logika aktualizacji wykryje to i nie zastosuje tej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-157">If an update is already installed, the update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="0d0e0-158">Po zainstalowaniu wszystkich poprawek użyj polecenia cmdlet `Get-HcsSystem`.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-158">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="0d0e0-159">Wersje powinny być następujące:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-159">The versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="0d0e0-160">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="0d0e0-160">To install and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="0d0e0-161">Użyj KB4037263 do instalowania aktualizacji oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-161">Use KB4037263 to install disk firmware updates.</span></span> <span data-ttu-id="0d0e0-162">Te aktualizacje wymagają zatrzymania pracy i zajmują około 30 minut.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-162">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="0d0e0-163">Można zdecydować się na zainstalowanie ich w zaplanowanym oknie obsługi, łącząc się z konsolą szeregową urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-163">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="0d0e0-164">Jeśli oprogramowanie układowe dysku jest już aktualne, nie będzie trzeba instalować te aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-164">If your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="0d0e0-165">Uruchom polecenie cmdlet `Get-HcsUpdateAvailability` z konsoli szeregowej urządzenia, aby sprawdzić, czy aktualizacje są dostępne i czy wymagają przerwania pracy (są przeznaczone do trybu konserwacji), czy nie (są przeznaczone do trybu normalnego).</span><span class="sxs-lookup"><span data-stu-id="0d0e0-165">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="0d0e0-166">Aby zainstalować aktualizacje oprogramowania układowego dysku, postępuj zgodnie z instrukcjami poniżej.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-166">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="0d0e0-167">Przełącz urządzenie do trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-167">Place the device in the maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="0d0e0-168">Nie należy używać komunikacji zdalnej programu Windows PowerShell, łącząc się z urządzeniem w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-168">Do not use Windows PowerShell remoting when connecting to a device in maintenance mode.</span></span> <span data-ttu-id="0d0e0-169">Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia podczas połączenia za pośrednictwem konsoli szeregowej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-169">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span>

    <span data-ttu-id="0d0e0-170">Ustaw kontroler w trybie konserwacji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-170">To place the controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="0d0e0-171">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-171">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="0d0e0-172">Oba kontrolery są następnie uruchamiane ponownie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-172">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="0d0e0-173">Aby zainstalować aktualizację oprogramowania układowego dysku, wpisz:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-173">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="0d0e0-174">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="0d0e0-175">Monitoruj postęp instalacji za pomocą polecenia `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-175">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="0d0e0-176">Aktualizacja będzie zakończona, gdy parametr `RunInProgress` zmieni wartość na `False`.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-176">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="0d0e0-177">Po zakończeniu instalacji kontroler, na którym została zainstalowana poprawka przeznaczona do trybu konserwacji, zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-177">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="0d0e0-178">Zaloguj się za pomocą opcji 1 (z pełnym dostępem) i sprawdź wersję oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-178">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="0d0e0-179">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="0d0e0-180">Oczekiwane wersje oprogramowania układowego dysku to:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-180">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="0d0e0-181">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-181">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="0d0e0-182">Uruchom polecenie `Get-HcsFirmwareVersion` na drugim kontrolerze, aby sprawdzić, czy wersja oprogramowania została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-182">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="0d0e0-183">Następnie możesz wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-183">You can then exit the maintenance mode.</span></span> <span data-ttu-id="0d0e0-184">W tym celu wpisz następujące polecenie dla każdego kontrolera urządzenia:</span><span class="sxs-lookup"><span data-stu-id="0d0e0-184">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="0d0e0-185">Po wyjściu z trybu konserwacji kontrolery zostaną ponownie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-185">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="0d0e0-186">Po oprogramowania układowego dysku skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie opuścił tryb konserwacji, wróć do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-186">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure portal.</span></span> <span data-ttu-id="0d0e0-187">Pamiętaj, że fakt zainstalowania aktualizacji przeznaczonych do trybu konserwacji może nie być widoczny w portalu nawet przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="0d0e0-187">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

