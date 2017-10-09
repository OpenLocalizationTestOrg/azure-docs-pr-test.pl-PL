## <a name="build-iot-edge"></a>Tworzenie krawędzi IoT

W tym samouczku używa niestandardowych toocommunicate modułów krawędzi IoT z hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie. W związku z tym należy toobuild hello krawędzi IoT modułów z kodu źródła niestandardowego. Hello następujące sekcje opisują sposób tooinstall krawędzi IoT i kompilacji hello niestandardowego modułu IoT krawędzi.

### <a name="install-iot-edge"></a>Zainstaluj krawędzi IoT

Witaj poniższych krokach opisano sposób tooinstall hello wstępnie skompilowany oprogramowanie krawędzi IoT na powitania Intel NUC:

1. Skonfiguruj repozytoriów pakietu inteligentne hello wymagane, uruchamiając następujące polecenia na powitania Intel NUC hello:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Wprowadź `y` po hello polecenie monituje zbyt**obejmują ten kanał?**.

1. Aktualizacja Menedżera pakietów inteligentne hello, uruchamiając następujące polecenie hello:

    ```bash
    smart update
    ```

1. Zainstaluj pakiet Azure IoT krawędzi hello, uruchamiając następujące polecenie hello:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Sprawdź instalacji hello uruchomionych powitania "Hello world" przykładowe. W tym przykładzie zapisuje plik log.txT toohello wiadomość hello world co pięć sekund. Witaj następujące polecenia Uruchom powitania "Hello world" próbki:

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Ignoruj wszystkie **nieprawidłowy argument** wiadomości po zatrzymaniu hello próbki.

    Użyj następującego polecenia tooview hello zawartość pliku dziennika hello hello:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli wystąpi błąd hello "pakiet nie zawiera util-linux deweloperów", spróbuj wykonać ponowny rozruch hello Intel NUC.
