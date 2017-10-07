---
title: "Centrum IoT słownik terminów aaaAzure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — słownik typowe terminy dotyczące tooAzure Centrum IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>Słownik terminów Centrum IoT
W tym artykule wymieniono niektóre hello typowe terminy używane w hello artykuły Centrum IoT.

## <a name="advanced-message-queueing-protocol"></a>Protokół usługi kolejkowania komunikatów zaawansowane
[Zaawansowane protokołu usługi kolejkowania komunikatów (AMQP)](https://www.amqp.org/) jest jedną z wiadomości powitania protokołów, które [Centrum IoT](#iot-hub) obsługuje do komunikowania się z urządzeniami. Aby uzyskać więcej informacji na temat hello protokoły, które obsługuje Centrum IoT obsługi komunikatów, zobacz [wysyłania i odbierania wiadomości z Centrum IoT](iot-hub-devguide-messaging.md).

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Witaj [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) to narzędzie do tworzenia i zarządzania zasobami na platformie Microsoft Azure i platform, open source, opartych na powłoki poleceń. Ta wersja hello interfejsu wiersza polecenia jest implementowane przy użyciu środowiska Node.js.

## <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0
Witaj [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) to narzędzie do tworzenia i zarządzania zasobami na platformie Microsoft Azure i platform, open source, opartych na powłoki poleceń. Ta wersja zapoznawcza hello interfejsu wiersza polecenia jest implementowane za pomocą języka Python.


## <a name="azure-iot-device-sdks"></a>Urządzenia IoT Azure SDK
Brak _urządzenia zestawów SDK_ dostępne dla wielu języków, które pozwalają toocreate [aplikacji dla urządzeń](#device-app) który interakcję z Centrum IoT. Witaj Centrum IoT samouczki wyjaśniają, jak toouse te zestawy SDK urządzenia. Kod źródłowy hello i uzyskać więcej informacji o urządzeniu hello zestawów SDK można znaleźć w tej witrynie GitHub [repozytorium](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-iot-edge"></a>Azure IoT Edge
Krawędź IoT umożliwia aplikacjom toowrite włączyć toocommunicate urządzeń połączonych z bramy z [Centrum IoT](#iot-hub). Witaj krawędzi IoT samouczki wyjaśniają, jak toouse tej usługi. Kod źródłowy hello i uzyskać więcej informacji o krawędzi IoT Azure można znaleźć w tej witrynie GitHub [repozytorium](https://github.com/Azure/iot-edge).

## <a name="azure-iot-service-sdks"></a>Zestawy Azure IoT usługi SDK
Brak _usługi SDK_ dostępne dla wielu języków, które pozwalają toocreate [zaplecza aplikacji](#back-end-app) który interakcję z Centrum IoT. Witaj Centrum IoT samouczki wyjaśniają, jak toouse te usługi SDK. Kod źródłowy hello i uzyskać więcej informacji o usłudze hello zestawów SDK można znaleźć w tej witrynie GitHub [repozytorium](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-portal"></a>Azure Portal
Witaj [portalu Microsoft Azure](https://portal.azure.com) to centralne miejsce, w którym można udostępnić i zarządzania zasobami platformy Azure. Organizuje ona jego zawartości przy użyciu _bloków_. W niektórych hello Centrum IoT samouczków, może być konieczne toouse hello [klasycznego portalu Azure](https://manage.windowsazure.com).

## <a name="azure-powershell"></a>Azure PowerShell
[Program Azure PowerShell](/powershell/azure/overview) jest zestawem poleceń cmdlet programu Windows PowerShell można użyć toomanage Azure. Można użyć hello toocreate poleceń cmdlet, testowania, wdrożenia i Zarządzaj rozwiązaniami i usługi dostarczane za pośrednictwem hello platformy Azure.

## <a name="azure-resource-manager"></a>Azure Resource Manager
[Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) pozwala toowork z zasobami hello w rozwiązaniu jako grupa. Można wdrożyć, zaktualizować lub usunięcie hello zasobów dla rozwiązania w jednej, skoordynowanej operacji.

## <a name="azure-service-bus"></a>Azure Service Bus
[Usługa Service Bus](../service-bus/index.md) zapewnia włączoną obsługę chmury komunikacji z obsługą wiadomości przedsiębiorstwa i obsługiwanych przez przekaźnik komunikacji, który pomaga połączyć rozwiązań lokalnych z chmurą hello. Niektóre samouczki Centrum IoT korzystają usługi Service Bus [kolejek](../service-bus-messaging/service-bus-messaging-overview.md).

## <a name="azure-storage"></a>Azure Storage
[Usługa Azure Storage](../storage/common/storage-introduction.md) jest rozwiązanie magazynu w chmurze. Obejmuje on hello usługi magazynu obiektów Blob służy toostore niestrukturalnych dane obiektu. Niektóre samouczki Centrum IoT używać magazynu obiektów blob.

## <a name="back-end-app"></a>Zaplecza aplikacji
W kontekście hello [Centrum IoT](#iot-hub), aplikacji wewnętrznych to aplikacja, która łączy tooone hello połączonej usługi punkty końcowe Centrum IoT. Na przykład aplikacji zaplecza może pobrać [urządzenia do chmury](#device-to-cloud)wiadomości lub zarządzać hello [rejestru tożsamości](#identity-registry). Zazwyczaj aplikacji zaplecza działa w chmurze hello, ale w wielu samouczki hello hello zaplecza aplikacji są konsoli aplikacje działające na komputerze deweloperskim lokalnego.

## <a name="built-in-endpoints"></a>Wbudowane punkty końcowe
Centrum IoT, co obejmuje wbudowane [punktu końcowego](iot-hub-devguide-endpoints.md) czyli zdarzenia koncentratora zgodny. Można użyć dowolnego mechanizm, który współpracuje z usługi Event Hubs tooread urządzenia do chmury wiadomości z tego punktu końcowego.

## <a name="cloud-gateway"></a>Brama chmury
Brama chmury umożliwia łączność urządzeń, które nie może połączyć bezpośrednio za[Centrum IoT](#iot-hub). Brama chmury jest hostowana w chmurze hello w tooa kontrast [bramy pola](#field-gateway) , na którym działa tooyour lokalnej urządzenia. Typowy przypadek użycia bramy chmury jest tooimplement translację protokołu dla urządzeń.

## <a name="cloud-to-device"></a>Chmury do urządzenia
Odwołuje się toomessages wysyłane z Centrum tooa podłączonego urządzenia IoT. Często komunikaty te są poleceniami, które poinstruować hello urządzenia tootake akcji. Aby uzyskać więcej informacji, zobacz [wysyłania i odbierania wiadomości z Centrum IoT](iot-hub-devguide-messaging.md).

## <a name="connection-string"></a>Parametry połączenia
Parametry połączenia należy użyć w aplikacji kod tooencapsulate hello informacje wymagane tooconnect tooan punktu końcowego. Ciąg połączenia obejmują zazwyczaj hello adres punktu końcowego hello i informacje o zabezpieczeniach, ale ciąg połączenia formatów różnią się w usługach. Istnieją dwa typy parametrów połączenia skojarzone z hello usługi Centrum IoT:
- *Parametry połączenia urządzenia* włączyć urządzeń tooconnect toohello urządzenia uwzględniającym punkty końcowe Centrum IoT.
- *Parametry połączenia Centrum IoT* umożliwić aplikacji wewnętrznej tooconnect toohello połączonej usługi punkty końcowe Centrum IoT.

## <a name="custom-endpoints"></a>Niestandardowe punkty końcowe
Można tworzyć niestandardowe [punkty końcowe](iot-hub-devguide-endpoints.md) na toodeliver Centrum IoT wiadomości wysyłane przez [reguły routingu](#routing-rules). Niestandardowe punkty końcowe bezpośrednie połączenie tooan Centrum zdarzeń, kolejki usługi Service Bus lub tematu usługi Service Bus.

## <a name="custom-gateway"></a>Bram
Brama umożliwia łączność urządzeń, które nie może połączyć bezpośrednio za[Centrum IoT](#iot-hub). Można użyć [Azure IoT krawędzi](#azure-iot-edge) toobuild niestandardowych bram, które implementuje niestandardowej logiki toohandle wiadomości, konwersje protokołu niestandardowego i innego typu przetwarzania na hello krawędzi.

## <a name="data-point-message"></a>Komunikat punktu danych
Komunikat punktu danych jest [urządzenia do chmury](#device-to-cloud) komunikat, który zawiera [telemetrii](#telemetry) dane, takie jak szybkości knie lub temperatury.

## <a name="desired-configuration"></a>Wymaganą konfiguracją
W kontekście hello [dwie urządzenia](iot-hub-devguide-device-twins.md), potrzeby toohello pełny zestaw właściwości oraz metadanych w Witaj dwie urządzenia, które mają być synchronizowane z urządzeniem hello odwołuje się konfiguracji.

## <a name="desired-properties"></a>Żądane właściwości
W kontekście hello [dwie urządzenia](iot-hub-devguide-device-twins.md), żądana właściwości to podsekcji hello dwie urządzenia, który jest używany z [zgłosił właściwości](#reported-properties) toosynchronize konfiguracji urządzenia lub warunku. Żądane właściwości można ustawić tylko [zaplecza aplikacji](#back-end-app) i są przestrzegane hello [aplikacji urządzenia](#device-app).

## <a name="device-to-cloud"></a>Urządzenia do chmury
Odwołuje się toomessages wysłany z podłączonego urządzenia[Centrum IoT](#iot-hub). Te komunikaty mogą być [punktu danych](#data-point-message) lub [interakcyjne](#interactive-message) wiadomości. Aby uzyskać więcej informacji, zobacz [wysyłania i odbierania wiadomości z Centrum IoT](iot-hub-devguide-messaging.md).

## <a name="device"></a>Urządzenie
W kontekście hello IoT urządzenie jest zwykle na małą skalę, autonomicznym urządzeniem może zbierać dane lub inne urządzenia. Na przykład urządzenie może być środowiska monitorowania urządzenia, lub do kontrolera hello nadchodzić i wentylatorów systemów w cieplarnianych. Witaj [katalogu urządzenia](https://catalog.azureiotsuite.com/) zawiera listę toowork certyfikowanych urządzeń sprzętowych z [Centrum IoT](#iot-hub).

## <a name="device-app"></a>Urządzenia aplikacji
Aplikacja urządzenia jest uruchamiana na Twojej [urządzenia](#device) i uchwytów hello komunikacji z Twojej [Centrum IoT](#iot-hub). Zwykle, użyj jednej z hello [urządzenia Azure IoT SDK](#azure-iot-device-sdks) podczas wdrożenia aplikacji urządzenia. W wielu hello IoT samouczków, użyj [symulowane urządzenie](#simulated-device) dla wygody.

## <a name="device-condition"></a>Stan urządzenia
Odwołuje się informacje o stanie toodevice, takich jak metoda łączności hello obecnie w użyciu, zgodnie z raportem [aplikacji urządzenia](#device-app). [Aplikacje urządzenia](#device-app) zgłaszać także ich możliwości. Można wysyłać zapytania dotyczące stanu i możliwości odpowiednie informacje przy użyciu twins urządzenia.

## <a name="device-data"></a>Dane urządzenia
Dane urządzenia odwołuje się toohello na urządzenie danych przechowywanych w Centrum IoT hello [rejestru tożsamości](#identity-registry). Jest to możliwe tooimport i wyeksportować te dane.

## <a name="device-explorer"></a>Eksplorator urządzenia
Hello [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) to narzędzie jest uruchamiana w systemie Windows, które umożliwia toomanage możesz urządzeń w hello [rejestru tożsamości](#identity-registry).hello narzędzia można również wysyłać i odbierać wiadomości tooyour urządzeń.

## <a name="device-identities-rest-api"></a>Interfejs API REST tożsamości urządzeń
Witaj [interfejsu API REST tożsamości urządzenia](https://docs.microsoft.com/rest/api/iothub/iothubresource) pozwala na urządzeniach zarejestrowanych w hello toomanage [rejestru tożsamości](#identity-registry) przy użyciu interfejsu API REST. Zazwyczaj należy użyć jednej z wyższego poziomu hello [usługi SDK](#azure-iot-service-sdks) pokazane na powitania samouczki Centrum IoT.

## <a name="device-identity"></a>Tożsamość urządzenia
Witaj tożsamości urządzenia hello Unikatowy identyfikator przypisany tooevery urządzenie jest zarejestrowane w hello [rejestru tożsamości](#identity-registry).

## <a name="device-management"></a>Zarządzanie urządzeniami
Zarządzanie urządzeniami obejmuje pełny cykl hello związane z zarządzaniem hello urządzeń w rozwiązania IoT, w tym planowania, inicjowania obsługi administracyjnej, konfigurowania, monitorowania i wycofywania.

## <a name="device-management-patterns"></a>Wzorce zarządzania urządzeniami
[Centrum IoT](#iot-hub) umożliwia typowe wzorce zarządzania urządzenie tym ponowny rozruch, wykonywanie ustawień fabrycznych i wykonywanie aktualizacji oprogramowania układowego na urządzeniach.

## <a name="device-messaging-rest-api"></a>Interfejs API REST komunikatów urządzenia
Można użyć hello [interfejsu API REST wiadomości urządzenia](https://docs.microsoft.com/rest/api/iothub/httpruntime) z urządzenia toosend urządzenia do chmury wiadomości tooan Centrum IoT i odbierania [chmury do urządzenia](#cloud-to-device) komunikaty z Centrum IoT. Zazwyczaj należy użyć jednej z wyższego poziomu hello [urządzenia zestawów SDK](#azure-iot-device-sdks) pokazane na powitania samouczki Centrum IoT.

## <a name="device-provisioning"></a>Inicjowanie obsługi administracyjnej urządzeń
Inicjowanie obsługi administracyjnej urządzeń jest hello proces dodawania początkowego hello [danych urządzenia](#device-data) toohello są przechowywane w rozwiązaniu. tooenable nowe Centrum tooyour tooconnect urządzenia, należy dodać urządzenia identyfikator i klucze toohello Centrum IoT [rejestru tożsamości](#identity-registry). W ramach procesu udostępniania hello może być konieczne tooinitialize dane specyficzne dla urządzeń w innych magazynach rozwiązania.

## <a name="device-twin"></a>Bliźniak urządzenia
A [dwie urządzenia](iot-hub-devguide-device-twins.md) jest dokumentem JSON, która przechowuje informacje o stanie urządzenia, takie jak metadanych, konfiguracji i warunki. [Centrum IoT](#iot-hub) będzie się powtarzał dwie urządzenia, dla wszystkich urządzeń, których udostępnianie w Centrum IoT. Twins urządzenia Włącz toosynchronize [warunki urządzenia](#device-condition) i konfiguracje między urządzeniem hello i rozwiązanie hello zaplecza. Umożliwia wysyłanie zapytań urządzenia twins toolocate określonymi urządzeniami i zbadać hello stanu długotrwałej operacji.

## <a name="device-twin-queries"></a>Urządzenie dwie zapytań
[Urządzenie dwie zapytania](iot-hub-devguide-query-language.md) hello Centrum IoT przypominającego SQL zapytań języka tooretrieve informacje z twins Twojego urządzenia. Można użyć hello sam Centrum IoT zapytania o informacje o języku tooretrieve [zadania](#job) uruchomiona w Centrum IoT.

## <a name="device-twin-rest-api"></a>Interfejs API REST dwie urządzenia
Można użyć hello [interfejsu API REST dwie urządzenia](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) z rozwiązania hello zaplecza toomanage twins Twojego urządzenia. Hello interfejsu API pozwala tooretrieve i aktualizacji [dwie urządzenia](#device-twin) właściwości i wywoływać [bezpośrednie metody](#direct-method). Zazwyczaj należy użyć jednej z wyższego poziomu hello [usługi SDK](#azure-iot-service-sdks) pokazane na powitania samouczki Centrum IoT.

## <a name="device-twin-synchronization"></a>Synchronizacja dwie urządzenia
Synchronizacji dwie urządzeń używa hello [żądanego właściwości](#desired-properties) w tooconfigure twins Twojego urządzenia urządzeniami i pobrać [zgłosił właściwości](#reported-properties) z toostore Twojego urządzenia w Witaj dwie urządzenia.

## <a name="direct-method"></a>Metoda bezpośrednia
A [metoda bezpośrednia](iot-hub-devguide-direct-methods.md) jest sposobem możesz tootrigger tooexecute metody, na urządzeniu przez wywołanie interfejsu API w Centrum IoT.

## <a name="endpoint"></a>Endpoint
Centrum IoT udostępnia wiele [punkty końcowe](iot-hub-devguide-endpoints.md) umożliwiających Centrum IoT toohello tooconnect aplikacji. Istnieją punkty końcowe skierowane do urządzenia, które włączyć urządzeń tooperform operacje, takie jak wysyłanie [urządzenia do chmury](#device-to-cloud) wiadomości i odbieranie [chmury do urządzenia](#cloud-to-device) wiadomości. Brak punktów końcowych zarządzania połączonej usługi, które umożliwiają [zaplecza aplikacji](#back-end-app) tooperform operacje, takie jak [tożsamości urządzenia](#device-identity) i zarządzanie dwie urządzenia. Brak połączonej usługi [wbudowane punkty końcowe](#built-in-endpoints) do odczytywania wiadomości urządzenia do chmury. Można utworzyć [niestandardowe punkty końcowe](#custom-endpoints) tooreceive urządzenia do chmury wiadomości wysyłane przez [reguły routingu](#routing-rules).

## <a name="event-hubs-service"></a>Usługa centra zdarzeń
[Centra zdarzeń](../event-hubs/event-hubs-what-is-event-hubs.md) jest wysoce skalowalna Usługa transferu danych, który może obsługiwać miliony zdarzeń na sekundę. Usługa Hello pozwala tooprocess i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello. Porównanie z hello usługi IoT Hub, zobacz [porównania Azure IoT Hub i usługi Azure Event Hubs](iot-hub-compare-event-hubs.md).

## <a name="event-hub-compatible-endpoint"></a>Punkt końcowy zgodnych z Centrum zdarzeń
tooread [urządzenia do chmury](#device-to-cloud) wiadomości wysyłane z Centrum IoT tooyour, można połączyć tooan punktu końcowego na Centrum i używać tych wiadomości tooread metody żadnych zgodnych z Centrum zdarzeń. Metody zgodnych z Centrum zdarzeń to, za pomocą hello [zestawów SDK centra zdarzeń](../event-hubs/event-hubs-programming-guide.md) i [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md).

## <a name="field-gateway"></a>Pole bramy
Brama pola umożliwia łączność urządzeń, które nie może połączyć bezpośrednio za[Centrum IoT](#iot-hub) są zwykle wdrażane lokalnie z urządzenia. Aby uzyskać więcej informacji, zobacz [co to jest Centrum IoT Azure?](iot-hub-what-is-iot-hub.md)

## <a name="free-account"></a>Bezpłatne konto
Można utworzyć [bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) toocomplete hello samouczki Centrum IoT i eksperymentować hello usługi IoT Hub (i innych usług Azure).

## <a name="gateway"></a>Brama
Brama umożliwia łączność urządzeń, które nie może połączyć bezpośrednio za[Centrum IoT](#iot-hub). Zobacz też [pola bramy](#field-gateway), [chmury bramy](#cloud-gateway), i [bram](#custom-gateway).

## <a name="identity-registry"></a>Tożsamość rejestru
Witaj [rejestru tożsamości](iot-hub-devguide-identity-registry.md) jest wbudowany składnik Centrum IoT, która przechowuje informacje o poszczególnych urządzeniach hello hello dozwolone Centrum IoT tooan tooconnect.

## <a name="interactive-message"></a>Interakcyjne wiadomości
Interakcyjne komunikat [chmury do urządzenia](#cloud-to-device) komunikat, który wyzwala natychmiastowych akcji w zaplecza rozwiązania hello. Na przykład urządzenie może wysyłać alarmu o niepowodzeniu, które powinny być automatycznie rejestrowane w tooa systemu CRM.

## <a name="iot-hub"></a>Usługa IoT Hub
Centrum IoT to w pełni zarządzana usługa platformy Azure, co umożliwia komunikację dwukierunkową i niezawodności między milionów urządzeń, a zaplecze rozwiązania. Aby uzyskać więcej informacji, zobacz [co to jest Centrum IoT Azure?](iot-hub-what-is-iot-hub.md) Przy użyciu programu [subskrypcji platformy Azure](#subscription), można utworzyć toohandle centra IoT z IoT wiadomości obciążeń.

## <a name="iot-hub-metrics"></a>Metryki Centrum IoT
[Centrum IoT metryki](iot-hub-metrics.md) udostępnia dane o stanie hello centra IoT hello w Twojej [subskrypcji platformy Azure](#subscription). Włącz metryki Centrum IoT można tooassess hello ogólną kondycję hello usługi i urządzenia hello połączone tooit. Metryki Centrum IoT ułatwiają Zobacz, co dzieje się z Centrum IoT i badania głównej przyczyny problemów bez konieczności toocontact pomocy technicznej platformy Azure.

## <a name="iot-hub-query-language"></a>Język zapytań Centrum IoT
Hello [język zapytań Centrum IoT](iot-hub-devguide-query-language.md) jest języka przypominającego SQL, która umożliwia tooquery Twojego [zadania](#job) i twins urządzenia.

## <a name="iot-hub-resource-provider-rest-api"></a>Dostawca zasobów Centrum IoT interfejsu API REST
Można użyć hello [interfejsu API REST dostawcy zasobów Centrum IoT](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage centra IoT hello w Twojej [subskrypcji platformy Azure](#subscription) wykonywania operacji, takich jak tworzenie, aktualizowanie i Usuwanie koncentratorów.

## <a name="iot-suite"></a>Pakiet IoT
Pakiet Azure IoT pakiety ze sobą wiele usług platformy Azure z wstępnie skonfigurowanych rozwiązań. Te wstępnie skonfigurowanych rozwiązań Włącz tooget szybko rozpocząć z implementacjami na trasie o typowych scenariuszach IoT. Aby uzyskać więcej informacji, zobacz [co to jest pakiet IoT Azure?](../iot-suite/iot-suite-overview.md)

## <a name="iothub-explorer"></a>Eksplorator Centrum iothub
Witaj [explorer Centrum iothub](https://github.com/azure/iothub-explorer) to narzędzie i platform, wiersza polecenia. Narzędzie Hello umożliwia możesz toomanage urządzeń w hello [rejestru tożsamości](#identity-registry), wysyłania i odbierania wiadomości oraz pliki z urządzeń i monitorować działania Centrum IoT.

## <a name="job"></a>Zadanie
Można użyć z zaplecza rozwiązania [zadania](iot-hub-devguide-jobs.md) tooschedule i śledzenie działań na zbiór urządzeń zarejestrowanych w Centrum IoT. Działania obejmują aktualizowanie urządzenia dwie [żądanego właściwości](#desired-properties), aktualizowania dwie urządzenia [tagi](#tags)i wywoływanie [bezpośrednie metody](#direct-method). [Centrum IoT](#iot-hub) używa również zadania zbyt[import eksport tooand](iot-hub-devguide-identity-registry.md#import-and-export-device-identities) z hello [rejestru tożsamości](#identity-registry).

## <a name="jobs-rest-api"></a>Zadania interfejsu API REST
Witaj [interfejsu API REST zadania](https://docs.microsoft.com/rest/api/iothub/jobapi) pozwala toomanage [zadania](#job) uruchomiona w Centrum IoT.

## <a name="module"></a>Moduł
W [Azure IoT krawędzi](iot-hub-linux-iot-edge-get-started.md), [modułu](iot-hub-linux-iot-edge-get-started.md) jest składnikiem, który wykonuje określone zadanie. Zadania mogą obejmować wprowadzania komunikatu z urządzenia, przekształcanie wiadomości lub wysyłania z Centrum IoT tooan wiadomości. Broker jest odpowiedzialny za przesyłanie dalej wiadomości między modułami. Azure IoT krawędzi obejmuje zestaw modułów próbki. Można również utworzyć niestandardowe moduły.

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/) jest jedną z wiadomości powitania protokołów, które [Centrum IoT](#iot-hub) obsługuje do komunikowania się z urządzeniami. Aby uzyskać więcej informacji na temat hello protokoły, które obsługuje Centrum IoT obsługi komunikatów, zobacz [wysyłania i odbierania wiadomości z Centrum IoT](iot-hub-devguide-messaging.md).

## <a name="operations-monitoring"></a>Monitorowanie operacji
Centrum IoT [operacje monitorowania](iot-hub-operations-monitoring.md) pozwala toomonitor hello stanu operacji w Centrum IoT w czasie rzeczywistym. [Centrum IoT](#iot-hub) śledzi zdarzenia przez różne kategorie działań. Można włączyć do wysyłania zdarzeń z tooan kategorii co najmniej jednego punktu końcowego Centrum IoT do przetwarzania. Możesz monitorować dane hello błędów lub konfigurowanie bardziej złożonych przetwarzania na podstawie wzorców danych.

## <a name="physical-device"></a>Urządzenie fizyczne
Urządzenie fizyczne jest prawdziwe urządzeniami, takimi jak Pi malina, który łączy tooan Centrum IoT. Dla wygody wiele samouczki Centrum IoT hello użyj [symulowane urządzeń](#simulated-device) tooenable przykłady toorun należy na komputerze lokalnym.

## <a name="primary-and-secondary-keys"></a>Klucze podstawowe i pomocnicze
Po podłączeniu urządzenia połączonej tooa lub punktu końcowego usługi połączonej w Centrum IoT z [ciąg połączenia](#connection-string) obejmuje toogrant klucza, możesz uzyskać dostępu do. Po dodaniu toohello urządzenia [rejestru tożsamości](#identity-registry) lub Dodaj [udostępnionych zasad dostępu](#shared-access-policy) tooyour koncentratora, usługa hello generuje klucza podstawowego i pomocniczego. Mając dwa klucze pozwala tooroll za pośrednictwem z jednego klucza tooanother po zaktualizowaniu klucza bez utraty Centrum IoT toohello dostępu.

## <a name="protocol-gateway"></a>Brama protokołu
Brama protokołu zwykle jest wdrażana w chmurze hello i zapewnia protokół usługi tłumaczeniowe w przypadku urządzeń łączących się za[Centrum IoT](#iot-hub). Aby uzyskać więcej informacji, zobacz [co to jest Centrum IoT Azure?](iot-hub-what-is-iot-hub.md)

## <a name="quotas-and-throttling"></a>Limity przydziału i ograniczanie wydajności
Istnieją różne [przydziały](iot-hub-devguide-quotas-throttling.md) , stosowane użycie tooyour [Centrum IoT](#iot-hub), duża liczba hello różne przydziały oparte na powitania warstwy hello Centrum IoT. [Centrum IoT](#iot-hub) ma również zastosowanie [ogranicza](iot-hub-devguide-quotas-throttling.md) tooyour użycie usługi hello w czasie wykonywania.

## <a name="reported-configuration"></a>Zgłoszony konfiguracji
W kontekście hello [dwie urządzenia](iot-hub-devguide-device-twins.md), zgłoszone konfiguracji odwołuje się toohello pełny zestaw właściwości i metadanych w hello dwie urządzenia, które powinny być raportowane zaplecza rozwiązania toohello.

## <a name="reported-properties"></a>Zgłoszony właściwości
W kontekście hello [dwie urządzenia](iot-hub-devguide-device-twins.md), zgłosiła właściwości jest podciągiem Witaj dwie urządzenia używane z [żądanego właściwości](#desired-properties) toosynchronize konfiguracji urządzenia lub warunku. Zgłoszone właściwości można ustawić tylko przez hello [aplikacji urządzenia](#device-app) i może odczytywać i sprawdzać za [zaplecza aplikacji](#back-end-app).

## <a name="resource-group"></a>Grupa zasobów
[Usługa Azure Resource Manager](#azure-resource-manager) toogroup grup zasobów używa ze sobą powiązane zasoby. Można jednocześnie używać operacji tooperform grupy zasobów, na wszystkich zasobów hello na powitania grupy.

## <a name="retry-policy"></a>Zasady ponawiania
Użyj toohandle zasady ponawiania [błędów przejściowych](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx) podczas łączenia tooa usługi w chmurze.

## <a name="routing-rules"></a>Reguły routingu
Możesz skonfigurować [reguły routingu](iot-hub-devguide-messages-read-custom.md) w Twojej IoT hub tooroute wiadomości urządzenia do chmury tooa [wbudowanym punktem końcowym](#built-in-endpoints) lub zbyt[niestandardowe punkty końcowe](#custom-endpoints) do przetworzenia przez kopii rozwiązania Zakończenie.

## <a name="sasl-plain"></a>ZWYKŁY SASL
ZWYKŁY SASL to protokół, który hello [AMQP](#advanced-message-queue-protocol) protokół używa tootransfer tokenów zabezpieczających.

## <a name="shared-access-signature"></a>Sygnatury dostępu współdzielonego
Udostępniony sygnatur dostępu (SAS) są mechanizmu uwierzytelniania na podstawie bezpiecznego wartości skrótu SHA-256 lub identyfikatorów URI. Uwierzytelniania sygnatury dostępu Współdzielonego ma dwa składniki: _zasad dostępu współużytkowanego_ i _sygnatura dostępu współdzielonego_ (często nazywane token). Urządzenie korzysta SAS tooauthenticate z Centrum IoT. [Aplikacje zaplecza](#back-end-app) za pomocą sygnatury dostępu Współdzielonego tooauthenticate hello połączonej usługi punkty końcowe Centrum IoT. Zwykle zawierają hello tokenu sygnatury dostępu Współdzielonego w hello [ciąg połączenia](#connection-string) że aplikacja korzysta z tooestablish Centrum IoT tooan połączenia.

## <a name="shared-access-policy"></a>Zasady dostępu współużytkowanego
Zasady dostępu współdzielonego definiuje hello uprawnienia tooanyone, który ma prawidłowy [klucz podstawowy lub pomocniczy](#primary-and-secondary-keys) skojarzone z tej zasady. Można zarządzać hello udostępnionych zasady dostępu i klucze Centrum w hello [portal](#azure-portal).

## <a name="simulated-device"></a>Symulowane urządzenie
Dla wygody wiele hello używanego przez Centrum IoT samouczki symulowane tooenable urządzeń możesz toorun przykłady na komputerze lokalnym. Z kolei [urządzenie fizyczne](#physical-device) jest prawdziwe urządzeniami, takimi jak Pi malina, który łączy tooan Centrum IoT.

## <a name="solution"></a>Rozwiązanie
A _rozwiązania_ mogą odwoływać się tooa rozwiązania Visual Studio, który zawiera jeden lub więcej projektów. A _rozwiązania_ może również znaleźć rozwiązania IoT tooan, który zawiera elementy, takie jak urządzenia, [aplikacji dla urządzeń](#device-app), Centrum IoT, innymi usługami platformy Azure i [zaplecza aplikacji](#back-end-app).

## <a name="subscription"></a>Subskrypcja
Jeśli karta ma miejsce jest subskrypcja platformy Azure. Tworzenie każdego zasobów platformy Azure lub usługi Azure, którego używasz jest skojarzony z jedną subskrypcją. Wiele przydziały mają zastosowanie również na poziomie hello subskrypcji.

## <a name="system-properties"></a>Właściwości systemu
W kontekście hello [dwie urządzenia](iot-hub-devguide-device-twins.md), system właściwości tylko do odczytu i zawierają informacje na temat użycia urządzenia hello takich jak ostatni stan połączenia i czasu działania.

## <a name="tags"></a>Tagi
W kontekście hello [dwie urządzenia](iot-hub-devguide-device-twins.md), tagi są metadane urządzenia przechowywane i pobierane przez hello zaplecza rozwiązania w postaci hello dokumentu JSON. Tagi nie są widoczne tooapps na urządzeniu.

## <a name="telemetry"></a>Telemetria
Urządzenia zbierania danych telemetrycznych, takich jak szybkości knie lub temperatury i użyj [punktu danych wiadomości](#data-point-messages) Centrum IoT tooan toosend hello telemetrii.

## <a name="token-service"></a>Usługa tokenu
Można użyć tooimplement usługi tokenu mechanizmu uwierzytelniania urządzeń. Używa Centrum IoT [udostępnionych zasad dostępu](#shared-access-policy) z **DeviceConnect** toocreate uprawnienia *zakres urządzeń* tokenów. Tokeny te umożliwiają Centrum IoT tooyour tooconnect urządzenia. Urządzenie korzysta tooauthenticate mechanizmu uwierzytelniania niestandardowego z usługą tokenu hello. Jeśli urządzenie hello uwierzytelnia się pomyślnie, usługi tokenu hello wystawia token sygnatury dostępu Współdzielonego dla hello urządzenia toouse tooaccess Centrum IoT.

## <a name="x509-client-certificate"></a>Certyfikat klienta X.509
Urządzenie może używać tooauthenticate certyfikatu X.509 z [Centrum IoT](#iot-hub). Za pomocą certyfikatu X.509 jest alternatywnych toousing [tokenu sygnatury dostępu Współdzielonego](#shared-access-signature).
