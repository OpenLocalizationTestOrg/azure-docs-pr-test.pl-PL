<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure i rejestrowanie urządzenia hello
1. Dostęp do interfejsu programu Windows PowerShell hello na konsoli szeregowej urządzenia StorSimple. Zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) instrukcje. **Można dokładnie procedury hello toofollow się lub nie będą mogli tooaccess hello konsoli.**
2. Hello otwartej sesji naciśnij klawisz Enter tooget czasu jeden wiersz polecenia. 
3. Będzie toochoose zostanie wyświetlony monit o hello języka dla danego urządzenia chcesz tooset. Określ język hello, a następnie naciśnij klawisz Enter. 
   
    ![Konfigurowanie i rejestrowanie urządzenia StorSimple 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. W menu konsoli szeregowej hello, które są prezentowane wybierz toolog opcja 1 na z pełnym dostępem. 
   
    ![Rejestrowanie urządzenia StorSimple 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Wykonaj kroki 5 – 12 tooconfigure hello minimalne wymagane ustawienia sieciowe urządzenia. **Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia hello hello toobe.** Witaj menu konsoli szeregowej wskazuje stan kontrolera hello w komunikacie transparentu hello. Jeśli nie masz połączenia kontrolera active toohello, odłącz, a następnie podłącz toohello aktywnym kontrolerze.
5. W wierszu polecenia hello wpisz hasło. Witaj domyślne hasło urządzenia to **Password1**.
6. Wpisz następujące polecenie hello:
   
     `Invoke-HcsSetupWizard` 
7. Kreator instalacji zostanie wyświetlony toohelp, skonfigurować ustawienia sieciowe hello hello urządzenia. Witaj Witaj Podaj następujące informacje: 
   
   * Adres IP interfejsu sieciowego 0 danych hello
   * Maska podsieci
   * Brama
   * Adres IP podstawowego serwera DNS
   * Adres IP podstawowego serwera NTP
     
     > [!NOTE]
     > Toowait może mieć kilka minut hello maskę podsieci i toobe ustawienia DNS hello zastosowane. Jeśli otrzymasz "hello urządzenie nie jest gotowe." komunikat o błędzie, sprawdź hello połączenie z siecią fizyczną w interfejsie sieciowym 0 danych hello na aktywnym kontrolerze.
     > 
     > 
8. Opcjonalnie skonfiguruj serwer proxy sieci Web. Konfiguracja serwera proxy sieci Web jest opcjonalna, jednak **warto wiedzieć, że w przypadku korzystania z serwera proxy sieci Web można go skonfigurować tylko w tym miejscu**. Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](../articles/storsimple/storsimple-configure-web-proxy.md). Jeśli wystąpiły problemy podczas tego kroku, zobacz tootroubleshooting wskazówki dotyczące [błędów podczas konfigurowania serwera proxy sieci web](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > Można nacisnąć klawisze Ctrl + C na wszelkie Kreator hello tooexit czasu. Wszystkie ustawienia zastosowane przed wydaniem tego polecenia zostaną zachowane.

1. Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa po pierwszej sesji hello i trzeba będzie toochange go w kolejnych sesjach. Po wyświetleniu monitu podaj hasło administratora urządzenia. Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków. Witaj hasło musi zawierać kombinację małych liter, wielkich liter, cyfr i znaków specjalnych.
2. hasło programu StorSimple Snapshot Manager Hello także ustawić w tym miejscu. To hasło jest używane podczas uwierzytelniania urządzenia na hoście systemu Windows z uruchomionym programem StorSimple Snapshot Manager. Po wyświetleniu monitu podaj hasło znak 14 too15. Witaj hasło musi zawierać kombinację trzech z następujących hello: małe litery, wielkie litery, liczbowego i znaki specjalne. 
   
   ![Rejestrowanie urządzenia StorSimple 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Hasło programu StorSimple Snapshot Manager hello w interfejsie usługi Menedżer StorSimple hello można zresetować. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[zmiany haseł usługi StorSimple hello przy użyciu usługi Menedżer StorSimple hello](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot wszelkie problemy w tym kroku, zobacz tootroubleshooting wskazówki dotyczące [błędy związane z toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. Ostatnim krokiem powitania w Kreatorze instalacji hello rejestruje urządzenia z hello usługi Menedżer StorSimple. W tym celu należy hello klucz rejestracji usługi, które zostały uzyskane w kroku 2. Po wpisaniu klucz rejestracji hello mogą być potrzebne toowait 2 – 3 minuty przed zarejestrowaniem urządzenia hello.
   
   tootroubleshoot wszelkie błędami rejestracji urządzenia, zobacz zbyt[błędy podczas rejestracji urządzenia](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Szczegółowe Rozwiązywanie problemów, można także odwoływać się zbyt[przykład rozwiązywania problemów krok po kroku](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Po hello urządzenie zostało zarejestrowane, zostanie wyświetlony klucz szyfrowania danych usługi. Skopiuj ten klucz i zapisz go w bezpiecznym miejscu.
   
   > [!WARNING]
   > Ten klucz będzie wymagany razem hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple. Odwołuje się zbyt[zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-security.md) Aby uzyskać więcej informacji na temat tego klucza.
   > 
   > 
   
    ![Rejestrowanie urządzenia StorSimple 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    toocopy hello tekst z okna konsoli szeregowej hello, po prostu zaznacz tekst hello. Powinien być toopaste mogli go w Schowku hello lub edytorze tekstu. Nie używaj klawiszy Ctrl + klucza szyfrowania danych usługi hello toocopy C. Przy użyciu klawiszy Ctrl + C spowoduje, że użytkownik tooexit hello Kreatora instalacji. W efekcie hasło administratora urządzenia hello i hasło programu StorSimple Snapshot Manager hello nie zostaną zmienione i hello urządzeniu zostanie przywrócone hasło domyślne toohello.
5. Zakończ hello konsoli szeregowej.
6. Zwraca toohello klasycznego portalu Azure i ukończyć powitalnych następujące kroki:
   
   1. Kliknij dwukrotnie użytkownika hello tooaccess usługi Menedżer StorSimple **Szybki Start** strony.
   2. Kliknij pozycję **View connected devices** (Wyświetl połączone urządzenia).
   3. Na powitania **urządzeń** Sprawdź hello urządzenie pomyślnie nawiązało toohello usługi sprawdzając stan hello. Witaj urządzenie powinno mieć stan **Online**. Jeśli urządzenie ma stan hello **Offline**, zaczekaj kilka minut, aż hello urządzenia toocome online.
   
   ![Strona Urządzenia StorSimple](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Po hello urządzenie jest w trybie online, podłącz kable sieciowe hello, które zostały odłączone hello na początku tego kroku.
   > 
   > 

Po hello urządzenie zostało pomyślnie zarejestrowane i nie przeszło do trybu online, możesz uruchomić hello `Test-HcsmConnection -Verbose` tooensure, który hello połączenie sieciowe jest w dobrej kondycji. Dla hello szczegółowe dane użycia tego polecenia cmdlet go za[Dokumentacja poleceń cmdlet dla Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Zobacz film](./media/storsimple-configure-and-register-device/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób tooconfigure i rejestrowanie urządzenia za pośrednictwem programu Windows PowerShell dla urządzenia StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

