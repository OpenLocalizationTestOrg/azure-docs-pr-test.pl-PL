> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a>Wprowadzenie

W [Rozpoczynanie pracy z Centrum IoT urządzenia twins][lnk-twin-tutorial], wiesz, jak metadanych urządzenia tooset z powrotem rozwiązania kończyć się przy użyciu *tagi*, raport warunków urządzenia z aplikacjami urządzenia przy użyciu *zgłosił właściwości*oraz badanie tych informacji przy użyciu języka przypominającego SQL.

Z tego samouczka, dowiesz się, jak toouse Witaj dwie urządzenia hello *żądanego właściwości* wraz z *zgłosił właściwości*, tooremotely Konfigurowanie aplikacji dla urządzeń. W szczególności w tym samouczku przedstawiono sposób zgłaszania dwie urządzenia oraz odpowiednie właściwości Włącz konfigurację wieloetapowych aplikację dla urządzeń i hello widoczność toohello zaplecza rozwiązania stanu hello tej operacji dla wszystkich urządzeń. Można znaleźć więcej informacji na temat roli hello konfiguracji urządzeń w [omówienie zarządzania urządzeniami z Centrum IoT][lnk-dm-overview].

Na wysokim poziomie za pomocą urządzenia twins umożliwia hello rozwiązania zaplecza toospecify hello odpowiednią konfigurację hello zarządzanych urządzeń, zamiast wysyłać określonych poleceń. To powoduje przełączenie urządzenia hello odpowiedzialnym za konfigurowanie hello najlepsze sposób tooupdate jego konfiguracji (bardzo ważne w scenariuszach IoT, których warunki określonego urządzenia wpływać na powitania możliwości tooimmediately wykonania określonych poleceń), podczas raportowania stale toohello zaplecze rozwiązania hello bieżący stan i potencjalne błędy hello procesu aktualizacji. Ten wzorzec jest toohello instrumentalnego zarządzanie dużymi zbiorami urządzeń, jak umożliwia hello rozwiązania zaplecza toohave pełny wgląd stanu hello hello procesu konfiguracji na wszystkich urządzeniach.

> [!NOTE]
> W scenariuszach, w którym urządzenia są kontrolowane w sposób większej liczby interaktywnych (Włącz wentylator z aplikacji kontrolowane przez użytkownika), należy rozważyć użycie [bezpośrednie metody][lnk-methods].
> 
> 

W tym samouczku zmiany zaplecza rozwiązania hello hello telemetrii konfiguracji urządzenia docelowego i, w wyniku którego hello aplikacji urządzenia następuje tooapply wieloetapowych procesu konfiguracji aktualizacji (na przykład oprogramowania modułu ponownego uruchomienia komputera, który to wymaganie Samouczek symuluje z opóźnieniem prosty).

zaplecza rozwiązania Hello przechowywana jest Konfiguracja hello hello urządzenia dwie właściwości żądaną w hello w następujący sposób:

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> Ponieważ konfiguracje mogą zostać obiektu złożonego, zazwyczaj są przypisane unikatowe identyfikatory (skróty lub [identyfikatorów GUID][lnk-guid]) toosimplify ich porównania.
> 
> 

Witaj aplikacji urządzenia raporty bieżącej konfiguracji dublowania hello wymaganą właściwość **telemetryConfig** w hello zgłoszonych właściwości:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

Należy zwrócić uwagę na sposób zgłaszania hello **telemetryConfig** ma dodatkowe właściwości **stanu**, używane tooreport hello stanu procesu aktualizacji konfiguracji hello.

Po odebraniu nowego wymaganą konfiguracją aplikacji urządzenia hello raportów oczekujących konfiguracji zmieniając hello informacji:

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

Następnie w późniejszym czasie, hello urządzenia aplikacji będzie zgłaszać hello powodzenie lub niepowodzenie tej operacji, aktualizując hello powyżej właściwości.
Należy zwrócić uwagę, jak zaplecza rozwiązania hello jest w stanie, w dowolnym momencie, stan hello tooquery hello proces konfiguracji wszystkich urządzeń hello.

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Tworzenie aplikacji symulowane urządzenie, który odbiera aktualizacje konfiguracji z zaplecza rozwiązania hello, a następnie raportuje wiele aktualizacji jako *zgłosił właściwości* konfiguracji hello zaktualizować procesu.
* Tworzenie zaplecza aplikacji czy aktualizacje hello wymaganą konfiguracją urządzenia, a następnie zapytania hello proces aktualizacji konfiguracji.

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
