### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Przygotowanie do instalacji wypychanej na serwerze z systemem Linux

1. Upewnij się, że istnieje połączenie sieciowe między hello komputera z systemem Linux i powitania serwera przetwarzania.
2. Tworzenie konta usługi serwera przetwarzania tego hello użyć tooaccess hello komputera. Witaj konto powinno być **głównego** użytkownika na serwerze Linux źródłowym hello. (Używają tego konta, tylko dla instalacji wypychanej hello i aktualizacji).
3. Sprawdź ten plik/etc/hosts hello na powitania źródłowy serwer ma wpisów, które mapują hello lokalną nazwą hosta tooIP skojarzonego z wszystkich kart sieciowych w systemie Linux.
4. Zainstaluj hello najnowszych pakietów openssh, serwer openssh i biblioteki openssl na komputerze hello, które mają tooreplicate.
5. Upewnij się, że protokół Secure Shell (SSH) jest włączony i uruchomiony na porcie 22.
6. Włączanie protokołu SFTP podsystemu i hasło uwierzytelniania w pliku sshd_config hello:
  1.  Zaloguj się jako użytkownik **root**.
  2.  W hello plik/etc/ssh/Znajdź hello wiersz, który rozpoczyna się od pliku sshd_config **PasswordAuthentication**.
  3.  Usuń znaczniki komentarza hello wiersza i zmień wartość hello zbyt**tak**.
  4.  Znajdź hello wiersza, który rozpoczyna się od **podsystemu** i Usuń komentarz linii hello.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Uruchom ponownie hello **sshd** usługi.

7. Dodaj konto hello, który został utworzony w CSPSConfigtool.
    1.  Zaloguj się tooyour serwera konfiguracji.
    2.  Otwórz plik **cspsconfigtool.exe**. (Jest ona dostępna jako skrót na pulpicie hello i w folderze %ProgramData%\home\svsystems\bin hello.)
    3.  Na powitania **Zarządzanie kontami** , kliknij pozycję **Dodaj konto**.
    4.  Dodaj utworzone konto hello. 
    5.  Wprowadź poświadczenia hello, używanych po włączeniu replikacji dla komputera.
