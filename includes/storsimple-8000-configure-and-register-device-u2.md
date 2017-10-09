<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="5f3fa-101">tooconfigure i rejestrowanie urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="5f3fa-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="5f3fa-102">Dostęp do interfejsu programu Windows PowerShell hello na konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="5f3fa-103">Zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="5f3fa-104">**Można dokładnie procedury hello toofollow się lub nie będą mogli tooaccess hello konsoli.**</span><span class="sxs-lookup"><span data-stu-id="5f3fa-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="5f3fa-105">W sesji hello otwartym, naciśnij klawisz **Enter** tooget czasu jeden wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="5f3fa-106">Będzie toochoose zostanie wyświetlony monit o hello języka dla danego urządzenia chcesz tooset.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="5f3fa-107">Określ hello języka, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="5f3fa-108">W menu konsoli szeregowej hello, które są prezentowane, wybierz opcję 1 zbyt**Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="5f3fa-109">Wykonaj kroki 5 – 12 tooconfigure hello minimalne wymagane ustawienia sieciowe urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="5f3fa-110">**Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia hello hello toobe.**</span><span class="sxs-lookup"><span data-stu-id="5f3fa-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="5f3fa-111">Witaj menu konsoli szeregowej wskazuje stan kontrolera hello w komunikacie transparentu hello.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="5f3fa-112">Jeśli nie masz połączenia kontrolera active toohello, odłącz, a następnie podłącz toohello aktywnym kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="5f3fa-113">W wierszu polecenia hello wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="5f3fa-114">Witaj domyślne hasło urządzenia to **Password1**.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="5f3fa-115">Witaj wpisz następujące polecenie: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="5f3fa-116">Kreator instalacji zostanie wyświetlony toohelp, skonfigurować ustawienia sieciowe hello hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="5f3fa-117">Witaj Witaj Podaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="5f3fa-118">Adres IP interfejsu sieciowego 0 danych hello</span><span class="sxs-lookup"><span data-stu-id="5f3fa-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="5f3fa-119">Maska podsieci</span><span class="sxs-lookup"><span data-stu-id="5f3fa-119">Subnet mask</span></span>
   * <span data-ttu-id="5f3fa-120">Brama</span><span class="sxs-lookup"><span data-stu-id="5f3fa-120">Gateway</span></span>
   * <span data-ttu-id="5f3fa-121">Adres IP podstawowego serwera DNS</span><span class="sxs-lookup"><span data-stu-id="5f3fa-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="5f3fa-122">Poniżej przedstawiono przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="5f3fa-123">W hello poprzedzających przykładowe dane wyjściowe widać, że hello system sprawdza poprawność ustawień sieciowych po każdym kroku w procesie hello.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="5f3fa-124">Toowait może mieć kilka minut hello maskę podsieci i toobe ustawienia DNS hello zastosowane.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="5f3fa-125">Jeśli zostanie wyświetlony komunikat o błędzie "Wyboru hello sieci łączności tooData 0", sprawdź połączenie z siecią fizyczną hello w interfejsie sieciowym 0 danych hello na aktywnym kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="5f3fa-126">Opcjonalnie skonfiguruj serwer proxy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="5f3fa-127">Konfiguracja serwera proxy sieci Web jest opcjonalna, jednak **warto wiedzieć, że w przypadku korzystania z serwera proxy sieci Web można go skonfigurować tylko w tym miejscu**.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="5f3fa-128">Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="5f3fa-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="5f3fa-129">Skonfiguruj podstawowy serwer NTP dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="5f3fa-130">Serwery NTP są wymagane, ponieważ urządzenie musi synchronizować czas do celów uwierzytelniania dostawców usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="5f3fa-131">Upewnij się, że sieć zezwala toopass ruch NTP z sieci centrum danych toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="5f3fa-132">Jeśli nie jest to możliwe, określ wewnętrzny serwer NTP.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="5f3fa-133">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="5f3fa-134">Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa po pierwszej sesji hello i trzeba będzie toochange teraz.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="5f3fa-135">Po wyświetleniu monitu podaj hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="5f3fa-136">Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="5f3fa-137">Witaj hasło musi zawierać trzy z następujących hello: małe litery, wielkie litery, liczbowego i znaki specjalne.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="5f3fa-138">Ostatnim krokiem powitania w Kreatorze instalacji hello rejestruje urządzenia z hello usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="5f3fa-139">W tym celu należy hello klucz rejestracji usługi, które zostały uzyskane w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="5f3fa-140">Po wpisaniu klucz rejestracji hello mogą być potrzebne toowait 2 – 3 minuty przed zarejestrowaniem urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5f3fa-141">Można nacisnąć klawisze Ctrl + C na wszelkie Kreator hello tooexit czasu.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="5f3fa-142">Jeżeli wprowadzono wszystkie ustawienia sieciowe hello (adres IP interfejsu dane 0, maskę podsieci i bramy), wpisy zostaną zachowane.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="5f3fa-143">Poniżej pokazano przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="5f3fa-144">Po hello urządzenie zostało zarejestrowane, zostanie wyświetlony klucz szyfrowania danych usługi.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="5f3fa-145">Skopiuj ten klucz i zapisz go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="5f3fa-146">**Ten klucz będzie wymagany razem hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple urządzenia.**</span><span class="sxs-lookup"><span data-stu-id="5f3fa-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="5f3fa-147">Odwołuje się zbyt[zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-security.md) Aby uzyskać więcej informacji na temat tego klucza.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Rejestrowanie urządzenia StorSimple 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="5f3fa-149">toocopy hello tekst z okna konsoli szeregowej hello, po prostu zaznacz tekst hello.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="5f3fa-150">Powinien być toopaste mogli go w Schowku hello lub edytorze tekstu.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="5f3fa-151">Nie używaj klawiszy Ctrl + klucza szyfrowania danych usługi hello toocopy C.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="5f3fa-152">Przy użyciu klawiszy Ctrl + C spowoduje, że użytkownik tooexit hello Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="5f3fa-153">W efekcie hasło administratora urządzenia hello nie zostaną zmienione i hello urządzeniu zostanie przywrócone hasło domyślne toohello.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="5f3fa-154">Zakończ hello konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="5f3fa-155">Zwraca toohello portalu Azure i ukończyć powitalnych następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="5f3fa-156">Przejdź tooyour usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="5f3fa-157">Kliknij pozycję **Urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="5f3fa-158">W hello tabelarycznej listę urządzeń Sprawdź, czy urządzenie hello pomyślnie połączył usługi toohello sprawdzając stan hello.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="5f3fa-159">Witaj urządzenie powinno mieć stan **gotowe tooset się**.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Strona Urządzenia StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="5f3fa-161">Mogą być potrzebne toowait kilka minut dla toochange stan urządzenia hello zbyt**gotowe tooset się**.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="5f3fa-162">Jeśli hello urządzenie nie jest wyświetlany na liście, należy się upewnić, czy sieć zapory została skonfigurowana zgodnie z opisem toomake [wymagań sieciowych dotyczących urządzenia StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="5f3fa-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="5f3fa-163">Sprawdź, czy port 9354 jest otwarty dla komunikacji wychodzącej, ponieważ jest on używany przez magistralę usług hello komunikacji urządzenie usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

