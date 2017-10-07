---
title: "Przepływ tooIP aaaIntroduction Sprawdź, czy w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie hello sieci IP obserwatora przepływu Sprawdź możliwości"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Wprowadzenie tooIP przepływu Sprawdź, czy w obserwatora sieciowego Azure

Przepływ IP Sprawdź kontroli, jeśli pakiet jest dozwolony lub odrzucany tooor z maszyny wirtualnej na podstawie informacji 5-elementowej. Te informacje składa się z kierunku, protokół lokalny adres IP, zdalny adres IP, portu lokalnego i portu zdalnego. Jeśli pakietów hello jest zabroniony przez grupę zabezpieczeń, zwracana jest nazwa hello hello reguła odmowy pakietów hello. Podczas gdy można wybrać dowolny źródłowy lub docelowy adres IP, funkcja ta ułatwia ona administratorom szybkie diagnozowanie problemów z łącznością z lub toohello internet i z lub toohello w środowisku lokalnym.

Sprawdź przepływ IP jest przeznaczony dla interfejsu sieciowego maszyny wirtualnej. Przepływ ruchu jest następnie zweryfikować oparte na powitania skonfigurowane ustawienia tooor z tym interfejs sieciowy. Ta funkcja jest przydatna w potwierdzaniu, jeśli zasada grupy zabezpieczeń sieci blokuje tooor ruch przychodzący lub wychodzący z maszyny wirtualnej.

Sprawdź wystąpienie toobe potrzeb obserwatora sieciowego utworzone we wszystkich regionach, że planujesz toorun IP przepływu. Obserwatora sieciowego jest usługą regionalnych i może być przeprowadzony tylko na zasobów w hello tego samego regionu. Nie dotyczy to powitalne Sprawdź wyniki przepływu IP jako trasy hello skojarzone z hello kart nadal będą zwracane.

![1][1]

## <a name="next-steps"></a>Następne kroki

Odwiedź stronę powitania po toolearn artykułu, jeśli pakiet jest dozwolony lub niedozwolony dla określonej maszyny wirtualnej za pośrednictwem portalu hello. [Sprawdź, czy ruch jest dozwolony na maszynie Wirtualnej z przepływem Sprawdź IP przy użyciu portalu hello](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












