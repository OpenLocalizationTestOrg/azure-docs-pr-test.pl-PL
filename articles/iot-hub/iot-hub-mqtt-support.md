---
title: "aaaUnderstand Obsługa MQTT Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Deweloper przewodnik — Obsługa urządzeń łączących się przy użyciu punktu końcowego urządzeń połączonych z Centrum IoT tooan hello MQTT protokołu. Zawiera informacje na temat wbudowana obsługa MQTT w hello zestawy SDK urządzenia Azure IoT."
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Komunikować się z Centrum IoT przy użyciu protokołu MQTT hello

Centrum IoT umożliwia toocommunicate urządzeń z hello urządzenia punkty końcowe Centrum IoT przy użyciu hello [MQTT v3.1.1] [ lnk-mqtt-org] protokołu na porcie 8883 lub v3.1.1 MQTT za pośrednictwem protokołu WebSocket na porcie 443. Centrum IoT wymaga wszystkie urządzenia komunikacji toobe zabezpieczone przy użyciu protokołu TLS/SSL (w związku z tym Centrum IoT nie obsługuje niezabezpieczonego połączenia za pośrednictwem portu 1883).

## <a name="connecting-tooiot-hub"></a>Łączenie tooIoT Centrum

Urządzenie można użyć Centrum IoT hello MQTT protokołu tooconnect tooan przy użyciu bibliotek hello hello [Azure IoT SDK] [ lnk-device-sdks] lub przy użyciu protokołu MQTT hello bezpośrednio.

## <a name="using-hello-device-sdks"></a>Za pomocą urządzenia hello zestawów SDK

[Zestawy SDK urządzenia] [ lnk-device-sdks] hello tej obsługi protokołu MQTT są dostępne dla języka Java, Node.js, C, C# i Python. urządzenie Hello zestawów SDK używać hello standardowe Centrum IoT połączenia ciąg tooestablish Centrum IoT tooan połączenia. Protokół MQTT hello toouse, powitania klienta protokołu parametr musi być ustawiony zbyt**MQTT**. Domyślnie urządzenia hello zestawów SDK łączą tooan Centrum IoT hello **CleanSession** zbyt ustawiona flaga**0** i użyj **QoS 1** w wymianie wiadomości powitania Centrum IoT.

Gdy urządzenie jest połączone tooan Centrum IoT, urządzenia hello zestawy SDK zapewniają metod, które umożliwiają wiadomości toosend urządzenia powitania tooand odbierać komunikaty z Centrum IoT.

Witaj Poniższa tabela zawiera linki toocode przykłady dla każdego obsługiwanego języka i określa hello parametru toouse tooestablish tooIoT połączenia koncentratora przy użyciu protokołu MQTT hello.

| Język | Parametr protokołu |
| --- | --- |
| [Node.js][lnk-sample-node] |Azure — iot urządzenie mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Migrowanie aplikacji urządzenia z protokołu AMQP tooMQTT

Jeśli używasz hello [urządzenia zestawów SDK][lnk-device-sdks], przełączania przy użyciu protokołu AMQP tooMQTT konieczna jest zmiana parametru protokołu hello w powitania klienta inicjowania, jak wspomniano wcześniej.

Po tej czynności upewnij się, że hello toocheck następujące elementy:

* Protokół AMQP zwraca błędy wiele warunków, gdy MQTT zakończy połączenie hello. W związku z tym wyjątku obsługi logiki ewentualnej konieczności wprowadzenia zmian.
* MQTT nie obsługuje hello *Odrzuć* operacji podczas odbierania [wiadomości chmury do urządzenia][lnk-messaging]. Jeśli aplikacja zaplecza musi tooreceive odpowiedzi z aplikacji urządzenia hello, rozważ użycie [bezpośrednie metody][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Przy użyciu protokołu MQTT hello bezpośrednio
Jeśli urządzenie nie można używać urządzeń hello zestawów SDK, nadal można połączyć z punktów końcowych urządzenie toohello przy użyciu protokołu MQTT hello na porcie 8883. W hello **CONNECT** pakietów hello urządzeń należy używać hello następujące wartości:

* Dla hello **ClientId** Użyj hello **deviceId**.
* Dla hello **Username** użyj `{iothubhostname}/{device_id}/api-version=2016-11-14`, gdzie {iothubhostname} jest hello pełne CName hello Centrum IoT.

    Na przykład, jeśli hello nazwa Centrum IoT to **contoso.azure devices.net** i jeśli hello nazwa urządzenia jest **MyDevice01**, hello pełne **Username** pole powinno zawierać `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Dla hello **hasło** Użyj tokenu sygnatury dostępu Współdzielonego. format Hello powitalne SAS token jest hello takie same jak w przypadku zarówno hello HTTP, jak i protokołów AMQP:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Aby uzyskać więcej informacji o tym, jak toogenerate tokeny sygnatury dostępu Współdzielonego, zobacz sekcję urządzenia hello [tokeny zabezpieczające przy użyciu Centrum IoT][lnk-sas-tokens].

    Podczas testowania, możesz również użyć hello [explorer urządzenia] [ lnk-device-explorer] tooquickly narzędzie do generowania tokenu sygnatury dostępu Współdzielonego, który możesz skopiować i wkleić w swoim własnym kodem:

  1. Przejdź toohello **zarządzania** karcie **Explorer urządzenia**.
  2. Kliknij przycisk **tokenu sygnatury dostępu Współdzielonego** (z góry po prawej).
  3. Na **SASTokenForm**, wybierz swoje urządzenie w hello **DeviceID** listy rozwijanej. Ustaw użytkownika **TTL**.
  4. Kliknij przycisk **Generuj** toocreate Twojego tokenu.

     Witaj tokenu sygnatury dostępu Współdzielonego, który jest generowany ma ta struktura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     Witaj częścią tego tokenu toouse jako hello **hasło** jest tooconnect pola przy użyciu MQTT: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

MQTT łączyć i Odłącz pakietów, Centrum IoT wystawia zdarzenie na powitania **operacje monitorowania** kanału o dodatkowe informacje, które mogą ułatwić tootroubleshoot problemy z połączeniem.

### <a name="sending-device-to-cloud-messages"></a>Wysyłanie wiadomości urządzenia do chmury

Po wprowadzeniu udane połączenie, urządzenie może wysyłać wiadomości tooIoT koncentratora za pomocą `devices/{device_id}/messages/events/` lub `devices/{device_id}/messages/events/{property_bag}` jako **nazwa tematu**. Witaj `{property_bag}` element włącza hello urządzenia toosend wiadomości z dodatkowych właściwości w formacie zakodowane w adresie url. Na przykład:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> To `{property_bag}` element hello używa tego samego kodowania, podobnie jak w przypadku ciągi zapytań w protokole hello HTTP.
>
>

Hello aplikacji urządzenia można także użyć `devices/{device_id}/messages/events/{property_bag}` jako hello **nazwa tematu zostanie** toodefine *będzie wiadomości* toobe przekazywane jako wiadomość telemetrii.

- Centrum IoT nie obsługuje komunikaty QoS 2. Jeśli aplikacja urządzenia publikuje komunikat z **QoS 2**, Centrum IoT zamyka hello połączenia sieciowego.
- Centrum IoT nie jest trwały Zachowaj wiadomości. Jeśli urządzenie wysyła wiadomość hello **Zachowaj** too1 ustawiona flaga, Centrum IoT dodaje hello **x-opt — Zachowaj** komunikat toohello właściwości aplikacji. W takim przypadku zamiast utrwalanie hello zachować wiadomości, Centrum IoT przekazuje toohello wewnętrznej bazy danych aplikacji.
- Centrum IoT obsługuje tylko jedno aktywne połączenie MQTT na urządzenie. Wszystkie nowe połączenie MQTT imieniu hello tego samego Identyfikatora urządzenia powoduje, że Centrum IoT toodrop hello istniejącego połączenia.

Aby uzyskać więcej informacji, zobacz [wiadomości przewodnik dewelopera][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Odbieranie komunikatów chmury do urządzenia

tooreceive wiadomości z Centrum IoT, urządzenie powinno Subskrybuj przy użyciu `devices/{device_id}/messages/devicebound/#` jako **filtru tematu**. Witaj wielopoziomowe symbolu wieloznacznego  **#**  w hello filtr tematu jest używany tylko tooallow hello urządzenia tooreceive dodatkowe właściwości w nazwie tematu hello. Centrum IoT nie zezwala na użycie hello hello  **#**  lub **?** symbole wieloznaczne w celu filtrowania tematy podrzędne. Ponieważ Centrum IoT nie jest brokera obsługi komunikatów pub-sub ogólnego przeznaczenia, obsługuje on tylko nazwy tematów hello udokumentowany i filtry tematu.

Hello urządzenia nie odbiera komunikaty z Centrum IoT, aż pomyślnie subskrybowanych tooits urządzenia punktu końcowego, reprezentowany przez hello `devices/{device_id}/messages/devicebound/#` filtru tematu. Po nawiązaniu pomyślnego subskrypcji, urządzenia hello uruchamia odbieranie wiadomości tylko chmury do urządzenia, które zostały wysłane tooit po czasie hello hello subskrypcji. Jeśli urządzenie hello nawiązanie połączenia z **CleanSession** zbyt ustawiona flaga**0**, subskrypcji hello jest trwała dla różnych sesji. W takim przypadku hello kolejnym nawiązaniu z **CleanSession 0** hello urządzenia odbiera komunikaty oczekujące, które zostały wysłane tooit gdy był on odłączony. Jeśli urządzenie hello używa **CleanSession** zbyt ustawiona flaga**1** , nie otrzyma komunikaty z Centrum IoT dopóki ją subskrybuje tooits urządzenia endpoint.

Centrum IoT zapewnia wiadomości powitania **nazwa tematu** `devices/{device_id}/messages/devicebound/`, lub `devices/{device_id}/messages/devicebound/{property_bag}` , jeśli nie ma żadnych właściwości komunikatu. `{property_bag}`zawiera pary klucz wartość zakodowane w adresie url właściwości komunikatu. Tylko właściwości aplikacji i użytkownika można ustawić właściwości (takie jak **messageId** lub **correlationId**) znajdują się w zbiorze właściwości hello. Nazwy właściwości systemu mają prefiks hello  **$** , właściwości aplikacji za pomocą hello oryginalna nazwa właściwości nie ma prefiksu.

Gdy aplikacja urządzenia subskrybuje temat tooa z **QoS 2**, Centrum IoT przyznaje maksymalny poziom QoS 1 w hello **SUBACK** pakietów. Po tym Centrum IoT zapewnia urządzenia toohello wiadomości przy użyciu QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Podczas pobierania właściwości dwie urządzenia

Po pierwsze urządzenie subskrybuje zbyt`$iothub/twin/res/#`, tooreceive hello operacji odpowiedzi. Następnie wysyła tootopic pusty komunikat `$iothub/twin/GET/?$rid={request id}`, z wypełnione wartością **identyfikator żądania**. Usługa hello wysyła następnie odpowiedź hello urządzenia dwie dane na temat `$iothub/twin/res/{status}/?$rid={request id}`, przy użyciu hello sam  **Identyfikator żądania** jako hello żądania.

Identyfikator żądania może być wszystkie prawidłowe wartości wartość właściwości komunikatu zgodnie [Centrum IoT wiadomości przewodnik dewelopera][lnk-messaging], i stan zostanie zweryfikowany jako liczba całkowita.
treść odpowiedzi Hello zawiera sekcja właściwości hello Witaj dwie urządzenia:

Witaj treść wpisu rejestru tożsamości hello ograniczone toohello "właściwości" elementu członkowskiego, na przykład:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

kody stanu możliwe Hello są następujące:

|Stan | Opis |
| ----- | ----------- |
| 200 | Powodzenie |
| 429 | Za dużo żądań (ograniczony), jak na [ograniczania Centrum IoT][lnk-quotas] |
| 5** | Błędy serwera |

Aby uzyskać więcej informacji, zobacz [urządzenia twins przewodnik dewelopera][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Aktualizacja właściwości zgłoszone dwie urządzenia

Witaj poniższa sekwencja zawiera opis jak urządzenie aktualizuje hello zgłosił właściwości w Witaj dwie urządzenie w Centrum IoT:

1. Urządzenia najpierw zasubskrybować toohello `$iothub/twin/res/#` operacji tematu tooreceive hello odpowiedzi z Centrum IoT.

1. Urządzenie wysyła wiadomość zawierającą hello urządzenia dwie aktualizacji toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` tematu. Ten komunikat zawiera **identyfikator żądania** wartość.

1. Witaj usługi, a następnie wysyła komunikat odpowiedzi, który zawiera hello nową wartość ETag hello kolekcji właściwości zgłoszony na temat `$iothub/twin/res/{status}/?$rid={request id}`. Ten komunikat odpowiedzi używa hello sam **identyfikator żądania** jako hello żądania.

treść komunikatu żądania Hello zawiera dokument JSON, który zawiera nowe wartości dla właściwości zgłoszone (nie właściwości lub metadanych może być modyfikowany).
Każdy element członkowski w dokumencie JSON hello aktualizacji lub Dodaj hello odpowiadającego mu członka w dokumencie dwie hello urządzenia. Zestaw elementów członkowskich za`null`, usuwa hello hello zawierający obiektu elementu członkowskiego. Na przykład:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

kody stanu możliwe Hello są następujące:

|Stan | Opis |
| ----- | ----------- |
| 200 | Powodzenie |
| 400 | Nieprawidłowe żądanie. Nieprawidłowo sformatowany kod JSON |
| 429 | Za dużo żądań (ograniczony), jak na [ograniczania Centrum IoT][lnk-quotas] |
| 5** | Błędy serwera |

Aby uzyskać więcej informacji, zobacz [urządzenia twins przewodnik dewelopera][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Odbieranie powiadomienia o aktualizacji odpowiednie właściwości

Gdy urządzenie jest podłączone, Centrum IoT wysyła powiadomienia toohello tematu `$iothub/twin/PATCH/properties/desired/?$version={new version}`, które zawierają hello zawartość aktualizacji hello wykonywane przez zaplecza rozwiązania hello. Na przykład:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Podobnie jak w przypadku aktualizacji właściwości `null` wartości oznacza, że hello JSON obiektu elementu członkowskiego jest usuwany.


> [!IMPORTANT] 
> Centrum IoT generuje powiadomienia o zmianie tylko wtedy, gdy urządzenia są połączone. Upewnij się, że hello tooimplement [przepływu ponowne łączenie urządzenia] [ lnk-devguide-twin-reconnection] tookeep hello żądanego właściwości między centrum IoT i hello aplikacji urządzenia.

Aby uzyskać więcej informacji, zobacz [urządzenia twins przewodnik dewelopera][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Metoda bezpośrednia tooa odpowiedź

Po pierwsze urządzenie ma toosubscribe zbyt`$iothub/methods/POST/#`. Centrum IoT wysyła tematu toohello żądania metody `$iothub/methods/POST/{method name}/?$rid={request id}`, poprawne dane JSON lub pustej treści.

toorespond, urządzenie hello wysyła wiadomość o poprawne dane JSON lub pustej treści tematu toohello `$iothub/methods/res/{status}/?$rid={request id}`, gdzie **identyfikator żądania** ma toomatch hello w hello komunikat żądania, i **stan** ma toobe liczbą całkowitą .

Aby uzyskać więcej informacji, zobacz [bezpośrednie przewodnik dewelopera metody][lnk-methods].

### <a name="additional-considerations"></a>Dodatkowe zagadnienia

Jako ostatecznego wchodzi w grę, jeśli potrzebujesz zachowanie protokołu MQTT hello toocustomize po stronie chmury hello, należy przejrzeć hello [brama protokołu Azure IoT] [ lnk-azure-protocol-gateway] umożliwiająca toodeploy wysokiej wydajności Protokół niestandardowych bramy, która bezpośrednio z Centrum IoT. Brama protokołu Azure IoT Hello umożliwia możesz toocustomize hello urządzenia protokołu tooaccommodate brownfield MQTT wdrożenia lub innych niestandardowych protokołów. Takie podejście wymaga jednak uruchamiania i działać brama protokołu niestandardowego.

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat protokołu MQTT hello, zobacz hello [dokumentacji MQTT][lnk-mqtt-docs].

toolearn więcej informacji na temat planowania wdrożenia Centrum IoT, zobacz:

* [Azure certyfikowane dla katalogu urządzenia IoT][lnk-devices]
* [Obsługa dodatkowych protokołów.][lnk-protocols]
* [Porównaj z usługi Event Hubs][lnk-compare]
* [Skalowanie, wysokiej dostępności i odzyskiwania po awarii][lnk-scaling]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
