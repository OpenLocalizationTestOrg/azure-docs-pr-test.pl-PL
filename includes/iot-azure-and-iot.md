
# <a name="azure-and-internet-of-things"></a>Platforma Azure i Internet rzeczy

Witamy na platformie Microsoft Azure oraz w Internecie rzeczy (IoT). Ten artykuł przedstawia typowe cechy rozwiązania IoT, które można wdrożyć przy użyciu usług platformy Azure. Rozwiązania IoT wymagają bezpiecznej, dwukierunkowej komunikacji między dużą liczbą urządzeń a zapleczem rozwiązania. Zaplecze rozwiązania może korzystać z automatycznej analizy predykcyjnej w celu uzyskiwania wglądu w dane ze strumienia zdarzeń przesyłanego z urządzenia do chmury.

Usługa [Azure IoT Hub][lnk-iot-hub] stanowi kluczowy element każdego rozwiązania IoT korzystającego z usług platformy Azure. IoT Hub to w pełni zarządzana usługa, która umożliwia bezpieczną i niezawodną dwukierunkową komunikację między milionami urządzeń IoT i zapleczem rozwiązania. 

[Pakiet IoT Azure][lnk-iot-suite] zapewnia pełne, kompleksowe wdrożenia tej architektury w określonych scenariuszach IoT. Na przykład:

* Rozwiązanie do *monitorowania zdalnego* umożliwia monitorowanie stanu urządzeń, takich jak automaty do sprzedaży.
* Rozwiązanie do *konserwacji predykcyjnej* pomaga przewidywać wymagania związane z konserwacją urządzeń, na przykład pomp w zdalnych przepompowniach, oraz unikać nieplanowanych przestojów.
* Rozwiązanie *połączonej fabryki* ułatwia łączenie z urządzeniami przemysłowymi oraz ich monitorowanie.

## <a name="iot-solution-architecture"></a>Architektura rozwiązania IoT

Poniższy schemat przedstawia typową architekturę rozwiązania IoT. Diagram nie obejmuje nazw żadnych konkretnych usług platformy Azure, ale zawiera opis kluczowych elementów ogólnej architektury rozwiązania IoT. W ramach tej architektury urządzenia IoT zbierają dane, które wysyłają do bramy chmury. Brama chmury udostępnia dane do przetwarzania przez inne usługi zaplecza. Zaplecze rozwiązania dostarcza dane do aplikacji branżowych lub osób pełniących rolę operatorów za pośrednictwem pulpitu nawigacyjnego lub raportów.

![Architektura rozwiązania IoT][img-solution-architecture]

> [!NOTE]
> Szczegółowe omówienie architektury IoT można znaleźć w temacie [Architektura referencyjna IoT platformy Microsoft Azure][lnk-refarch].

### <a name="device-connectivity"></a>Łączność urządzeń

W ramach tego rozwiązania IoT urządzenia wysyłają dane telemetryczne, np. odczyty czujników z przepompowni, do punktu końcowego w chmurze w celu ich przechowywania i przetwarzania. W scenariuszu konserwacji predykcyjnej zaplecze rozwiązania może używać strumienia danych z czujnika do określenia, kiedy dana pompa wymaga konserwacji. Urządzenia mogą również odbierać komunikaty przesyłane z chmury do urządzenia oraz odpowiadać na nie, odczytując komunikaty z punktu końcowego w chmurze. W scenariuszu konserwacji predykcyjnej zaplecze rozwiązania może na przykład wysyłać komunikaty do innych pomp w przepompowni w celu zainicjowania zmiany trasy przepływów przed samym rozpoczęciem zaplanowanej konserwacji. Procedura ta pozwala inżynierom serwisu natychmiast rozpocząć rozwiązywanie problemów.

Jedno z największych wyzwań w projektach IoT polega na tym, jak w sposób niezawodny i bezpieczny połączyć urządzenia z zapleczem rozwiązania. Urządzenia IoT charakteryzują się innymi cechami niż pozostałe rozwiązania klienckie, takie jak przeglądarki i aplikacje mobilne. Urządzenia IoT:

* są często systemami osadzonymi bez osoby pełniącej rolę operatora;
* mogą być wdrażane w lokalizacjach zdalnych, gdzie dostęp fizyczny jest bardzo kosztowny;
* mogą być dostępne tylko za pośrednictwem zaplecza rozwiązania. Nie istnieje inny sposób interakcji z urządzeniem;
* mogą mieć ograniczone zasoby w zakresie zasilania i przetwarzania;
* mogą korzystać z przerywanej, powolnej lub kosztownej łączności sieciowej;
* mogą wymagać używania zastrzeżonych, niestandardowych lub branżowych protokołów aplikacji;
* mogą być tworzone przy użyciu szerokiej gamy popularnych platform sprzętowych i programowych.

Oprócz powyższych wymagań każde rozwiązanie IoT musi również zapewniać skalowalność, bezpieczeństwo i niezawodność. Ustalony zbiór wymogów dotyczących łączności jest trudny i czasochłonny we wdrażaniu przy użyciu tradycyjnych technologii, takich jak kontenery sieci Web i brokery obsługujące komunikaty. Usługa Azure IoT Hub i zestawy SDK urządzeń Azure IoT ułatwiają wdrażanie rozwiązań, które spełniają te wymagania.

Urządzenie może komunikować się bezpośrednio z punktem końcowym bramy chmury. Jeśli urządzenie nie może użyć żadnych protokołów komunikacyjnych obsługiwanych przez bramę chmury, może nawiązać połączenie za pośrednictwem bramy pośredniej. Na przykład [brama protokołu IoT Azure][lnk-protocol-gateway] może wykonać translację protokołu, jeśli urządzenia nie mogą używać żadnych protokołów obsługiwanych przez usługę IoT Hub.

### <a name="data-processing-and-analytics"></a>Przetwarzanie danych i analiza

Większość operacji przetwarzania danych w chmurze jest realizowana na poziomie zaplecza rozwiązania IoT. Zaplecze rozwiązania IoT:

* odbiera telemetrię z urządzeń we właściwej skali i określa sposób przetwarzania i przechowywania tych danych; 
* umożliwia wysyłanie poleceń z chmury do konkretnych urządzeń;
* zapewnia funkcje rejestracji, które pozwalają aprowizować urządzenia oraz kontrolować łączenie się urządzeń z infrastrukturą;
* umożliwia śledzenie stanu urządzeń i monitorowanie ich działania.

W scenariuszu konserwacji predykcyjnej zaplecze rozwiązania przechowuje historyczne dane telemetryczne. Zaplecze rozwiązania może użyć tych danych w celu zidentyfikowania wzorców, które wskazują na konieczność przeprowadzenia konserwacji danej pompy.

Rozwiązania IoT mogą obejmować automatyczne pętle sprzężenia zwrotnego. Na przykład moduł analityczny zaplecza rozwiązania może rozpoznać na podstawie telemetrii, że temperatura określonego urządzenia przekracza normalne poziomy działania. Następnie rozwiązanie może wysłać do urządzenia polecenie podjęcia akcji naprawczej.

### <a name="presentation-and-business-connectivity"></a>Prezentacja i łączność biznesowa

Warstwa prezentacji i łączności biznesowej umożliwia użytkownikom końcowym interakcję z rozwiązaniem IoT i urządzeniami. Pozwala użytkownikom wyświetlać i analizować dane zbierane z urządzeń. Widoki te mogą mieć formę pulpitów nawigacyjnych lub raportów, które zawierają zarówno dane historyczne, jak i dane uzyskiwane niemal w czasie rzeczywistym. Na przykład operator może sprawdzić stan określonej przepompowni i wyświetlić wszystkie alerty wygenerowane przez system. Ta warstwa umożliwia także integrację zaplecza rozwiązania IoT z istniejącymi aplikacjami branżowymi w celu ich powiązania w ramach procesów biznesowych i przepływów pracy przedsiębiorstwa. Na przykład rozwiązanie do konserwacji predykcyjnej można zintegrować z systemem planowania. Gdy rozwiązanie wykryje, że jakaś pompa wymaga konserwacji, system planowania zarezerwuje wizytę serwisanta w przepompowni.

![Pulpit nawigacyjny rozwiązania IoT][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-iot-hub]: ../articles/iot-hub/iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: ../articles/iot-suite/iot-suite-overview.md
[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
