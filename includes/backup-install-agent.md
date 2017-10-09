## <a name="download-install-and-register-hello-azure-backup-agent"></a>Pobieranie, instalowanie i rejestrowanie agenta usługi Kopia zapasowa Azure hello
Po utworzeniu magazynu usługi Kopia zapasowa Azure hello, powinien być zainstalowany agent na wszystkich maszynach systemu Windows (Windows Server, klienta systemu Windows, serwer System Center Data Protection Manager lub serwer kopii zapasowej Azure machine), które umożliwia wykonywanie kopii zapasowych danych i aplikacji tooAzure.

1. Zaloguj się toohello [portalu zarządzania](https://manage.windowsazure.com/)
2. Kliknij przycisk **usług odzyskiwania**, a następnie wybierz pozycję hello magazynu kopii zapasowych, które mają tooregister z serwerem. zostanie wyświetlona strona Szybki Start powitania dla tego magazynu kopii zapasowych.
   
    ![Szybki start](./media/backup-install-agent/quickstart.png)
3. Na stronie Szybki Start powitania kliknij hello **klienta dla systemu Windows Server lub System Center Data Protection Manager lub Windows** opcję w obszarze **Pobierz agenta**. Kliknij przycisk **zapisać** toocopy on toohello komputera lokalnego.
   
    ![Zapisz agenta](./media/backup-install-agent/agent.png)
4. Po zainstalowaniu agenta powitania kliknij dwukrotnie MARSAgentInstaller.exe toolaunch hello instalacji agenta usługi Kopia zapasowa Azure hello. Wybierz folder instalacji hello i pliki tymczasowe folderu wymagane dla hello agenta. Określona lokalizacja pamięci podręcznej Hello musi mieć wolnego miejsca, czyli co najmniej 5% hello dane kopii zapasowej.
5. Jeśli używasz toohello tooconnect serwera proxy internet w hello **konfiguracji serwera Proxy** ekranu, wprowadź szczegóły serwera proxy hello. Jeśli korzystasz z uwierzytelnionego serwera proxy, wprowadź szczegóły nazwy i hasła użytkownika hello na tym ekranie.
6. agent usługi Kopia zapasowa Azure Hello instaluje .NET Framework 4.5 i programu Windows PowerShell (Jeśli nie jest dostępna) toocomplete hello instalację.
7. Po zainstalowaniu agenta powitania kliknij hello **kontynuować tooRegistration** toocontinue przycisk z hello przepływu pracy.
   
   ![Zarejestruj subskrypcję](./media/backup-install-agent/register.png)
8. Na ekranie poświadczenia magazynu hello Przeglądaj plik poświadczeń magazynu wybierz hello tooand, który został wcześniej pobrany.
   
    ![Poświadczenia magazynu](./media/backup-install-agent/vc.png)
   
    Plik poświadczeń magazynu Hello jest prawidłowa tylko dla 48 godzin (po jej pobraniu, z portalu hello). W razie wystąpienia błędu w tym ekranie (np. "poświadczenia magazynu utracił ważność podany plik"), toohello logowania portalu Azure i poświadczenia magazynu hello pobierania pliku ponownie.
   
    Upewnij się, że ten plik poświadczeń magazynu hello jest dostępna w lokalizacji, którą można uzyskać, sprawdzając hello instalacji aplikacji. Jeśli wystąpią błędy powiązane, poświadczenia magazynu hello kopii pliku tooa lokalizacji tymczasowej na tej maszynie i ponów próbę wykonania operacji hello.
   
    Jeśli wystąpi błąd poświadczeń magazynu nieprawidłowe (np. "udostępniono nieprawidłowe poświadczenia magazynu") hello plik jest uszkodzony lub jest nie ma hello najnowszych poświadczeń skojarzonych z hello usługą odzyskiwania. Ponów operację powitania po pobraniu nowego pliku poświadczeń magazynu z portalu hello. Ten błąd zazwyczaj występuje Jeśli hello użytkownik kliknie hello **poświadczenia magazynu pobierania** opcję hello portalu Azure, szybkie naciśnięcie. W takim przypadku tylko hello drugi plik poświadczeń magazynu jest nieprawidłowa.
9. W hello **ustawienie szyfrowania** ekranu, można wygenerować hasło lub podać hasło (co najmniej 16 znaków). Należy pamiętać, toosave hello hasła w bezpiecznym miejscu.
   
    ![Szyfrowanie](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Jeśli hello zgubienia lub zapomnienia hasła; Microsoft nie może pomóc w odzyskiwaniu danych kopii zapasowej hello. użytkownik końcowy Hello jest właścicielem hello hasło szyfrowania i Microsoft nie ma wgląd w hello hasło używane przez użytkownika końcowego hello. Zapisz plik hello w bezpiecznej lokalizacji, zgodnie z wymaganiami podczas operacji odzyskiwania.
   > 
   > 
10. Po kliknięciu hello **Zakończ** przycisku, hello maszyna zarejestrowana pomyślnie toohello magazynu i są teraz gotowe toostart tworzenie kopii zapasowej tooMicrosoft Azure.
11. Podczas korzystania z autonomicznej kopia zapasowa Microsoft Azure można zmodyfikować ustawienia hello określony podczas rejestracji hello w przepływie pracy, klikając hello **Zmień właściwości** opcji w przystawki programu mmc usługi Kopia zapasowa Azure hello w.
    
    ![Zmień właściwości](./media/backup-install-agent/change.png)
    
    Alternatywnie, korzystając z programu Data Protection Manager, można zmodyfikować ustawienia hello określony podczas przepływu pracy rejestracji hello klikając hello **Konfiguruj** opcję, wybierając **Online** w obszarze hello **Zarządzania** kartę.
    
    ![Konfigurowanie usługi Azure Backup](./media/backup-install-agent/configure.png)

