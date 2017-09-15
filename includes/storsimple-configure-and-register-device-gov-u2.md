<!--author=SharS last changed: 02/22/2016-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="4846d-101">Konfigurowanie i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="4846d-101">To configure and register the device</span></span>
1. <span data-ttu-id="4846d-102">Przejdź do interfejsu programu Windows PowerShell na konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4846d-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="4846d-103">Instrukcje można znaleźć w temacie [Nawiązywanie połączenia z konsolą szeregową urządzenia przy użyciu programu PuTTY](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="4846d-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="4846d-104">**Pamiętaj, aby dokładnie wykonać procedurę, w przeciwnym wypadku nie uzyskasz dostępu do konsoli.**</span><span class="sxs-lookup"><span data-stu-id="4846d-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="4846d-105">W otwartej sesji naciśnij jednokrotnie klawisz Enter, aby wyświetlić wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="4846d-105">In the session that opens up, press Enter one time to get a command prompt.</span></span>
3. <span data-ttu-id="4846d-106">Zostanie wyświetlony monit o wybranie języka dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4846d-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="4846d-107">Wybierz język, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="4846d-107">Specify the language, and then press Enter.</span></span>
   
    ![Konfigurowanie i rejestrowanie urządzenia StorSimple 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="4846d-109">W przedstawionym menu konsoli szeregowej wybierz opcję 1, aby zalogować się z pełnymi uprawnieniami dostępu.</span><span class="sxs-lookup"><span data-stu-id="4846d-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span>
   
    ![Rejestrowanie urządzenia StorSimple 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="4846d-111">Wykonaj poniższe kroki, aby skonfigurować minimalne wymagane ustawienia sieciowe urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4846d-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4846d-112">Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4846d-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="4846d-113">Menu konsoli szeregowej wskazuje stan kontrolera w komunikacie transparentu.</span><span class="sxs-lookup"><span data-stu-id="4846d-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="4846d-114">Jeśli nie są łączy się z aktywnym kontrolerem, odłącz, a następnie połącz się z aktywnym kontrolerem.</span><span class="sxs-lookup"><span data-stu-id="4846d-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="4846d-115">W wierszu polecenia wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="4846d-115">At the command prompt, type your password.</span></span> <span data-ttu-id="4846d-116">Domyślne hasło urządzenia to **Password1**.</span><span class="sxs-lookup"><span data-stu-id="4846d-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="4846d-117">Wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4846d-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="4846d-118">Zostanie uruchomiony Kreator instalacji, który ułatwi konfigurowanie ustawień sieciowych urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4846d-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="4846d-119">Podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="4846d-119">Supply the following information:</span></span>
      
      * <span data-ttu-id="4846d-120">Adres IP interfejsu sieciowego 0 danych</span><span class="sxs-lookup"><span data-stu-id="4846d-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="4846d-121">Maska podsieci</span><span class="sxs-lookup"><span data-stu-id="4846d-121">Subnet mask</span></span>
      * <span data-ttu-id="4846d-122">Brama</span><span class="sxs-lookup"><span data-stu-id="4846d-122">Gateway</span></span>
      * <span data-ttu-id="4846d-123">Adres IP podstawowego serwera DNS</span><span class="sxs-lookup"><span data-stu-id="4846d-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="4846d-124">Adres IP podstawowego serwera NTP</span><span class="sxs-lookup"><span data-stu-id="4846d-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="4846d-125">Może być konieczne Poczekaj kilka minut, aż maski podsieci i zastosowanie ustawień DNS.</span><span class="sxs-lookup"><span data-stu-id="4846d-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="4846d-126">Opcjonalnie Skonfiguruj serwer proxy sieci web.</span><span class="sxs-lookup"><span data-stu-id="4846d-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="4846d-127">Mimo że konfiguracja serwera proxy sieci web jest opcjonalne, należy pamiętać, że jeśli używasz serwera proxy sieci web, można skonfigurować tylko go tutaj.</span><span class="sxs-lookup"><span data-stu-id="4846d-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="4846d-128">Aby uzyskać więcej informacji, zobacz temat [Konfigurowanie serwera proxy sieci Web dla urządzenia](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="4846d-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="4846d-129">Naciśnij klawisze Ctrl + C, aby zakończyć działanie Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="4846d-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="4846d-130">Zainstaluj aktualizacje w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4846d-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="4846d-131">Aby ustawić adresy IP na obu kontrolerów, użyj następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4846d-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="4846d-132">W wierszu polecenia Uruchom `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="4846d-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="4846d-133">Możesz powiadamiania o dostępnych aktualizacjach.</span><span class="sxs-lookup"><span data-stu-id="4846d-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="4846d-134">Uruchom polecenie `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="4846d-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="4846d-135">To polecenie można uruchomić na dowolnym węźle.</span><span class="sxs-lookup"><span data-stu-id="4846d-135">You can run this command on any node.</span></span> <span data-ttu-id="4846d-136">Aktualizacje zostaną zastosowane do pierwszego kontrolera, kontrolera zostaną przełączone awaryjnie i następnie aktualizacje zostaną zastosowane na innym kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="4846d-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="4846d-137">Możesz monitorować postęp aktualizacji, uruchamiając `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="4846d-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="4846d-138">Następujące przykładowe dane wyjściowe pokazują aktualizację w toku.</span><span class="sxs-lookup"><span data-stu-id="4846d-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="4846d-139">Następujące przykładowe dane wyjściowe wskazują, że aktualizacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="4846d-139">The following sample output indicates that the update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="4846d-140">Może upłynąć do 11 godzin zastosowanie wszystkich aktualizacji, w tym aktualizacje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4846d-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>
8. <span data-ttu-id="4846d-141">Uruchom następujące polecenie cmdlet, aby wskazywały na urządzeniu do portalu Microsoft Azure dla instytucji rządowych (ponieważ wskazuje publicznego klasycznego portalu Azure domyślnie).</span><span class="sxs-lookup"><span data-stu-id="4846d-141">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="4846d-142">Spowoduje to ponowne uruchomienie obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="4846d-142">This will restart both controllers.</span></span> <span data-ttu-id="4846d-143">Zalecane jest użycie dwóch sesji programu PuTTY można jednocześnie połączyć do obu kontrolerów, tak aby były widoczne po uruchomieniu każdego kontrolera.</span><span class="sxs-lookup"><span data-stu-id="4846d-143">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="4846d-144">Zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="4846d-144">You will see a confirmation message.</span></span> <span data-ttu-id="4846d-145">Zaakceptuj wartość domyślną (**Y**).</span><span class="sxs-lookup"><span data-stu-id="4846d-145">Accept the default (**Y**).</span></span>
9. <span data-ttu-id="4846d-146">Uruchom następujące polecenie cmdlet, aby wznowić instalację:</span><span class="sxs-lookup"><span data-stu-id="4846d-146">Run the following cmdlet to resume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Kreator instalacji Wznów](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="4846d-148">Po wznowieniu Instalatora, Kreator będzie wersji Update 2.</span><span class="sxs-lookup"><span data-stu-id="4846d-148">When you resume setup, the wizard will be the Update 2 version.</span></span>
10. <span data-ttu-id="4846d-149">Zaakceptuj ustawienia sieciowe.</span><span class="sxs-lookup"><span data-stu-id="4846d-149">Accept the network settings.</span></span> <span data-ttu-id="4846d-150">Po zaakceptowaniu każdego ustawienia, zobaczą komunikat dotyczący sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="4846d-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="4846d-151">Ze względów bezpieczeństwa hasło administratora urządzenia wygasa po pierwszej sesji i należy je teraz zmienić.</span><span class="sxs-lookup"><span data-stu-id="4846d-151">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="4846d-152">Po wyświetleniu monitu podaj hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4846d-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="4846d-153">Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="4846d-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="4846d-154">Hasło musi zawierać trzy z wymienionych elementów: małe litery, wielkie litery, cyfry i znaki specjalne.</span><span class="sxs-lookup"><span data-stu-id="4846d-154">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Rejestrowanie urządzenia StorSimple 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="4846d-156">W ostatnim kroku Kreatora instalacji wykonywana jest rejestracja urządzenia w usłudze StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="4846d-156">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="4846d-157">W tym celu należy klucz rejestracji usługi uzyskany w [krok 2: pobieranie klucza rejestracji usługi](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="4846d-157">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="4846d-158">Po podaniu klucza rejestracji konieczne może być zaczekanie 2-3 minut, zanim urządzenie zostanie zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="4846d-158">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4846d-159">Możesz nacisnąć klawisze Ctrl + C i zakończyć działanie Kreatora instalacji w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="4846d-159">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="4846d-160">Jeżeli wprowadzono wszystkie ustawienia sieciowe (adres IP dla protokołu Data 0, maskę podsieci i bramę), wpisy zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="4846d-160">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Postęp rejestracji StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="4846d-162">Po zarejestrowaniu urządzenia zostanie wyświetlony klucz szyfrowania danych usługi.</span><span class="sxs-lookup"><span data-stu-id="4846d-162">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="4846d-163">Skopiuj ten klucz i zapisz go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="4846d-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="4846d-164">**Ten klucz będzie wymagany razem z kluczem rejestracji usługi w celu rejestracji dodatkowych urządzeń w usłudze StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="4846d-164">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="4846d-165">Więcej informacji na temat tego klucza znajduje się w temacie [Zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="4846d-165">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Rejestrowanie urządzenia StorSimple 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="4846d-167">Aby skopiować tekst z okna konsoli szeregowej, po prostu zaznacz tekst.</span><span class="sxs-lookup"><span data-stu-id="4846d-167">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="4846d-168">Następnie możesz wkleić go do schowka lub w dowolnym edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="4846d-168">You should then be able to paste it in the clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="4846d-169">NIE używaj klawiszy Ctrl + C do kopiowania klucza szyfrowania danych usługi.</span><span class="sxs-lookup"><span data-stu-id="4846d-169">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="4846d-170">Użycie klawiszy Ctrl + C spowoduje zakończenie działania Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="4846d-170">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="4846d-171">W efekcie hasło administratora urządzenia nie zostanie zmienione, a na urządzeniu zostanie przywrócone hasło domyślne.</span><span class="sxs-lookup"><span data-stu-id="4846d-171">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
14. <span data-ttu-id="4846d-172">Zakończ działanie konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="4846d-172">Exit the serial console.</span></span>
15. <span data-ttu-id="4846d-173">Wróć do portalu Azure dla instytucji rządowych i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4846d-173">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="4846d-174">Kliknij dwukrotnie usługę StorSimple Manager, aby przejść do strony **Szybki Start**.</span><span class="sxs-lookup"><span data-stu-id="4846d-174">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="4846d-175">Kliknij pozycję **View connected devices** (Wyświetl połączone urządzenia).</span><span class="sxs-lookup"><span data-stu-id="4846d-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="4846d-176">Na stronie **Urządzenia** zweryfikuj, czy urządzenie pomyślnie nawiązało połączenie z usługą, sprawdzając jego stan.</span><span class="sxs-lookup"><span data-stu-id="4846d-176">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="4846d-177">Urządzenie powinno mieć stan **Online**.</span><span class="sxs-lookup"><span data-stu-id="4846d-177">The device status should be **Online**.</span></span>
       
        ![Strona Urządzenia StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="4846d-179">Jeśli urządzenie ma stan **Offline**, zaczekaj kilka minut, aż urządzenie przejdzie do trybu online.</span><span class="sxs-lookup"><span data-stu-id="4846d-179">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span>
       
        <span data-ttu-id="4846d-180">Jeśli po kilku minutach urządzenie jest wciąż w trybie offline, sprawdź, czy sieć zapory została skonfigurowana zgodnie z opisem [wymagań sieciowych dotyczących urządzenia StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="4846d-180">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="4846d-181">Sprawdź, czy port 9354 jest otwarty dla komunikacji wychodzącej, ponieważ jest on używany przez magistralę usług do komunikacji między usługą i urządzeniem w usłudze StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="4846d-181">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager Service-to-device communication.</span></span>

