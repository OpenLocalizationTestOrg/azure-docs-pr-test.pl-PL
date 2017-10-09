## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>Przy użyciu tooauthenticate poświadczeń magazynu z hello usługi Kopia zapasowa Azure
Witaj lokalnego serwera (Windows klienta lub serwera systemu Windows Server lub programu Data Protection Manager) musi toobe, aby go może tworzyć kopie zapasowe danych tooAzure uwierzytelnienie z magazynu kopii zapasowych. Hello uwierzytelnianie odbywa się przy użyciu "magazynu poświadczeń". pojęcie Hello poświadczenia magazynu to podobne pojęcia toohello "ustawień publikowania" pliku, który jest używany w programie Azure PowerShell.

### <a name="what-is-hello-vault-credential-file"></a>Co to jest plik poświadczeń magazynu hello?
Plik poświadczeń magazynu Hello jest certyfikatem generowane przez portal powitania dla każdego magazynu kopii zapasowych. Hello portal przekazuje następnie hello toohello klucza publicznego usługi kontroli dostępu (ACS). Hello klucza prywatnego certyfikatu hello stają się dostępne toohello użytkownika jako część przepływu pracy hello, które jest podawana jako dane wejściowe w hello maszyny rejestracji w przepływie pracy. To jest uwierzytelniany hello maszyny toosend dane kopii zapasowej tooan zidentyfikowane magazynu w hello usługi Kopia zapasowa Azure.

poświadczenia magazynu Hello jest używany tylko podczas rejestracji hello w przepływie pracy. Jest tooensure odpowiedzialność hello użytkownika, który hello pliku nie zostaną ujawnione poświadczenia magazynu. Jeśli znajduje się w ręce hello dowolny złośliwy użytkownik, plik poświadczeń magazynu hello może być używane tooregister inne maszyny przed hello tego samego magazynu. Jednak ponieważ hello dane kopii zapasowej jest zaszyfrowany przy użyciu hasła, który należy toohello klienta, dane kopii zapasowej nie zostaną ujawnione. toomitigate tego problemu, poświadczenia magazynu ustawiono tooexpire w 48hrs. Poświadczenia magazynu hello magazynu kopii zapasowych można pobrać dowolną liczbę razy —, lecz tylko hello najnowszy plik poświadczeń magazynu jest stosowany podczas rejestracji hello w przepływie pracy.

### <a name="download-hello-vault-credential-file"></a>Pobierz plik poświadczeń magazynu hello
Plik poświadczeń magazynu Hello jest pobierana za pośrednictwem bezpiecznego kanału z hello portalu Azure. Witaj usługi Azure Backup nie rozpoznaje hello klucza prywatnego certyfikatu hello i w portalu hello lub usługi hello hello klucz prywatny nie jest trwały. Użyj hello następujące kroki toodownload hello magazynu poświadczeń pliku tooa komputera lokalnego.

1. Zaloguj się toohello [portalu zarządzania](https://manage.windowsazure.com/)
2. Polecenie **usług odzyskiwania** w okienku nawigacji po lewej stronie powitania i wybierz hello magazynu kopii zapasowych, które zostały utworzone. Polecenie hello chmury ikona tooget toohello Szybki Start widoku hello magazynu kopii zapasowych.
   
   ![Szybki przegląd](./media/backup-download-credentials/quickview.png)
3. Na stronie Szybki Start powitania kliknij **poświadczenia magazynu pobierania**. Hello portal generuje plik poświadczeń magazynu hello, który ma zostać udostępnione do pobrania.
   
   ![Do pobrania](./media/backup-download-credentials/downloadvc.png)
4. Hello portal wygeneruje poświadczenie magazynu przy użyciu kombinacji nazwy magazynu hello i hello bieżącą datę. Kliknij przycisk **zapisać** toodownload hello magazynu poświadczeń toohello lokalnego konta pobiera folderu lub wybierz Zapisz jako z hello zapisać menu toospecify lokalizację hello poświadczenia magazynu.

### <a name="note"></a>Uwaga
* Upewnij się, że poświadczenia magazynu hello został zapisany w lokalizacji, w których może uzyskać dostęp z komputera. Jeśli jest on przechowywany w udziale plików/SMB, sprawdź, czy uprawnienia dostępu hello.
* Plik poświadczeń magazynu Hello jest używany tylko podczas rejestracji hello w przepływie pracy.
* Plik poświadczeń magazynu Hello wygasa po 48hrs i może zostać pobrany z portalu hello.
* Zobacz toohello kopia zapasowa Azure [— często zadawane pytania](../articles/backup/backup-azure-backup-faq.md) wszelkie pytania na powitania przepływu pracy.

