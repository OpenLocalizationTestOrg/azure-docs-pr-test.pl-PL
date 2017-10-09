<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure i rejestrowanie urządzenia hello
1. Dostęp do interfejsu programu Windows PowerShell hello na konsoli szeregowej urządzenia StorSimple. Zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) instrukcje. **Można dokładnie procedury hello toofollow się lub nie będą mogli tooaccess hello konsoli.**
2. Hello otwartej sesji naciśnij klawisz Enter tooget czasu jeden wiersz polecenia. 
3. Będzie toochoose zostanie wyświetlony monit o hello języka dla danego urządzenia chcesz tooset. Określ język hello, a następnie naciśnij klawisz Enter. 
   
    ![Konfigurowanie i rejestrowanie urządzenia StorSimple 1](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. W menu konsoli szeregowej hello, które są prezentowane wybierz toolog opcja 1 na z pełnym dostępem. 
   
    ![Rejestrowanie urządzenia StorSimple 2](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Wykonaj kroki 5 – 12 tooconfigure hello minimalne wymagane ustawienia sieciowe urządzenia. **Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia hello hello toobe.** Witaj menu konsoli szeregowej wskazuje stan kontrolera hello w komunikacie transparentu hello. Jeśli nie masz połączenia kontrolera active toohello, odłącz, a następnie podłącz toohello aktywnym kontrolerze.
5. W wierszu polecenia hello wpisz hasło. Witaj domyślne hasło urządzenia to **Password1**.
6. Witaj wpisz następujące polecenie: `Invoke-HcsSetupWizard`. 
7. Kreator instalacji zostanie wyświetlony toohelp, skonfigurować ustawienia sieciowe hello hello urządzenia. Witaj Witaj Podaj następujące informacje: 
   
   * Adres IP interfejsu sieciowego 0 danych hello
   * Maska podsieci
   * Brama
   * Adres IP podstawowego serwera DNS
     
        Należy pamiętać, że hello system sprawdza poprawność ustawień sieciowych po każdym kroku w procesie hello.
     
     > [!NOTE]
     > Toowait może mieć kilka minut hello maskę podsieci i toobe ustawienia DNS hello zastosowane. Jeśli zostanie wyświetlony komunikat o błędzie "Wyboru hello sieci łączności tooData 0", sprawdź połączenie z siecią fizyczną hello w interfejsie sieciowym 0 danych hello na aktywnym kontrolerze.
     > 
     > 
8. Opcjonalnie skonfiguruj serwer proxy sieci Web. Konfiguracja serwera proxy sieci Web jest opcjonalna, jednak **warto wiedzieć, że w przypadku korzystania z serwera proxy sieci Web można go skonfigurować tylko w tym miejscu**. Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Skonfiguruj podstawowy serwer NTP dla urządzenia. Serwery NTP są wymagane, ponieważ urządzenie musi synchronizować czas do celów uwierzytelniania dostawców usługi w chmurze. Upewnij się, że sieć zezwala toopass ruch NTP z sieci centrum danych toohello Internet. Jeśli nie jest to możliwe, określ wewnętrzny serwer NTP. 
10. Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa po pierwszej sesji hello i trzeba będzie toochange teraz. Po wyświetleniu monitu podaj hasło administratora urządzenia. Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków. Witaj hasło musi zawierać trzy z następujących hello: małe litery, wielkie litery, liczbowego i znaki specjalne.
    
    <br/>![Rejestrowanie urządzenia StorSimple 5](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. Ostatnim krokiem powitania w Kreatorze instalacji hello rejestruje urządzenia z hello usługi Menedżer StorSimple. W tym celu należy hello klucz rejestracji usługi, które zostały uzyskane w kroku 2. Po wpisaniu klucz rejestracji hello mogą być potrzebne toowait 2 – 3 minuty przed zarejestrowaniem urządzenia hello.
    
    > [!NOTE]
    > Można nacisnąć klawisze Ctrl + C na wszelkie Kreator hello tooexit czasu. Jeżeli wprowadzono wszystkie ustawienia sieciowe hello (adres IP interfejsu dane 0, maskę podsieci i bramy), wpisy zostaną zachowane.
    > 
    > 
    
    ![Rejestrowanie urządzenia StorSimple 6](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Po hello urządzenie zostało zarejestrowane, zostanie wyświetlony klucz szyfrowania danych usługi. Skopiuj ten klucz i zapisz go w bezpiecznym miejscu. **Ten klucz będzie wymagany razem hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple.** Odwołuje się zbyt[zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-security.md) Aby uzyskać więcej informacji na temat tego klucza.
    
    ![Rejestrowanie urządzenia StorSimple 7](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > toocopy hello tekst z okna konsoli szeregowej hello, po prostu zaznacz tekst hello. Powinien być toopaste mogli go w Schowku hello lub edytorze tekstu. Nie używaj klawiszy Ctrl + klucza szyfrowania danych usługi hello toocopy C. Przy użyciu klawiszy Ctrl + C spowoduje, że użytkownik tooexit hello Kreatora instalacji. W efekcie hasło administratora urządzenia hello nie zostaną zmienione i hello urządzeniu zostanie przywrócone hasło domyślne toohello.
    > 
    > 
13. Zakończ hello konsoli szeregowej.
14. Zwraca toohello klasycznego portalu Azure i ukończyć powitalnych następujące kroki:
    
    1. Kliknij dwukrotnie użytkownika hello tooaccess usługi Menedżer StorSimple **Szybki Start** strony.
    2. Kliknij pozycję **View connected devices** (Wyświetl połączone urządzenia).
    3. Na powitania **urządzeń** Sprawdź hello urządzenie pomyślnie nawiązało toohello usługi sprawdzając stan hello. Witaj urządzenie powinno mieć stan **Online**.
       
        ![Strona Urządzenia StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Jeśli urządzenie ma stan hello **Offline**, zaczekaj kilka minut, aż hello urządzenia toocome online. 
       
        Jeśli urządzenie hello jest wciąż w trybie offline, po upływie kilku minut, a następnie należy się upewnić, czy sieć zapory została skonfigurowana zgodnie z opisem toomake [wymagań sieciowych dotyczących urządzenia StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Sprawdź, czy port 9354 jest otwarty dla komunikacji wychodzącej, ponieważ jest on używany przez magistralę usług hello komunikacji usługi urządzeń Menedżer StorSimple.

