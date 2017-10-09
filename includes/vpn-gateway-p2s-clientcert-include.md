Każdy komputer kliencki, który łączy tooa sieci wirtualnej za pomocą punkt-lokacja musi mieć zainstalowany certyfikat klienta. certyfikat klienta na powitania jest generowany na podstawie certyfikatu głównego hello i zainstalowane na każdym komputerze klienckim. Jeśli nie jest zainstalowany prawidłowy certyfikat klienta i hello klient próbuje toohello tooconnect sieci wirtualnej, uwierzytelnianie nie powiedzie się.

Możesz wygenerować unikatowy certyfikat dla każdego klienta, lub można użyć hello sam certyfikatu dla wielu klientów. Witaj korzyści toogenerating unikatowych klientów certyfikatów jest hello możliwości toorevoke jeden certyfikat. W przeciwnym razie, jeśli wielu klientów przy użyciu hello tego samego certyfikatu klienta, należy toorevoke, masz toogenerate i zainstalować nowe certyfikaty dla wszystkich hello klientów, którzy używają tooauthenticate tego certyfikatu.

Można wygenerować certyfikaty klienta przy użyciu hello następujące metody:

- **Certyfikat przedsiębiorstwa:**

  - Jeśli korzystasz z rozwiązania certyfikatu przedsiębiorstwa, wygenerować certyfikat klienta w formacie wartości nazwy wspólnej hello "name@yourdomain.com", zamiast format "nazwa domeny\nazwa" hello.
  - Upewnij się, że certyfikat klienta na powitania jest oparty na szablonie certyfikatu "User" hello, takim jak pierwszy element listy użyj hello hello "Uwierzytelnienie klienta", zamiast inteligentne Logowanie karty itp. Zaznacz opcję certyfikat z hello przez dwukrotne kliknięcie powitania klienta certyfikatu i wyświetlanie **szczegóły > ulepszone użycie klucza**.

- **Certyfikat główny z podpisem własnym:** jest ważne, należy wykonać kroki hello w jednym z artykułów certyfikatu hello P2S poniżej. W przeciwnym razie hello certyfikaty klienta, którą utworzysz nie będzie zgodny z połączeń P2S i klientów wystąpi błąd podczas próby tooconnect. kroki Hello w jednym z hello następujące artykuły wygenerować certyfikat klienta zgodne: 

  * [Windows 10 PowerShell instrukcjami](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): instrukcje te wymagają certyfikatów toogenerate systemu Windows 10 i programu PowerShell. Witaj certyfikatów, które są generowane można zainstalować na dowolnym obsługiwany klient P2S.
  * [Instrukcje MakeCert](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): MakeCert Użyj, jeśli nie mają dostępu do systemu Windows 10 tooa toouse toogenerate certyfikaty. Przestarzałe MakeCert, ale nadal można użyć certyfikatów toogenerate MakeCert. Witaj certyfikatów, które są generowane można zainstalować na dowolnym obsługiwany klient P2S.

  Podczas generowania certyfikatu klienta z podpisem głównego certyfikatu przy użyciu hello poprzedzających instrukcji, został automatycznie zainstalowany na komputerze hello użytą toogenerate go. Jeśli chcesz tooinstall certyfikat klienta na innym komputerze klienckim, należy tooexport go w formie pliku PFX, wraz z hello całego łańcucha certyfikatów. Spowoduje to utworzenie pliku PFX, zawierający informacje certyfikatu głównego hello jest wymagany na potrzeby uwierzytelniania powitania klienta toosuccessfully. Dla czynności tooexport certyfikatu, zobacz [certyfikaty — eksportowanie certyfikatu klienta](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientexport).
