> [!div class="op_single_selector"]
> * [Urządzenie: Node.js, usługa: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Urządzenie: Node.js, usługa: C#](../articles/iot-hub/iot-hub-csharp-node-device-management-get-started.md)
> * [Urządzeń: Usługa języka Java: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)

Zaplecza aplikacji można użyć Centrum IoT Azure w nim elementów podstawowych, takich jak [dwie urządzenia] [ lnk-devtwin] i [bezpośrednie metody][lnk-c2dmethod], tooremotely uruchomić i monitorować Akcje zarządzania urządzeniami na urządzeniach. Ten samouczek pokazuje, jak aplikacji zaplecza i aplikacji urządzenia współpracują ze sobą tooinitiate i monitorować za pomocą Centrum IoT ponowne uruchomienie urządzenia zdalnego.

Z wewnętrznym aplikacji w chmurze hello za pomocą akcji zarządzania metoda bezpośrednia tooinitiate urządzenia (takie jak ponowne uruchomienie komputera, resetowanie do ustawień fabrycznych i aktualizacji oprogramowania układowego). urządzenie Hello jest odpowiedzialny za:

* Obsługa hello metoda żądania wysyłane z Centrum IoT.
* Inicjowanie hello odpowiednich akcji urządzenia na urządzeniu hello.
* Dostarczanie aktualizacji stanu za pośrednictwem *zgłosił właściwości* tooIoT koncentratora.

Umożliwia aplikacji zaplecza w hello chmury toorun urządzenia dwie zapytania tooreport na powitania postępu działań zarządzania urządzeniami.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
