> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

Bliźniacze reprezentacje urządzeń to dokumenty JSON, które przechowują informacje o stanie urządzenia (metadane, konfiguracje i warunki). Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia, które łączy tooit.

Użyj twins urządzenia do:

* Przechowywania metadanych urządzenie z Twojego zaplecza rozwiązania.
* Raport bieżące informacje o stanie, takie jak dostępne możliwości i warunki (na przykład hello łączności metodę) z aplikacją urządzenia.
* Synchronizuj stan hello długotrwałe przepływów pracy (takich jak aktualizacje oprogramowania układowego i konfiguracji), między aplikacją urządzenia i aplikacji zaplecza.
* Zapytanie z metadanych urządzeniami, konfiguracji lub stanu.

> [!NOTE]
> Twins urządzenia są przeznaczone do synchronizacji i do wykonywania zapytań w konfiguracji urządzeń i warunki. Więcej informacje na kiedy toouse twins urządzenie znajduje się w [zrozumieć urządzenia twins][lnk-twins].

Twins urządzeń są przechowywane w Centrum IoT i zawierają:

* *tagi*, dostępny tylko dla hello rozwiązania zaplecza; metadane urządzenia
* *żądany właściwości*, można modyfikować przez rozwiązanie hello obiektów JSON wstecz zakończenia i według przez aplikację urządzenia hello; i
* *zgłoszone właściwości*, można modyfikować przez aplikację urządzenia hello i czytelna dla zaplecza rozwiązania hello obiektów JSON. Znaczniki i właściwości nie mogą zawierać tablic, ale może być zagnieżdżone obiekty.

![][img-twin]

Ponadto zaplecza rozwiązania hello mogą wysyłać zapytania oparte na wszystkich hello powyżej danych twins urządzenia.
Odwołuje się zbyt[zrozumieć twins urządzenia] [ lnk-twins] uzyskać więcej informacji o urządzeniu twins i toohello [język zapytań Centrum IoT] [ lnk-query] odwołania na potrzeby zapytań.

> [!NOTE]
> W tej chwili twins urządzenia są dostępne tylko z urządzeń łączących tooIoT Centrum przy użyciu protokołu MQTT hello. Zobacz toohello [Obsługa MQTT] [ lnk-devguide-mqtt] artykuł, aby uzyskać instrukcje dotyczące tooconvert istniejących urządzeń aplikacji toouse MQTT.

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Tworzenie aplikacji zaplecza, który dodaje *tagi* tooa dwie urządzeń i aplikacji symulowane urządzenie, która raportuje łączność kanału jako *podać właściwość* na powitania dwie urządzenia.
* Wyślij zapytanie do urządzeń z zaplecza aplikacji hello tagów i właściwości wcześniej utworzony za pomocą filtrów.

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md