<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="3d2cc-101">Aby pobrać poprawki</span><span class="sxs-lookup"><span data-stu-id="3d2cc-101">To download hotfixes</span></span>

<span data-ttu-id="3d2cc-102">Wykonaj następujące kroki, aby pobrać aktualizację oprogramowania z Wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="3d2cc-103">Uruchom program Internet Explorer i przejdź pod adres [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3d2cc-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="3d2cc-104">Jeśli po raz pierwszy używasz Wykazu usługi Microsoft Update na danym komputerze, po wyświetleniu monitu o zainstalowanie dodatku Wykazu usługi Microsoft Update kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Instalowanie wykazu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="3d2cc-106">W polu wyszukiwania Wykazu usługi Microsoft Update wprowadź numer w bazie wiedzy (KB) dla poprawki, którą chcesz pobrać, na przykład **4011839**, a następnie kliknij przycisk **Wyszukaj**.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="3d2cc-107">Zostanie wyświetlona lista poprawek zawierająca na przykład pozycję **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="3d2cc-109">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-109">Click **Download**.</span></span> <span data-ttu-id="3d2cc-110">Określ lokalizację lokalną, do której mają trafiać pobrane pliki, albo **przejdź** do takiej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="3d2cc-111">Kliknij przycisk pliki do pobrania do określonej lokalizacji i folderu.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="3d2cc-112">Folder można też skopiować do udziału sieciowego osiągalnego z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="3d2cc-113">Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli (**4011841**) i pobierz odpowiednie pliki do określonych folderów wymienione w powyższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-113">Search for any additional hotfixes listed in the table above (**4011841**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="3d2cc-114">Poprawki musi być dostępny z obu kontrolerów, aby wykryć potencjalne komunikaty o błędach z kontrolera elementu równorzędnego.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="3d2cc-115">Poprawki muszą zostać skopiowane do 3 oddzielnych folderów.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="3d2cc-116">Na przykład aktualizacja oprogramowania/Cis/MDS agenta urządzenia mogą być kopiowane w _FirstOrderUpdate_ folderu, mógł zostać skopiowany wszystkich innych Brak aktualizacji w _SecondOrderUpdate_ folderu, i aktualizacje trybu konserwacji skopiowany w _ThirdOrderUpdate_ folderu.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="3d2cc-117">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego</span><span class="sxs-lookup"><span data-stu-id="3d2cc-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="3d2cc-118">Wykonaj następujące kroki, aby zainstalować i zweryfikować poprawki przeznaczone do trybu normalnego.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="3d2cc-119">Jeśli zostały już one zainstalowane za pomocą klasycznej witryny Azure Portal, przejdź do [instalowania i weryfikowania poprawek przeznaczonych do trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="3d2cc-119">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="3d2cc-120">Aby zainstalować poprawki, przejdź do interfejsu programu Windows PowerShell na konsoli szeregowej Twojego urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="3d2cc-121">Postępuj zgodnie ze szczegółowymi instrukcjami w części [Nawiązywanie połączenia z konsolą szeregową urządzenia przy użyciu programu PuTTY](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="3d2cc-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="3d2cc-122">W wierszy polecenia naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="3d2cc-123">Wybierz **opcję 1**, aby zalogować się do urządzenia z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="3d2cc-124">Zalecamy, aby najpierw zainstalować poprawkę na kontrolerze pasywnym.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="3d2cc-125">Aby zainstalować poprawkę, w wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="3d2cc-126">W powyższym poleceniu użyj adresu IP zamiast nazwy DNS w ścieżce udziału.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="3d2cc-127">Parametr Credential jest używany tylko wtedy, gdy uzyskuje się dostęp do uwierzytelnionego udziału.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="3d2cc-128">Użycie parametru Credential jest zalecane przy uzyskiwaniu dostępu do udziałów.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="3d2cc-129">Nawet udziały otwarte dla wszystkich nie są zwykle otwarte dla użytkowników nieuwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="3d2cc-130">Po wyświetleniu monitu podaj hasło.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-130">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="3d2cc-131">Przykładowe dane wyjściowe dotyczące instalacji aktualizacji stosowanych w pierwszej kolejności są pokazane poniżej.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="3d2cc-132">Pierwszą aktualizacją kolejności należy wskazać określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-132">For the first order update, you need to point to the specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="3d2cc-133">Wpisz **Y**, gdy zostanie wyświetlony monit o potwierdzenie instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="3d2cc-134">Monitoruj aktualizację za pomocą polecenia cmdlet `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="3d2cc-135">Aktualizacja zakończy się najpierw na kontrolerze pasywnym.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="3d2cc-136">Gdy kontroler pasywny zostanie zaktualizowany, nastąpi przejście do trybu failover i aktualizacja zostanie zastosowana na drugim kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="3d2cc-137">Aktualizacja zostanie zakończona po zaktualizowaniu obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="3d2cc-138">Następujące przykładowe dane wyjściowe pokazują aktualizację w toku.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="3d2cc-139">Gdy aktualizacja będzie w toku, parametr `RunInprogress` będzie mieć wartość `True`.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="3d2cc-140">Następujące przykładowe dane wyjściowe wskazują, że aktualizacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="3d2cc-141">Gdy aktualizacja zostanie zakończona, parametr `RunInProgress` będzie mieć wartość `False`.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="3d2cc-142">Czasem polecenie cmdlet zgłasza wartość `False`, gdy aktualizacja jest ciągle w toku.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="3d2cc-143">Aby upewnić się, że instalacja poprawki została zakończona, zaczekaj kilka minut, uruchom ponownie to polecenie i sprawdź, czy parametr `RunInProgress` ma wartość `False`.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="3d2cc-144">Jeśli tak jest, instalowanie poprawki zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-144">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="3d2cc-145">Po zakończeniu aktualizowania oprogramowania sprawdź wersje oprogramowania systemu.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="3d2cc-146">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="3d2cc-147">Powinny zostać wyświetlone następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-147">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="3d2cc-148">Jeśli numer wersji nie zmieni się po zastosowaniu aktualizacji, wskazuje to, że stosowanie poprawki nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-148">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="3d2cc-149">Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="3d2cc-150">Należy ponownie uruchomić aktywnym kontrolerze za pośrednictwem `Restart-HcsController` polecenia cmdlet przed zastosowaniem na następną aktualizację.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
7. <span data-ttu-id="3d2cc-151">Powtórz kroki 3 – 5, aby zainstalować agenta konfiguracji (ci) / MDS pobrane do Twojej _FirstOrderUpdate_ folderu.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-151">Repeat steps 3-5 to install the Cis/MDS agent downloaded to your _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="3d2cc-152">Powtórz kroki od 3 do 5, aby zainstalować aktualizacje stosowane w drugiej kolejności.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-152">Repeat steps 3-5 to install the second order updates.</span></span> <span data-ttu-id="3d2cc-153">**Drugi kolejność aktualizacji, można zainstalować wiele aktualizacji, uruchamiając tylko `Start-HcsHotfix cmdlet` i wskazujący folder zawierający drugi kolejność aktualizacji. Polecenie cmdlet będzie wykonywać wszystkie dostępne aktualizacje w folderze.**</span><span class="sxs-lookup"><span data-stu-id="3d2cc-153">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span></span> <span data-ttu-id="3d2cc-154">Jeśli aktualizacja jest już zainstalowana, logika aktualizacji wykryje to i nie zastosuje tej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-154">If an update is already installed, the update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="3d2cc-155">Po zainstalowaniu wszystkich poprawek użyj polecenia cmdlet `Get-HcsSystem`.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-155">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="3d2cc-156">Wersje powinny być następujące:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-156">The versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="3d2cc-157">Aby zainstalować i zweryfikować poprawki przeznaczone do trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="3d2cc-157">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="3d2cc-158">Użyj poprawki KB4011837, aby zainstalować aktualizacje oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-158">Use KB4011837 to install disk firmware updates.</span></span> <span data-ttu-id="3d2cc-159">Te aktualizacje wymagają zatrzymania pracy i zajmują około 30 minut.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-159">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="3d2cc-160">Można zdecydować się na zainstalowanie ich w zaplanowanym oknie obsługi, łącząc się z konsolą szeregową urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-160">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="3d2cc-161">Pamiętaj, że jeśli oprogramowanie układowe dysku jest już aktualne, tych aktualizacji nie trzeba instalować.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-161">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="3d2cc-162">Uruchom polecenie cmdlet `Get-HcsUpdateAvailability` z konsoli szeregowej urządzenia, aby sprawdzić, czy aktualizacje są dostępne i czy wymagają przerwania pracy (są przeznaczone do trybu konserwacji), czy nie (są przeznaczone do trybu normalnego).</span><span class="sxs-lookup"><span data-stu-id="3d2cc-162">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="3d2cc-163">Aby zainstalować aktualizacje oprogramowania układowego dysku, postępuj zgodnie z instrukcjami poniżej.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-163">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="3d2cc-164">Przełącz urządzenie do trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-164">Place the device in the maintenance mode.</span></span> <span data-ttu-id="3d2cc-165">**Pamiętaj, że łącząc się z urządzeniem w trybie konserwacji, nie należy łączyć się zdalnie z programu Windows PowerShell. Zamiast tego należy uruchomić to polecenie cmdlet na kontrolerze urządzenia podczas połączenia za pośrednictwem konsoli szeregowej urządzenia.**</span><span class="sxs-lookup"><span data-stu-id="3d2cc-165">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span></span> <span data-ttu-id="3d2cc-166">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="3d2cc-167">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-167">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="3d2cc-168">Oba kontrolery są następnie uruchamiane ponownie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-168">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="3d2cc-169">Aby zainstalować aktualizację oprogramowania układowego dysku, wpisz:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-169">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="3d2cc-170">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="3d2cc-171">Monitoruj postęp instalacji za pomocą polecenia `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-171">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="3d2cc-172">Aktualizacja będzie zakończona, gdy parametr `RunInProgress` zmieni wartość na `False`.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-172">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="3d2cc-173">Po zakończeniu instalacji kontroler, na którym została zainstalowana poprawka przeznaczona do trybu konserwacji, zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-173">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="3d2cc-174">Zaloguj się za pomocą opcji 1 (z pełnym dostępem) i sprawdź wersję oprogramowania układowego dysku.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-174">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="3d2cc-175">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="3d2cc-176">Oczekiwane wersje oprogramowania układowego dysku to:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-176">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="3d2cc-177">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
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
   
    <span data-ttu-id="3d2cc-178">Uruchom polecenie `Get-HcsFirmwareVersion` na drugim kontrolerze, aby sprawdzić, czy wersja oprogramowania została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-178">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="3d2cc-179">Następnie możesz wyjść z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-179">You can then exit the maintenance mode.</span></span> <span data-ttu-id="3d2cc-180">W tym celu wpisz następujące polecenie dla każdego kontrolera urządzenia:</span><span class="sxs-lookup"><span data-stu-id="3d2cc-180">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="3d2cc-181">Po wyjściu z trybu konserwacji kontrolery zostaną ponownie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-181">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="3d2cc-182">Gdy aktualizacje oprogramowania układowego dysku zostaną pomyślnie zastosowane i urządzenie wyjdzie z trybu konserwacji, wróć do klasycznej witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-182">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="3d2cc-183">Pamiętaj, że fakt zainstalowania aktualizacji przeznaczonych do trybu konserwacji może nie być widoczny w portalu nawet przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="3d2cc-183">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

