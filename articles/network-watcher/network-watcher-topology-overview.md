---
title: Wprowadzenie do topologii w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera przegląd możliwości topologii obserwatora sieciowego"
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
ms.openlocfilehash: 42443f614b76b8180ac163b9889163021adbf048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a>Wprowadzenie do topologii w obserwatora sieciowego Azure

Topologia zwraca wykres zasobów sieciowych w sieci wirtualnej. Wykres przedstawia połączenia między zasobami do reprezentowania łączność sieciową pełnego.

![Omówienie topologii][1]

W portalu topologii zwraca obiekty zasobów na poszczególnych sieci wirtualnej. Relacje są określone przez linie między zasobami zasobów poza region obserwatora sieciowego, nawet jeśli w zasobie grupy nie zostaną wyświetlone. Zasoby zwracane w widoku portalu są podzbiorem składników sieciowych, które są wyświetlone na wykresie. Aby wyświetlić pełną listę zasobów sieciowych, można użyć [PowerShell](network-watcher-topology-powershell.md) lub [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Wystąpienie Monitora sieci jest wymagana w każdym regionie, który chcesz uruchomić topologii.

Ponieważ zasoby są zwracane połączenia między nimi są modelowane w obszarze dwie relacje.

- **Zawieranie** — przykład: sieć wirtualna zawiera podsieci, która zawiera karty Sieciowej
- **Skojarzone** — przykład: A kart interfejsu Sieciowego jest skojarzona z maszyną Wirtualną

### <a name="next-steps"></a>Następne kroki

Dowiedz się, jak za pomocą programu PowerShell można pobrać widoku topologii odwiedzając [topologii obserwatora sieciowego przy użyciu programu PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
