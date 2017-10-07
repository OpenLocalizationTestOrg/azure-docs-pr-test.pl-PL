---
title: "aaaUnderstand hello Azure IoT Hub tożsamości rejestru | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — opis hello rejestru tożsamości Centrum IoT i w jaki sposób toouse on toomanage urządzenia. Zawiera informacje na temat hello importowanie i eksportowanie tożsamości urządzenia w partii."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>Zrozumienie hello rejestru tożsamości w Centrum IoT

Centrum IoT, co ma rejestru tożsamości, która przechowuje informacje o urządzeniach hello dozwolone Centrum IoT toohello tooconnect. Zanim urządzenie można połączyć z Centrum IoT tooan, musi to być wpis dla tego urządzenia w rejestrze tożsamości Centrum IoT hello. Urządzenie musi uwierzytelniać również z Centrum IoT hello na podstawie poświadczeń przechowywanych w rejestrze tożsamości hello.

Identyfikator urządzenia Hello przechowywane w rejestrze tożsamości hello jest rozróżniana wielkość liter.

Na wysokim poziomie rejestru tożsamości hello jest kolekcją obsługą REST zasoby tożsamości urządzenia. Po dodaniu wpisu w rejestrze tożsamości hello Centrum IoT tworzy zestaw zasobów na urządzenie, takie jak kolejki hello, która zawiera komunikatów w locie chmury do urządzenia.

### <a name="when-toouse"></a>Gdy toouse

Należy używać hello tożsamości rejestru:

* Zainicjować obsługę administracyjną urządzeń, które łączą się z Centrum IoT tooyour.
* Kontrolowanie punkty końcowe skierowane do urządzenia koncentratora na urządzenie dostępu tooyour.

> [!NOTE]
> rejestru tożsamości Hello nie zawiera żadnych metadane specyficzne dla aplikacji.

## <a name="identity-registry-operations"></a>Operacje rejestru tożsamości

Witaj w rejestrze tożsamości Centrum IoT przedstawia hello następujące operacje:

* Tworzenie tożsamości urządzenia
* Zaktualizuj tożsamości urządzenia
* Pobieranie tożsamości urządzenia według Identyfikatora
* Usuwanie tożsamości urządzenia
* Aż too1000 tożsamości
* Eksportuj wszystkie magazynu obiektów blob tooAzure tożsamości
* Importuj tożsamości z magazynu obiektów blob platformy Azure

Te operacje można użyć optymistycznej współbieżności, jak określono w [RFC7232][lnk-rfc7232].

> [!IMPORTANT]
> Witaj tylko sposób tooretrieve wszystkich tożsamości w rejestrze tożsamości Centrum IoT jest toouse hello [wyeksportować] [ lnk-export] funkcji.

Centrum IoT rejestru tożsamości:

* Nie zawiera żadnych metadanych aplikacji.
* Możliwy jak słownika, za pomocą hello **deviceId** jako hello klucza.
* Nie obsługuje obszerne zapytań.

Rozwiązania IoT zwykle ma oddzielny magazyn określonego rozwiązania zawierającego metadane specyficzne dla aplikacji. Na przykład hello określonego rozwiązania magazynu w rozwiązaniu inteligentne budynku będzie rejestrować hello miejsca, w której jest wdrażane czujnik temperatury.

> [!IMPORTANT]
> Hello tożsamości rejestru należy używać tylko do zarządzania urządzeniami i Inicjowanie obsługi operacji. Wykonywanie operacji w rejestrze tożsamości hello wysokiej przepływności operacji w czasie wykonywania nie należy uwzględniać. Na przykład sprawdzanie stanu połączenia hello urządzenia przed wysłaniem polecenia nie jest obsługiwany wzorzec. Upewnij się, że hello toocheck [ograniczania szybkości] [ lnk-quotas] hello rejestru tożsamości i hello [pulsu urządzenia] [ lnk-guidance-heartbeat] wzorca.

## <a name="disable-devices"></a>Wyłącz urządzenia

Urządzenia można wyłączyć, aktualizując hello **stan** właściwość identity w rejestrze tożsamości hello. Zazwyczaj korzystają z tej właściwości, w przypadku dwóch scenariuszy:

* Podczas inicjowania obsługi administracyjnej procesu aranżacji. Aby uzyskać więcej informacji, zobacz [Inicjowanie obsługi administracyjnej urządzeń][lnk-guidance-provisioning].
* Jeśli z jakiegokolwiek powodu, należy rozważyć zostanie naruszony lub przestał nieautoryzowanego urządzenia.

## <a name="import-and-export-device-identities"></a>Importowanie i eksportowanie tożsamości urządzenia

Z Centrum IoT rejestru tożsamości, można wyeksportować tożsamości urządzenia w trybie zbiorczym, za pomocą operacji asynchronicznych na powitania [punktu końcowego dostawcy zasobów Centrum IoT][lnk-endpoints]. Eksporty są długotrwałe zadania korzystające z danych tożsamości urządzenia dostarczonych przez klienta obiektów blob kontenera toosave odczytać z rejestru tożsamości hello.

Tożsamości urządzenia w rejestrze tożsamości Centrum zbiorczego tooan IoT, można importować za pomocą operacji asynchronicznych na powitania [punktu końcowego dostawcy zasobów Centrum IoT][lnk-endpoints]. Importy są długotrwałych zadań, korzystających z danych w danych tożsamości urządzenia toowrite kontener blob dostarczonych przez klienta w rejestrze tożsamości hello.

* Aby uzyskać szczegółowe informacje na temat hello importowanie i eksportowanie interfejsów API, zobacz [interfejsy API REST dostawcy zasobów Centrum IoT][lnk-resource-provider-apis].
* toolearn więcej informacji na temat uruchamiania importowania i eksportowania zadań, zobacz [zbiorcze Zarządzanie tożsamościami urządzenia IoT Hub][lnk-bulk-identity].

## <a name="device-provisioning"></a>Inicjowanie obsługi administracyjnej urządzeń

dane urządzenia Hello przechowujący danego rozwiązania IoT zależy od hello szczególne wymagania rozwiązania. Ale co najmniej rozwiązanie musi przechowywać tożsamości urządzenia i klucze uwierzytelniania. Centrum IoT Azure obejmuje rejestru tożsamości, które można przechowywać wartości dla każdego urządzenia, takie jak nazwy, klucze uwierzytelniania i kodów stanu. Rozwiązanie można używać innych usług Azure, takich jak magazyn tabel, magazyn obiektów blob lub toostore DB rozwiązania Cosmos danych dodatkowych urządzeń.

*Inicjowanie obsługi administracyjnej urządzeń* jest hello proces dodawania magazynów toohello hello wstępna urządzenia w rozwiązaniu. tooenable nowe Centrum tooyour tooconnect urządzenia, należy dodać urządzenia identyfikator i klucze toohello rejestru tożsamości Centrum IoT. W ramach procesu udostępniania hello może być konieczne tooinitialize dane specyficzne dla urządzeń w innych magazynach rozwiązania.

## <a name="device-heartbeat"></a>Urządzenie pulsu

Witaj Centrum IoT tożsamości Rejestr zawiera pole o nazwie **element connectionState**. Używaj tylko hello **element connectionState** pole w czasie projektowania i debugowania. Rozwiązania IoT nie należy zbadać hello pola w czasie wykonywania. Na przykład nie zapytanie hello **element connectionState** toocheck pola, jeśli urządzenie jest podłączone, aby wysłać wiadomość SMS lub wiadomości chmury do urządzenia.

Jeśli rozwiązania IoT musi tooknow, jeśli urządzenie jest podłączone, należy zaimplementować hello *wzorzec pulsu*.

We wzorcu pulsu hello urządzenie hello wysyła komunikaty urządzenia do chmury co najmniej raz co stałej ilości czasu (na przykład co najmniej raz na godzinę). W związku z tym nawet jeśli urządzenie nie ma żadnych toosend danych, nadal wysyła komunikat pusty urządzenia do chmury (zazwyczaj z właściwością, która identyfikuje ją jako pulsu). Na stronie usługi hello hello rozwiązania przechowuje mapy z hello ostatni Puls dla każdego urządzenia. Rozwiązanie hello nie pojawi się komunikat pulsu w czasie hello oczekiwano z urządzenia hello, zakłada, że występuje problem z urządzeniem hello.

Bardziej złożone wdrożenia mogą zawierać informacje hello z [operacje monitorowania] [ lnk-devguide-opmon] tooidentify urządzenia, które próbujesz tooconnect lub komunikowania się, ale się niepowodzeniem. Podczas implementowania wzorzec pulsu hello, upewnij się, że toocheck [IoT Hub przydziały i limity][lnk-quotas].

> [!NOTE]
> Jeśli połączenie hello używa rozwiązania IoT stan wyłącznie toodetermine: Określa, czy toosend wiadomości chmury do urządzenia, i wiadomości są nie emisji toolarge zestawy urządzeń, należy rozważyć użycie hello prostsze *krótki czas wygaśnięcia* wzorca. Ten wzorzec osiąga hello sam powoduje jako utrzymania rejestru stanu połączenia urządzenia przy użyciu wzorca pulsu hello, będąc bardziej wydajne. Jeśli żądanie jest komunikat potwierdzenia, Centrum IoT może powiadomić o urządzeń, które są komunikaty o stanie tooreceive i nie są.

## <a name="device-lifecycle-notifications"></a>Powiadomienia dotyczące cyklu życia urządzenia

Centrum IoT można powiadomić rozwiązania IoT, po utworzeniu lub usunięciu, wysyłając powiadomienia dotyczące cyklu życia urządzenia tożsamości urządzenia. toodo tak, rozwiązania IoT musi toocreate trasy i równości źródła danych hello tooset zbyt*DeviceLifecycleEvents*. Domyślnie są wysyłane nie powiadomienia dotyczące cyklu życia, oznacza to, że istnieje wstępnie ma takie tras. komunikat powiadomienia Hello zawiera właściwości, oraz i treść.

Właściwości: Właściwości systemu wiadomości są poprzedzane prefiksem hello `'$'` symbolu.

| Nazwa | Wartość |
| --- | --- |
$content — typ | application/json |
$iothub-enqueuedtime |  Czas wysłania powiadomienia hello |
$iothub-komunikat-źródła | deviceLifecycleEvents |
$content-kodowania | UTF-8 |
opType | **createDeviceIdentity** lub **deleteDeviceIdentity** |
hubName | Nazwa centrum IoT |
deviceId | Identyfikator urządzenia hello |
operationTimestamp | Sygnatura czasowa ISO8601 operacji |
Centrum iothub komunikat schemacie | deviceLifecycleNotification |

Treść: W tej sekcji jest w formacie JSON i przedstawia Witaj dwie z hello utworzone tożsamości urządzenia. Na przykład:

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>Tematy odwołań:

Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat hello rejestru tożsamości.

## <a name="device-identity-properties"></a>Właściwości tożsamości urządzenia

Tożsamości urządzenia są reprezentowane jako dokumenty JSON z hello następujące właściwości:

| Właściwość | Opcje | Opis |
| --- | --- | --- |
| deviceId |wymagane, tylko do odczytu na aktualizacje |Ciąg z uwzględnieniem wielkości liter (up too128 znaków) znaki alfanumeryczne ASCII 7-bitowego + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Identyfikator generacji |wymagane, tylko do odczytu |IoT generowanych przez koncentrator, z uwzględnieniem wielkości liter ciąg się too128 znaków. Ta wartość jest używana toodistinguish urządzeniom hello tego samego **deviceId**, gdy został usunięty i utworzony ponownie. |
| Element etag |wymagane, tylko do odczytu |Ciąg reprezentujący słaby element ETag hello tożsamości urządzenia, jak na [RFC7232][lnk-rfc7232]. |
| uwierzytelniania |Opcjonalne |Obiekt złożony zawierające materiały informacji i zabezpieczeń uwierzytelniania. |
| auth.symkey |Opcjonalne |Złożony obiekt zawierający podstawowy i klucz pomocniczy, są przechowywane w formacie base64. |
| status |Wymagane |Wskaźnik dostępu. Może być **włączone** lub **wyłączone**. Jeśli **włączone**, hello urządzenie może tooconnect. Jeśli **wyłączone**, to urządzenie nie ma dostępu do dowolnego punktu końcowego skierowane do urządzenia. |
| statusReason |Opcjonalne |128 znaków długości ciągu z tego powodu hello magazynów dla stanu tożsamości urządzenia hello. Dozwolone są wszystkie znaki UTF-8. |
| statusUpdateTime |tylko do odczytu |Wskaźnik danych czasowych, przedstawiający hello Data i godzina ostatniej aktualizacji stanu hello. |
| Element connectionState |tylko do odczytu |Pole wskazujący stan połączenia: albo **połączony** lub **Rozłączono**. To pole reprezentuje Widok Centrum IoT dla stanu połączenia urządzenia hello hello. **Ważne**: w tym polu należy używać tylko na potrzeby tworzenia/debugowania. Stan połączenia Hello jest aktualizowany tylko w przypadku urządzeń przy użyciu MQTT lub AMQP. Ponadto jest oparty na poziomie protokołu ping (ping MQTT lub polecenia ping protokołu AMQP) i może mieć Maksymalne opóźnienie tylko 5 minut. Z tego względu mogą być fałszywych alarmów, takie jak urządzenia zgłoszone jako połączona, ale które zostały odłączone. |
| connectionStateUpdatedTime |tylko do odczytu |Wskaźnik danych czasowych, przedstawiający Data hello i ostatni stan połączenia hello czasu został zaktualizowany. |
| lastActivityTime |tylko do odczytu |Wskaźnik danych czasowych, przedstawiający hello Data i czas ostatniego hello urządzenia podłączone, odebranych lub wysłanych wiadomości. |

> [!NOTE]
> Stan połączenia tylko może reprezentować hello Widok Centrum IoT dla stanu hello hello połączenia. Stan toothis aktualizacje mogą być opóźnione w zależności od warunków sieciowych i konfiguracji.

## <a name="additional-reference-material"></a>Odwołanie dodatkowe materiały

Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:

* [Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.
* [Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello i ograniczanie zachowań stosowane toohello usługi IoT Hub.
* [Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.
* [Język zapytań Centrum IoT] [ lnk-query] opisuje tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend hello.
* [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.

## <a name="next-steps"></a>Następne kroki

Teraz wiesz już, jak toouse hello Centrum IoT tożsamości rejestru, może Cię zainteresować następujące tematy przewodnik dewelopera Centrum IoT hello:

* [Kontrola dostępu tooIoT Centrum][lnk-devguide-security]
* [Urządzenie twins toosynchronize stanu i konfiguracji][lnk-devguide-device-twins]
* [Wywoływanie metody bezpośrednio na urządzeniu][lnk-devguide-directmethods]
* [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]

Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello samouczka Centrum IoT:

* [Rozpoczynanie pracy z Centrum IoT Azure][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
