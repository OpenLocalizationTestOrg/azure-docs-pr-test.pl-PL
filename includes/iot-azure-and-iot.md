
# <a name="azure-and-internet-of-things"></a>Platforma Azure i Internet rzeczy

Witamy tooMicrosoft Azure i hello Internetu rzeczy (IoT). W tym artykule przedstawiono architekturę rozwiązania IoT opisującą typowe cechy rozwiązania IoT, które można wdrożyć przy użyciu usług Azure hello. Rozwiązania IoT wymagają, aby zabezpieczyć komunikację dwukierunkową między urządzeniami, prawdopodobnie numerowanie hello miliony i zaplecza rozwiązania. Na przykład zaplecza rozwiązania może używać automatycznej analizy predykcyjnej toouncover insights z strumienia zdarzeń urządzenia do chmury.

Usługa Azure IoT Hub stanowi kluczowy element podczas wdrażania tej architektury rozwiązania IoT przy użyciu usług platformy Azure. Pakiet IoT zapewnia pełne, kompleksowe wdrożenia tej architektury w określonych scenariuszach IoT. Na przykład:

* Witaj *monitorowania zdalnego* rozwiązanie umożliwia toomonitor hello stanu urządzeń, takich jak automaty.
* Witaj *konserwacji predykcyjnej* rozwiązanie pomaga tooanticipate potrzeby obsługi urządzeń, takich jak pomp w zdalnych przepompowniach i tooavoid niezaplanowanych przestojów.
* Witaj *połączonych fabryki* rozwiązanie pomaga tooconnect i monitorować urządzenia przemysłowych.

## <a name="iot-solution-architecture"></a>Architektura rozwiązania IoT

powitania po diagram przedstawia typową architekturę rozwiązania IoT. Hello diagram nie zawiera nazwy hello żadnych określonych usług platformy Azure, ale zawiera opis kluczowych elementów ogólnej architektury rozwiązania IoT hello. W ramach tej architektury urządzenia IoT zbierają dane przesyłane tooa bramy chmury. Witaj brama chmury udostępnia dane hello przetwarzania przez inne usługi zaplecza, z których dane są dostarczane aplikacji biznesowych z tooother lub operatory toohuman za pośrednictwem pulpitu nawigacyjnego lub innych urządzeń do prezentacji.

![Architektura rozwiązania IoT][img-solution-architecture]

> [!NOTE]
> Szczegółowe omówienie architektury IoT, zobacz hello [architektura referencyjna IoT platformy Microsoft Azure][lnk-refarch].

### <a name="device-connectivity"></a>Łączność urządzeń

W ramach tej architektury rozwiązania IoT urządzenia wysyłają dane telemetryczne, np. odczyty czujników z przepompowni, punktu końcowego w chmurze tooa do przechowywania i przetwarzania. W scenariuszu konserwacji predykcyjnej hello rozwiązania zaplecze może używać strumienia hello toodetermine danych czujnika, kiedy określona pompa wymaga konserwacji. Urządzenia można odbierać i odpowiadać wiadomości toocloud do urządzenia, odczytując komunikaty z punktu końcowego w chmurze. Na przykład w rozwiązaniu hello scenariuszu konserwacji predykcyjnej hello zaplecza może wysyłanie wiadomości tooother pomp w hello przekazywanie toobegin stacji przekierowanie przepływów tuż przed konserwacji toostart. Ta procedura czy upewnij się, że inżynierem konserwacji hello można rozpocząć natychmiast po przybyciu.

Jedną z największych wyzwań stojących hello przed projektami IoT jest sposób tooreliably i bezpieczne łączenie z zaplecza urządzeń toohello rozwiązania. Urządzenia IoT charakteryzują się innymi cechami jako porównaniu tooother klientów, takich jak przeglądarki i aplikacje mobilne. Urządzenia IoT:

* są często systemami osadzonymi bez osoby pełniącej rolę operatora;
* mogą być wdrażane w lokalizacjach zdalnych, gdzie dostęp fizyczny jest bardzo kosztowny;
* Mogą być dostępne tylko za pośrednictwem zaplecza rozwiązania hello. Nie ma żadnych toointeract sposób hello urządzenia.
* mogą mieć ograniczone zasoby w zakresie zasilania i przetwarzania;
* mogą korzystać z przerywanej, powolnej lub kosztownej łączności sieciowej;
* Może być konieczne toouse aplikacji zastrzeżonych, niestandardowych lub specyficznych dla branży protokołów.
* mogą być tworzone przy użyciu szerokiej gamy popularnych platform sprzętowych i programowych.

Ponadto toohello powyższych wymagań każde rozwiązanie IoT musi również zapewniać skali, bezpieczeństwa i niezawodności. Witaj wynikowy zbiór wymogów dotyczących łączności jest trudny i czasochłonny tooimplement przy użyciu tradycyjnych technologii, takich jak kontenery sieci web i brokery. Centrum IoT Azure i hello zestawy SDK urządzenia Azure IoT umożliwiają łatwiejsze rozwiązań tooimplement, które spełniają te wymagania.

Urządzenie może komunikować się bezpośrednio z punktem końcowym bramy chmury, lub jeśli urządzenie hello nie może używać żadnych protokołów komunikacyjnych hello, które hello obsługuje bramy chmury, można połączyć za pośrednictwem bramy pośredniej. Na przykład Witaj [brama protokołu Azure IoT] [ lnk-protocol-gateway] można wykonać translacji protokołów, jeśli urządzenia nie można używać żadnych protokołów hello, które obsługuje Centrum IoT.

### <a name="data-processing-and-analytics"></a>Przetwarzanie danych i analiza

W chmurze hello zaplecza rozwiązania IoT jest, gdzie występuje najczęściej hello przetwarzania danych, takich jak filtrowania i agregowania telemetrii oraz tooother usług routingu. Witaj zaplecza rozwiązania IoT:

* Odbiera telemetrię na dużą skalę z urządzeń i określa, jak tooprocess i przechowywania tych danych. 
* Może umożliwić toosend poleceń z hello chmury toospecific urządzenia.
* Zapewnia możliwości rejestracji urządzenia, które umożliwiają tooprovision urządzenia i toocontrol urządzeń, które są dozwolone tooconnect tooyour infrastruktury.
* Umożliwia tootrack możesz hello stanu urządzeń i monitorowanie ich działania.

W scenariuszu konserwacji predykcyjnej hello zaplecza hello rozwiązania przechowuje historyczne dane telemetryczne. zaplecza rozwiązania Hello można użyć tego wzorców tooidentify toouse danych wskazują, że jest w danej przepompowni z powodu konserwacji.

Rozwiązania IoT mogą obejmować automatyczne pętle sprzężenia zwrotnego. Na przykład moduł analityczny zaplecza rozwiązania hello może rozpoznać na podstawie telemetrii, będącą hello temperatura określonego urządzenia przekracza normalne poziomy działania. rozwiązanie Hello następnie mogą wysyłać polecenia urządzenia toohello, instrukcją tootake działań naprawczych.

### <a name="presentation-and-business-connectivity"></a>Prezentacja i łączność biznesowa

Warstwa łączności prezentacji i business Hello umożliwia użytkownikom końcowym, toointeract z hello rozwiązania IoT i urządzeniami hello. Go włącza tooview użytkowników i analizować dane hello zbierane z urządzeń. Widoki te mogą mieć formę hello pulpitów nawigacyjnych i raportów analizy Biznesowej, które zawierają zarówno dane historyczne lub niemal w czasie rzeczywistym. Na przykład operator można sprawdzić hello stan określonej przepompowni i wyświetlić wszystkie alerty wygenerowane przez hello system. Ta warstwa umożliwia także integrację hello zaplecza rozwiązania IoT z istniejących aplikacji biznesowych z tootie enterprise procesów biznesowych i przepływów pracy. Na przykład rozwiązanie do konserwacji predykcyjnej hello można zintegrować z systemem planowania tej dokumentacji książki toovisit inżynier przepompowni podczas hello rozwiązanie zidentyfikuje pompę wymagającą konserwacji.

![Pulpit nawigacyjny rozwiązania IoT][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
