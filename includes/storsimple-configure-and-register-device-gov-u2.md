<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="e181b-101">tooconfigure i rejestrowanie urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="e181b-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="e181b-102">Dostęp do interfejsu programu Windows PowerShell hello na konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e181b-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="e181b-103">Zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="e181b-103">See [Use PuTTY tooconnect toohello device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="e181b-104">**Można dokładnie procedury hello toofollow się lub nie będą mogli tooaccess hello konsoli.**</span><span class="sxs-lookup"><span data-stu-id="e181b-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="e181b-105">Hello otwartej sesji naciśnij klawisz Enter tooget czasu jeden wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="e181b-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span>
3. <span data-ttu-id="e181b-106">Będzie toochoose zostanie wyświetlony monit o hello języka dla danego urządzenia chcesz tooset.</span><span class="sxs-lookup"><span data-stu-id="e181b-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="e181b-107">Określ język hello, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="e181b-107">Specify hello language, and then press Enter.</span></span>
   
    ![Konfigurowanie i rejestrowanie urządzenia StorSimple 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="e181b-109">W menu konsoli szeregowej hello, które są prezentowane wybierz toolog opcja 1 na z pełnym dostępem.</span><span class="sxs-lookup"><span data-stu-id="e181b-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span>
   
    ![Rejestrowanie urządzenia StorSimple 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="e181b-111">Wykonaj następujące kroki tooconfigure hello minimalne wymagane ustawienia sieciowe urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="e181b-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e181b-112">Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia hello hello toobe.</span><span class="sxs-lookup"><span data-stu-id="e181b-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="e181b-113">Witaj menu konsoli szeregowej wskazuje stan kontrolera hello w komunikacie transparentu hello.</span><span class="sxs-lookup"><span data-stu-id="e181b-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="e181b-114">Jeśli nie są podłączone toohello aktywnym kontrolerze, odłącz, a następnie podłącz toohello aktywnym kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="e181b-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="e181b-115">W wierszu polecenia hello wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="e181b-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="e181b-116">Witaj domyślne hasło urządzenia to **Password1**.</span><span class="sxs-lookup"><span data-stu-id="e181b-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="e181b-117">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e181b-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="e181b-118">Kreator instalacji zostanie wyświetlony toohelp, skonfigurować ustawienia sieciowe hello hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e181b-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="e181b-119">Witaj Podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="e181b-119">Supply hello following information:</span></span>
      
      * <span data-ttu-id="e181b-120">Adres IP interfejsu sieciowego 0 danych</span><span class="sxs-lookup"><span data-stu-id="e181b-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="e181b-121">Maska podsieci</span><span class="sxs-lookup"><span data-stu-id="e181b-121">Subnet mask</span></span>
      * <span data-ttu-id="e181b-122">Brama</span><span class="sxs-lookup"><span data-stu-id="e181b-122">Gateway</span></span>
      * <span data-ttu-id="e181b-123">Adres IP podstawowego serwera DNS</span><span class="sxs-lookup"><span data-stu-id="e181b-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="e181b-124">Adres IP podstawowego serwera NTP</span><span class="sxs-lookup"><span data-stu-id="e181b-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e181b-125">Toowait może mieć kilka minut hello maskę podsieci i zastosować toobe ustawień DNS.</span><span class="sxs-lookup"><span data-stu-id="e181b-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="e181b-126">Opcjonalnie Skonfiguruj serwer proxy sieci web.</span><span class="sxs-lookup"><span data-stu-id="e181b-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="e181b-127">Mimo że konfiguracja serwera proxy sieci web jest opcjonalne, należy pamiętać, że jeśli używasz serwera proxy sieci web, można skonfigurować tylko go tutaj.</span><span class="sxs-lookup"><span data-stu-id="e181b-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="e181b-128">Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="e181b-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="e181b-129">Naciśnij klawisze Ctrl + C tooexit hello Kreator.</span><span class="sxs-lookup"><span data-stu-id="e181b-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="e181b-130">Zainstaluj aktualizacje hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e181b-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="e181b-131">Użyj następującego polecenia cmdlet tooset adresów IP na obu kontrolerów hello hello:</span><span class="sxs-lookup"><span data-stu-id="e181b-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="e181b-132">W wierszu polecenia hello Uruchom `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="e181b-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="e181b-133">Możesz powiadamiania o dostępnych aktualizacjach.</span><span class="sxs-lookup"><span data-stu-id="e181b-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="e181b-134">Uruchom polecenie `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="e181b-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="e181b-135">To polecenie można uruchomić na dowolnym węźle.</span><span class="sxs-lookup"><span data-stu-id="e181b-135">You can run this command on any node.</span></span> <span data-ttu-id="e181b-136">Aktualizacje zostaną zastosowane na powitania pierwszego kontrolera, kontrolera hello zostaną przełączone awaryjnie i następnie hello aktualizacje zostaną zastosowane na hello inny kontroler.</span><span class="sxs-lookup"><span data-stu-id="e181b-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="e181b-137">Możesz monitorować postęp hello aktualizacji hello uruchamiając `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="e181b-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="e181b-138">Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku.</span><span class="sxs-lookup"><span data-stu-id="e181b-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="e181b-139">Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="e181b-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="e181b-140">Może potrwać godziny too11 tooapply hello wszystkie aktualizacje, w tym hello aktualizacje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e181b-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>
8. <span data-ttu-id="e181b-141">Uruchom hello następującego polecenia cmdlet toopoint hello urządzenia toohello Microsoft Azure dla instytucji rządowych portal (ponieważ domyślnie wskazuje toohello publicznego klasyczny portal Azure).</span><span class="sxs-lookup"><span data-stu-id="e181b-141">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="e181b-142">Spowoduje to ponowne uruchomienie obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="e181b-142">This will restart both controllers.</span></span> <span data-ttu-id="e181b-143">Zaleca się użycie dwóch sesji programu PuTTY toosimultaneously połączyć tooboth kontrolerów, tak aby były widoczne po uruchomieniu każdego kontrolera.</span><span class="sxs-lookup"><span data-stu-id="e181b-143">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="e181b-144">Zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="e181b-144">You will see a confirmation message.</span></span> <span data-ttu-id="e181b-145">Zaakceptuj domyślną hello (**Y**).</span><span class="sxs-lookup"><span data-stu-id="e181b-145">Accept hello default (**Y**).</span></span>
9. <span data-ttu-id="e181b-146">Uruchom powitania po zakończeniu instalacji tooresume polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e181b-146">Run hello following cmdlet tooresume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Kreator instalacji Wznów](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="e181b-148">Po wznowieniu instalacji Kreator hello będzie wersji hello Update 2.</span><span class="sxs-lookup"><span data-stu-id="e181b-148">When you resume setup, hello wizard will be hello Update 2 version.</span></span>
10. <span data-ttu-id="e181b-149">Zaakceptuj ustawienia sieciowe hello.</span><span class="sxs-lookup"><span data-stu-id="e181b-149">Accept hello network settings.</span></span> <span data-ttu-id="e181b-150">Po zaakceptowaniu każdego ustawienia, zobaczą komunikat dotyczący sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="e181b-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="e181b-151">Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa po pierwszej sesji hello i trzeba będzie toochange teraz.</span><span class="sxs-lookup"><span data-stu-id="e181b-151">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="e181b-152">Po wyświetleniu monitu podaj hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e181b-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="e181b-153">Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="e181b-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="e181b-154">Witaj hasło musi zawierać trzy z następujących hello: małe litery, wielkie litery, liczbowego i znaki specjalne.</span><span class="sxs-lookup"><span data-stu-id="e181b-154">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Rejestrowanie urządzenia StorSimple 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="e181b-156">Ostatnim krokiem powitania w Kreatorze instalacji hello rejestruje urządzenia z hello usługi Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e181b-156">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="e181b-157">W tym celu będzie konieczne hello klucz rejestracji usługi uzyskany w [krok 2: Pobierz klucz rejestracji usługi hello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="e181b-157">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="e181b-158">Po wpisaniu klucz rejestracji hello mogą być potrzebne toowait 2 – 3 minuty przed zarejestrowaniem urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="e181b-158">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e181b-159">Można nacisnąć klawisze Ctrl + C na wszelkie Kreator hello tooexit czasu.</span><span class="sxs-lookup"><span data-stu-id="e181b-159">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="e181b-160">Jeżeli wprowadzono wszystkie ustawienia sieciowe hello (adres IP interfejsu dane 0, maskę podsieci i bramy), wpisy zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="e181b-160">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Postęp rejestracji StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="e181b-162">Po hello urządzenie zostało zarejestrowane, zostanie wyświetlony klucz szyfrowania danych usługi.</span><span class="sxs-lookup"><span data-stu-id="e181b-162">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="e181b-163">Skopiuj ten klucz i zapisz go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e181b-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="e181b-164">**Ten klucz będzie wymagany razem hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple.**</span><span class="sxs-lookup"><span data-stu-id="e181b-164">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="e181b-165">Odwołuje się zbyt[zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-security.md) Aby uzyskać więcej informacji na temat tego klucza.</span><span class="sxs-lookup"><span data-stu-id="e181b-165">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Rejestrowanie urządzenia StorSimple 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="e181b-167">toocopy hello tekst z okna konsoli szeregowej hello, po prostu zaznacz tekst hello.</span><span class="sxs-lookup"><span data-stu-id="e181b-167">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="e181b-168">Powinien być toopaste mogli go w Schowku hello lub edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="e181b-168">You should then be able toopaste it in hello clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="e181b-169">Nie używaj klawiszy Ctrl + klucza szyfrowania danych usługi hello toocopy C.</span><span class="sxs-lookup"><span data-stu-id="e181b-169">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="e181b-170">Przy użyciu klawiszy Ctrl + C spowoduje, że użytkownik tooexit hello Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="e181b-170">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="e181b-171">W efekcie hasło administratora urządzenia hello nie zostaną zmienione i hello urządzeniu zostanie przywrócone hasło domyślne toohello.</span><span class="sxs-lookup"><span data-stu-id="e181b-171">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
14. <span data-ttu-id="e181b-172">Zakończ hello konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="e181b-172">Exit hello serial console.</span></span>
15. <span data-ttu-id="e181b-173">Zwraca toohello Portal Azure dla instytucji rządowych i ukończyć powitalnych następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e181b-173">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="e181b-174">Kliknij dwukrotnie użytkownika hello tooaccess usługi Menedżer StorSimple **Szybki Start** strony.</span><span class="sxs-lookup"><span data-stu-id="e181b-174">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="e181b-175">Kliknij pozycję **View connected devices** (Wyświetl połączone urządzenia).</span><span class="sxs-lookup"><span data-stu-id="e181b-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="e181b-176">Na powitania **urządzeń** Sprawdź hello urządzenie pomyślnie nawiązało toohello usługi sprawdzając stan hello.</span><span class="sxs-lookup"><span data-stu-id="e181b-176">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="e181b-177">Witaj urządzenie powinno mieć stan **Online**.</span><span class="sxs-lookup"><span data-stu-id="e181b-177">hello device status should be **Online**.</span></span>
       
        ![Strona Urządzenia StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="e181b-179">Jeśli urządzenie ma stan hello **Offline**, zaczekaj kilka minut, aż hello urządzenia toocome online.</span><span class="sxs-lookup"><span data-stu-id="e181b-179">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span>
       
        <span data-ttu-id="e181b-180">Jeśli urządzenie hello jest wciąż w trybie offline, po upływie kilku minut, a następnie należy się upewnić, czy sieć zapory została skonfigurowana zgodnie z opisem toomake [wymagań sieciowych dotyczących urządzenia StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e181b-180">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="e181b-181">Sprawdź, czy port 9354 jest otwarty dla komunikacji wychodzącej, ponieważ jest on używany przez magistralę usług hello komunikacji usługi urządzeń Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e181b-181">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager Service-to-device communication.</span></span>

