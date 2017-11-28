<!--author=SharS last changed: 03/17/2016-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="885ef-101">Aby pobrać poprawki</span><span class="sxs-lookup"><span data-stu-id="885ef-101">To download hotfixes</span></span>
<span data-ttu-id="885ef-102">Wykonaj poniższe kroki, aby pobrać aktualizację oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="885ef-102">Perform the following steps to download the software update.</span></span>

1. <span data-ttu-id="885ef-103">Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="885ef-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="885ef-104">Jeśli po raz pierwszy używasz Wykazu usługi Microsoft Update na danym komputerze, po wyświetleniu monitu o zainstalowanie dodatku Wykazu usługi Microsoft Update kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="885ef-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="885ef-105">![Zainstaluj katalogu](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="885ef-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="885ef-106">W polu wyszukiwania z wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) poprawki do pobrania, na przykład **3063418**, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="885ef-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="885ef-107">Zobaczysz **StorSimple aktualizacja 1.2 urządzenia aktualizacja** pakietu.</span><span class="sxs-lookup"><span data-stu-id="885ef-107">You will see the **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="885ef-108">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="885ef-108">Click **Add**.</span></span> <span data-ttu-id="885ef-109">Aktualizacja zostanie dodany do koszyka.</span><span class="sxs-lookup"><span data-stu-id="885ef-109">The update will be added to the basket.</span></span>
5. <span data-ttu-id="885ef-110">Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli (**3043005** i **3063416**) i Dodaj każdy koszyka.</span><span class="sxs-lookup"><span data-stu-id="885ef-110">Search for any additional hotfixes listed in the table above (**3043005** and **3063416**), and add each the basket.</span></span>
6. <span data-ttu-id="885ef-111">Kliknij pozycję **Wyświetl koszyk**.</span><span class="sxs-lookup"><span data-stu-id="885ef-111">Click **View Basket**.</span></span>
   
    ![Wyświetl koszyk](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="885ef-113">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="885ef-113">Click **Download**.</span></span> <span data-ttu-id="885ef-114">Określ lokalizację lokalną, do której mają trafiać pobrane pliki, albo **przejdź** do takiej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="885ef-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="885ef-115">Aktualizacje zostaną pobrane do wskazanej lokalizacji i umieszczone w podfolderze o nazwie takiej samej jak aktualizacja.</span><span class="sxs-lookup"><span data-stu-id="885ef-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="885ef-116">Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="885ef-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="885ef-117">Poprawki musi być dostępny z obu kontrolerów, aby wykryć potencjalne komunikaty o błędach z kontrolera elementu równorzędnego.</span><span class="sxs-lookup"><span data-stu-id="885ef-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="885ef-118">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego</span><span class="sxs-lookup"><span data-stu-id="885ef-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="885ef-119">Wykonaj poniższe kroki, aby zainstalować i sprawdź poprawki tryb zwykły.</span><span class="sxs-lookup"><span data-stu-id="885ef-119">Perform the following steps to install and verify the regular-mode hotfixes.</span></span> <span data-ttu-id="885ef-120">Jeśli została już zainstalowana ich przy użyciu portalu Azure, przejdź do [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="885ef-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="885ef-121">Aby zainstalować aktualizację oprogramowania, dostęp do interfejsu programu Windows PowerShell na konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="885ef-121">To install the software update, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="885ef-122">Postępuj zgodnie ze szczegółowymi instrukcjami w części [Nawiązywanie połączenia z konsolą szeregową urządzenia przy użyciu programu PuTTY](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="885ef-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="885ef-123">W wierszy polecenia naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="885ef-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="885ef-124">Wybierz **opcję 1**, aby zalogować się do urządzenia z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="885ef-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="885ef-125">Aby zainstalować pakiet aktualizacji, w wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="885ef-125">To install the update package, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="885ef-126">W powyższym poleceniu użyj adresu IP zamiast nazwy DNS w ścieżce udziału.</span><span class="sxs-lookup"><span data-stu-id="885ef-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="885ef-127">Parametr Credential jest używany tylko wtedy, gdy uzyskuje się dostęp do uwierzytelnionego udziału.</span><span class="sxs-lookup"><span data-stu-id="885ef-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="885ef-128">Użycie parametru Credential jest zalecane przy uzyskiwaniu dostępu do udziałów.</span><span class="sxs-lookup"><span data-stu-id="885ef-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="885ef-129">Nawet udziały otwarte dla wszystkich nie są zwykle otwarte dla użytkowników nieuwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="885ef-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="885ef-130">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="885ef-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="885ef-131">Wpisz **Y**, gdy zostanie wyświetlony monit o potwierdzenie instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="885ef-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="885ef-132">Monitoruj aktualizację za pomocą polecenia cmdlet `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="885ef-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="885ef-133">Następujące przykładowe dane wyjściowe pokazują aktualizację w toku.</span><span class="sxs-lookup"><span data-stu-id="885ef-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="885ef-134">Gdy aktualizacja będzie w toku, parametr `RunInprogress` będzie mieć wartość `True`.</span><span class="sxs-lookup"><span data-stu-id="885ef-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="885ef-135">Następujące przykładowe dane wyjściowe wskazują, że aktualizacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="885ef-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="885ef-136">Gdy aktualizacja zostanie zakończona, parametr `RunInProgress` będzie mieć wartość `False`.</span><span class="sxs-lookup"><span data-stu-id="885ef-136">The `RunInProgress` will be `False` when the update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="885ef-137">Czasem polecenie cmdlet zgłasza wartość `False`, gdy aktualizacja jest ciągle w toku.</span><span class="sxs-lookup"><span data-stu-id="885ef-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="885ef-138">Aby upewnić się, że instalacja poprawki została zakończona, zaczekaj kilka minut, uruchom ponownie to polecenie i sprawdź, czy parametr `RunInProgress` ma wartość `False`.</span><span class="sxs-lookup"><span data-stu-id="885ef-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="885ef-139">Jeśli tak jest, instalowanie poprawki zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="885ef-139">If it is, then the hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="885ef-140">Po zakończeniu aktualizowania oprogramowania sprawdź wersje oprogramowania systemu.</span><span class="sxs-lookup"><span data-stu-id="885ef-140">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="885ef-141">Wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="885ef-141">Type the following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="885ef-142">Powinny zostać wyświetlone następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="885ef-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="885ef-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="885ef-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="885ef-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="885ef-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="885ef-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="885ef-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="885ef-146">Po zastosowaniu tej aktualizacji nie należy zmieniać numerów wersji, wskazuje, że poprawka nie zastosować.</span><span class="sxs-lookup"><span data-stu-id="885ef-146">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="885ef-147">Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.</span><span class="sxs-lookup"><span data-stu-id="885ef-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="885ef-148">Powtórz kroki 3 – 5, aby zainstalować poprawkę pozostałych tryb zwykły (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="885ef-148">Repeat steps 3-5 to install the remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="885ef-149">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="885ef-149">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="885ef-150">Użyj KB3063416 do instalowania aktualizacji oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="885ef-150">Use KB3063416 to install disk firmware updates.</span></span> <span data-ttu-id="885ef-151">Te aktualizacje zakłócenie i zająć około 30 do 45 minut, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="885ef-151">These are disruptive updates and take around 30-45 minutes to complete.</span></span> <span data-ttu-id="885ef-152">Można zdecydować się na zainstalowanie ich w zaplanowanym oknie obsługi, łącząc się z konsolą szeregową urządzenia.</span><span class="sxs-lookup"><span data-stu-id="885ef-152">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="885ef-153">Aby zainstalować aktualizacje oprogramowania układowego dysku, postępuj zgodnie z instrukcjami poniżej.</span><span class="sxs-lookup"><span data-stu-id="885ef-153">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="885ef-154">Ustaw urządzenia w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="885ef-154">Place the device in Maintenance mode.</span></span> <span data-ttu-id="885ef-155">Należy pamiętać, że nie należy używać komunikacji zdalnej programu Windows PowerShell podczas nawiązywania połączenia z urządzeniem w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="885ef-155">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="885ef-156">Musisz uruchomić to polecenie cmdlet na kontrolerze urządzenia podczas połączenia za pośrednictwem konsoli szeregowej urządzenia.</span><span class="sxs-lookup"><span data-stu-id="885ef-156">You will need to run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="885ef-157">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="885ef-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="885ef-158">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="885ef-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="885ef-159">Zarówno kontrolery następnie uruchom ponownie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="885ef-159">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="885ef-160">Aby zainstalować aktualizację oprogramowania układowego dysku, wpisz:</span><span class="sxs-lookup"><span data-stu-id="885ef-160">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="885ef-161">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="885ef-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="885ef-162">Monitoruj postęp instalacji za pomocą polecenia `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="885ef-162">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="885ef-163">Aktualizacja będzie zakończona, gdy parametr `RunInProgress` zmieni wartość na `False`.</span><span class="sxs-lookup"><span data-stu-id="885ef-163">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="885ef-164">Po zakończeniu instalacji, kontroler, na którym zainstalowano poprawkę trybu konserwacji zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="885ef-164">After the installation is complete, the controller on which the maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="885ef-165">Zaloguj się za pomocą opcji 1 (z pełnym dostępem) i sprawdź wersję oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="885ef-165">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="885ef-166">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="885ef-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="885ef-167">Oczekiwane wersje oprogramowania układowego dysku to:</span><span class="sxs-lookup"><span data-stu-id="885ef-167">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="885ef-168">Uruchom polecenie `Get-HcsFirmwareVersion` na drugim kontrolerze, aby sprawdzić, czy wersja oprogramowania została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="885ef-168">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="885ef-169">Następnie możesz wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="885ef-169">You can then exit the maintenance mode.</span></span> <span data-ttu-id="885ef-170">Wpisz następujące polecenie dla każdego kontrolera urządzenia:</span><span class="sxs-lookup"><span data-stu-id="885ef-170">Type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="885ef-171">Kontrolery Uruchom ponownie po wyjściu z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="885ef-171">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="885ef-172">Gdy aktualizacje oprogramowania układowego dysku zostaną pomyślnie zastosowane i urządzenie wyjdzie z trybu konserwacji, wróć do klasycznej witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="885ef-172">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="885ef-173">Należy pamiętać, że portalu nie mogą być wyświetlane, czy zainstalowane aktualizacje trybu konserwacji na 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="885ef-173">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

