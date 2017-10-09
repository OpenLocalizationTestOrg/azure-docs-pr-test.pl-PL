---
title: "wskazówki rozwiązania pakiet IoT Azure fabryki aaaConnected | Dokumentacja firmy Microsoft"
description: "Opis hello Azure IoT wstępnie skonfigurowane rozwiązanie połączone architektura jej i fabryki."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki

Witaj pakiet IoT połączone fabryki [wstępnie skonfigurowane rozwiązanie] [ lnk-preconfigured-solutions] jest implementacją rozwiązania przemysłowych end-to-end który:

* Łączy tooboth symulowane urządzeń przemysłowych uruchamiania OPC UA serwerów w wierszach produkcji symulowane fabryki i rzeczywistego urządzenia server OPC UA. Aby uzyskać więcej informacji na temat OPC UA Zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).
* Pokazuje operacyjne kluczowe wskaźniki wydajności oraz ogólną wydajność sprzętu dla tych urządzeń i linii produkcyjnych.
* Pokazuje, jak można toointeract używanych w systemach server OPC UA aplikacji opartej na chmurze.
* Umożliwia tooconnect możesz własnych urządzeń serwera OPC UA.
* Umożliwia toobrowse i zmodyfikuj hello OPC UA danych serwera.
* Integruje się z hello Azure czas serii Insights (TSI) usługi tooprovide niestandardowych widoków danych hello z serwerów OPC UA.

Za pomocą hello rozwiązania jako punkt początkowy dla własnego implementacji i [dostosować] [ lnk-customize] on toomeet własnych konkretnych potrzeb biznesowych.

W tym artykule przedstawiono niektóre kluczowe elementy hello hello połączone fabryki rozwiązania tooenable toounderstand jej działania. Ta wiedza ułatwi Ci:

* Rozwiązywanie problemów w rozwiązaniu hello.
* Planowanie sposobu toocustomize toohello rozwiązania toomeet indywidualnymi wymaganiami.
* Projektowanie własnego rozwiązania IoT korzystającego z usług Azure.

Aby uzyskać więcej informacji, zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Architektura logiczna

powitania po diagram przedstawia hello logiczne składniki hello wstępnie skonfigurowane rozwiązanie:

![Architektura logiczna połączonej fabryki][connected-factory-logical]

## <a name="communication-patterns"></a>Wzorce komunikacji

rozwiązanie Hello używa hello [specyfikacji UA OPC Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT danych telemetrycznych OPC UA Centrum w formacie JSON. rozwiązanie Hello używa hello [wydawcy OPC](https://github.com/Azure/iot-edge-opc-publisher) krawędzi IoT modułu, w tym celu.

rozwiązanie Hello ma również klienta OPC UA zintegrowany z aplikacją sieci web, który może nawiązywać połączenia z serwerami lokalnymi OPC UA. Witaj, klient używa [wstecznego serwera proxy](https://wikipedia.org/wiki/Reverse_proxy) i odbiera pomocy z Centrum IoT toomake hello połączenia bez konieczności otwartych portów w zaporze lokalne powitania. Ten wzorzec komunikacji jest zwany [komunikacją wspieraną przez usługę](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). rozwiązanie Hello używa hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) krawędzi IoT modułu, w tym celu.


## <a name="simulation"></a>Symulacja

Witaj symulowane stacji i wykonywania produkcyjnym hello symulowane systemów (rynkowej) tworzą wiersza produkcyjnym fabryki. Witaj symulowanego urządzenia i hello modułu wydawcy OPC są oparte na powitania [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] opublikowanych przez hello OPC Foundation.

Witaj OPC serwera Proxy i OPC wydawcy są zaimplementowane jako modułów na podstawie [Azure IoT krawędzi][lnk-Azure-IoT-Gateway]. Każda symulowana linia produkcyjna ma dołączoną wyznaczoną bramę.

Wszystkie składniki symulacji działają w kontenerach platformy Docker hostowanych na maszynie wirtualnej platformy Azure z systemem Linux. symulacji Hello jest skonfigurowany toorun osiem symulowane wiersze produkcji domyślnie.

## <a name="simulated-production-line"></a>Symulowana linia produkcyjna

Na linii produkcyjnej są produkowane części. Składa się ona z różnych stacji: stacji montażowej, stacji testowania i stacji pakowania.

Symulacja Hello uruchamia i aktualizuje dane hello udostępniane za pośrednictwem hello OPC UA węzłów. Wszystkie stacje symulowane wiersza produkcyjnym są zorkiestrowana przez hello rynkowej za pośrednictwem OPC UA.

## <a name="simulated-manufacturing-execution-system"></a>Symulowany system zarządzania produkcją

Witaj rynkowej monitoruje każdej stacji wiersza produkcyjnym hello za pośrednictwem zmiany stanu stacji toodetect OPC UA. Wywołuje OPC UA metody toocontrol hello stacji, a przekazuje produktu z jednej stacji toohello dalej do czasu ukończenia.

## <a name="gateway-opc-publisher-module"></a>Moduł wydawcy OPC bramy

Moduł wydawcy OPC łączy toohello stacji OPC UA serwery i subskrybuje toobe węzłów OPC toohello opublikowane. Moduł Hello konwertuje hello węzeł danych do formatu JSON, szyfruje go i wysyła tooIoT koncentratora jako OPC UA Pub/komunikatów.

Moduł wydawcy OPC Hello tylko wymaga port wychodzący protokołu https (port 443) i może współpracować z istniejącej infrastruktury przedsiębiorstwa.

## <a name="gateway-opc-proxy-module"></a>Moduł serwera proxy OPC bramy

Hello modułu Proxy UA OPC bramy tuneli binarne OPC UA polecenia i kontroli wiadomości i wymaga tylko port wychodzący protokołu https (port 443). Może on współdziałać z istniejącą infrastrukturą przedsiębiorstwa, w tym z internetowymi serwerami proxy.

Używa urządzenia IoT Hub metody tootransfer packetized TCP/IP danych w warstwie aplikacji hello, a w związku z tym zapewnia punkt końcowy relacji zaufania, szyfrowania danych i integralności przy użyciu protokołu SSL/TLS.

Hello OPC UA protokołu binarnego przekazywane za pośrednictwem serwera proxy hello, sama używa UA uwierzytelniania i szyfrowania.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Witaj bramy OPC wydawcy modułu subskrybuje tooOPC UA serwera węzłów toodetect zmianę hello wartości danych. W przypadku wykrycia zmian danych w jednym z węzłów hello, ten moduł następnie wysyła komunikaty tooAzure Centrum IoT.

Centrum IoT zapewnia tooAzure źródła zdarzeń TSI. TSI magazynów danych przez 30 dni, w oparciu sygnatury czasowe podłączonych toohello wiadomości. Te dane obejmują:

* Identyfikator ApplicationUri serwera OPC UA
* Identyfikator NodeId serwera OPC UA
* Wartość węzła hello
* Sygnaturę czasową źródła
* Nazwę DisplayName serwera OPC UA

Obecnie TSI nie zezwala klientom toocustomize, jak długo życzą tookeep hello danych.

Usługa TSI przesyła zapytania o dane węzła przy użyciu funkcji SearchSpan (Time.From, Time.To) i agreguje je według identyfikatora ApplicationUri, NodeId lub nazwy DisplayName serwera OPC UA.

tooretrieve hello danych hello mierników OEE i wskaźnik KPI i hello czasu serii wykresów są agregowane przez liczbę zdarzeń, Sum, Avg, Min i Max.

szeregów czasowych Hello są tworzone za pomocą innego procesu. OEE i wskaźników KPI są obliczane na podstawie danych podstawowych stacji i przepuszcza dla topologii hello (wiersze produkcji, fabryki, enterprise) w aplikacji hello.

Ponadto szeregów czasowych dla topologii OEE i wskaźnik KPI jest obliczana w aplikacji hello zawsze, gdy obiekt timespan wyświetlane jest gotowy. Na przykład widok dzisiaj hello jest aktualizowany co godzinę pełna.

Widok serii czasu Hello danych węzła pochodzi bezpośrednio z TSI przy użyciu agregacji dla timespan.

## <a name="iot-hub"></a>Usługa IoT Hub
Witaj [Centrum IoT] [ lnk-IoT Hub] odbiera dane przesyłane z hello OPC wydawcy modułu w chmurze hello i ułatwia usługi Azure TSI toohello dostępne. 

Witaj Centrum IoT w rozwiązaniu hello również:
- Przechowuje rejestr tożsamości, który przechowuje hello identyfikatorów dla wszystkich modułów wydawcy OPC i wszystkich modułów Proxy OPC.
- Jest używany jako kanał transportu dla komunikacji dwukierunkowej hello OPC modułu Proxy.

## <a name="azure-storage"></a>Azure Storage
rozwiązanie Hello używa magazynu obiektów blob platformy Azure jako magazynu danych na dysku dla danych wdrażania maszyny Wirtualnej i toostore hello.

## <a name="web-app"></a>Aplikacja internetowa
Aplikacja sieci web Hello wdrożony jako część hello wstępnie skonfigurowane rozwiązanie obejmuje zintegrowanym klientem OPC UA, przetwarzania alertów i wizualizacja danych telemetrycznych.

## <a name="next-steps"></a>Następne kroki

Aby kontynuować, wprowadzenie pakiet IoT odczytując hello następujące artykuły:

* [Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]
* [Wdrożyć bramę Windows lub Linux hello połączone fabryki wstępnie rozwiązania](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
