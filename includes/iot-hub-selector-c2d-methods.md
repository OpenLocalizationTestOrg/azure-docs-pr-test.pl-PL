> [!div class="op_single_selector"]
> * [Node.js](../articles/iot-hub/iot-hub-node-node-direct-methods.md)
> * [C#/node.js](../articles/iot-hub/iot-hub-csharp-node-direct-methods.md)
> * [C#](../articles/iot-hub/iot-hub-csharp-csharp-direct-methods.md)
> * [Java](../articles/iot-hub/iot-hub-java-java-direct-methods.md)

Centrum IoT Azure jest w pełni zarządzaną usługę, która zapewnia niezawodne i bezpieczną komunikację dwukierunkową między milionów urządzeń i rozwiązanie zaplecza. Samouczki poprzedniego ([Rozpoczynanie pracy z Centrum IoT] i [wysyłać chmury do urządzenia z Centrum IoT]) ilustrują hello podstawowych urządzenia do chmury i chmury do urządzenia obsługi funkcji Centrum IoT. Centrum IoT umożliwia także hello metody nietrwałe tooinvoke możliwości na urządzeniach z hello chmury. Bezpośrednie metody reprezentują interakcji żądanie odpowiedź znać stan hello hello wywołanie z urządzenia tooan podobne, wywołaj HTTP, w tym ich powodzenie lub niepowodzenie natychmiast (po limitu określonego przez użytkownika) toolet hello użytkownika. [Wywoływanie metody bezpośrednio na urządzeniu] [ lnk-devguide-methods] opisano metody bezpośredniego bardziej szczegółowo i zawiera wskazówki dotyczące po toouse bezpośrednie metody zamiast wiadomości chmury do urządzenia lub odpowiednie właściwości.

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Użyj hello Azure toocreate portalu Centrum IoT i Utwórz tożsamość urządzenia w Centrum IoT.
* Tworzenie aplikacji symulowane urządzenie, który ma bezpośredni metodę, która może być wywoływany przez hello chmury.
* Utwórz aplikację konsoli, która wywołuje metodę bezpośrednio w aplikacji symulowane urządzenie hello za pośrednictwem Centrum IoT.

> [!NOTE]
> W tej chwili bezpośrednie są tylko obsługiwana w urządzeń łączących się za Centrum tooIoT hello MQTT protokołu. Zobacz toohello [Obsługa MQTT] [ lnk-devguide-mqtt] artykuł, aby uzyskać instrukcje dotyczące tooconvert istniejących urządzeń aplikacji toouse MQTT.


[lnk-devguide-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md

[wysyłać chmury do urządzenia z Centrum IoT]: ../articles/iot-hub/iot-hub-csharp-csharp-c2d.md
[Rozpoczynanie pracy z Centrum IoT]: ../articles/iot-hub/iot-hub-node-node-getstarted.md