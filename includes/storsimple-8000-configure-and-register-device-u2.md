<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>tooconfigure i rejestrowanie urządzenia hello

1. Dostęp do interfejsu programu Windows PowerShell hello na konsoli szeregowej urządzenia StorSimple. Zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) instrukcje. **Można dokładnie procedury hello toofollow się lub nie będą mogli tooaccess hello konsoli.**

2. W sesji hello otwartym, naciśnij klawisz **Enter** tooget czasu jeden wiersz polecenia.

3. Będzie toochoose zostanie wyświetlony monit o hello języka dla danego urządzenia chcesz tooset. Określ hello języka, a następnie naciśnij klawisz **Enter**.

4. W menu konsoli szeregowej hello, które są prezentowane, wybierz opcję 1 zbyt**Zaloguj się przy użyciu pełnego dostępu**.
     Wykonaj kroki 5 – 12 tooconfigure hello minimalne wymagane ustawienia sieciowe urządzenia. **Te kroki konfiguracji należy wykonać na aktywnym kontrolerze urządzenia hello hello toobe.** Witaj menu konsoli szeregowej wskazuje stan kontrolera hello w komunikacie transparentu hello. Jeśli nie masz połączenia kontrolera active toohello, odłącz, a następnie podłącz toohello aktywnym kontrolerze.

5. W wierszu polecenia hello wpisz hasło. Witaj domyślne hasło urządzenia to **Password1**.

6. Witaj wpisz następujące polecenie: `Invoke-HcsSetupWizard`.

7. Kreator instalacji zostanie wyświetlony toohelp, skonfigurować ustawienia sieciowe hello hello urządzenia. Witaj Witaj Podaj następujące informacje:
   
   * Adres IP interfejsu sieciowego 0 danych hello
   * Maska podsieci
   * Brama
   * Adres IP podstawowego serwera DNS

   Poniżej przedstawiono przykładowe dane wyjściowe.

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
    W hello poprzedzających przykładowe dane wyjściowe widać, że hello system sprawdza poprawność ustawień sieciowych po każdym kroku w procesie hello.

     > [!NOTE]
     > Toowait może mieć kilka minut hello maskę podsieci i toobe ustawienia DNS hello zastosowane. Jeśli zostanie wyświetlony komunikat o błędzie "Wyboru hello sieci łączności tooData 0", sprawdź połączenie z siecią fizyczną hello w interfejsie sieciowym 0 danych hello na aktywnym kontrolerze.

8. Opcjonalnie skonfiguruj serwer proxy sieci Web. Konfiguracja serwera proxy sieci Web jest opcjonalna, jednak **warto wiedzieć, że w przypadku korzystania z serwera proxy sieci Web można go skonfigurować tylko w tym miejscu**. Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Skonfiguruj podstawowy serwer NTP dla urządzenia. Serwery NTP są wymagane, ponieważ urządzenie musi synchronizować czas do celów uwierzytelniania dostawców usługi w chmurze. Upewnij się, że sieć zezwala toopass ruch NTP z sieci centrum danych toohello Internet. Jeśli nie jest to możliwe, określ wewnętrzny serwer NTP.

    Poniżej pokazano przykładowe dane wyjściowe.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Ze względów bezpieczeństwa hasło administratora urządzenia hello wygasa po pierwszej sesji hello i trzeba będzie toochange teraz. Po wyświetleniu monitu podaj hasło administratora urządzenia. Prawidłowe hasło administratora urządzenia musi zawierać od 8 do 15 znaków. Witaj hasło musi zawierać trzy z następujących hello: małe litery, wielkie litery, liczbowego i znaki specjalne.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. Ostatnim krokiem powitania w Kreatorze instalacji hello rejestruje urządzenia z hello usługi Menedżer StorSimple urządzenia. W tym celu należy hello klucz rejestracji usługi, które zostały uzyskane w kroku 2. Po wpisaniu klucz rejestracji hello mogą być potrzebne toowait 2 – 3 minuty przed zarejestrowaniem urządzenia hello.
    
    > [!NOTE]
    > Można nacisnąć klawisze Ctrl + C na wszelkie Kreator hello tooexit czasu. Jeżeli wprowadzono wszystkie ustawienia sieciowe hello (adres IP interfejsu dane 0, maskę podsieci i bramy), wpisy zostaną zachowane.
    
    Poniżej pokazano przykładowe dane wyjściowe.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Po hello urządzenie zostało zarejestrowane, zostanie wyświetlony klucz szyfrowania danych usługi. Skopiuj ten klucz i zapisz go w bezpiecznym miejscu. **Ten klucz będzie wymagany razem hello usługi rejestracji klucza tooregister dodatkowych urządzeń z hello usługi Menedżer StorSimple urządzenia.** Odwołuje się zbyt[zabezpieczenia usługi StorSimple](../articles/storsimple/storsimple-security.md) Aby uzyskać więcej informacji na temat tego klucza.
    
    ![Rejestrowanie urządzenia StorSimple 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > toocopy hello tekst z okna konsoli szeregowej hello, po prostu zaznacz tekst hello. Powinien być toopaste mogli go w Schowku hello lub edytorze tekstu. Nie używaj klawiszy Ctrl + klucza szyfrowania danych usługi hello toocopy C. Przy użyciu klawiszy Ctrl + C spowoduje, że użytkownik tooexit hello Kreatora instalacji. W efekcie hasło administratora urządzenia hello nie zostaną zmienione i hello urządzeniu zostanie przywrócone hasło domyślne toohello.
    
13. Zakończ hello konsoli szeregowej.
14. Zwraca toohello portalu Azure i ukończyć powitalnych następujące kroki:
    
    1. Przejdź tooyour usługi Menedżer urządzeń StorSimple.
    2. Kliknij pozycję **Urządzenia**.
    3. W hello tabelarycznej listę urządzeń Sprawdź, czy urządzenie hello pomyślnie połączył usługi toohello sprawdzając stan hello. Witaj urządzenie powinno mieć stan **gotowe tooset się**.
       
        ![Strona Urządzenia StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Mogą być potrzebne toowait kilka minut dla toochange stan urządzenia hello zbyt**gotowe tooset się**.
       
        Jeśli hello urządzenie nie jest wyświetlany na liście, należy się upewnić, czy sieć zapory została skonfigurowana zgodnie z opisem toomake [wymagań sieciowych dotyczących urządzenia StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md). Sprawdź, czy port 9354 jest otwarty dla komunikacji wychodzącej, ponieważ jest on używany przez magistralę usług hello komunikacji urządzenie usługi Menedżer StorSimple urządzenia.

