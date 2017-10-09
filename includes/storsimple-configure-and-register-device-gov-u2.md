<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure i rejestrowanie urządzenia hello
1. Dostęp do interfejsu programu Windows PowerShell hello na konsoli szeregowej urządzenia StorSimple. Zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) instrukcje. **Można dokładnie procedury hello toofollow się lub nie będą mogli tooaccess hello konsoli.**
2. Hello otwartej sesji naciśnij klawisz Enter tooget czasu jeden wiersz polecenia.
3. Będzie toochoose zostanie wyświetlony monit o hello języka dla danego urządzenia chcesz tooset. Określ język hello, a następnie naciśnij klawisz Enter.
   
    ![Konfigurowanie i rejestrowanie urządzenia StorSimple 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. W menu konsoli szeregowej hello, które są prezentowane wybierz toolog opcja 1 na z pełnym dostępem.
   
    ![Rejestrowanie urządzenia StorSimple 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Wykonaj następujące kroki tooconfigure hello minimalne wymagane ustawienia sieciowe urządzenia hello.
   
   > [!IMPORTANT]
   > Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia hello hello toobe. Witaj menu konsoli szeregowej wskazuje stan kontrolera hello w komunikacie transparentu hello. Jeśli nie są podłączone toohello aktywnym kontrolerze, odłącz, a następnie podłącz toohello aktywnym kontrolerze.
   > 
   > 
   
   1. W wierszu polecenia hello wpisz hasło. Witaj domyślne hasło urządzenia to **Password1**.
   2. Wpisz następujące polecenie hello:
      
        `Invoke-HcsSetupWizard`
   3. Kreator instalacji zostanie wyświetlony toohelp, skonfigurować ustawienia sieciowe hello hello urządzenia. Witaj Podaj następujące informacje:
      
      * Adres IP interfejsu sieciowego 0 danych
      * Maska podsieci
      * Brama
      * Adres IP podstawowego serwera DNS
      * Adres IP podstawowego serwera NTP
      
      > [!NOTE]
      > Toowait może mieć kilka minut hello maskę podsieci i zastosować toobe ustawień DNS.
      > 
      > 
   4. Opcjonalnie Skonfiguruj serwer proxy sieci web.
      
      > [!IMPORTANT]
      > Mimo że konfiguracja serwera proxy sieci web jest opcjonalne, należy pamiętać, że jeśli używasz serwera proxy sieci web, można skonfigurować tylko go tutaj. Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](../articles/storsimple/storsimple-configure-web-proxy.md).
      > 
      > 
6. Naciśnij klawisze Ctrl + C tooexit hello Kreator.
7. Zainstaluj aktualizacje hello w następujący sposób:
   
   1. Użyj następującego polecenia cmdlet tooset adresów IP na obu kontrolerów hello hello:
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. W wierszu polecenia hello Uruchom `Get-HcsUpdateAvailability`. Możesz powiadamiania o dostępnych aktualizacjach.
   3. Uruchom polecenie `Start-HcsUpdate`. To polecenie można uruchomić na dowolnym węźle. Aktualizacje zostaną zastosowane na powitania pierwszego kontrolera, kontrolera hello zostaną przełączone awaryjnie i następnie hello aktualizacje zostaną zastosowane na hello inny kontroler.
      
      Możesz monitorować postęp hello aktualizacji hello uruchamiając `Get-HcsUpdateStatus`.    
      
      Witaj przykładowe dane wyjściowe wyglądają następująco hello aktualizacji w toku.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      Hello następujące przykładowe dane wyjściowe wskazuje, że aktualizacja hello zostało zakończone.
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      Może potrwać godziny too11 tooapply hello wszystkie aktualizacje, w tym hello aktualizacje systemu Windows.
8. Uruchom hello następującego polecenia cmdlet toopoint hello urządzenia toohello Microsoft Azure dla instytucji rządowych portal (ponieważ domyślnie wskazuje toohello publicznego klasyczny portal Azure). Spowoduje to ponowne uruchomienie obu kontrolerów. Zaleca się użycie dwóch sesji programu PuTTY toosimultaneously połączyć tooboth kontrolerów, tak aby były widoczne po uruchomieniu każdego kontrolera.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Zostanie wyświetlony komunikat potwierdzenia. Zaakceptuj domyślną hello (**Y**).
9. Uruchom powitania po zakończeniu instalacji tooresume polecenia cmdlet:
   
    `Invoke-HcsSetupWizard`
   
    ![Kreator instalacji Wznów](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   Po wznowieniu instalacji Kreator hello będzie wersji hello Update 2.
10. Zaakceptuj ustawienia sieciowe hello. Po zaakceptowaniu każdego ustawienia, zobaczą komunikat dotyczący sprawdzania poprawności.
11. Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa po pierwszej sesji hello i trzeba będzie toochange teraz. Po wyświetleniu monitu podaj hasło administratora urządzenia. Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków. Witaj hasło musi zawierać trzy z następujących hello: małe litery, wielkie litery, liczbowego i znaki specjalne.
    
    <br/>![Rejestrowanie urządzenia StorSimple 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. Ostatnim krokiem powitania w Kreatorze instalacji hello rejestruje urządzenia z hello usługi Menedżer StorSimple. W tym celu będzie konieczne hello klucz rejestracji usługi uzyskany w [krok 2: Pobierz klucz rejestracji usługi hello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Po wpisaniu klucz rejestracji hello mogą być potrzebne toowait 2 – 3 minuty przed zarejestrowaniem urządzenia hello.
    
    > [!NOTE]
    > Można nacisnąć klawisze Ctrl + C na wszelkie Kreator hello tooexit czasu. Jeżeli wprowadzono wszystkie ustawienia sieciowe hello (adres IP interfejsu dane 0, maskę podsieci i bramy), wpisy zostaną zachowane.
    > 
    > 
    
    ![Postęp rejestracji StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Po hello urządzenie zostało zarejestrowane, zostanie wyświetlony klucz szyfrowania danych usługi. Skopiuj ten klucz i zapisz go w bezpiecznym miejscu. **Ten klucz będzie wymagany razem hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple.** Odwołuje się zbyt[zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-security.md) Aby uzyskać więcej informacji na temat tego klucza.
    
    ![Rejestrowanie urządzenia StorSimple 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > toocopy hello tekst z okna konsoli szeregowej hello, po prostu zaznacz tekst hello. Powinien być toopaste mogli go w Schowku hello lub edytorze tekstu.
    > 
    > Nie używaj klawiszy Ctrl + klucza szyfrowania danych usługi hello toocopy C. Przy użyciu klawiszy Ctrl + C spowoduje, że użytkownik tooexit hello Kreatora instalacji. W efekcie hasło administratora urządzenia hello nie zostaną zmienione i hello urządzeniu zostanie przywrócone hasło domyślne toohello.
    > 
    > 
14. Zakończ hello konsoli szeregowej.
15. Zwraca toohello Portal Azure dla instytucji rządowych i ukończyć powitalnych następujące kroki:
    
    1. Kliknij dwukrotnie użytkownika hello tooaccess usługi Menedżer StorSimple **Szybki Start** strony.
    2. Kliknij pozycję **View connected devices** (Wyświetl połączone urządzenia).
    3. Na powitania **urządzeń** Sprawdź hello urządzenie pomyślnie nawiązało toohello usługi sprawdzając stan hello. Witaj urządzenie powinno mieć stan **Online**.
       
        ![Strona Urządzenia StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        Jeśli urządzenie ma stan hello **Offline**, zaczekaj kilka minut, aż hello urządzenia toocome online.
       
        Jeśli urządzenie hello jest wciąż w trybie offline, po upływie kilku minut, a następnie należy się upewnić, czy sieć zapory została skonfigurowana zgodnie z opisem toomake [wymagań sieciowych dotyczących urządzenia StorSimple](../articles/storsimple/storsimple-system-requirements.md).
       
        Sprawdź, czy port 9354 jest otwarty dla komunikacji wychodzącej, ponieważ jest on używany przez magistralę usług hello komunikacji usługi urządzeń Menedżer StorSimple.

