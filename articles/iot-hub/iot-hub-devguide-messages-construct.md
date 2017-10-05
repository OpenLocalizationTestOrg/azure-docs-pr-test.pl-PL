---
title: Zrozumienie format komunikatu Centrum IoT Azure | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — w tym formacie i oczekiwanej zawartości wiadomości Centrum IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: e6eafb1a0030b022da2b5d0b787e092f3067c99f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Tworzenie i odczytywanie wiadomości Centrum IoT

Aby obsługiwać bezproblemowe współdziałanie różnych protokołów, Centrum IoT definiuje wspólne format komunikatu do wszystkich protokołów skierowane do urządzenia. Ten format komunikatu jest używana zarówno dla [urządzenia do chmury] [ lnk-d2c] i [chmury do urządzenia] [ lnk-c2d] wiadomości. [Komunikat Centrum IoT] [ lnk-messaging] obejmuje:

* Zestaw *właściwości systemu*. Właściwości, które będą interpretowane przez Centrum IoT, i ustawia. Ten zestaw jest wcześniej.
* Zestaw *właściwości aplikacji*. Słownik właściwości ciągu, definiujące aplikacji i dostępu, bez konieczności wykonywania deserializacji treści komunikatu. Centrum IoT nigdy nie modyfikuje tych właściwości.
* Nieprzezroczysta treść binarnego.

Nazwy i wartości właściwości mogą zawierać tylko znaki alfanumeryczne ASCII, oraz ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`` podczas możesz:

* Wysyłanie wiadomości urządzenia do chmury przy użyciu protokołu HTTP.
* Wysyłanie wiadomości chmury do urządzenia.

Aby uzyskać więcej informacji na temat kodowania i dekodowania wiadomości wysłane przy użyciu różnych protokołów, zobacz [Azure IoT SDK][lnk-sdks].

Poniższa lista zawiera zbiór właściwości systemu w komunikatach Centrum IoT.

| Właściwość | Opis |
| --- | --- |
| Identyfikator komunikatu |Identyfikator użytkownika można ustawić dla komunikatu używanego dla wzorców żądanie odpowiedź. Format: Wielkość liter ciąg (maksymalnie 128 znaków) znaki alfanumeryczne ASCII 7-bitowego + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Numer sekwencyjny |Liczba (unikatowy dla urządzenia kolejki) przypisywany przez Centrum IoT do każdej wiadomości chmury do urządzenia. |
| Do |Miejsca docelowego określonego w [chmury do urządzenia] [ lnk-c2d] wiadomości. |
| ExpiryTimeUtc |Data i godzina wygaśnięcia wiadomości. |
| EnqueuedTime |Data i godzina [chmury do urządzenia] [ lnk-c2d] wiadomość została odebrana przez Centrum IoT. |
| CorrelationId |Właściwości ciągu w komunikacie odpowiedzi, zazwyczaj zawierający identyfikator komunikatu żądania wzorce żądanie odpowiedź. |
| Nazwa użytkownika |Identyfikator używany do określenia pochodzenia wiadomości. Komunikaty są generowane przez Centrum IoT, jest ustawiona `{iot hub name}`. |
| ACK. |Generator komunikat opinii. Ta właściwość jest używana w komunikatach chmury do urządzenia do Centrum IoT można wygenerować opinii komunikaty w wyniku użycia komunikatu żądania przez urządzenie. Możliwe wartości: **Brak** (domyślnie): żaden komunikat opinii jest generowany, **dodatnią**: Jeśli wiadomość została ukończona, wyświetlony komunikat opinii **ujemna**: odbierania wiadomość wygasł (lub osiągnięto dostarczania maksymalna liczba) bez przez urządzenia, lub **pełne**: zarówno dodatnie i ujemne. Aby uzyskać więcej informacji, zobacz [komunikatu opinii][lnk-feedback]. |
| ConnectionDeviceId |Identyfikator ustawione przez Centrum IoT na wiadomości urządzenia do chmury. Zawiera on **deviceId** urządzenia wysyłającego wiadomość. |
| ConnectionDeviceGenerationId |Identyfikator ustawione przez Centrum IoT na wiadomości urządzenia do chmury. Zawiera on **generationId** (zgodnie [właściwości tożsamości urządzenia][lnk-device-properties]) urządzenia, która wysłała wiadomość. |
| ConnectionAuthMethod |Metoda uwierzytelniania, ustawione przez Centrum IoT na wiadomości urządzenia do chmury. Ta właściwość zawiera informacje na temat metody uwierzytelniania używany do uwierzytelniania urządzeń wysyłania wiadomości. Aby uzyskać więcej informacji, zobacz [urządzenia do chmury ochrony przed fałszowaniem][lnk-antispoofing]. |

## <a name="message-size"></a>Rozmiar komunikatu

Centrum IoT mierzy rozmiar wiadomości w sposób niezależny od protokołu, biorąc pod uwagę rzeczywiste ładunku. Wyrażony w bajtach rozmiar jest obliczany jako sumę następujących elementów:

* Treść rozmiar w bajtach.
* Rozmiar w bajtach wszystkich wartości właściwości systemu wiadomości.
* Rozmiar w bajtach wszystkich użytkownika nazwy i wartości właściwości.

Nazwy i wartości właściwości są ograniczone do znaków ASCII, dlatego rozmiar w bajtach równa długość ciągów.

## <a name="next-steps"></a>Następne kroki

Uzyskać informacji na temat limitów rozmiarów wiadomości w Centrum IoT, zobacz [przydziały Centrum IoT i ograniczania przepustowości][lnk-quotas].

Aby dowiedzieć się, jak utworzyć i odczytywać wiadomości w różnych językach programowania Centrum IoT, zobacz [wprowadzenie] [ lnk-get-started] samouczki.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
