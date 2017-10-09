---
title: Skalowanie Centrum IoT aaaAzure | Dokumentacja firmy Microsoft
description: "Jak tooscale Twojego toosupport Centrum IoT z przepływności przewidywanego wiadomości. Zawiera podsumowanie hello obsługiwana przepływność dla każdej warstwy i opcje dotyczące dzielenia na fragmenty."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>Skalować rozwiązania IoT hub
Centrum IoT Azure może obsługiwać tooa milionów jednocześnie podłączonego urządzenia. Aby uzyskać więcej informacji, zobacz [Centrum IoT cennik][lnk-pricing]. Każda jednostka Centrum IoT umożliwia pewną liczbę wiadomości codzienne.

tooproperly skalować rozwiązania należy wziąć pod uwagę określonego korzystanie z Centrum IoT. W szczególności należy wziąć pod uwagę przepływności szczytu hello wymagane hello następujące kategorie działań:

* Komunikaty z urządzenia do chmury
* Komunikaty chmury do urządzenia
* Operacje rejestru tożsamości

W dodatkowych toothis przepływności informacji, zobacz [Centrum IoT przydziały i limity] [ IoT Hub quotas and throttles] i odpowiednio zaprojektować rozwiązanie.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Przepustowość urządzenia do chmury i chmury do urządzenia wiadomości
Hello najlepsze sposób toosize rozwiązania IoT Hub jest tooevaluate hello ruchu na podstawie jednostkę.

Urządzenia do chmury wiadomości zgodna z tymi wytycznymi długoterminowa przepustowość.

| Warstwa | Długoterminowa przepustowość | Wskaźnik wysyłania stałej |
| --- | --- | --- |
| S1 |Zapasowej too1111 KB na minutę na jednostkę<br/>(1,5 GB/dzień/jednostka) |Średnia 278 komunikatów na minutę na jednostkę<br/>(400 000 komunikatów/dzień na jednostkę) |
| S2 |Zapasowej too16 MB na minutę na jednostkę<br/>(22.8 GB/dzień/jednostka) |Średnia 4,167 komunikatów na minutę na jednostkę<br/>(6 mln wiadomości/dzień na jednostkę) |
| S3 |Zapasowej too814 MB na minutę na jednostkę<br/>(1144.4 GB/dzień/jednostka) |Średnia 208,333 komunikatów na minutę na jednostkę<br/>(300 milionów wiadomości/dzień na jednostkę) |

## <a name="identity-registry-operation-throughput"></a>Przepływność operacji rejestru tożsamości
Operacje rejestru tożsamości Centrum IoT nie powinni toobe czasu wykonywania operacji, ponieważ są one przede wszystkim pokrewne toodevice inicjowania obsługi administracyjnej.

Dla określonego serii numerów wydajności, zobacz [Centrum IoT przydziały i limity][IoT Hub quotas and throttles].

## <a name="sharding"></a>Dzielenia na fragmenty
Podczas jednego centrum IoT można skalować toomillions urządzenia, czasami rozwiązanie wymaga charakterystyk wydajności zależnych, które pojedynczego Centrum IoT nie może zagwarantować. W takim przypadku zaleca się partycji urządzenia do wielu centra IoT. Centra IoT wielu smooth seria ruchu i uzyskiwanie przepustowość wymagana hello lub szybkości działania, które są wymagane.

## <a name="next-steps"></a>Następne kroki
toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
