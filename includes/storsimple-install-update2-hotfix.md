<!--author=alkohli last changed: 03/17/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="12434-101">poprawki toodownload</span><span class="sxs-lookup"><span data-stu-id="12434-101">toodownload hotfixes</span></span>
<span data-ttu-id="12434-102">Wykonywanie poniższych czynności toodownload hello aktualizacja z hello wykazu aktualizacji usługi Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="12434-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="12434-103">Uruchom program Internet Explorer i przejdź zbyt[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="12434-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="12434-104">Jeśli jest to pierwsza przy użyciu hello wykazu usługi Microsoft Update na tym komputerze, kliknij przycisk **zainstalować** gdy zostanie wyświetlony monit o tooinstall hello dodatek wykazu usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="12434-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="12434-105">![Zainstaluj katalogu](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="12434-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="12434-106">W polu wyszukiwania hello hello wykazu usługi Microsoft Update, wprowadź numer bazy wiedzy Knowledge Base (KB) hello hello poprawki mają toodownload, na przykład **3121901**, a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="12434-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="12434-107">Witaj poprawka zostanie wyświetlona na liście, na przykład **zbiorczą oprogramowania pakietu aktualizacji w wersji 2.0 dla z serii StorSimple 8000**.</span><span class="sxs-lookup"><span data-stu-id="12434-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Przeszukiwanie wykazu](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="12434-109">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="12434-109">Click **Add**.</span></span> <span data-ttu-id="12434-110">Witaj aktualizacja została dodana toohello koszyka.</span><span class="sxs-lookup"><span data-stu-id="12434-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="12434-111">Wyszukaj wszystkie dodatkowe poprawki wymienione w powyższej tabeli hello (**3121900**, **3080728**, **3090322**, i **3121899**) i Dodaj każdy Witaj koszyka.</span><span class="sxs-lookup"><span data-stu-id="12434-111">Search for any additional hotfixes listed in hello table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each hello basket.</span></span>
6. <span data-ttu-id="12434-112">Kliknij pozycję **Wyświetl koszyk**.</span><span class="sxs-lookup"><span data-stu-id="12434-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="12434-113">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="12434-113">Click **Download**.</span></span> <span data-ttu-id="12434-114">Określ lub **Przeglądaj** tooa lokalnego lokalizację hello pobiera tooappear.</span><span class="sxs-lookup"><span data-stu-id="12434-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="12434-115">Witaj aktualizacje zostaną pobrane toohello określonej lokalizacji i umieszczane w podfolderze o hello takie same nazwy co hello update.</span><span class="sxs-lookup"><span data-stu-id="12434-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="12434-116">Hello folder można także skopiowany tooa udział sieciowy, który jest dostępny z urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="12434-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="12434-117">poprawki Hello musi być dostępny z obu toodetect kontrolerów wszelkie potencjalne błędy komunikaty z hello równorzędnej kontrolera.</span><span class="sxs-lookup"><span data-stu-id="12434-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="12434-118">tooinstall i sprawdź regularne poprawki</span><span class="sxs-lookup"><span data-stu-id="12434-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="12434-119">Wykonaj następujące kroki tooinstall hello i sprawdź regular poprawki.</span><span class="sxs-lookup"><span data-stu-id="12434-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="12434-120">Jeśli zainstalowano je przy użyciu hello portalu Azure przejdź za[zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="12434-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="12434-121">tooinstall hello poprawki interfejsu programu Windows PowerShell hello dostępu na konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="12434-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="12434-122">Wykonaj hello szczegółowe instrukcje w [konsoli szeregowej przy użyciu programu PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="12434-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="12434-123">W wierszu polecenia hello naciśnij **Enter**.</span><span class="sxs-lookup"><span data-stu-id="12434-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="12434-124">Wybierz **opcję 1** toolog toohello urządzenia z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="12434-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="12434-125">poprawka hello tooinstall hello wiersza polecenia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="12434-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="12434-126">Użyj adresu IP, a nie DNS w ścieżce udziału hello powyżej polecenia.</span><span class="sxs-lookup"><span data-stu-id="12434-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="12434-127">Parametr credential Hello jest używany tylko wtedy, gdy uzyskujesz dostęp do udziału uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="12434-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="12434-128">Zalecamy użycie udziałów tooaccess parametr credential hello.</span><span class="sxs-lookup"><span data-stu-id="12434-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="12434-129">Nawet udziałów, które są otwarte za "wszyscy" są zwykle nie otworzyć toounauthenticated użytkowników.</span><span class="sxs-lookup"><span data-stu-id="12434-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="12434-130">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="12434-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="12434-131">Typ **Y** gdy zostanie wyświetlony monit o tooconfirm hello instalacji poprawki.</span><span class="sxs-lookup"><span data-stu-id="12434-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="12434-132">Monitoruj hello aktualizacji za pomocą hello `Get-HcsUpdateStatus` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="12434-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="12434-133">Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku.</span><span class="sxs-lookup"><span data-stu-id="12434-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="12434-134">Witaj `RunInprogress` będzie `True` podczas aktualizacji hello jest w toku.</span><span class="sxs-lookup"><span data-stu-id="12434-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="12434-135">Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="12434-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="12434-136">Witaj `RunInProgress` będzie `False` po zakończeniu aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="12434-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="12434-137">Czasami hello raporty polecenia cmdlet `False` podczas aktualizacji hello jest nadal w toku.</span><span class="sxs-lookup"><span data-stu-id="12434-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="12434-138">tooensure, który hello poprawka została ukończona, poczekaj kilka minut, ponownie uruchomić to polecenie i sprawdź, że hello `RunInProgress` jest `False`.</span><span class="sxs-lookup"><span data-stu-id="12434-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="12434-139">Jeśli tak jest, poprawki hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="12434-139">If it is, then hello hotfix has completed.</span></span>

6. <span data-ttu-id="12434-140">Po oprogramowania hello aktualizacji jest pełna, powtórz kroki 3 – 5 tooinstall i monitor hello SaaS agenta i MDS agenta.</span><span class="sxs-lookup"><span data-stu-id="12434-140">After hello software update is complete, repeat steps 3-5 tooinstall and monitor hello SaaS agent and MDS agent .</span></span> <span data-ttu-id="12434-141">Upewnij się, że `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` została zainstalowana przed `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="12434-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="12434-142">Sprawdź wersje oprogramowania hello systemu.</span><span class="sxs-lookup"><span data-stu-id="12434-142">Verify hello system software versions.</span></span> <span data-ttu-id="12434-143">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="12434-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="12434-144">Powinny pojawić się hello następujące wersje:</span><span class="sxs-lookup"><span data-stu-id="12434-144">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="12434-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="12434-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="12434-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="12434-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="12434-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="12434-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="12434-148">Jeśli po zastosowaniu aktualizacji hello nie należy zmieniać numerów wersji hello, oznacza to, że ta poprawka hello nie powiodło się tooapply.</span><span class="sxs-lookup"><span data-stu-id="12434-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="12434-149">Jeśli widzisz coś takiego, skontaktuj się z [pomocą techniczną firmy Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) w celu uzyskania dalszej pomocy.</span><span class="sxs-lookup"><span data-stu-id="12434-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="12434-150">Powtórz kroki 3 – 5 tooinstall hello pozostałych regular poprawki.</span><span class="sxs-lookup"><span data-stu-id="12434-150">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="12434-151">Witaj sterownik LSI - KB3121900</span><span class="sxs-lookup"><span data-stu-id="12434-151">hello LSI driver - KB3121900</span></span>
   * <span data-ttu-id="12434-152">Witaj Storport update - KB3080728</span><span class="sxs-lookup"><span data-stu-id="12434-152">hello Storport update - KB3080728</span></span>
   * <span data-ttu-id="12434-153">Witaj Spaceport update - KB3090322</span><span class="sxs-lookup"><span data-stu-id="12434-153">hello Spaceport update - KB3090322</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="12434-154">tooinstall i sprawdź poprawki trybu konserwacji</span><span class="sxs-lookup"><span data-stu-id="12434-154">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="12434-155">Użyj aktualizacji oprogramowania układowego dysku tooinstall KB3121899.</span><span class="sxs-lookup"><span data-stu-id="12434-155">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="12434-156">Te aktualizacje zakłócenie i podejmij toocomplete około 30 minut.</span><span class="sxs-lookup"><span data-stu-id="12434-156">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="12434-157">Można wybrać tooinstall je w oknie obsługi planowanych przez łączącego konsoli szeregowej urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="12434-157">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="12434-158">Uwaga: Jeśli oprogramowanie układowe dysku jest już aktualne, nie należy tooinstall te aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="12434-158">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="12434-159">Uruchom hello `Get-HcsUpdateAvailability` polecenia cmdlet z hello toocheck konsoli szeregowej urządzenia, jeśli aktualizacje są dostępne i czy hello aktualizacji są destrukcyjne (trybu konserwacji) lub Brak (tryb regularne) aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="12434-159">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="12434-160">aktualizacje oprogramowania układowego tooinstall hello dysku, wykonaj poniższe instrukcje hello.</span><span class="sxs-lookup"><span data-stu-id="12434-160">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="12434-161">Ustaw hello urządzenia w trybie konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="12434-161">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="12434-162">Należy pamiętać, że nie należy używać komunikacji zdalnej programu Windows PowerShell podczas łączenia tooa urządzenia w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="12434-162">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="12434-163">Zamiast tego Uruchom to polecenie cmdlet na kontrolerze urządzenia hello podczas połączenia za pośrednictwem konsoli szeregowej urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="12434-163">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="12434-164">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="12434-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="12434-165">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="12434-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="12434-166">Zarówno kontrolery hello następnie uruchom ponownie w trybie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="12434-166">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="12434-167">tooinstall hello dysku aktualizacji oprogramowania układowego, wpisz:</span><span class="sxs-lookup"><span data-stu-id="12434-167">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="12434-168">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="12434-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="12434-169">Monitor hello Instaluj postępu przy użyciu `Get-HcsUpdateStatus` polecenia.</span><span class="sxs-lookup"><span data-stu-id="12434-169">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="12434-170">Witaj aktualizacja została ukończona, gdy hello `RunInProgress` zmiany zbyt`False`.</span><span class="sxs-lookup"><span data-stu-id="12434-170">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="12434-171">Po zakończeniu instalacji hello hello kontrolera, na które hello zainstalowano poprawkę trybu konserwacji zostanie uruchomiony ponownie.</span><span class="sxs-lookup"><span data-stu-id="12434-171">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="12434-172">Zaloguj się jako opcja 1 z pełnym dostępem i sprawdź, wersja oprogramowania układowego hello dysku.</span><span class="sxs-lookup"><span data-stu-id="12434-172">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="12434-173">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="12434-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="12434-174">Witaj oczekiwanych wersji oprogramowania układowego dysku:</span><span class="sxs-lookup"><span data-stu-id="12434-174">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="12434-175">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="12434-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
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
   
    <span data-ttu-id="12434-176">Uruchom hello `Get-HcsFirmwareVersion` polecenie hello drugi kontroler tooverify który hello wersji oprogramowania została zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="12434-176">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="12434-177">Następnie można zakończyć tryb konserwacji hello.</span><span class="sxs-lookup"><span data-stu-id="12434-177">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="12434-178">toodo tak, wpisz następujące polecenie dla każdego kontrolera urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="12434-178">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="12434-179">kontrolery Hello ponownie po wyjściu z trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="12434-179">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="12434-180">Po oprogramowania układowego dysku hello skutecznym zastosowaniu wszystkich aktualizacji, a urządzenie hello opuścił tryb konserwacji, zwracany toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="12434-180">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="12434-181">Należy pamiętać, że tego portalu hello nie mogą być wyświetlane, czy zainstalowane aktualizacje w trybie konserwacji hello przez 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="12434-181">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

