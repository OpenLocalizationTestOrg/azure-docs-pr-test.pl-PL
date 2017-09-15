<!--author=alkohli last changed: 09/01/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="af30c-101">Aby pobrać poprawki</span><span class="sxs-lookup"><span data-stu-id="af30c-101">To download hotfixes</span></span>
<span data-ttu-id="af30c-102">Wykonaj następujące kroki, aby pobrać aktualizację oprogramowania z Wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="af30c-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="af30c-103">Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="af30c-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="af30c-104">Jeśli po raz pierwszy używasz Wykazu usługi Microsoft Update na danym komputerze, po wyświetleniu monitu o zainstalowanie dodatku Wykazu usługi Microsoft Update kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="af30c-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="af30c-105">![Zainstaluj katalogu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="af30c-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="af30c-106">W polu wyszukiwania z wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) poprawki do pobrania, na przykład **3186843**, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="af30c-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3186843**, and then click **Search**.</span></span>
   
    <span data-ttu-id="af30c-107">Poprawka zostanie wyświetlona na liście, na przykład **zbiorczą 3.0 aktualizacji pakietu oprogramowania dla z serii StorSimple 8000**.</span><span class="sxs-lookup"><span data-stu-id="af30c-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 3.0 for StorSimple 8000 Series**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="af30c-109">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="af30c-109">Click **Add**.</span></span> <span data-ttu-id="af30c-110">Aktualizacja zostanie dodana do koszyka.</span><span class="sxs-lookup"><span data-stu-id="af30c-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="af30c-111">Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli (**3186859**) i Dodaj do koszyka.</span><span class="sxs-lookup"><span data-stu-id="af30c-111">Search for any additional hotfixes listed in the table above (**3186859**), and add each to the basket.</span></span>
6. <span data-ttu-id="af30c-112">Kliknij pozycję **Wyświetl koszyk**.</span><span class="sxs-lookup"><span data-stu-id="af30c-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="af30c-113">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="af30c-113">Click **Download**.</span></span> <span data-ttu-id="af30c-114">Określ lokalizację lokalną, do której mają trafiać pobrane pliki, albo **przejdź** do takiej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="af30c-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="af30c-115">Aktualizacje są pobierane do określonej lokalizacji i umieszczane w podfolderze o takiej samej nazwie, jak w przypadku aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="af30c-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="af30c-116">Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="af30c-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="af30c-117">Poprawki musi być dostępny z obu kontrolerów, aby wykryć potencjalne komunikaty o błędach z kontrolera elementu równorzędnego.</span><span class="sxs-lookup"><span data-stu-id="af30c-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="af30c-118">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego</span><span class="sxs-lookup"><span data-stu-id="af30c-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="af30c-119">Wykonaj następujące kroki, aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego.</span><span class="sxs-lookup"><span data-stu-id="af30c-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="af30c-120">Jeśli została już zainstalowana ich przy użyciu portalu Azure, przejdź do [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="af30c-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="af30c-121">Aby zainstalować poprawki, przejdź do interfejsu programu Windows PowerShell na konsoli szeregowej Twojego urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="af30c-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="af30c-122">Postępuj zgodnie ze szczegółowymi instrukcjami w części [Nawiązywanie połączenia z konsolą szeregową urządzenia przy użyciu programu PuTTY](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="af30c-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="af30c-123">W wierszy polecenia naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="af30c-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="af30c-124">Wybierz **opcję 1**, aby zalogować się do urządzenia z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="af30c-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="af30c-125">Zalecamy, aby najpierw zainstalować poprawkę na kontrolerze pasywnym.</span><span class="sxs-lookup"><span data-stu-id="af30c-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="af30c-126">Aby zainstalować poprawkę, w wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="af30c-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="af30c-127">W powyższym poleceniu użyj adresu IP zamiast nazwy DNS w ścieżce udziału.</span><span class="sxs-lookup"><span data-stu-id="af30c-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="af30c-128">Parametr Credential jest używany tylko wtedy, gdy uzyskuje się dostęp do uwierzytelnionego udziału.</span><span class="sxs-lookup"><span data-stu-id="af30c-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="af30c-129">Użycie parametru Credential jest zalecane przy uzyskiwaniu dostępu do udziałów.</span><span class="sxs-lookup"><span data-stu-id="af30c-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="af30c-130">Nawet udziały otwarte dla wszystkich nie są zwykle otwarte dla użytkowników nieuwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="af30c-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="af30c-131">Po wyświetleniu monitu podaj hasło.</span><span class="sxs-lookup"><span data-stu-id="af30c-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="af30c-132">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="af30c-132">A sample output is shown below.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="af30c-133">Wpisz **Y**, gdy zostanie wyświetlony monit o potwierdzenie instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="af30c-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="af30c-134">Monitoruj aktualizację za pomocą polecenia cmdlet `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="af30c-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="af30c-135">Aktualizacja zakończy się najpierw na kontrolerze pasywnym.</span><span class="sxs-lookup"><span data-stu-id="af30c-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="af30c-136">Gdy kontroler pasywny zostanie zaktualizowany, nastąpi przejście do trybu failover i aktualizacja zostanie zastosowana na drugim kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="af30c-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="af30c-137">Aktualizacja zostanie zakończona po zaktualizowaniu obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="af30c-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="af30c-138">Następujące przykładowe dane wyjściowe pokazują aktualizację w toku.</span><span class="sxs-lookup"><span data-stu-id="af30c-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="af30c-139">Gdy aktualizacja będzie w toku, parametr `RunInprogress` będzie mieć wartość `True`.</span><span class="sxs-lookup"><span data-stu-id="af30c-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="af30c-140">Następujące przykładowe dane wyjściowe wskazują, że aktualizacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="af30c-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="af30c-141">Gdy aktualizacja zostanie zakończona, parametr `RunInProgress` będzie mieć wartość `False`.</span><span class="sxs-lookup"><span data-stu-id="af30c-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > <span data-ttu-id="af30c-142">Czasem polecenie cmdlet zgłasza wartość `False`, gdy aktualizacja jest ciągle w toku.</span><span class="sxs-lookup"><span data-stu-id="af30c-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="af30c-143">Aby upewnić się, że instalacja poprawki została zakończona, zaczekaj kilka minut, uruchom ponownie to polecenie i sprawdź, czy parametr `RunInProgress` ma wartość `False`.</span><span class="sxs-lookup"><span data-stu-id="af30c-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="af30c-144">Jeśli tak jest, instalowanie poprawki zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="af30c-144">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="af30c-145">Po zakończeniu aktualizowania oprogramowania sprawdź wersje oprogramowania systemu.</span><span class="sxs-lookup"><span data-stu-id="af30c-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="af30c-146">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="af30c-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="af30c-147">Powinny zostać wyświetlone następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="af30c-147">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     <span data-ttu-id="af30c-148">Po zastosowaniu tej aktualizacji nie należy zmieniać numerów wersji, wskazuje, że poprawka nie zastosować.</span><span class="sxs-lookup"><span data-stu-id="af30c-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="af30c-149">Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.</span><span class="sxs-lookup"><span data-stu-id="af30c-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="af30c-150">Przed zastosowaniem pozostałych aktualizacji musisz uruchomić ponownie kontroler aktywny za pomocą polecenia cmdlet `Restart-HcsController`.</span><span class="sxs-lookup"><span data-stu-id="af30c-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="af30c-151">Powtórz kroki 3 – 5, aby zainstalować poprawkę sterowników i oprogramowania układowego LSI **KB3186859**.</span><span class="sxs-lookup"><span data-stu-id="af30c-151">Repeat steps 3-5 to install the LSI driver and firmware hotfix **KB3186859**.</span></span> <span data-ttu-id="af30c-152">Po zainstalowaniu poprawki należy użyć `Get-HcsSystem` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="af30c-152">After the hotfix is installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="af30c-153">Wersja LSI powinny być:</span><span class="sxs-lookup"><span data-stu-id="af30c-153">The LSI version should be:</span></span>
   
   * `Lsisas2Version: 2.0.78.00`
3. <span data-ttu-id="af30c-154">Powtórz kroki 3 – 5, aby zainstalować aktualizację Storport i Spaceport **KB3121261**.</span><span class="sxs-lookup"><span data-stu-id="af30c-154">Repeat steps 3-5 to install the Storport and Spaceport update **KB3121261**.</span></span>
4. <span data-ttu-id="af30c-155">Jeśli aktualizacja Update 2 lub starszej wersji, zostanie również należy pobrać:</span><span class="sxs-lookup"><span data-stu-id="af30c-155">If you are updating from Update 2 or earlier version, you will also need to download:</span></span>
   
   * <span data-ttu-id="af30c-156">poprawka iSCSI przy użyciu KB3146621</span><span class="sxs-lookup"><span data-stu-id="af30c-156">iSCSI fix using KB3146621</span></span>
   * <span data-ttu-id="af30c-157">Poprawka WMI za pomocą KB3103616</span><span class="sxs-lookup"><span data-stu-id="af30c-157">WMI fix using KB3103616</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="af30c-158">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="af30c-158">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="af30c-159">Użyj KB3121899 do instalowania aktualizacji oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="af30c-159">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="af30c-160">Te aktualizacje wymagają zatrzymania pracy i zajmują około 30 minut.</span><span class="sxs-lookup"><span data-stu-id="af30c-160">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="af30c-161">Można zdecydować się na zainstalowanie ich w zaplanowanym oknie obsługi, łącząc się z konsolą szeregową urządzenia.</span><span class="sxs-lookup"><span data-stu-id="af30c-161">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="af30c-162">Pamiętaj, że jeśli oprogramowanie układowe dysku jest już aktualne, tych aktualizacji nie trzeba instalować.</span><span class="sxs-lookup"><span data-stu-id="af30c-162">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="af30c-163">Uruchom polecenie cmdlet `Get-HcsUpdateAvailability` z konsoli szeregowej urządzenia, aby sprawdzić, czy aktualizacje są dostępne i czy wymagają przerwania pracy (są przeznaczone do trybu konserwacji), czy nie (są przeznaczone do trybu normalnego).</span><span class="sxs-lookup"><span data-stu-id="af30c-163">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="af30c-164">Aby zainstalować aktualizacje oprogramowania układowego dysku, postępuj zgodnie z instrukcjami poniżej.</span><span class="sxs-lookup"><span data-stu-id="af30c-164">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="af30c-165">Ustaw urządzenia w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="af30c-165">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="af30c-166">Należy pamiętać, że nie należy używać komunikacji zdalnej programu Windows PowerShell podczas nawiązywania połączenia z urządzeniem w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="af30c-166">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="af30c-167">Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia podczas połączenia za pośrednictwem konsoli szeregowej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="af30c-167">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="af30c-168">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="af30c-168">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="af30c-169">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="af30c-169">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="af30c-170">Zarówno kontrolery następnie uruchom ponownie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="af30c-170">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="af30c-171">Aby zainstalować aktualizację oprogramowania układowego dysku, wpisz:</span><span class="sxs-lookup"><span data-stu-id="af30c-171">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="af30c-172">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="af30c-172">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="af30c-173">Monitoruj postęp instalacji za pomocą polecenia `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="af30c-173">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="af30c-174">Aktualizacja będzie zakończona, gdy parametr `RunInProgress` zmieni wartość na `False`.</span><span class="sxs-lookup"><span data-stu-id="af30c-174">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="af30c-175">Po zakończeniu instalacji kontroler, na którym została zainstalowana poprawka przeznaczona do trybu konserwacji, zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="af30c-175">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="af30c-176">Zaloguj się za pomocą opcji 1 (z pełnym dostępem) i sprawdź wersję oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="af30c-176">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="af30c-177">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="af30c-177">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="af30c-178">Oczekiwane wersje oprogramowania układowego dysku to:</span><span class="sxs-lookup"><span data-stu-id="af30c-178">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="af30c-179">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="af30c-179">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="af30c-180">Uruchom polecenie `Get-HcsFirmwareVersion` na drugim kontrolerze, aby sprawdzić, czy wersja oprogramowania została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="af30c-180">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="af30c-181">Następnie możesz wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="af30c-181">You can then exit the maintenance mode.</span></span> <span data-ttu-id="af30c-182">W tym celu wpisz następujące polecenie dla każdego kontrolera urządzenia:</span><span class="sxs-lookup"><span data-stu-id="af30c-182">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="af30c-183">Kontrolery Uruchom ponownie po wyjściu z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="af30c-183">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="af30c-184">Gdy aktualizacje oprogramowania układowego dysku zostaną pomyślnie zastosowane i urządzenie wyjdzie z trybu konserwacji, wróć do klasycznej witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="af30c-184">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="af30c-185">Należy pamiętać, że portalu nie mogą być wyświetlane, czy zainstalowane aktualizacje trybu konserwacji na 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="af30c-185">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

