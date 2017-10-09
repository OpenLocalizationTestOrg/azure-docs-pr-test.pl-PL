## <a name="configure-hello-nodejs-simulated-device"></a>Skonfiguruj hello Node.js symulowane urządzenie
1. Na powitania zdalnego pulpitu nawigacyjnego monitorowania, kliknij przycisk **+ Dodaj urządzenie** , a następnie dodaj *urządzeń niestandardowych*. Zanotuj hello Centrum IoT nazwy hosta, identyfikator urządzenia i klucz urządzenia. Należy je później w tym samouczku podczas przygotowywania hello remote_monitoring.js urządzenia klienta aplikacji.
2. Upewnij się, że wersji środowiska Node.js 0.12.x lub nowszy jest zainstalowany na komputerze deweloperskim. Uruchom `node --version` w wierszu polecenia lub w wersji hello toocheck powłoki. Aby dowiedzieć się, jak za pomocą pakietu Menedżera tooinstall Node.js w systemie Linux, zobacz [instalowanie Node.js za pomocą Menedżera pakietów][node-linux].
3. Po zainstalowaniu programu Node.js w klonowania hello najnowszą wersję hello [azure iot-sdk węzłami] [ lnk-github-repo] komputerze deweloperskim tooyour repozytorium. Zawsze używaj hello **wzorca** gałęzi do najnowszej wersji hello hello bibliotek i przykładów.
4. Z kopii lokalnej hello [azure iot-sdk węzłami] [ lnk-github-repo] repozytorium, hello kopiowania następujące dwa pliki z hello węzła/urządzenia/przykłady tooan pustego folderu na komputerze deweloperskim:
   
   * Packages.JSON
   * remote_monitoring.js
5. Otwórz plik remote_monitoring.js hello i wyszukaj powitania po definicji zmiennej:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Zastąp **[parametry połączenia Centrum IoT urządzenia]** z parametrów połączenia urządzenia. Użyj hello wartości dla nazwy hosta Centrum IoT, identyfikator urządzenia i klucz urządzenia, który należy zanotować w kroku 1. Ciąg połączenia urządzenia ma hello następującego formatu:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Jeśli nazwa hosta z Centrum IoT jest **contoso** i identyfikator urządzenia jest **mydevice**, ciąg połączenia prawdopodobnie hello następującego fragmentu:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Zapisz plik hello. Uruchom następujące polecenia w powłoce lub wiersza polecenia w folderze hello, który zawiera te pliki tooinstall hello niezbędne pakiety hello, a następnie uruchom hello przykładowej aplikacji:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Obserwować dynamiczne telemetrii w akcji
pulpit nawigacyjny Hello zawiera hello temperatury i wilgotności dane telemetryczne z istniejących urządzeń symulowane hello:

![Witaj domyślnego pulpitu nawigacyjnego][image1]

W przypadku wybrania hello Node.js symulowane urządzenie uruchomienia w poprzedniej sekcji hello Zobacz temperatury, wilgotności i dane telemetryczne temperatury zewnętrznych:

![Dodaj pulpit nawigacyjny toohello temperatury zewnętrznych][image2]

rozwiązanie monitorowania zdalnego Hello automatycznie wykrywa typ telemetrii dodatkowe temperatury zewnętrznych hello i dodaje go wykresu toohello na powitania pulpitu nawigacyjnego.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png