---
title: "aaaOverview Azure IoT krawędzi | Dokumentacja firmy Microsoft"
description: "Opisano hello klucza architektury pojęcia w programie Azure IoT Edge takie jak bramy, moduły i brokerów."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Azure IoT krawędzi architektury pojęcia.

Przed sprawdzić wszelkie przykładowy kod lub utworzyć własne pole bramę, używając krawędzi IoT, zapoznaj się hello podstawowe pojęcia, które stanowi podstawę hello architektury IoT krawędzi.

## <a name="iot-edge-modules"></a>Moduły krawędzi IoT

Tworzenie bramy Azure IoT krawędzi, tworząc i składanie *modułów krawędzi IoT*. Użyj modułów *wiadomości* tooexchange danych ze sobą. Moduł odbiera komunikat, wykonuje akcję na nim opcjonalnie przekształca je w nowej wiadomości i publikuje ją dla tooprocess innych modułów. Niektóre moduły mogą jedynie tworzyć nowe komunikaty i nigdy nie przetwarzają komunikatów przychodzących. Łańcuch modułów tworzy potoku przetwarzania danych z każdego modułu wykonania transformację na powitania danych w jednym punkcie w tym potoku.

![Łańcuch modułów w bramie utworzonej przy użyciu usługi Azure IoT Edge][1]

Krawędź IoT zawiera hello następujące składniki:

* Moduły wstępnie napisane wykonać typowe funkcje bramy.
* interfejsy Hello a developer służy toowrite niestandardowe moduły.
* Witaj toodeploy niezbędne infrastruktury, a następnie uruchom zestaw modułów.

Hello SDK udostępnia warstwę abstrakcji, która umożliwia toorun bram toobuild na różnych systemów operacyjnych i platform.

![Warstwa abstrakcji usługi Azure IoT Edge][2]

## <a name="messages"></a>Komunikaty

Chociaż planowanie modułów przekazywania wiadomości tooeach innych jest tooconceptualize wygodny sposób, w jaki sposób funkcje bramy, go nie odzwierciedlają dokładnie co się stanie. Moduły krawędzi IoT Użyj toocommunicate brokera ze sobą. Moduły publikowania komunikatów brokera toohello (przy użyciu wzorce obsługi komunikatów, takie jak magistrala lub publikowania/subskrypcji), a następnie zezwolić na powitania brokera trasy hello komunikat toohello modułów połączonych tooit.

Moduł używa hello **Broker_Publish** funkcji toopublish brokera toohello komunikatów. Hello broker zapewnia moduł tooa wiadomości przez funkcję wywołania zwrotnego. Komunikat składa się z zestawu właściwości klucz/wartość oraz zawartości przekazywanej w postaci bloku pamięci.

![Rola Hello hello brokera w programie Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a>Routing i filtrowanie komunikatów

Istnieją dwa sposoby toodirect wiadomości toohello poprawne krawędzi IoT modułów:

* Można przekazać zestawu łączy mogą zostać przekazane brokera toohello będzie wówczas traktował brokera hello hello źródłowy i odbiorczy dla każdego modułu.
* Moduł można filtrować według właściwości hello wiadomości powitania.

Moduł tylko powinien operować na komunikat, jeśli wiadomość hello jest przeznaczony dla niego. Łącza i efektywnie filtrowania wiadomości utworzyć potok wiadomości.

## <a name="next-steps"></a>Następne kroki

Zobacz te pojęcia stosowane w próbce można uruchomić toosee [architektura Eksplorowanie usługi Azure IoT krawędzi][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md