<!--author=alkohli last changed: 05/19/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="9309c-101">poprawki toodownload</span><span class="sxs-lookup"><span data-stu-id="9309c-101">toodownload hotfixes</span></span>
<span data-ttu-id="9309c-102">Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="9309c-103">Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9309c-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="9309c-104">Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="9309c-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="9309c-105">![Zainstaluj katalogu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="9309c-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="9309c-106">W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello hello poprawki mają toodownload, na przykład **3179904**, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="9309c-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="9309c-107">Witaj poprawka zostanie wyświetlona na liście, na przykład **zbiorczą 2.2 aktualizacji pakietu oprogramowania dla z serii StorSimple 8000**.</span><span class="sxs-lookup"><span data-stu-id="9309c-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="9309c-109">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9309c-109">Click **Add**.</span></span> <span data-ttu-id="9309c-110">Witaj aktualizacja została dodana toohello koszyka.</span><span class="sxs-lookup"><span data-stu-id="9309c-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="9309c-111">Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli hello (**3103616**, **3146621**) i Dodaj każdy koszyka toohello.</span><span class="sxs-lookup"><span data-stu-id="9309c-111">Search for any additional hotfixes listed in hello table above (**3103616**, **3146621**), and add each toohello basket.</span></span>
6. <span data-ttu-id="9309c-112">Kliknij pozycję **Wyświetl koszyk**.</span><span class="sxs-lookup"><span data-stu-id="9309c-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="9309c-113">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="9309c-113">Click **Download**.</span></span> <span data-ttu-id="9309c-114">Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear.</span><span class="sxs-lookup"><span data-stu-id="9309c-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="9309c-115">Witaj aktualizacje zostaną pobrane toohello określonej lokalizacji i umieścić w podfolderze o hello takie same nazwy co hello update.</span><span class="sxs-lookup"><span data-stu-id="9309c-115">hello updates are downloaded toohello specified location and placed in a sub-folder with hello same name as hello update.</span></span> <span data-ttu-id="9309c-116">Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="9309c-117">poprawki Hello musi być dostępny z obu toodetect kontrolerów wszelkie potencjalne błędy komunikaty z hello równorzędnej kontrolera.</span><span class="sxs-lookup"><span data-stu-id="9309c-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="9309c-118">tooinstall i sprawdź regularne poprawki</span><span class="sxs-lookup"><span data-stu-id="9309c-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="9309c-119">Wykonaj następujące kroki tooinstall hello i sprawdź regular poprawki.</span><span class="sxs-lookup"><span data-stu-id="9309c-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="9309c-120">Jeśli zainstalowano je przy użyciu hello portalu Azure przejdź za[zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="9309c-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="9309c-121">tooinstall hello poprawki interfejsu programu Windows PowerShell hello dostępu na konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9309c-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="9309c-122">Wykonaj hello szczegółowe instrukcje w [konsoli szeregowej przy użyciu programu PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="9309c-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="9309c-123">W wierszu polecenia hello naciśnij **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9309c-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="9309c-124">Wybierz **opcję 1** toolog toohello urządzenia z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="9309c-124">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="9309c-125">Zalecamy zainstalowanie poprawki hello na kontrolerze pasywnym hello najpierw.</span><span class="sxs-lookup"><span data-stu-id="9309c-125">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="9309c-126">poprawka hello tooinstall hello wiersza polecenia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="9309c-126">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="9309c-127">Użyj adresu IP, a nie DNS w ścieżce udziału hello powyżej polecenia.</span><span class="sxs-lookup"><span data-stu-id="9309c-127">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="9309c-128">Parametr credential Hello jest używany tylko wtedy, gdy uzyskujesz dostęp do udziału uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="9309c-128">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="9309c-129">Zalecamy użycie udziałów tooaccess parametr credential hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-129">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="9309c-130">Nawet udziałów, które są otwarte za "wszyscy" są zwykle nie otworzyć toounauthenticated użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9309c-130">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="9309c-131">Podaj hasło powitania po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="9309c-131">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="9309c-132">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9309c-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="9309c-133">Typ **Y** gdy zostanie wyświetlony monit o tooconfirm hello instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="9309c-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9309c-134">Jeśli instalowanie aktualizacji 2.2, instalować tylko plik binarny hello poprzedzone znakiem "wszystkie hcsmdssoftwareudpate".</span><span class="sxs-lookup"><span data-stu-id="9309c-134">If installing Update 2.2, only install hello binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="9309c-135">Nie należy instalować hello konfiguracji (ci) i hello MDS agent aktualizacji poprzedzone znakiem all cismdsagentupdatebundle.</span><span class="sxs-lookup"><span data-stu-id="9309c-135">Do not install hello Cis and hello MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="9309c-136">Błąd toodo tak spowoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="9309c-136">Failure toodo so will result in an error.</span></span> 

5. <span data-ttu-id="9309c-137">Monitoruj hello aktualizacji za pomocą hello `Get-HcsUpdateStatus` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9309c-137">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="9309c-138">Hello aktualizacji zakończy się najpierw na powitania pasywnym kontrolera.</span><span class="sxs-lookup"><span data-stu-id="9309c-138">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="9309c-139">Po kontrolera pasywnym hello jest aktualizowany, będą trybu failover i aktualizacji hello następnie zostaną zastosowane na hello inny kontroler.</span><span class="sxs-lookup"><span data-stu-id="9309c-139">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="9309c-140">Witaj aktualizacja została ukończona, gdy obu kontrolerów hello są aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="9309c-140">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="9309c-141">Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku.</span><span class="sxs-lookup"><span data-stu-id="9309c-141">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="9309c-142">Witaj `RunInprogress` będzie `True` podczas aktualizacji hello jest w toku.</span><span class="sxs-lookup"><span data-stu-id="9309c-142">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="9309c-143">Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="9309c-143">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="9309c-144">Witaj `RunInProgress` będzie `False` po zakończeniu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-144">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="9309c-145">Czasami hello raporty polecenia cmdlet `False` podczas aktualizacji hello jest nadal w toku.</span><span class="sxs-lookup"><span data-stu-id="9309c-145">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="9309c-146">tooensure, który hello poprawka została ukończona, poczekaj kilka minut, ponownie uruchomić to polecenie i sprawdź, że hello `RunInProgress` jest `False`.</span><span class="sxs-lookup"><span data-stu-id="9309c-146">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="9309c-147">Jeśli tak jest, poprawki hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="9309c-147">If it is, then hello hotfix has completed.</span></span>

1. <span data-ttu-id="9309c-148">Po zakończeniu aktualizacji oprogramowania hello Sprawdź wersje oprogramowania hello systemu.</span><span class="sxs-lookup"><span data-stu-id="9309c-148">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="9309c-149">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="9309c-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="9309c-150">Powinny pojawić się hello następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="9309c-150">You should see hello following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="9309c-151">Jeśli po zastosowaniu aktualizacji hello nie należy zmieniać numerów wersji hello, oznacza to, że ta poprawka hello nie powiodło się tooapply.</span><span class="sxs-lookup"><span data-stu-id="9309c-151">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="9309c-152">Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.</span><span class="sxs-lookup"><span data-stu-id="9309c-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="9309c-153">Należy ponownie uruchomić hello na aktywnym kontrolerze za pośrednictwem hello `Restart-HcsController` polecenia cmdlet przed zastosowaniem hello pozostałych aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9309c-153">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="9309c-154">Powtórz kroki 3 – 5 tooinstall hello pozostałych regular poprawki.</span><span class="sxs-lookup"><span data-stu-id="9309c-154">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="9309c-155">Aktualizacja iSCSI Hello KB3146621</span><span class="sxs-lookup"><span data-stu-id="9309c-155">hello iSCSI update KB3146621</span></span>
   * <span data-ttu-id="9309c-156">Aktualizacja WMI Hello KB3103616</span><span class="sxs-lookup"><span data-stu-id="9309c-156">hello WMI update KB3103616</span></span>
3. <span data-ttu-id="9309c-157">Pomiń ten krok, jeśli są aktualizowane z Update 2.</span><span class="sxs-lookup"><span data-stu-id="9309c-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="9309c-158">Aktualizowania z poprzednich tooUpdate w wersji 2, konieczne będzie również toodownload:</span><span class="sxs-lookup"><span data-stu-id="9309c-158">If you are updating from a version prior tooUpdate 2, you will also need toodownload:</span></span>

    - <span data-ttu-id="9309c-159">Sterownik Hello LSI KB3121900</span><span class="sxs-lookup"><span data-stu-id="9309c-159">hello LSI driver KB3121900</span></span>

    - <span data-ttu-id="9309c-160">Aktualizacja Spaceport Hello KB3090322</span><span class="sxs-lookup"><span data-stu-id="9309c-160">hello Spaceport update KB3090322</span></span>

    - <span data-ttu-id="9309c-161">Aktualizacja Storport Hello KB3080728</span><span class="sxs-lookup"><span data-stu-id="9309c-161">hello Storport update KB3080728</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="9309c-162">tooinstall i sprawdź poprawki trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="9309c-162">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="9309c-163">Użyj aktualizacji oprogramowania układowego dysku tooinstall KB3121899.</span><span class="sxs-lookup"><span data-stu-id="9309c-163">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="9309c-164">Te aktualizacje zakłócenie i podejmij toocomplete około 30 minut.</span><span class="sxs-lookup"><span data-stu-id="9309c-164">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="9309c-165">Można wybrać tooinstall je w oknie obsługi planowanych przez łączącego konsoli szeregowej urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="9309c-165">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="9309c-166">Uwaga: Jeśli oprogramowanie układowe dysku jest już aktualne, nie należy tooinstall te aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="9309c-166">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="9309c-167">Uruchom hello `Get-HcsUpdateAvailability` polecenia cmdlet z hello toocheck konsoli szeregowej urządzenia, jeśli aktualizacje są dostępne i czy hello aktualizacji są destrukcyjne (trybu konserwacji) lub Brak (tryb regularne) aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="9309c-167">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="9309c-168">aktualizacje oprogramowania układowego tooinstall hello dysku, wykonaj poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-168">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="9309c-169">Ustaw hello urządzenia w trybie konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-169">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="9309c-170">Należy pamiętać, że nie należy używać komunikacji zdalnej programu Windows PowerShell podczas łączenia tooa urządzenia w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9309c-170">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="9309c-171">Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia hello podczas połączenia za pośrednictwem konsoli szeregowej urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-171">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="9309c-172">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="9309c-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="9309c-173">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9309c-173">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="9309c-174">Zarówno kontrolery hello następnie uruchom ponownie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9309c-174">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="9309c-175">tooinstall hello dysku aktualizacji oprogramowania układowego, wpisz:</span><span class="sxs-lookup"><span data-stu-id="9309c-175">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="9309c-176">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9309c-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="9309c-177">Monitor hello Instaluj postępu przy użyciu `Get-HcsUpdateStatus` polecenia.</span><span class="sxs-lookup"><span data-stu-id="9309c-177">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="9309c-178">Witaj aktualizacja została ukończona, gdy hello `RunInProgress` zmiany zbyt`False`.</span><span class="sxs-lookup"><span data-stu-id="9309c-178">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="9309c-179">Po zakończeniu instalacji hello hello kontrolera, na które hello zainstalowano poprawkę trybu konserwacji zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="9309c-179">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="9309c-180">Zaloguj się jako opcja 1 z pełnym dostępem i sprawdź, wersja oprogramowania układowego hello dysku.</span><span class="sxs-lookup"><span data-stu-id="9309c-180">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="9309c-181">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="9309c-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="9309c-182">Witaj oczekiwanych wersji oprogramowania układowego dysku:</span><span class="sxs-lookup"><span data-stu-id="9309c-182">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="9309c-183">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9309c-183">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="9309c-184">Uruchom hello `Get-HcsFirmwareVersion` polecenie hello drugi kontroler tooverify który hello wersji oprogramowania została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="9309c-184">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="9309c-185">Następnie można zakończyć tryb konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="9309c-185">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="9309c-186">toodo tak, wpisz następujące polecenie dla każdego kontrolera urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="9309c-186">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="9309c-187">kontrolery Hello ponownie po wyjściu z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9309c-187">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="9309c-188">Po oprogramowania układowego dysku hello skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie hello opuścił tryb konserwacji, zwracany toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9309c-188">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="9309c-189">Należy pamiętać, że tego portalu hello nie mogą być wyświetlane, czy zainstalowane aktualizacje w trybie konserwacji hello przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="9309c-189">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

