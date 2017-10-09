> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

Ten artykuł zawiera szczegółowe wskazówki dotyczące hello [Hello World przykładowy kod] [ lnk-helloworld-sample] tooillustrate hello podstawowych składników hello [Azure IoT krawędzi] [ lnk-iot-edge] architektury. Witaj w przykładzie użyto hello Azure IoT krawędzi toobuild proste bramy, która rejestruje co pięć sekund pliku tooa komunikat "hello world".

Przewodnik składa się z następujących elementów:

* **Hello World przykładowa architektura**: w tym artykule opisano sposób [pojęcia architektury Azure IoT krawędzi] [ lnk-edge-concepts] się przykład Witaj świecie toohello oraz sposób składniki hello dopasowania.
* **Jak toobuild hello próbki**: hello kroki wymagane toobuild hello próbki.
* **Jak toorun hello próbki**: hello kroki wymagane toorun hello próbki. 
* **Dane wyjściowe zazwyczaj**: przykład hello output tooexpect po uruchomieniu hello próbki.
* **Wstawki kodu**: kolekcja tooshow wstawki kodu jak przykładowa aplikacja hello Hello World implementuje klucza składniki bramy IoT krawędzi.


## <a name="hello-world-sample-architecture"></a>Przykładowa architektura Witaj, świecie
Przykładowa aplikacja Hello Hello World przedstawiono hello pojęcia opisane w poprzedniej sekcji hello. Przykładowa aplikacja Hello Hello World implementuje bramy IoT krawędzi, która ma potoku składają się z dwóch modułów krawędzi IoT:

* Witaj *Witaj świecie* moduł tworzy komunikat co pięć sekund i przekazuje je toohello rejestratora modułu.
* Witaj *rejestratora* wiadomości powitania zapisy modułu odbierze tooa pliku.

![Architektura przykładowej aplikacji Hello world utworzonej przy użyciu usługi Azure IoT Edge][4]

Zgodnie z opisem w poprzedniej sekcji hello, hello World Hello modułu nie zostały spełnione komunikatów bezpośrednio modułu rejestratora toohello co pięć sekund. Zamiast tego należy go publikuje brokera toohello komunikatów co pięć sekund.

Moduł rejestratora Hello odbiera wiadomości powitania od brokera hello i działa na niego, zapisywanie hello zawartość pliku tooa wiadomość hello.

Moduł rejestratora Hello wykorzystuje tylko komunikaty z hello brokera, nigdy nie publikuje nowy brokera toohello wiadomości.

![Jak brokera hello tras wiadomości między modułami w programie Azure IoT Edge][5]

Witaj ilustracji powyżej przedstawiono architekturę hello Przykładowa aplikacja hello Hello World i ścieżek względnych hello toohello pliki źródłowe, które implementuje różnych części próbki hello w hello [repozytorium][lnk-iot-edge]. Eksploruj hello kod na własną lub hello wstawki kodu za pomocą poniżej jako przewodnika.

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md