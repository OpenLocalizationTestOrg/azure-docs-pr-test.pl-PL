---
title: "Brama protokołu IoT aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak toouse Azure IoT protokołu możliwości Centrum IoT tooextend bramy i protokół obsługi tooenable urządzeń tooconnect tooyour Centrum przy użyciu protokołów nie natywnie obsługiwane przez Centrum IoT."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Obsługa protokołów dodatkowych Centrum IoT
Centrum IoT Azure natywnie obsługuje komunikację za pośrednictwem protokołów hello MQTT, AMQP i HTTP. W niektórych przypadkach urządzenia lub pola bramy może nie być możliwe toouse, jeden z tych standardowych protokołów i wymaga dostosowania protokołu. W takich przypadkach można użyć niestandardowych bramy. Niestandardowe bramy można włączyć protokołu dostosowanie punkty końcowe Centrum IoT mostkowanie hello tooand ruchu z Centrum IoT. Można użyć hello [brama protokołu Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) jako dostosowania protokołu tooenable bram dla Centrum IoT.

## Brama protokołu IoT Azure
Brama protokołu Azure IoT Hello to struktura służąca do dostosowania protokołu, który jest przeznaczony dla wysokiej skali, komunikację dwukierunkową urządzenie z Centrum IoT. Brama protokołu Hello jest przekazujące składnik, który akceptuje połączenia urządzenia za pośrednictwem określonego protokołu. Tworzy ono hello ruchu tooIoT Centrum za pośrednictwem protokołu AMQP 1.0. Brama protokołu Azure IoT Hello jest dostępny jako oprogramowanie open source project tooprovide możliwość dodawania obsługę różnych protokołów i protokołów.

Brama protokołu hello na platformie Azure w taki sposób, skalowalnej można wdrożyć za pomocą usługi Azure Service Fabric, roli proces roboczy usług Azure Cloud Services lub maszyn wirtualnych systemu Windows. Ponadto bramy protokołu hello można wdrożyć w środowiskach lokalnych, takich jak pole bram.

Brama protokołu Azure IoT Hello zawiera karty protokołu MQTT, która umożliwia możesz toocustomize hello zachowanie protokołu MQTT w razie potrzeby. Ponieważ Centrum IoT udostępnia wbudowaną obsługę protokołu v3.1.1 MQTT hello, tylko warto za pomocą karty protokołu MQTT hello, jeśli protokół dostosowań lub określonych wymagań dotyczących dodatkowe funkcje są wymagane.

Karta MQTT Hello przedstawiono również hello model programowania do tworzenia protokołu kart dla innych protokołów. Ponadto model programowania protokołu bramy hello Azure IoT umożliwia specjalizowany tooplug w składnikach niestandardowych do przetwarzania, takich jak niestandardowe uwierzytelnianie, przekształcenia wiadomości, kompresji i dekompresji lub szyfrowania i odszyfrowywania ruchu między urządzeniami hello i Centrum IoT.

Elastyczność brama protokołu hello i implementacji MQTT znajdują się w projekcie oprogramowania typu open source. Dzięki temu toocustomize hello implementacji zgodnie z potrzebami.

## Następne kroki
więcej informacji na temat brama protokołu Azure IoT hello toolearn i w jaki sposób toouse i wdrożyć go jako część rozwiązania IoT, zobacz:

* [Repozytorium brama protokołu IoT Azure w serwisie GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Przewodnik dewelopera bramy protokołu Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn więcej informacji na temat planowania wdrożenia Centrum IoT, zobacz:

* [Porównaj z usługi Event Hubs][lnk-compare]
* [Skalowanie, wysokiej dostępności i odzyskiwania po awarii][lnk-scaling]
* [Przewodnik dewelopera Centrum IoT][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
