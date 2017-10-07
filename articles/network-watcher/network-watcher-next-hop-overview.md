---
title: przeskoku toonext aaaIntroduction obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie hello obserwatora sieciowego następnego przeskoku możliwości"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Wprowadzenie przeskoku toonext obserwatora sieciowego Azure

Ruch z maszyny Wirtualnej jest wysyłany tooa docelowym oparte na trasach efektywne hello skojarzony z jedną kartą sieciową. Następny przeskok pobiera typ następnego przeskoku hello i adres IP pakietu z określonej maszyny wirtualnej i karty sieciowej. Dzięki temu toodetermine hello pakietów jest docelowy skierowanego toohello lub jest holed ruchu hello jest czarny. Niepoprawna konfiguracja tras przez użytkownika hello, w których ruch jest ukierunkowanej tooan lokalnej lokalizacji lub urządzenie wirtualne, może spowodować problemy tooconnectivity. Następny przeskok zwraca również wartość tabeli tras hello skojarzone z następnego przeskoku hello. Podczas wykonywania zapytania następnego przeskoku, jeśli trasa hello jest zdefiniowana jako trasy zdefiniowane przez użytkownika, zostanie zwrócony tej trasy. W przeciwnym razie wartość następnego skoku zwraca "Trasa systemowa".

![następnego przeskoku — omówienie][1]

Witaj poniżej znajduje się lista hello następnego przeskoku typów, które mogą być zwrócone podczas wykonywania zapytania w następnym przeskoku.

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Brak

### <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toouse następnego przeskoku toofind problemy z połączeniem sieciowym, odwiedzając [wyboru hello następnego przeskoku na maszynie Wirtualnej](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













