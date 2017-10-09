<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="01617-101">poprawki toodownload</span><span class="sxs-lookup"><span data-stu-id="01617-101">toodownload hotfixes</span></span>

<span data-ttu-id="01617-102">Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="01617-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="01617-103">Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="01617-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="01617-104">Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="01617-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Instalowanie wykazu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="01617-106">W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello hello poprawki mają toodownload, na przykład **4037264**, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="01617-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="01617-107">Witaj poprawka zostanie wyświetlona na liście, na przykład **zbiorczą 5.0 aktualizacji pakietu oprogramowania dla z serii StorSimple 8000**.</span><span class="sxs-lookup"><span data-stu-id="01617-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="01617-109">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="01617-109">Click **Download**.</span></span> <span data-ttu-id="01617-110">Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear.</span><span class="sxs-lookup"><span data-stu-id="01617-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="01617-111">Kliknij przycisk pliki hello toodownload toohello określić lokalizację i folderu.</span><span class="sxs-lookup"><span data-stu-id="01617-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="01617-112">Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="01617-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="01617-113">Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli hello (**4037266**), i wymienione w powyższej tabeli hello odpowiadającego hello pobierania plików toohello określonych folderów.</span><span class="sxs-lookup"><span data-stu-id="01617-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="01617-114">poprawki Hello musi być dostępny z obu toodetect kontrolerów wszelkie potencjalne błędy komunikaty z hello równorzędnej kontrolera.</span><span class="sxs-lookup"><span data-stu-id="01617-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="01617-115">Witaj poprawek należy skopiować w oddzielnych folderach 3.</span><span class="sxs-lookup"><span data-stu-id="01617-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="01617-116">Na przykład aktualizacja oprogramowania/Cis/MDS agenta urządzenia hello mogą zostać skopiowane w _FirstOrderUpdate_ folderu, hello wszystkie inne aktualizacje Brak mógł zostać skopiowany w hello _SecondOrderUpdate_ folderu, i aktualizacje trybu konserwacji skopiowany w _ThirdOrderUpdate_ folderu.</span><span class="sxs-lookup"><span data-stu-id="01617-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="01617-117">tooinstall i sprawdź regularne poprawki</span><span class="sxs-lookup"><span data-stu-id="01617-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="01617-118">Wykonaj następujące kroki tooinstall hello i sprawdź regular poprawki.</span><span class="sxs-lookup"><span data-stu-id="01617-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="01617-119">Jeśli zainstalowano je przy użyciu hello portalu Azure przejdź za[zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="01617-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="01617-120">tooinstall hello poprawki interfejsu programu Windows PowerShell hello dostępu na konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="01617-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="01617-121">Wykonaj hello szczegółowe instrukcje w [konsoli szeregowej przy użyciu programu PuTTy tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="01617-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="01617-122">W wierszu polecenia hello naciśnij **Enter**.</span><span class="sxs-lookup"><span data-stu-id="01617-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="01617-123">Wybierz **opcję 1** toolog toohello urządzenia z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="01617-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="01617-124">Zalecamy zainstalowanie poprawki hello na kontrolerze pasywnym hello najpierw.</span><span class="sxs-lookup"><span data-stu-id="01617-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="01617-125">poprawka hello tooinstall hello wiersza polecenia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="01617-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="01617-126">Użyj adresu IP, a nie DNS w ścieżce udziału hello powyżej polecenia.</span><span class="sxs-lookup"><span data-stu-id="01617-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="01617-127">Parametr credential Hello jest używany tylko wtedy, gdy uzyskujesz dostęp do udziału uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="01617-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="01617-128">Zalecamy użycie udziałów tooaccess parametr credential hello.</span><span class="sxs-lookup"><span data-stu-id="01617-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="01617-129">Nawet udziałów, które są otwarte za "wszyscy" są zwykle nie otworzyć toounauthenticated użytkowników.</span><span class="sxs-lookup"><span data-stu-id="01617-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="01617-130">Podaj hasło powitania po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="01617-130">Supply hello password when prompted.</span></span> <span data-ttu-id="01617-131">Poniżej przedstawiono przykładowe dane wyjściowe instalowania hello pierwszy kolejność aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="01617-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="01617-132">Hello pierwszej kolejności aktualizacji należy toopoint toohello określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="01617-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="01617-133">Należy zainstalować hello _HcsSoftwareUpdate.exe_ pierwszy.</span><span class="sxs-lookup"><span data-stu-id="01617-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="01617-134">Po zakończeniu tej instalacji, następnie zainstalować _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="01617-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="01617-135">Typ **Y** gdy zostanie wyświetlony monit o tooconfirm hello instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="01617-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="01617-136">Monitoruj hello aktualizacji za pomocą hello `Get-HcsUpdateStatus` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01617-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="01617-137">Hello aktualizacji zakończy się najpierw na powitania pasywnym kontrolera.</span><span class="sxs-lookup"><span data-stu-id="01617-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="01617-138">Po kontrolera pasywnym hello jest aktualizowany, będą trybu failover i aktualizacji hello następnie zostaną zastosowane na hello inny kontroler.</span><span class="sxs-lookup"><span data-stu-id="01617-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="01617-139">Witaj aktualizacja została ukończona, gdy obu kontrolerów hello są aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="01617-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="01617-140">Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku.</span><span class="sxs-lookup"><span data-stu-id="01617-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="01617-141">Witaj `RunInprogress` jest `True` po aktualizacji hello jest w toku.</span><span class="sxs-lookup"><span data-stu-id="01617-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="01617-142">Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="01617-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="01617-143">Witaj `RunInProgress` jest `False` po zakończeniu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="01617-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="01617-144">Czasami hello raporty polecenia cmdlet `False` podczas aktualizacji hello jest nadal w toku.</span><span class="sxs-lookup"><span data-stu-id="01617-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="01617-145">tooensure, który hello poprawka została ukończona, poczekaj kilka minut, ponownie uruchomić to polecenie i sprawdź, że hello `RunInProgress` jest `False`.</span><span class="sxs-lookup"><span data-stu-id="01617-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="01617-146">Jeśli tak jest, poprawki hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="01617-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="01617-147">Po zakończeniu aktualizacji oprogramowania hello Sprawdź wersje oprogramowania hello systemu.</span><span class="sxs-lookup"><span data-stu-id="01617-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="01617-148">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="01617-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="01617-149">Powinny pojawić się hello następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="01617-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="01617-150">Jeśli numer wersji hello nie zmienia się po zastosowaniu aktualizacji hello, oznacza to, że ta poprawka hello nie powiodło się tooapply.</span><span class="sxs-lookup"><span data-stu-id="01617-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="01617-151">Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.</span><span class="sxs-lookup"><span data-stu-id="01617-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="01617-152">Należy ponownie uruchomić hello na aktywnym kontrolerze za pośrednictwem hello `Restart-HcsController` polecenia cmdlet przed zastosowaniem hello następną aktualizację.</span><span class="sxs-lookup"><span data-stu-id="01617-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="01617-153">Powtórz kroki od 3 do 6 tooinstall hello _CisMDSAgentupdate.exe_ agent pobierany tooyour _FirstOrderUpdate_ folderu.</span><span class="sxs-lookup"><span data-stu-id="01617-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="01617-154">Powtórz kroki od 3 do 6 tooinstall hello drugi kolejność aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="01617-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="01617-155">Drugi kolejność aktualizacji, można zainstalować wiele aktualizacji tylko uruchamiając hello `Start-HcsHotfix cmdlet` i wskazujący toohello folder zawierający drugi aktualizacje kolejności.</span><span class="sxs-lookup"><span data-stu-id="01617-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="01617-156">polecenia cmdlet Hello wykona wszystkie dostępne aktualizacje hello w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="01617-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="01617-157">Jeśli aktualizacja jest już zainstalowana, logika aktualizacji hello wykryje, że i nie zastosować tę aktualizację.</span><span class="sxs-lookup"><span data-stu-id="01617-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="01617-158">Po zainstalowaniu wszystkich hello poprawek, użyj hello `Get-HcsSystem` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01617-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="01617-159">wersje Hello powinny być:</span><span class="sxs-lookup"><span data-stu-id="01617-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="01617-160">tooinstall i sprawdź poprawki trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="01617-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="01617-161">Użyj aktualizacji oprogramowania układowego dysku tooinstall KB4037263.</span><span class="sxs-lookup"><span data-stu-id="01617-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="01617-162">Te aktualizacje zakłócenie i podejmij toocomplete około 30 minut.</span><span class="sxs-lookup"><span data-stu-id="01617-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="01617-163">Można wybrać tooinstall je w oknie obsługi planowanych przez łączącego konsoli szeregowej urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="01617-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="01617-164">Jeśli oprogramowanie układowe dysku jest już aktualne, nie ma potrzeby tooinstall te aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="01617-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="01617-165">Uruchom hello `Get-HcsUpdateAvailability` polecenia cmdlet z hello toocheck konsoli szeregowej urządzenia, jeśli aktualizacje są dostępne i czy hello aktualizacji są destrukcyjne (trybu konserwacji) lub Brak (tryb regularne) aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="01617-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="01617-166">aktualizacje oprogramowania układowego tooinstall hello dysku, wykonaj poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="01617-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="01617-167">Ustaw hello urządzenia w trybie konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="01617-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="01617-168">Nie należy używać komunikacji zdalnej programu Windows PowerShell, łącząc tooa urządzenia w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="01617-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="01617-169">Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia hello podczas połączenia za pośrednictwem konsoli szeregowej urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="01617-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="01617-170">Kontroler hello tooplace w trybie konserwacji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="01617-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="01617-171">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="01617-171">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="01617-172">Zarówno kontrolery hello następnie uruchom ponownie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="01617-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="01617-173">tooinstall hello dysku aktualizacji oprogramowania układowego, wpisz:</span><span class="sxs-lookup"><span data-stu-id="01617-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="01617-174">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="01617-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="01617-175">Monitor hello Instaluj postępu przy użyciu `Get-HcsUpdateStatus` polecenia.</span><span class="sxs-lookup"><span data-stu-id="01617-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="01617-176">Witaj aktualizacja została ukończona, gdy hello `RunInProgress` zmiany zbyt`False`.</span><span class="sxs-lookup"><span data-stu-id="01617-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="01617-177">Po zakończeniu instalacji hello hello kontrolera, na które hello zainstalowano poprawkę trybu konserwacji zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="01617-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="01617-178">Zaloguj się jako opcja 1 z pełnym dostępem i sprawdź, wersja oprogramowania układowego hello dysku.</span><span class="sxs-lookup"><span data-stu-id="01617-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="01617-179">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="01617-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="01617-180">Witaj oczekiwanych wersji oprogramowania układowego dysku:</span><span class="sxs-lookup"><span data-stu-id="01617-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="01617-181">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="01617-181">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="01617-182">Uruchom hello `Get-HcsFirmwareVersion` polecenie hello drugi kontroler tooverify który hello wersji oprogramowania została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="01617-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="01617-183">Następnie można zakończyć tryb konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="01617-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="01617-184">toodo tak, wpisz następujące polecenie dla każdego kontrolera urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="01617-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="01617-185">kontrolery Hello ponownie po wyjściu z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="01617-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="01617-186">Po oprogramowania układowego dysku hello skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie hello opuścił tryb konserwacji, zwracany toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="01617-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="01617-187">Należy pamiętać, że tego portalu hello nie mogą być wyświetlane, czy zainstalowane aktualizacje w trybie konserwacji hello przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="01617-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

