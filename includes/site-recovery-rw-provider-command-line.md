UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ InstallDrive <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < toobe adresów IP używanych do transferu danych] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Parametry:

* /ServerMode: obowiązkowy. Określa, czy oba serwery konfiguracji i procesu hello powinien być zainstalowany lub hello tylko serwer przetwarzania. Wartości wejściowe: CS, PS.
* InstallLocation: obowiązkowy. folder Hello w hello, które składniki są zainstalowane.
* /MySQLCredsFilePath. Obowiązkowy. Ścieżka pliku Hello, w których hello MySQL są przechowywane poświadczenia serwera. Witaj plik powinien być w następującym formacie:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. Obowiązkowy. Lokalizacja pliku poświadczeń magazynu hello Hello
* /EnvType. Obowiązkowy. Typ Hello instalacji. Wartości: VMware, NonVMware
* / PSIP i /CSIP. Obowiązkowy. adres IP Hello powitania serwera przetwarzania i serwer konfiguracji.
* /PassphraseFilePath. Obowiązkowy. Lokalizacja Hello hello hasło pliku.
* /BypassProxy. Opcjonalny. Określa, że ten serwer konfiguracji hello łączy tooAzure bez serwera proxy.
* /ProxySettingsFilePath. Opcjonalny. Ustawienia serwera proxy (hello domyślny serwer proxy wymaga uwierzytelniania lub niestandardowego serwera proxy). Witaj plik powinien być w następującym formacie:
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. Opcjonalny. numer portu Hello dane replikacji.
* SkipSpaceCheck. Opcjonalny. Pomiń sprawdzanie miejsca dla pamięci podręcznej.
* AcceptThirdpartyEULA. Obowiązkowy. Akceptuje Umowa licencyjna EULA hello innych firm.
* ShowThirdpartyEULA. Obowiązkowy. Wyświetla umowę licencyjną innej firmy. Jeśli zostanie podany w danych wejściowych, wszystkie inne parametry są ignorowane.
