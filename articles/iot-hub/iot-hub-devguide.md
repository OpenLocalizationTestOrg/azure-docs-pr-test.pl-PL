---
title: Centrum IoT Azure w przewodniku aaaDeveloper | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera usługi Azure IoT Hub Hello omówiono punktów końcowych, zabezpieczeń, hello rejestru tożsamości, zarządzanie urządzeniami, bezpośrednie metody, twins urządzenia, przekazywania plików, zadania, hello język zapytań Centrum IoT i wiadomości."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Przewodnik dewelopera Centrum IoT Azure

Centrum IoT Azure jest w pełni zarządzaną usługę, która umożliwia włączanie i niezawodności komunikację dwukierunkową między milionów urządzeń i zaplecze rozwiązania.

Centrum IoT Azure oferuje:

* Bezpieczna komunikacja przy użyciu poświadczeń zabezpieczeń urządzenia i kontrola dostępu.
* Wiele opcji komunikacji hiperskali urządzenia do chmury i chmury do urządzenia.
* Kolejność przechowywania informacji o stanie na urządzenie i metadanych.
* Łatwe urządzenia łączność z bibliotekami urządzenia dla hello najbardziej popularnych języków i platform.

Ten przewodnik dewelopera Centrum IoT zawiera hello następujące artykuły:

* [Wskazówki dotyczące komunikacji urządzenia do chmury] [ lnk-d2c-guidance] ułatwia wybór między wiadomości urządzenia do chmury, dwie urządzenia zgłoszonego właściwości i przekazywania pliku.
* [Wskazówki dotyczące komunikacji chmury do urządzenia] [ lnk-c2d-guidance] ułatwia wybór między metody bezpośredniego, odpowiednie właściwości dwie urządzenia i komunikaty chmury do urządzenia.
* [Urządzenia do chmury i wiadomości z Centrum IoT chmury do urządzenia] [ devguide-messaging] opisuje hello komunikatów funkcje (urządzenia do chmury i chmury do urządzenia) udostępnia Centrum IoT.
  * [Wysyłanie wiadomości urządzenia do chmury tooIoT Centrum][devguide-messages-d2c].
  * [Odczytywać wiadomości urządzenia do chmury z wbudowanym punktem końcowym hello][devguide-builtin].
  * [Użyj niestandardowe punkty końcowe i reguły routingu dla komunikatów urządzenia do chmury][devguide-custom].
  * [Wysyłanie wiadomości chmury do urządzenia z Centrum IoT][devguide-messages-c2d].
  * [Tworzenie i odczytywanie wiadomości Centrum IoT][devguide-format].
* [Przekazywanie plików z urządzenia] [ devguide-upload] w tym artykule opisano, jak można przekazać pliki z urządzenia. Hello artykuł zawiera także informacje dotyczące hello się, że procesu przekazywania hello powiadomienia mogą wysyłać.
* [Zarządzanie tożsamościami urządzenie w Centrum IoT] [ devguide-identities] opisuje jakie informacje o każdej Centrum IoT magazyny rejestru tożsamości i jak można uzyskać dostęp i zmodyfikować go.
* [Kontrolowanie dostępu tooIoT Centrum] [ devguide-security] opisano hello zabezpieczeń modelu używanego toogrant tooIoT Centrum funkcje dostępu dla urządzenia i składniki w chmurze. Hello artykuł zawiera informacje dotyczące używania tokenów i certyfikaty X.509 i szczegóły hello uprawnień, które mogą udzielać dostępu.
* [Stan toosynchronize twins urządzenia i konfiguracje] [ devguide-device-twins] opisuje hello *dwie urządzenia* koncepcji i hello funkcji eksponuje takich jak synchronizowanie urządzenia z urządzenia dwie. Witaj artykuł zawiera informacje na temat hello danych przechowywanych w dwie urządzenia.
* [Wywoływanie metody bezpośrednio na urządzeniu] [ devguide-directmethods] opisuje hello cyklem życia metoda bezpośrednia informacji na temat sposobu metody tooinvoke na urządzeniu z zaplecza hello aplikacji i uchwytem metoda bezpośrednia na urządzeniu.
* [Planowanie zadań na wielu urządzeniach] [ devguide-jobs] zawiera opis sposobu tworzenia harmonogramu zadań na wielu urządzeniach. Witaj artykule opisano sposób toosubmit zadań wykonywanie zadań wykonywania metoda bezpośrednia aktualizacja urządzenia przy użyciu podwójnego urządzenia. Opisuje również, jak tooquery hello stanu zadania.
* [Odwołanie — wybierz protokół komunikacyjny] [ devguide-protocol] opisuje hello protokołów komunikacyjnych, że Centrum IoT do komunikacji urządzeń i obsługuje listy hello porty, które powinno być otwarte.
* [Odwołanie — punkty końcowe Centrum IoT] [ devguide-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji obsługi i zarządzania. Witaj opisano również sposób możesz utworzyć dodatkowe punkty końcowe w Centrum IoT i w jaki sposób toouse pola bramy tooenable urządzeń łączności tooyour Centrum IoT punktów końcowych w scenariuszach niestandardowym.
* [Odwołanie - Centrum IoT zapytania języka twins urządzenia, zadania i rozsyłania wiadomości] [ devguide-query] opisuje tego języka zapytań Centrum IoT, umożliwiający tooretrieve informacje z Centrum zadań i twins urządzenia.
* [Odwołanie - przydziały i ograniczenia przepustowości] [ devguide-quotas] podsumowuje przydziały hello w hello usługi IoT Hub i hello ograniczania zachowanie można oczekiwać, że toosee przekracza limit przydziału.
* [Odwołanie — cennik] [ devguide-pricing] zawiera ogólne informacje dotyczące różnych jednostki SKU i cenach dla Centrum IoT i szczegółowe informacje o sposobie hello różne funkcje Centrum IoT są mierzone jako wiadomości przez Centrum IoT.
* [Odwołanie - urządzeń i usług zestawów SDK] [ devguide-sdks] list hello Azure IoT SDK można użyć toodevelop aplikacji usług i urządzeń, które współdziałają z Centrum IoT. Artykuł Hello zawiera dokumentacja interfejsu API tooonline łącza.
* [Odwołanie — Obsługa MQTT Centrum IoT] [ devguide-mqtt] zawiera szczegółowe informacje o sposobie obsługi protokołu MQTT hello w Centrum IoT. Hello artykule opisano obsługę hello wbudowanych toohello protokołu MQTT hello Azure IoT SDK i zawiera informacje dotyczące używania protokołu MQTT hello bezpośrednio.
* [Słownik] [ devguide-glossary] listę typowe terminy związane z Centrum IoT.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
