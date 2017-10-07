---
title: "filtry połączenia IP Centrum IoT aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak adresy IP toouse, które filtrowania tooblock połączenia z określonego adresu IP dla Centrum Azure IoT tooyour. Możesz zablokować połączenia z poszczególnych lub zakresów adresów IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>Używanie filtrów IP

Zabezpieczenia są istotnym elementem każde rozwiązanie IoT oparte na usłudze Azure IoT Hub. Czasami potrzebny tooexplicitly określić hello adresów IP, z których urządzenia można podłączyć jako część konfiguracji zabezpieczeń. Witaj _filtrów IP_ pozwala tooconfigure reguł odrzucenia lub akceptować ruch z określonych adresów IPv4.

## <a name="when-toouse"></a>Gdy toouse

Istnieją dwa określonych przypadków użycia, gdy punkty końcowe Centrum IoT hello tooblock przydatne dla określonych adresów IP nie jest:

- Centrum IoT powinny odbierać dane tylko z określonego zakresu adresów IP i odrzucić wszystkie inne elementy. Na przykład w przypadku korzystania z Centrum IoT [Azure Express Route] toocreate prywatnych połączeń między centrum IoT i infrastruktury lokalnej.
- Należy tooreject ruchu z adresów IP, które zostały zidentyfikowane jako podejrzane przez administratora Centrum IoT hello.

## <a name="how-filter-rules-are-applied"></a>Sposób stosowania reguły filtrowania

reguły filtra IP Hello są stosowane w hello poziomu usług Centrum IoT. W związku z tym reguł filtru IP hello zastosować tooall połączeń z urządzeniami i aplikacjami zaplecza za pomocą obsługiwanych protokołów.

Każda próba połączenia z adresu IP odpowiadającego wydzielenia reguły IP w Centrum IoT odbiera kod stanu 401 nieautoryzowane i opis. komunikat odpowiedzi Hello nie mogą zawierać hello IP reguły.

## <a name="default-setting"></a>Ustawienie domyślne

Domyślnie program hello **filtrów IP** siatki w portalu hello Centrum IoT jest pusta. To ustawienie domyślne oznacza, że Centrum akceptuje połączenia dowolnego adresu IP. To ustawienie domyślne to równoważne tooa regułę, która akceptuje zakres adresów IP 0.0.0.0/0 hello.

![Filtr IP domyślnych Centrum IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>Dodawanie lub edytowanie reguły filtru adresu IP

Po dodaniu reguły filtru adresu IP, zostanie wyświetlony monit o hello następujące wartości:

- **Nazwę reguły filtru IP** który musi być unikatowy, bez uwzględniania wielkości liter, alfanumeryczne ciąg się too128 znaków. Tylko plus znaki alfanumeryczne ASCII 7-bitowego hello `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` są akceptowane.
- Wybierz **Odrzuć** lub **zaakceptować** jako hello **akcji** reguły filtru IP hello.
- Podaj pojedynczy adres IPv4 lub blok adresów IP w notacji CIDR. Na przykład w CIDR 192.168.100.0/22 notacji reprezentuje hello 1024 adresy IPv4 z 192.168.100.0 too192.168.103.255.

![Dodaj Centrum IoT tooan reguły filtru adresu IP][img-ip-filter-add-rule]

Po zapisaniu hello reguły, zostanie wyświetlony alert informujący, że aktualizacja hello jest w toku.

![Powiadomienie o zapisywaniu regułę filtru IP][img-ip-filter-save-new-rule]

Witaj **Dodaj** opcja jest wyłączona po przejściu hello maksymalnie 10 reguł filtru IP.

Dwukrotne kliknięcie hello wiersza, który zawiera reguły hello można edytować istniejącą regułę.

> [!NOTE]
> Odrzucanie IP adresy można zapobiec innymi usługami Azure (np. Azure Stream Analytics, maszynach wirtualnych platformy Azure lub hello Explorer urządzenia w portalu hello) interakcję z Centrum IoT hello.

> [!WARNING]
> Jeśli używasz usługi Azure Stream Analytics (ASA) tooread komunikaty z Centrum IoT z filtrowania IP włączone, użyj nazwy Centrum zdarzeń zgodnych hello i punktu końcowego Centrum IoT w hello ASA parametry połączenia.

## <a name="delete-an-ip-filter-rule"></a>Usuń regułę filtru IP

toodelete reguły filtru adresu IP, wybierz co najmniej jedną regułę hello siatki i kliknij przycisk **usunąć**.

![Usuń regułę filtru IP Centrum IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>Szacowanie reguły filtru adresu IP

Reguły filtru IP są stosowane w kolejności i hello Pierwsza reguła określa, czy adres IP hello dopasowań hello zaakceptować lub odrzucić akcji.

Na przykład jeśli adresy tooaccept w 192.168.100.0/22 zakresu hello i odrzucić wszystkie inne hello pierwszą regułę w siatce hello powinna obsługiwać 192.168.100.0/22 zakres adresów hello. Reguła dalej Hello Odrzuć wszystkie adresy przy użyciu hello zakresu 0.0.0.0/0.

Można zmienić kolejność hello reguł filtru IP w siatce hello klikając hello pionowy Wielokropek na powitania początku wiersza i przy użyciu przeciągania i upuść.

filtru IP nowego toosave reguły kolejności, kliknij przycisk **zapisać**.

![Zmień kolejność hello reguł filtru IP Centrum IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a>Następne kroki

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

- [Operacje monitorowania][lnk-monitor]
- [Metryki Centrum IoT][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md