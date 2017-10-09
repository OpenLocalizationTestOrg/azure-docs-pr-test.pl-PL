---
title: "Omówienie Centrum IoT aaaAzure | Dokumentacja firmy Microsoft"
description: "Omówienie hello usługa Azure IoT Hub: co to jest Centrum IoT, łączność urządzeń, internet rzeczy wzorców komunikacji, bramy i hello przy pomocy usługi komunikacji wzorzec"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Omówienie hello usługi Centrum IoT Azure

Zapraszamy tooAzure Centrum IoT. Ten artykuł zawiera omówienie Centrum IoT Azure i opisuje Dlaczego warto korzystać z tej usługi tooimplement rozwiązania Internetu rzeczy (IoT). Azure IoT Hub to w pełni zarządzana usługa, która umożliwia bezpieczną i niezawodną dwukierunkową komunikację między milionami urządzeń IoT i zapleczem rozwiązania. Usługa Azure IoT Hub:

* zapewnia wiele opcji komunikacji z urządzenia do chmury i z chmury do urządzenia, w tym jednokierunkowe komunikaty, transfer plików i metody typu żądanie-odpowiedź;
* Zawiera wbudowane deklaratywne wiadomości routingu tooother usług platformy Azure.
* udostępnia zsynchronizowane informacje o stanie i magazyn metadanych urządzenia z możliwością tworzenia zapytań;
* umożliwia bezpieczne komunikowanie się i kontrolę dostępu przy użyciu kluczy zabezpieczeń lub certyfikatów X.509 dla poszczególnych urządzeń;
* udostępnia rozbudowane funkcje monitorowania zdarzeń zarządzania dotyczących łączności i tożsamości urządzeń;
* Zawiera urządzenia biblioteki dla hello najbardziej popularnych języków i platform.

Artykuł Hello [porównania Centrum IoT i usługi Event Hubs] [ lnk-compare] opisuje hello podstawowych różnic między te dwie usługi i zaznacza hello zalety korzystania z Centrum IoT w Twojego rozwiązania IoT.

Aby uzyskać więcej informacji dotyczących sposobu Azure i Centrum IoT zabezpieczanie rozwiązania IoT, zobacz [zabezpieczeń Internetu rzeczy z hello tła][lnk-security-ground-up].

![Usługa Azure IoT Hub jako brama chmury w rozwiązaniu Internetu rzeczy][img-architecture]

> [!NOTE]
> Szczegółowe omówienie architektury IoT, zobacz hello [architektura referencyjna IoT platformy Microsoft Azure][lnk-refarch].

## <a name="iot-device-connectivity-challenges"></a>Wyzwania dotyczące łączności z urządzeniami IoT

Centrum IoT i hello biblioteki urządzenia pomocy toomeet hello wyzwania dotyczące tooreliably i bezpieczne łączenie z zaplecza urządzeń toohello rozwiązania. Urządzenia IoT:

* są często systemami osadzonymi bez osoby pełniącej rolę operatora;
* mogą znajdować się w lokalizacjach zdalnych, gdzie dostęp fizyczny jest kosztowny;
* Mogą być dostępne tylko za pośrednictwem zaplecza rozwiązania hello.
* mogą mieć ograniczone zasoby w zakresie zasilania i przetwarzania;
* mogą korzystać z przerywanej, powolnej lub kosztownej łączności sieciowej;
* Może być konieczne toouse aplikacji zastrzeżonych, niestandardowych lub specyficznych dla branży protokołów.
* mogą być tworzone przy użyciu szerokiej gamy popularnych platform sprzętowych i programowych.

Ponadto toohello powyższych wymagań każde rozwiązanie IoT musi również zapewniać skali, bezpieczeństwa i niezawodności. Witaj wynikowy zbiór wymogów dotyczących łączności jest trudny i czasochłonny tooimplement, używając tradycyjnych technologii, takich jak kontenery sieci web, a brokerzy obsługi wiadomości.

## <a name="why-use-azure-iot-hub"></a>Dlaczego warto korzystać z usługi Azure IoT Hub

Ponadto zestaw sformatowanego tooa [urządzenia do chmury] [ lnk-d2c-guidance] i [chmury do urządzenia] [ lnk-c2d-guidance] opcji komunikacji, wiadomości, w tym pliku adresy Centrum IoT Azure transferów i metody "żądanie-odpowiedź" hello urządzenia łączności trudności w hello następujące sposoby:

* **Bliźniacze reprezentacje urządzeń**. Dzięki [bliźniaczym reprezentacjom urządzeń][lnk-twins] możesz przechowywać i synchronizować metadane urządzenia i informacje o stanie oraz tworzyć dotyczące ich zapytania. Bliźniacze reprezentacje urządzeń to dokumenty JSON, które przechowują informacje o stanie urządzenia (metadane, konfiguracje i warunki). Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia połączyć z tooIoT koncentratora.

* **Uwierzytelnianie poszczególnych urządzeń i bezpieczna łączność**. Umożliwia obsługę każdego z jego własnej [klucz zabezpieczeń] [ lnk-devguide-security] tooenable on tooIoT tooconnect koncentratora. Witaj [rejestru tożsamości Centrum IoT] [ lnk-devguide-identityregistry] przechowuje tożsamości urządzenia i klucze w rozwiązaniu. Zaplecze rozwiązania można dodać tooallow poszczególne urządzenia lub Odmów list tooenable pełną kontrolę nad uzyskiwania dostępu do urządzenia.

* **Urządzenia chmury trasy wiadomości tooAzure usługi na podstawie reguł deklaratywne**. Centrum IoT umożliwia możesz toodefine wiadomości tras na podstawie routingu toocontrol reguł, w którym Centrum wysyła komunikaty urządzenia do chmury. Reguły routingu nie wymagają toowrite można dowolny kod i może być hello miejsca dystrybucja niestandardowy komunikat po wprowadzanie.

* **Monitorowanie operacji dotyczących łączności urządzeń**. Dostępne są szczegółowe dzienniki zawierające operacje zarządzania tożsamościami urządzeń i zdarzenia dotyczące łączności urządzeń. Ta nowa możliwość monitorowania pozwala Twojej IoT rozwiązania tooidentify problemy z łącznością, takich jak urządzenia, które tooconnect z nieprawidłowe poświadczenia, spróbuj zbyt często wysyłać wiadomości lub odrzucić wszystkie komunikaty chmury do urządzenia.

* **Obszerny zestaw bibliotek urządzeń**. Dostępne są [zestawy SDK urządzeń Azure IoT][lnk-device-sdks], które obsługują różne języki i platformy, na przykład język C w przypadku wielu dystrybucji systemu Linux, systemu Windows czy systemów operacyjnych czasu rzeczywistego. Zestawy SDK urządzeń Azure IoT obsługują także języki zarządzane, takie jak C#, Java i JavaScript.

* **Protokoły i możliwość rozszerzania infrastruktury IoT**. Jeśli rozwiązania nie można użyć bibliotek urządzenia hello, Centrum IoT udostępnia publiczne protokół, który umożliwia urządzeń toonatively Użyj hello MQTT v3.1.1, protokołu HTTP 1.1 lub protokołów AMQP 1.0. Można również rozszerzyć zasięg toosupport Centrum IoT dla protokołów niestandardowych:

  * Tworzenie bramy pola z [Azure IoT krawędzi] [ lnk-iot-edge] konwertująca tooone Twojego protokołu niestandardowego elementu hello zrozumiał trzy protokoły Centrum IoT.
  * Dostosowywanie hello [brama protokołu Azure IoT][protocol-gateway], składnik typu open source, który działa w chmurze hello.

* **Skalowalność**. Centrum IoT Azure skaluje toomillions równocześnie połączonych urządzeń miliony zdarzeń na sekundę.

## <a name="gateways"></a>Bramy

Bramy w rozwiązania IoT jest zwykle [bramy protokołu] [ lnk-iotedge] wdrożonej w chmurze hello lub [bramy pola] [ lnk-field-gateway] czyli wdrożonym lokalnie przez urządzenia. Brama protokołu wykonuje translację protokołu, na przykład MQTT tooAMQP. Brama pola można uruchomić analytics na krawędzi hello, podejmowanie decyzji zależne od czasu opóźnienia tooreduce, świadczenia usług zarządzania urządzeniami, wymuszanie zabezpieczeń i prywatności ograniczenia i przeprowadzić translacji protokołów. Oba typy bram pełnią rolę pośredników między urządzeniami i usługą IoT Hub.

Działanie bramy w terenie jest inne niż w przypadku urządzenia zapewniającego prosty routing ruchu (takiego jak zapora lub translator adresów sieciowych) — zwykle odgrywa ona aktywną rolę w zarządzaniu dostępem i przepływem informacji w rozwiązaniu.

Rozwiązanie może zawierać zarówno bramę protokołu, jak i bramę w terenie.

## <a name="how-does-iot-hub-work"></a>Jak działa usługa IoT Hub?

Centrum IoT Azure implementuje hello [przy pomocy usługi komunikacji] [ lnk-service-assisted-pattern] wzorzec toomediate hello interakcje między urządzeniami i rozwiązania zaplecza. Celem Hello przy pomocy usługi komunikacji jest tooestablish godne zaufania, dwukierunkowej komunikacji ścieżek między system kontroli, takich jak Centrum IoT i urządzenia specjalnych, które zostały wdrożone w niezaufanych fizycznego miejsca. wzorzec Hello ustanawia hello następujące zasady:

* Bezpieczeństwo jest nadrzędne w stosunku do wszystkich innych funkcji.

* Urządzenia nie akceptują niechcianej komunikacji z sieci. Urządzenie ustanawia wszystkie połączenia i trasy tylko w oparciu o reguły ruchu wychodzącego. Dla tooreceive urządzenia polecenie z zaplecza rozwiązania hello hello urządzenia muszą regularnie inicjować toocheck połączenia dla dowolnego tooprocess oczekującego polecenia.

* Urządzenia należy łączyć się tylko tooor ustanowić usług znane toowell trasy one są połączyć za pomocą, takich jak Centrum IoT.

* ścieżki komunikacji Hello między urządzeniami a usługą lub między urządzeniem a brama jest chroniona w warstwie protokołu aplikacji hello.

* Autoryzacja i uwierzytelnianie na poziomie systemu są oparte na tożsamościach poszczególnych urządzeń. Dzięki temu uprawnienia i poświadczenia dostępu mogą być niemal natychmiast odwoływane.

* Umożliwiają to komunikację dwukierunkową do urządzeń połączonych toopower sporadycznie termin lub problemy z łącznością, przytrzymując poleceń i powiadomień urządzenia, dopóki urządzenie łączy tooreceive je. Centrum IoT przechowuje kolejek specyficzne dla urządzenia dla polecenia hello, wysyłane.

* Aplikacji ładunek danych jest zabezpieczony oddzielnie dla chronionych przesyłania za pośrednictwem bramy tooa określonej usługi.

Hello przenośnych branży używa hello wzorzec przy pomocy usługi komunikacji w usługi powiadomień wypychanych tooimplement znaczne skali takich jak [usługi powiadomień wypychanych systemu Windows][lnk-wns], [Usługi Google Cloud Messaging][lnk-google-messaging], i [Apple Push Notification Service][lnk-apple-push].

Usługa IoT Hub jest obsługiwana przy użyciu ścieżki publicznej komunikacji równorzędnej usługi ExpressRoute.

## <a name="next-steps"></a>Następne kroki

Zobacz toolearn jak toosend wiadomości z urządzenia i ich odbierania z Centrum IoT, jak również sposób kieruje komunikat tooconfigure [wysyłania i odbierania wiadomości z Centrum IoT][lnk-send-messages].

toolearn Centrum IoT umożliwia zarządzanie urządzeniami oparte na standardach tooremotely można zarządzać, konfigurowanie i zaktualizować urządzenia, zobacz [omówienie zarządzania urządzeniami z Centrum IoT][lnk-device-management].

aplikacje klienckie tooimplement w różnych systemach operacyjnych i platform sprzętowych urządzeń, można użyć urządzenia Azure IoT hello zestawów SDK. urządzenie Hello zestawów SDK obejmują bibliotek, które ułatwiają wysyłanie danych telemetrycznych tooan IoT hub i odbieranie chmury do urządzenia wiadomości. Jeśli używasz urządzenia hello zestawów SDK, możesz wybrać spośród różnych toocommunicate protokoły sieci z Centrum IoT. toolearn więcej, zobacz hello [informacji o urządzeniu zestawów SDK][lnk-device-sdks].

tooget uruchomiono pisanie kodu i systemem niektóre przykłady, zobacz hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-get-started] samouczka.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "Service Assisted Communication (Komunikacja korzystająca z usług) — wpis na blogu autorstwa Clemensa Vastersa"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
