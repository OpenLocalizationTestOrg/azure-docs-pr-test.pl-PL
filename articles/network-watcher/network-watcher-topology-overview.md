---
title: tootopology aaaIntroduction w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie funkcji topologii hello obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Wprowadzenie tootopology w obserwatora sieciowego Azure

Topologia zwraca wykres zasobów sieciowych w sieci wirtualnej. Witaj wykres przedstawia hello połączenia między łączności sieciowej tooend hello zasobów toorepresent hello zakończenia.

![Omówienie topologii][1]

W portalu hello topologii zwraca obiekty zasobów hello na poszczególnych sieci wirtualnej. Relacje Hello są określone przez linie między zasobami hello zasobów poza region obserwatora sieciowego hello, nawet jeśli w zasobie hello grupy nie zostaną wyświetlone. zasoby Hello zwracane w widoku portalu hello są podzbiorem hello składników sieciowych, które są wyświetlone na wykresie. toosee hello pełną listę zasobów sieciowych można użyć [PowerShell](network-watcher-topology-powershell.md) lub [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Wystąpienie Monitora sieci jest wymagana w każdym regionie, który ma być toorun topologii.

Ponieważ zasoby są zwracane hello połączenia między nimi są modelowane w obszarze dwie relacje.

- **Zawieranie** — przykład: sieć wirtualna zawiera podsieci, która zawiera karty Sieciowej
- **Skojarzone** — przykład: A kart interfejsu Sieciowego jest skojarzona z maszyną Wirtualną

### <a name="next-steps"></a>Następne kroki

Dowiedz się, jak wyświetlić toouse PowerShell tooretrieve hello topologii odwiedzając [topologii obserwatora sieciowego przy użyciu programu PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
