---
title: format komunikatu Centrum IoT Azure aaaUnderstand | Dokumentacja firmy Microsoft
description: "Przewodnik dewelopera — tym hello format i oczekiwanej zawartości wiadomości Centrum IoT."
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
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Tworzenie i odczytywanie wiadomości Centrum IoT

bezproblemowe współdziałanie toosupport różnych protokołów, Centrum IoT definiuje wspólne format komunikatu do wszystkich protokołów skierowane do urządzenia. Ten format komunikatu jest używana zarówno dla [urządzenia do chmury] [ lnk-d2c] i [chmury do urządzenia] [ lnk-c2d] wiadomości. [Komunikat Centrum IoT] [ lnk-messaging] obejmuje:

* Zestaw *właściwości systemu*. Właściwości, które będą interpretowane przez Centrum IoT, i ustawia. Ten zestaw jest wcześniej.
* Zestaw *właściwości aplikacji*. Słownik właściwości ciągu, definiujące aplikacji hello i dostępu, bez konieczności treści wiadomości powitania toodeserialize. Centrum IoT nigdy nie modyfikuje tych właściwości.
* Nieprzezroczysta treść binarnego.

Nazwy i wartości właściwości mogą zawierać tylko znaki alfanumeryczne ASCII, oraz ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`` podczas możesz:

* Wysyłanie wiadomości urządzenia do chmury przy użyciu protokołu HTTP hello.
* Wysyłanie wiadomości chmury do urządzenia.

Aby uzyskać więcej informacji o tym, jak tooencode i dekodowania wiadomości wysłane przy użyciu różnych protokołów, zobacz [Azure IoT SDK][lnk-sdks].

Witaj w poniższej tabeli wymieniono hello zbiór właściwości systemu w komunikatach Centrum IoT.

| Właściwość | Opis |
| --- | --- |
| Identyfikator komunikatu |Identyfikator użytkownika można ustawić wiadomość hello używane w przypadku wzorców żądanie odpowiedź. Format: Wielkość liter ciąg (up too128 znaków) znaki alfanumeryczne ASCII 7-bitowego + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Numer sekwencyjny |Numer (unikatowy dla urządzenia kolejki) przypisany przez komunikatu chmura urządzenie tooeach Centrum IoT. |
| zbyt|Miejsca docelowego określonego w [chmury do urządzenia] [ lnk-c2d] wiadomości. |
| ExpiryTimeUtc |Data i godzina wygaśnięcia wiadomości. |
| EnqueuedTime |Data i godzina hello [chmury do urządzenia] [ lnk-c2d] wiadomość została odebrana przez Centrum IoT. |
| CorrelationId |Właściwości ciągu w komunikacie odpowiedzi, zazwyczaj zawierający identyfikator komunikatu żądania hello wzorce "żądanie-odpowiedź" hello. |
| Nazwa użytkownika |Identyfikator używany toospecify hello pochodzenia wiadomości. Gdy komunikaty są generowane przez Centrum IoT, ustawiono zbyt`{iot hub name}`. |
| ACK. |Generator komunikat opinii. Ta właściwość jest używana w wiadomości chmury do urządzenia toorequest Centrum IoT toogenerate opinii komunikaty w wyniku użycia hello wiadomość hello hello urządzeń. Możliwe wartości: **Brak** (domyślnie): żaden komunikat opinii jest generowany, **dodatnią**: Jeśli wiadomość hello została ukończona, wyświetlony komunikat opinii **ujemna**: odbierania wiadomość ważność wiadomości powitania (lub osiągnięto dostarczania maksymalna liczba) bez przez urządzenie hello lub **pełne**: zarówno dodatnie i ujemne. Aby uzyskać więcej informacji, zobacz [komunikatu opinii][lnk-feedback]. |
| ConnectionDeviceId |Identyfikator ustawione przez Centrum IoT na wiadomości urządzenia do chmury. Zawiera on hello **deviceId** hello urządzenia, który wysłał wiadomość hello. |
| ConnectionDeviceGenerationId |Identyfikator ustawione przez Centrum IoT na wiadomości urządzenia do chmury. Zawiera on hello **generationId** (zgodnie [właściwości tożsamości urządzenia][lnk-device-properties]) urządzenia hello, który wysłał wiadomość hello. |
| ConnectionAuthMethod |Metoda uwierzytelniania, ustawione przez Centrum IoT na wiadomości urządzenia do chmury. Ta właściwość zawiera informacje dotyczące wysyłania wiadomości powitania hello uwierzytelniania metodę tooauthenticate hello urządzenia. Aby uzyskać więcej informacji, zobacz [urządzenia toocloud ochrony przed fałszowaniem][lnk-antispoofing]. |

## <a name="message-size"></a>Rozmiar komunikatu

Centrum IoT mierzy rozmiar wiadomości w sposób niezależny od protokołu, biorąc pod uwagę tylko ładunku rzeczywiste hello. Hello wyrażony w bajtach rozmiar jest obliczany jako suma hello hello następujące:

* Witaj treści rozmiar w bajtach.
* Witaj rozmiar w bajtach wszystkich wartości hello właściwości systemu wiadomość hello.
* Witaj rozmiar w bajtach wszystkich użytkownika nazwy i wartości właściwości.

Nazwy i wartości właściwości są ograniczone tooASCII znaków, dlatego hello długość ciągów hello równa hello rozmiar w bajtach.

## <a name="next-steps"></a>Następne kroki

Uzyskać informacji na temat limitów rozmiarów wiadomości w Centrum IoT, zobacz [przydziały Centrum IoT i ograniczania przepustowości][lnk-quotas].

toolearn toocreate i czytać wiadomości Centrum IoT w różnych językach programowania, zobacz temat hello [wprowadzenie] [ lnk-get-started] samouczki.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
