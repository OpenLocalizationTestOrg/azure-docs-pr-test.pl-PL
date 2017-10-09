# <a name="secure-your-iot-deployment"></a>Zabezpieczanie wdrożenia IoT
Ten artykuł zawiera hello następnego poziomu szczegółów dla zabezpieczanie hello infrastruktury opartej na usłudze Azure IoT Internetu rzeczy (IoT). Łączy tooimplementation poziomu szczegółowe informacje dotyczące konfigurowania i wdrażania poszczególnych składników. Umożliwia także porównania i dostępnych wyborów między różnymi metodami konkurencyjnych.

Zabezpieczanie hello Azure IoT wdrożenia można podzielić na następujące trzy obszary zabezpieczeń hello:

* **Zasady zabezpieczeń urządzeń**: Zabezpieczanie urządzenia IoT hello, gdy jest wdrożony w hello wild.
* **Zabezpieczenia połączeń**: zapewnienie wszystkie dane przesyłane między hello urządzenia IoT i Centrum IoT jest poufny i odporne.
* **Chmury zabezpieczeń**: zapewnienie środków toosecure danych, podczas gdy przechodzi przez i są przechowywane w chmurze hello.

![Trzy obszary zabezpieczeń][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Zabezpieczenia, inicjowanie obsługi administracyjnej urządzeń i uwierzytelniania
Witaj pakiet IoT Azure zabezpiecza urządzenia IoT przy hello następujących dwóch metod:

* Zapewniając klucz unikatową tożsamość (tokeny zabezpieczające) dla każdego urządzenia, które mogą być używane przez hello toocommunicate urządzenia z hello Centrum IoT.
* Za pomocą na urządzeniach [certyfikatu X.509] [ lnk-x509] i klucza prywatnego, co oznacza, że tooauthenticate hello urządzenia toohello Centrum IoT. Ta metoda uwierzytelniania zapewnia, że hello klucza prywatnego na urządzeniu hello nie jest znany poza urządzenia hello w dowolnym momencie zapewnia wyższy poziom zabezpieczeń.

Metoda tokenu zabezpieczeń Hello zapewnia uwierzytelnianie dla każdego wywołania wprowadzone przez tooIoT urządzenia hello Centrum kojarząc hello tooeach klucza symetrycznego wywołania. Uwierzytelnianie oparte na X.509 w warstwie fizycznej hello jako część ustanawianie połączenia TLS hello pozwala na uwierzytelnianie urządzenia IoT. metody opartej na tokenie zabezpieczeń Hello może służyć bez uwierzytelniania hello X.509, który jest mniej bezpieczne wzorca. Hello wybór między Witaj dwie metody jest głównie definiowane przez hello jak bezpieczne uwierzytelnianie urządzenia musi toobe i dostępności bezpieczny magazyn na urządzeniu hello (toostore hello klucza prywatnego bezpieczny).

## <a name="iot-hub-security-tokens"></a>Tokeny zabezpieczeń usługi IoT Hub
Centrum IoT używa zabezpieczeń tokeny tooauthenticate urządzeń i usług tooavoid wysyłania kluczy hello sieci. Ponadto tokeny zabezpieczające są ograniczone w czas ważności i zakres. Usługa Azure IoT zestawy SDK automatycznie generować tokeny bez konieczności żadnej specjalnej konfiguracji. Niektóre scenariusze, jednak wymagają hello toogenerate użytkownika i korzystać bezpośrednio tokenów zabezpieczających. Należą do bezpośredniego użycia hello powierzchni MQTT AMQP i HTTP hello lub hello implementacji wzorca usługi tokenu hello.

Więcej informacji na temat struktury hello tokenu zabezpieczającego hello i jego użycia można znaleźć w hello następujące artykuły:

* [Struktura tokenu zabezpieczeń][lnk-security-tokens]
* [Tokeny sygnatury dostępu Współdzielonego jako urządzenie][lnk-sas-tokens]

Każdy Centrum IoT ma [rejestru tożsamości] [ lnk-identity-registry] które może być używane toocreate zasobów na urządzenie w hello usługi, takie jak kolejki, która zawiera locie wiadomości chmury do urządzenia i tooallow toohello dostępu punkty końcowe skierowane do urządzenia. Hello rejestru tożsamości Centrum IoT zapewnia bezpieczne przechowywanie tożsamości urządzenia i kluczy zabezpieczeń dla rozwiązania. Osoby lub grupy tożsamości urządzenia można dodać tooan Zezwalaj listy lub listę zablokowanych umożliwiające pełną kontrolę nad uzyskiwania dostępu do urządzenia. Witaj poniższe artykuły zawierają więcej szczegółowych informacji o strukturze hello hello rejestru tożsamości i obsługiwane operacje.

[Centrum IoT obsługuje protokoły, takie jak MQTT, AMQP i HTTP][lnk-protocols]. Każdy z tych protokołów inaczej Użyj tokeny zabezpieczające z tooIoT urządzenia IoT hello Centrum:

* AMQP: SASL zwykłe i opartego na oświadczeniach AMQP zabezpieczeń ({policyName}@sas.root. { iothubName} w przypadku hello tokenów z poziomu Centrum IoT; {deviceId} w przypadku tokeny zakres urządzenia).
* MQTT: POŁĄCZ pakiet używa {deviceId} jako hello {ClientId}, {IoThubhostname} / {deviceId} w hello **Username** pola i sygnatury dostępu Współdzielonego token w hello **hasło** pola.
* HTTP: Nieprawidłowy token jest w nagłówku żądania autoryzacji hello.

Centrum IoT tożsamości rejestru można poświadczenia zabezpieczeń używane tooconfigure na urządzenia i kontrola dostępu. Jednak jeśli rozwiązania IoT ma już znaczącą inwestycję w [schemat rejestru i/lub uwierzytelnianie tożsamości urządzeń niestandardowych][lnk-custom-auth], może być zintegrowany istniejącej infrastruktury z Centrum IoT Tworząc usługi tokenu.

### <a name="x509-certificate-based-device-authentication"></a>Uwierzytelnianie urządzenia na podstawie certyfikatu X.509
Witaj użycie [oparta na urządzeniach certyfikatu X.509] [ lnk-use-x509] i jego skojarzony prywatnych i publicznych pary kluczy umożliwia dodatkowe uwierzytelnianie w warstwie fizycznej hello. klucz prywatny Hello jest bezpiecznie przechowywana w hello urządzenia i nie jest wykrywalny poza hello urządzenia. Certyfikat X.509 Hello zawiera informacje o urządzeniu hello, takich jak identyfikator urządzenia i inne szczegóły organizacji. Podpis certyfikatu hello jest generowany przy użyciu klucza prywatnego hello.

Przepływ inicjowania obsługi administracyjnej urządzeniu wysokiego poziomu:

* Kojarzenie identyfikator tooa urządzenie fizyczne — tożsamości urządzenia i/lub urządzeń toohello skojarzony certyfikat X.509 podczas produkcji lub oddanie urządzenia.
* Utwórz tożsamość odpowiadającego mu wpisu w Centrum IoT — tożsamości urządzenia i informacje o urządzeniu skojarzony w hello rejestru tożsamości Centrum IoT.
* Bezpiecznie przechowywać odcisk palca certyfikatu X.509 w rejestrze tożsamości Centrum IoT.

### <a name="root-certificate-on-device"></a>Certyfikat główny na urządzeniu
Podczas ustanawiania bezpiecznego połączenia TLS z Centrum IoT, urządzenia IoT hello uwierzytelnia Centrum IoT użycie certyfikatu głównego, który jest częścią urządzenia hello zestawu SDK. Dla klienta hello C zestawu SDK hello certyfikat znajduje się w folderze hello "\\c\\certyfikaty" w katalogu głównym hello hello repozytorium. Chociaż te certyfikaty główne są długotrwałe, nadal mogą wygaśnięcia lub zostać odwołane. Jeśli nie istnieje sposób aktualizowania hello certyfikatu na urządzeniu hello hello się, że urządzenie może nie być w stanie połączyć z toosubsequently toohello Centrum IoT (lub inne usługi w chmurze). Posiadanie certyfikatu głównego hello tooupdate oznacza, że po wdrożeniu urządzenia IoT hello skutecznie zmniejszyć to zagrożenie.

## <a name="securing-hello-connection"></a>Zabezpieczanie hello połączenia
Połączenie z Internetem hello urządzenia IoT i Centrum IoT jest zabezpieczone przy użyciu hello standard zabezpieczeń TLS (Transport Layer). Usługa Azure IoT obsługuje [protokołu TLS 1.2][lnk-tls12], protokołu TLS 1.1 i TLS 1.0, w tej kolejności. Obsługa protokołu TLS 1.0 jest zapewniana tylko zgodności z poprzednimi wersjami. Ponieważ zapewnia najwyższy poziom zabezpieczeń hello zaleca się toouse protokołu TLS 1.2.

Pakiet Azure IoT obsługuje hello następujące mechanizmy szyfrowania w podanej kolejności.

| Mechanizmy szyfrowania | długość |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 secp384r1 ECDH (0xc028) (korektora FS 7680 bits RSA) |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 secp256r1 ECDH (0xc027) (korektora FS 3072 bits RSA) |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (korektora FS 7680 bits RSA) |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (korektora FS 3072 bits RSA) |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Zabezpieczanie hello chmury
Centrum IoT Azure umożliwia określenie [zasady kontroli dostępu w] [ lnk-protocols] dla każdego klucza zabezpieczeń. Używa ona hello następującego zestawu uprawnień toogrant dostępu tooeach punkty końcowe Centrum IoT. Uprawnienia ograniczyć tooan dostępu hello, Centrum IoT oparta na funkcjach.

* **RegistryRead**. Przyznaje dostęp do odczytu toohello tożsamości rejestru. Aby uzyskać więcej informacji, zobacz [rejestru tożsamości][lnk-identity-registry].
* **RegistryReadWrite**. Udziela dostępu odczytu i zapisu toohello rejestrze tożsamości. Aby uzyskać więcej informacji, zobacz [rejestru tożsamości][lnk-identity-registry].
* **ServiceConnect**. Przyznaje dostęp komunikacji usługi połączonej toocloud i monitorowania punktów końcowych. Na przykład, domyślnie przyzna uprawnienie tooback-end chmury usługi tooreceive urządzenia do chmury wiadomości, wysyłanie komunikatów chmury do urządzenia i pobierać hello odpowiedniego potwierdzeń dostarczenia.
* **DeviceConnect**. Udziela dostępu do punktów końcowych toodevice uwzględniającym. Na przykład przyznaje uprawnienia do toosend urządzenia do chmury wiadomości i odbieranie komunikatów chmury do urządzenia. To uprawnienie jest używany przez urządzenia.

Istnieją dwa sposoby tooobtain **DeviceConnect** uprawnienia z Centrum IoT z [tokeny zabezpieczające][lnk-sas-tokens]: przy użyciu klucza tożsamość urządzenia lub klucza dostępu współdzielonego. Ponadto jest ważne toonote uwidocznionego wszystkie funkcje dostępny z urządzenia zgodnie z projektem w punktach końcowych z prefiksem `/devices/{deviceId}`.

[Składniki usługi można generować tylko tokeny zabezpieczające] [ lnk-service-tokens] przy użyciu udostępnionych przyznanie odpowiednich uprawnień hello zasad dostępu.

Centrum IoT Azure i innych usług, które mogą być częścią rozwiązania hello Zezwalaj na zarządzanie użytkownikami przy użyciu hello Azure Active Directory.

Dane pozyskanych przez Centrum IoT Azure mogą być używane w wielu różnych usług, takich jak usługi Azure Stream Analytics i magazynu obiektów blob platformy Azure. Usługi te umożliwiają dostęp do funkcji zarządzania. Więcej informacji na temat tych usług i dostępne opcje poniżej:

* [Usługa Azure DocumentDB][lnk-docdb]: skalowalne, pełni indeksowana bazy danych usługi częściowo ustrukturyzowanych danych zarządza metadanych dla urządzeń hello udostępnieniem, takich jak atrybuty, konfiguracji i właściwości zabezpieczeń. Usługa DocumentDB oferuje przetwarzanie wysokiej wydajności i wysokiej przepustowości, niezależny od schematu indeksowania danych i interfejs zaawansowanych zapytań SQL.
* [Usługa Azure Stream Analytics][lnk-asa]: strumienia w czasie rzeczywistym przetwarzania w chmurze hello, która umożliwia toorapidly możesz opracowywania i wdrażania analytics niskokosztowych rozwiązań toouncover w czasie rzeczywistym wgląd w dane dotyczące urządzeń, czujników, Infrastruktura i aplikacje. Hello danych z tej usługi pełni zarządzane można skalować tooany woluminów jednocześnie uzyskanie wysokiej przepływności, małych opóźnień i elastyczność.
* [Usługa Azure App Service][lnk-appservices]: cloud platform toobuild zaawansowanych sieci web i aplikacji mobilnych, łączących toodata w dowolnym miejscu; w chmurze hello lub lokalnie. Twórz interesujące aplikacje mobilne dla systemów iOS, Android i Windows. Integracja z oprogramowanie jako usługa (SaaS) i enterprise aplikacji za pomocą toodozens poza pole łączności z usługami w chmurze i aplikacje przedsiębiorstwa. Kod w języku ulubionych i IDE aplikacje sieci web toobuild (.NET, Node.js, PHP, Python lub Java) i interfejsów API szybciej niż kiedykolwiek wcześniej.
* [Logic Apps][lnk-logicapps]: funkcja Logic Apps hello Azure App Service ułatwia integrują się z istniejącymi systemami — biznesowych IoT rozwiązania tooyour i automatyzację procesów przepływu pracy. Logic Apps umożliwia deweloperom przepływy pracy toodesign uruchamianych wyzwalaczami i wykonujących serie kroków, reguł i akcji, które toointegrate łączniki zaawansowanych za pomocą procesów biznesowych. Logic Apps zapewnia łączność poza pole tooa przeważająca ekosystemu SaaS, oparte na chmurze i lokalnych aplikacji.
* [Magazyn obiektów blob platformy Azure][lnk-blob]: magazynu w chmurze niezawodnych i ekonomiczny dla danych hello, że urządzenia wysyłać toohello chmury.

## <a name="conclusion"></a>Podsumowanie
Ten artykuł zawiera omówienie wdrożenia poziomu szczegółów dotyczących projektowania i wdrażania infrastruktury IoT przy użyciu usługi Azure IoT. Konfigurowanie każdego składnika toobe bezpiecznego jest klucz do zabezpieczania hello całej infrastruktury IoT. dostępne w usłudze Azure IoT decyzji projektowych Hello Podaj pewnego poziomu elastyczność i możliwość wyboru; Jednak każdy wybór może mieć wpływ na bezpieczeństwo. Zaleca się każdy z tych opcji oceniane za pośrednictwem na podstawie oceny ryzyka/kosztów.

[img-overview]: media/iot-secure-your-deployment/overview.png

[lnk-security-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../articles/iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-use-x509]: ../articles/iot-hub/iot-hub-devguide-security.md
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../articles/iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/
