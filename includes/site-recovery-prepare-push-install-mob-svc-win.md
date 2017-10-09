### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Przygotowanie do instalacji wypychanej na komputerze z systemem Windows

1. Upewnij się, że istnieje połączenie sieciowe między komputerem z systemem Windows hello i powitania serwera przetwarzania.
2. Tworzenie konta usługi serwera przetwarzania tego hello użyć tooaccess hello komputera. Witaj, konto musi mieć prawa administratora (lokalnego lub domeny). (Używają tego konta, tylko dla instalacji wypychanej hello i dla aktualizacji agenta).

   > [!NOTE]
   > Jeśli nie używasz konta domeny, należy wyłączyć kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello. toodisable kontroli dostępu użytkownika zdalnego, w kluczu rejestru HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System hello, Dodaj nową wartość typu DWORD: **LocalAccountTokenFilterPolicy**. Ustaw wartość hello zbyt**1**. toodo to polecenia polecenie w wierszu, uruchom następujące polecenie hello:  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. W Zaporze systemu Windows na komputerze hello ma tooprotect, wybierz opcję **Zezwalaj aplikacji lub funkcji przez zaporę**. Włącz **udostępnianie plików i drukarek** i **Instrumentacji zarządzania Windows (WMI)**. Dla komputerów, które należą do domeny tooa można skonfigurować ustawienia zapory hello za pomocą obiektu zasad grupy (GPO).

   ![Ustawienia zapory](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Dodaj konto hello, który został utworzony w CSPSConfigtool.
    1.  Zaloguj się tooyour serwera konfiguracji.
    2.  Otwórz plik **cspsconfigtool.exe**. (Jest ona dostępna jako skrót na pulpicie hello i w folderze %ProgramData%\home\svsystems\bin hello.)
    3.  Na powitania **Zarządzanie kontami** wybierz opcję **Dodaj konto**.
    4.  Dodaj utworzone konto hello.
    5.  Wprowadź poświadczenia hello, używanych po włączeniu replikacji dla komputera.
