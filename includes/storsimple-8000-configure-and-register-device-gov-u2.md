<!--author=SharS last changed: 06/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure i rejestrowanie urządzenia hello
1. Dostęp do interfejsu programu Windows PowerShell hello na konsoli szeregowej urządzenia StorSimple. Zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) instrukcje. **Można dokładnie procedury hello toofollow się lub nie będą mogli tooaccess hello konsoli.**
2. W sesji hello otwartym, naciśnij klawisz **Enter** tooget czasu jeden wiersz polecenia.
3. Będzie toochoose zostanie wyświetlony monit o hello języka dla danego urządzenia chcesz tooset. Określ hello języka, a następnie naciśnij klawisz **Enter**.
   
    ![Konfigurowanie i rejestrowanie urządzenia StorSimple 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. W menu konsoli szeregowej hello, które są prezentowane wybierz toolog opcja 1 na z pełnym dostępem.
   
    ![Rejestrowanie urządzenia StorSimple 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Wykonaj następujące kroki tooconfigure hello minimalne wymagane ustawienia sieciowe urządzenia hello.
   
   > [!IMPORTANT]
   > Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia hello hello toobe. Witaj menu konsoli szeregowej wskazuje stan kontrolera hello w komunikacie transparentu hello. Jeśli nie są podłączone toohello aktywnym kontrolerze, odłącz, a następnie podłącz toohello aktywnym kontrolerze.
   
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
    
   4. Opcjonalnie Skonfiguruj serwer proxy sieci web.
      
      > [!IMPORTANT]
      > Mimo że konfiguracja serwera proxy sieci web jest opcjonalne, należy pamiętać, że jeśli używasz serwera proxy sieci web, można skonfigurować tylko go tutaj. Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](../articles/storsimple/storsimple-configure-web-proxy.md).
     
6. Naciśnij klawisze Ctrl + C tooexit hello Kreator.
8. Uruchom hello następującego polecenia cmdlet toopoint hello urządzenia toohello Microsoft Azure dla instytucji rządowych portal (ponieważ domyślnie wskazuje toohello publicznego klasyczny portal Azure). Spowoduje to ponowne uruchomienie obu kontrolerów. Zaleca się użycie dwóch sesji programu PuTTY toosimultaneously połączyć tooboth kontrolerów, tak aby były widoczne po uruchomieniu każdego kontrolera.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Zostanie wyświetlony komunikat potwierdzenia. Zaakceptuj domyślną hello (**Y**).
9. Uruchom powitania po zakończeniu instalacji tooresume polecenia cmdlet:
   
    `Invoke-HcsSetupWizard`
   
    ![Kreator instalacji Wznów](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
10. Zaakceptuj ustawienia sieciowe hello. Po zaakceptowaniu każdego ustawienia, zobaczą komunikat dotyczący sprawdzania poprawności.
11. Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa po pierwszej sesji hello i trzeba będzie toochange teraz. Po wyświetleniu monitu podaj hasło administratora urządzenia. Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków. Witaj hasło musi zawierać trzy z następujących hello: małe litery, wielkie litery, liczbowego i znaki specjalne.
    
    <br/>![Rejestrowanie urządzenia StorSimple 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. Ostatnim krokiem powitania w Kreatorze instalacji hello rejestruje urządzenia z hello usługi Menedżer StorSimple urządzenia. W tym celu będzie konieczne hello klucz rejestracji usługi uzyskany w [krok 2: Pobierz klucz rejestracji usługi hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Po wpisaniu klucz rejestracji hello mogą być potrzebne toowait 2 – 3 minuty przed zarejestrowaniem urządzenia hello.
    
    > [!NOTE]
    > Można nacisnąć klawisze Ctrl + C na wszelkie Kreator hello tooexit czasu. Jeżeli wprowadzono wszystkie ustawienia sieciowe hello (adres IP interfejsu dane 0, maskę podsieci i bramy), wpisy zostaną zachowane.
    
    ![Postęp rejestracji StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Po hello urządzenie zostało zarejestrowane, zostanie wyświetlony klucz szyfrowania danych usługi. Skopiuj ten klucz i zapisz go w bezpiecznym miejscu. **Ten klucz jest wymagany w przypadku hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple urządzenia.** Odwołuje się zbyt[zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-8000-security.md) Aby uzyskać więcej informacji na temat tego klucza.
    
    ![Rejestrowanie urządzenia StorSimple 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)
    > [!IMPORTANT]
    > toocopy hello tekst z okna konsoli szeregowej hello, po prostu zaznacz tekst hello. Powinien być toopaste mogli go w Schowku hello lub edytorze tekstu.
    > 
    > Nie używaj **klawisze Ctrl + C** klucza szyfrowania danych usługi hello toocopy. Przy użyciu **klawisze Ctrl + C** spowoduje tooexit hello Kreator. W efekcie hasło administratora urządzenia hello nie zostaną zmienione i hello urządzeniu zostanie przywrócone hasło domyślne toohello.
    
14. Zakończ hello konsoli szeregowej.
15. Zwraca toohello Portal Azure dla instytucji rządowych i ukończyć powitalnych następujące kroki:
    
    1. Przejdź tooyour usługi Menedżer urządzeń StorSimple.
    2. Kliknij pozycję **Urządzenia**. Z listy hello urządzeń należy zidentyfikować urządzenie hello czy ddeploying. Sprawdź, czy urządzenie hello pomyślnie połączył usługi toohello sprawdzając stan hello. Witaj urządzenie powinno mieć stan **Online**.
            
        Jeśli urządzenie ma stan hello **Offline**, zaczekaj kilka minut, aż hello urządzenia toocome online.
       
        Jeśli urządzenie hello jest wciąż w trybie offline, po upływie kilku minut, a następnie należy się upewnić, czy sieć zapory została skonfigurowana zgodnie z opisem toomake [wymagań sieciowych dotyczących urządzenia StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).
       
        Sprawdź, czy port 9354 jest otwarty dla komunikacji wychodzącej, ponieważ jest on używany przez magistralę usług hello komunikacji usługi urządzenia StorSimple Menedżera urządzeń.

