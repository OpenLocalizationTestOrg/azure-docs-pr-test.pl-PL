---
title: "aaaAzure IoT wstępnie rozwiązania | Dokumentacja firmy Microsoft"
description: "Opis hello Azure IoT wstępnie rozwiązań i ich architektura z zasobami tooadditional łącza."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Co to są hello pakiet IoT Azure wstępnie rozwiązania?

rozwiązania pakiet IoT Azure wstępnie Hello są implementacje typowe wzorce rozwiązania IoT wdrożenie tooAzure przy użyciu Twojej subskrypcji. Program hello wstępnie rozwiązań:

* Jako punktu wyjściowego dla własnych rozwiązań IoT.
* toolearn typowe wzorce projektowania rozwiązania IoT i rozwoju.

Poszczególnych wstępnie skonfigurowanych rozwiązań jest pełna, end-to-end implementacji, że używa symulowane telemetrii toogenerate urządzeń.

Można pobrać toocustomize kodu źródłowego pełną hello i rozszerzyć hello toomeet rozwiązania IoT indywidualnymi wymaganiami.

> [!NOTE]
> toodeploy hello wstępnie rozwiązania, odwiedź stronę [pakiet IoT Microsoft Azure][lnk-azureiotsuite]. Artykuł Hello [Rozpoczynanie pracy z rozwiązania IoT wstępnie hello] [ lnk-getstarted-preconfigured] zawiera więcej informacji na temat sposobu rozwiązania hello toodeploy i uruchom jeden z.

Witaj poniższej tabeli przedstawiono sposób rozwiązania hello mapowania toospecific IoT funkcje:

| Rozwiązanie | Wprowadzanie danych | Tożsamość urządzenia | Zarządzanie urządzeniami | Sterowanie i kontrola | Reguły i akcje | Analiza predykcyjna |
| --- | --- | --- | --- | --- | --- | --- |
| [Zdalne monitorowanie][lnk-getstarted-preconfigured] |Tak |Tak |Tak |Tak |Tak |- |
| [Konserwacja zapobiegawcza][lnk-predictive-maintenance] |Tak |Tak |- |Tak |Tak |Tak |
| [Połączona fabryka][lnk-getstarted-factory] |Tak |Tak |Tak |Tak |Tak |- |

* *Wprowadzanie danych*: transfer danych przychodzących danych w chmurze toohello skali.
* *Tożsamość urządzenia*: Zarządzanie tożsamościami unikatowych urządzeń i sterowanie rozwiązanie toohello dostępu do urządzenia.
* *Zarządzanie urządzeniami*: zarządzanie metadanymi urządzeń i wykonywanie operacji, takich jak ponowne uruchamianie urządzeń i aktualizacje oprogramowania układowego.
* *Polecenia i kontroli*: toocause hello urządzenia tootake Action, wysyłania wiadomości tooa urządzenia z hello chmury.
* *Reguły i akcje*: tooact określonych danych urządzenia do chmury oraz zaplecza rozwiązania hello używa reguł.
* *Analizy predykcyjnej*: zaplecza rozwiązania hello analizuje toopredict danych urządzenia do chmury, gdy określonych akcji powinny mieć miejsce. Na przykład analizowanie powietrznego aparat telemetrii toodetermine podczas konserwacji aparatu.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>Omówienie wstępnie skonfigurowanego rozwiązania monitorowania zdalnego

Wybraliśmy się, że toodiscuss hello zdalnego wstępnie skonfigurowane rozwiązanie monitorowania w tym artykule, ponieważ zastosowano wiele wspólne elementy projektów, które hello udziału innych rozwiązań.

Witaj poniższym diagramie przedstawiono kluczowe elementy hello hello zdalne monitorowanie rozwiązania. Witaj poniższe sekcje zawierają więcej informacji na temat tych elementów.

![Architektura wstępnie skonfigurowanego rozwiązania monitorowania zdalnego][img-remote-monitoring-arch]

## <a name="devices"></a>Urządzenia

Podczas wdrażania hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie czterech symulowanego urządzenia są wstępnie przygotowany w rozwiązaniu hello, symulującą urządzenie chłodzące. Symulowane urządzenia mają wbudowany model generowania wartości temperatury i wilgotności, który emituje dane telemetryczne. Te symulowane urządzenia mogą wykonywać następujące działania:

- Ilustrowanie hello end-to-end przepływu danych za pośrednictwem hello rozwiązania.
- Zapewniać wygodne źródło danych telemetrycznych.
- Podaj docelowy dla metod lub poleceń, jeśli jesteś deweloperem zaplecza za pomocą rozwiązania hello jako punkt początkowy dla implementacji niestandardowych.

Witaj symulowane urządzeń w rozwiązaniu hello mogą odpowiadać toohello po komunikacji chmury do urządzenia:

- *Metody ([bezpośrednie metody][lnk-direct-methods])*: metoda komunikacja dwukierunkowa, gdzie podłączonego urządzenia jest oczekiwany toorespond natychmiast.
- *Polecenia (chmury do urządzenia wiadomości)*: metoda komunikacja jednokierunkowa, gdy urządzenie pobiera polecenia hello z kolejki trwałe.

Porównanie tych różnych rozwiązań zawiera temat [Wskazówki dotyczące komunikacji z chmury do urządzenia][lnk-c2d-guidance].

Kiedy urządzenie łączy najpierw tooIoT Centrum w hello wstępnie skonfigurowane rozwiązanie, wysyła urządzenia informacji komunikat toohello koncentratora. Ten komunikat wylicza metody hello hello urządzenia mogą odpowiadać na. W zdalnym wstępnie skonfigurowane rozwiązanie monitorujące hello symulowanego urządzenia obsługują tych metod:

* *Inicjowanie aktualizacji oprogramowania układowego*: Ta metoda inicjuje zadania asynchronicznego na powitania tooperform urządzenia aktualizacji oprogramowania. zadanie asynchroniczne Hello używa właściwości zgłoszone toodeliver stan aktualizacji toohello rozwiązania z pulpitu nawigacyjnego.
* *Ponowny rozruch*: Ta metoda powoduje hello symulowane urządzenie tooreboot.
* *FactoryReset*: Ta metoda wyzwala resetowania hello symulowane urządzenie do ustawień fabrycznych.

Kiedy urządzenie łączy najpierw tooIoT Centrum w hello wstępnie skonfigurowane rozwiązanie, wysyła urządzenia informacji komunikat toohello koncentratora. Ten komunikat wylicza hello hello urządzenia mogą odpowiadać na polecenia. W zdalnym wstępnie skonfigurowane rozwiązanie monitorujące hello symulowanego urządzenia obsługują następujące polecenia:

* *Urządzenia polecenie ping*: hello odpowiedzi polecenia toothis o potwierdzenie. To polecenie jest przydatne w przypadku sprawdzanie urządzenia hello jest nadal aktywne i nasłuchiwania.
* *Uruchom Telemetrii*: nakazuje toostart urządzenia hello wysyłania danych telemetrycznych.
* *Zatrzymaj Telemetrii*: nakazuje toostop urządzenia hello wysyłania danych telemetrycznych.
* *Zmień temperatury Ustaw punkt*: formanty hello symulowane temperatury telemetrii wartości hello urządzenie wysyła. To polecenie jest przydatne w przypadku testowania logiki zaplecza.
* *Dane telemetryczne diagnostycznych*: kontroluje, czy urządzenie hello należy wysłać temperatury zewnętrznych hello jako telemetrii.
* *Zmiany stanu urządzenia*: ustawia hello urządzenia stan metadanych właściwości hello raporty dotyczące urządzeń. To polecenie jest przydatne w przypadku testowania logiki zaplecza.

Możesz dodać więcej rozwiązania toohello symulowanego urządzenia, które Emituj hello tego samego telemetrii i toohello odpowiedź tej samej metody i poleceń.

Ponadto tooresponding toocommands i metody rozwiązania hello używa [twins urządzenia][lnk-device-twin]. Urządzenia używają urządzeń twins tooreport właściwości wartości toohello zaplecza rozwiązania. pulpit nawigacyjny rozwiązania Hello używa wartości właściwości toonew potrzeby tooset twins urządzenia na urządzeniach. Na przykład podczas raporty urządzeń hello symulowane procesu aktualizacji oprogramowania układowego hello hello stan hello zaktualizowane przy użyciu właściwości zgłoszony.

## <a name="iot-hub"></a>Usługa IoT Hub

W tym rozwiązaniu wstępnie skonfigurowane hello wystąpienia Centrum IoT odpowiada toohello *brama chmury* w typowym [architektury rozwiązania IoT][lnk-what-is-azure-iot].

Centrum IoT odbiera telemetrię z urządzeń hello w jednym punkcie końcowym. Centrum IoT zachowuje również odpowiedniego dla urządzenia punktów końcowych, gdzie poszczególne urządzenia mogą pobierać hello poleceń, które są wysyłane tooit.

Centrum IoT Hello udostępnia telemetrii hello odebranych za pośrednictwem telemetrii po stronie usługi hello odczytać punktu końcowego.

możliwości zarządzania urządzeniami Hello Centrum IoT umożliwia toomanage możesz właściwości urządzenia z hello rozwiązanie portalu i harmonogram zadań wykonujących operacje takie jak:

- Ponowne uruchamianie urządzenia
- Zmienianie stanów urządzenia
- Przeprowadzanie aktualizacji oprogramowania układowego

## <a name="azure-stream-analytics"></a>Usługa Azure Stream Analytics

Witaj wstępnie skonfigurowane rozwiązanie zawiera trzy [Azure Stream Analytics] [ lnk-asa] (ASA) zadania toofilter hello telemetrii strumienia z hello urządzeń:

* *Zadanie DeviceInfo* -Centrum zdarzeń tooan danych dane wyjściowe, który przekierowuje rejestrze urządzeń rozwiązania toohello komunikaty dotyczące rejestracji urządzenia. Rejestr tego urządzenia to baza danych Azure Cosmos DB. Komunikaty te są wysyłane, gdy pierwszy raz łączy urządzenie lub w odpowiedzi tooa **zmienić stan urządzenia** polecenia.
* *Zadanie telemetrii* — wysyła wszystkie nieprzetworzone dane telemetryczne tooAzure magazyn obiektów blob chłodni i oblicza wyświetlane na pulpicie nawigacyjnym rozwiązania hello agregacji danych telemetrycznych.
* *Zadanie reguły* — filtry hello strumienia danych telemetrycznych dla wartości, które przekraczają progów żadnych reguł i dane wyjściowe hello Centrum zdarzeń tooan danych. Po regułę, widok pulpitu nawigacyjnego portalu rozwiązania hello wyświetla to zdarzenie jako nowy wiersz w tabeli historii alarm hello. Te reguły można również uruchomić akcję na podstawie ustawień hello zdefiniowane na powitania **reguły** i **akcje** widoków w hello rozwiązanie portalu.

W tym rozwiązaniu wstępnie skonfigurowane hello ASA zadania stanowią część toohello **zaplecza rozwiązania IoT** w typowym [architektury rozwiązania IoT][lnk-what-is-azure-iot].

## <a name="event-processor"></a>Procesor zdarzeń

W tym rozwiązaniu wstępnie skonfigurowane procesora zdarzeń hello jest częścią hello **zaplecza rozwiązania IoT** w typowym [architektury rozwiązania IoT][lnk-what-is-azure-iot].

Witaj **DeviceInfo** i **reguły** ASA zadania wysyłania ich koncentratory tooEvent dane wyjściowe w celu dostarczania usług zaplecza tooother. używa rozwiązania Hello [EventProcessorHost] [ lnk-event-processor] działania wystąpienia [zadania WebJob][lnk-web-job], wiadomości powitania tooread z tych centrów zdarzeń. Witaj **EventProcessorHost** używa:
- Witaj **DeviceInfo** tooupdate hello urządzenia danych w bazie danych DB rozwiązania Cosmos hello.
- Witaj **reguły** tooinvoke hello logiki aplikacji i aktualizacji hello alerty danych wyświetlane w portalu rozwiązania hello.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>Rejestr tożsamości urządzeń, bliźniacza reprezentacja urządzenia i usługa Cosmos DB

Każde wystąpienie usługi IoT Hub zawiera [rejestr tożsamości urządzeń][lnk-identity-registry], który przechowuje klucze urządzeń. Centrum IoT używa tych informacji uwierzytelniania urządzeń — urządzenia muszą zostać zarejestrowane i ma prawidłowy klucz, zanim można połączyć toohello Centrum.

A [dwie urządzenia] [ lnk-device-twin] jest zarządzane przez Centrum IoT hello dokumentu JSON. Bliźniacza reprezentacja urządzenia zawiera następujące elementy:

- Właściwości zgłoszone wysyłane przez hello urządzenia toohello koncentratora. Te właściwości można wyświetlić w portalu rozwiązania hello.
- Odpowiednie właściwości, które mają toosend toohello urządzenia. Te właściwości można ustawić w hello rozwiązanie portalu.
- Tagi, które istnieją tylko w Witaj dwie urządzenia, a nie na powitania urządzenia. Te listy toofilter tagi urządzeń można użyć w portalu rozwiązania hello.

To rozwiązanie wymaga urządzenia twins toomanage urządzenia metadanych. rozwiązanie Hello używa również dodatkowe urządzenia określonego rozwiązania danych toostore bazy danych DB rozwiązania Cosmos takich jak polecenia hello obsługiwane przez każdego urządzenia i hello historii poleceń.

rozwiązanie Hello musi również przechowywać hello informacji w rejestrze tożsamości urządzeń hello synchronizowane z hello zawartość bazy danych DB rozwiązania Cosmos hello. Witaj **EventProcessorHost** używa hello danych z **DeviceInfo** toomanage hello synchronizacji zadania stream analytics.

## <a name="solution-portal"></a>Portal rozwiązania

![portal rozwiązania][img-dashboard]

portal rozwiązania Hello jest UI opartych na sieci web, który jest wdrożony toohello chmurze jako część hello wstępnie skonfigurowane rozwiązanie. Umożliwia on wykonywanie następujących czynności:

* Wyświetlanie historii danych telemetrycznych i alarmów na pulpicie nawigacyjnym.
* Aprowizacja nowych urządzeń.
* Monitorowanie urządzeń i zarządzanie nimi.
* Wysyłanie poleceń toospecific urządzeń.
* Wywoływanie metod na konkretnych urządzeniach.
* Zarządzanie regułami i akcjami.
* Planowanie zadań toorun na co najmniej jedno urządzenie.

W tym rozwiązaniu wstępnie skonfigurowane, portal rozwiązania hello jest częścią hello **zaplecza rozwiązania IoT** i część hello **łączności przetwarzania i biznesowych** w typowych hello [rozwiązania IoT Architektura][lnk-what-is-azure-iot].

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat architektury rozwiązań IoT, zobacz dokument [Microsoft Azure IoT services: Reference Architecture][lnk-refarch] (Usługi Microsoft Azure IoT: architektura referencyjna).

Teraz wiesz, jakie wstępnie skonfigurowane rozwiązanie jest, możesz rozpocząć pracę, wdrażając hello *monitorowania zdalnego* wstępnie skonfigurowane rozwiązanie: [Rozpoczynanie pracy z rozwiązaniami hello wstępnie] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
