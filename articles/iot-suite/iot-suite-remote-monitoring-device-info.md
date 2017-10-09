---
title: "aaaDevice informacji metadanych w hello zdalne monitorowanie rozwiązania | Dokumentacja firmy Microsoft"
description: "Opis hello Azure IoT wstępnie skonfigurowane rozwiązanie monitorowania zdalnego i jego architektury."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Urządzenie informacji metadanych w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie

Hello pakiet Azure IoT zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, przedstawiono podejście do zarządzania urządzeniami metadanych. W tym artykule przedstawiono podejście hello to rozwiązanie ma tooenable toounderstand możesz:

* Jakie rozwiązania hello metadanych urządzeń są przechowywane.
* Sposób rozwiązania hello zarządza hello metadane urządzenia.

## <a name="context"></a>Kontekst

Witaj monitorowania zdalnego wstępnie skonfigurowane rozwiązanie używa [Centrum IoT Azure] [ lnk-iot-hub] tooenable toohello danych toosend Twojego urządzenia w chmurze. rozwiązanie Hello przechowuje informacje o urządzeniach w trzech różnych miejscach:

| Lokalizacja | Informacje przechowywane | Wdrażanie |
| -------- | ------------------ | -------------- |
| Tożsamość rejestru | Identyfikator urządzenia, klucze uwierzytelniania, włączony stan | Wbudowane tooIoT Centrum |
| Twins urządzenia | Metadane: właściwości zgłoszone, odpowiednie właściwości, znaczniki | Wbudowane tooIoT Centrum |
| Cosmos DB | Historię poleceń i — metoda | Niestandardowe dla rozwiązania |

Centrum IoT obejmuje [rejestrze tożsamości urządzeń] [ lnk-identity-registry] toomanage dostęp do Centrum IoT tooan i używa [twins urządzenia] [ lnk-device-twin] toomanage metadane urządzenia . Istnieje również zdalnego monitorowania określonego rozwiązania *rejestru urządzenia* który przechowuje historię poleceń i metody. zdalne monitorowanie używa rozwiązania Hello [DB rozwiązania Cosmos] [ lnk-docdb] tooimplement bazy danych magazynu niestandardowego dla historii poleceń i metody.

> [!NOTE]
> Hello zdalnego wstępnie skonfigurowane rozwiązanie monitorujące zachowuje rejestrze tożsamości urządzeń hello zsynchronizowane z hello informacji w bazie danych DB rozwiązania Cosmos hello. Oba rozwiązania używają hello określenie tej samej toouniquely identyfikator urządzenia każde urządzenie podłączone tooyour Centrum IoT.

## <a name="device-metadata"></a>Metadane urządzenia

Centrum IoT przechowuje [dwie urządzenia] [ lnk-device-twin] dla poszczególnych urządzeń fizycznych i symulowane podłączonej tooa zdalne monitorowanie rozwiązania. rozwiązanie Hello używa urządzenia twins toomanage hello metadane skojarzone z urządzeń. Dwie urządzenia jest dokumentem JSON obsługiwany przez Centrum IoT i rozwiązania hello używa hello toointeract API Centrum IoT z twins urządzenia.

Dwie urządzenia przechowuje trzy rodzaje metadanych:

- *Zgłoszone właściwości* są wysyłane z Centrum IoT tooan przez urządzenie. W hello zdalnego rozwiązanie monitorujące, symulowanego urządzenia wysyłają właściwości zgłoszone podczas rozruchu, a w odpowiedzi zbyt**zmienić stan urządzenia** polecenia i metod. Można wyświetlić właściwości zgłoszone w hello **listę urządzeń** i **szczegóły urządzenia** w hello rozwiązanie portalu. Zgłoszony właściwości są tylko do odczytu.
- *Żądany właściwości* są pobierane z Centrum IoT hello przez urządzenia. Jest odpowiedzialny za hello toomake urządzenia hello żadnej konfiguracji niezbędne zmiany na urządzeniu hello. Jest również odpowiedzialność hello hello urządzenia tooreport hello zmiany toohello zapasowego Centrum jako właściwość zgłoszony. Można ustawić wartości właściwości żądaną za pośrednictwem portalu rozwiązania hello.
- *Tagi* istnieje tylko w Witaj dwie urządzenia i nigdy nie są synchronizowane z urządzeniem. Można ustawić wartości tagów w portalu rozwiązania hello i ich używać, aby filtrować listę hello urządzeń. rozwiązanie Hello używa również tag tooidentify hello ikona toodisplay dla urządzenia w portalu rozwiązania hello.

Przykład zgłosił, że właściwości z urządzeń hello symulowane obejmują producenta, numer modelu szerokości geograficznej i długości. Symulowane urządzeń również zwrócić hello lista metod obsługiwanych zgłoszone właściwości.

> [!NOTE]
> Witaj kodu symulowane urządzenie używa tylko hello **Desired.Config.TemperatureMeanValue** i **Desired.Config.TelemetryInterval** odpowiednie właściwości tooupdate hello zgłosił odesłał właściwości tooIoT koncentratora. Wszystkie inne żądanej właściwości żądania zmiany są ignorowane.

Urządzenia informacji metadanych dokumentem JSON przechowywane w bazie danych programu hello urządzenia rejestru DB rozwiązania Cosmos ma hello następujące struktury:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Informacje o urządzeniu mogą obejmować metadanych toodescribe hello telemetrii hello urządzenie wysyła tooIoT koncentratora. rozwiązanie monitorowania zdalnego Hello używa tego toocustomize metadanych telemetrii sposób wyświetlania pulpitu nawigacyjnego hello [dynamiczne telemetrii][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Cykl życia

Po utworzeniu urządzenia w portalu rozwiązania hello, rozwiązanie hello tworzy wpis w hello polecenie toostore bazy danych DB rozwiązania Cosmos i historii — metoda. W tym momencie rozwiązanie hello również tworzy wpis dla urządzenia hello w rejestrze tożsamości urządzeń hello, który generuje hello klucze hello urządzenie używa tooauthenticate z Centrum IoT. Tworzy dwie urządzenia.

Kiedy urządzenie łączy się najpierw toohello rozwiązania, wysyła zgłoszone właściwości oraz komunikat z informacjami urządzenia. Witaj zgłosił, że wartości właściwości są automatycznie zapisywane w Witaj dwie urządzenia. Witaj zgłosił, że właściwości zawierają hello producenta urządzenia, numer modelu, numer seryjny i listę obsługiwanych metod. komunikat z informacjami urządzenia Hello zawiera listę hello hello poleceń, które obsługuje hello urządzenie tym informacje o żadnych parametrów polecenia. Gdy rozwiązanie hello odbiera ten komunikat, aktualizuje informacje o urządzeniu hello w hello DB rozwiązania Cosmos w bazie danych.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Umożliwia wyświetlanie i edytowanie informacji o urządzeniu w portalu rozwiązania hello

Witaj listy urządzenia w portalu rozwiązania hello wyświetla następujące właściwości urządzenia jako kolumny domyślnie hello: **stan**, **DeviceId**, **producenta**, **Numer modelu**, **numer seryjny**, **oprogramowania układowego**, **platformy**, **procesora**i  **Zainstalowana pamięć RAM**. Można dostosować hello kolumn, klikając **Edytor kolumn**. Witaj właściwości urządzenia **szerokości geograficznej** i **geograficzne** dysków na pulpicie nawigacyjnym hello hello lokalizacji w hello mapy Bing.

![Edytor kolumn na liście urządzeń][img-device-list]

W hello **szczegóły urządzenia** okienku w portalu rozwiązania hello, można edytować odpowiednie właściwości i tagi (zgłosić właściwości są tylko do odczytu).

![W okienku szczegółów urządzenia][img-device-edit]

Można użyć hello rozwiązanie portalu tooremove urządzenia z rozwiązania. Po usunięciu urządzenia rozwiązania hello usuwa hello urządzenia wpis w rejestrze tożsamości, a następnie usuwa Witaj dwie urządzenia. Witaj rozwiązania spowoduje również usunięcie urządzenia toohello powiązane informacje z bazy danych DB rozwiązania Cosmos hello. Aby móc usunąć urządzenie, należy ją wyłączyć.

![Usuwanie urządzenia][img-device-remove]

## <a name="device-information-message-processing"></a>Przetwarzanie komunikatów informacji urządzenia

Komunikaty informacyjne urządzenia wysyłane przez urządzenie różnią się od komunikatów telemetrii. Komunikaty informacyjne urządzenia obejmują hello poleceń, które urządzenia mogą odpowiadać na, a cała historia polecenia. Centrum IoT, sama nie ma informacji o metadanych hello komunikat z informacjami urządzenia i procesy hello wiadomości w hello samo przetwarza komunikat dowolnego urządzenia do chmury. W hello zdalne monitorowanie rozwiązania [Azure Stream Analytics] [ lnk-stream-analytics] zadania (ASA) odczytuje wiadomości powitania z Centrum IoT. Witaj **DeviceInfo** filtry dla wiadomości, które zawierają zadania stream analytics **"ObjectType": "DeviceInfo"** i przekazuje je toohello **EventProcessorHost** hosta wystąpienie, które uruchamia zadanie sieci web. Logikę hello **EventProcessorHost** wystąpienie używa hello urządzenia identyfikator toofind hello DB rozwiązania Cosmos rekordu hello określonych urządzeń i aktualizacji hello rekordu.

> [!NOTE]
> Komunikat z informacjami urządzenia jest standardowy komunikat urządzenia do chmury. rozwiązanie Hello rozróżnia komunikaty informacyjne urządzenia i dane telemetryczne wiadomości przy użyciu ASA zapytań.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu learning, jak można dostosować hello wstępnie rozwiązania można eksplorować niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:

* [Omówienie rozwiązania konserwacji predykcyjnej wstępnie][lnk-predictive-overview]
* [Często zadawane pytania dotyczące Pakietu IoT][lnk-faq]
* [Zabezpieczenia IoT z hello tła w][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
