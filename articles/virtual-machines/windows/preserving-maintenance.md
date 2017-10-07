---
title: AAA konserwacji zachowania maszyny Wirtualnej dla maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Migracja w miejscu maszyny Wirtualnej pamięci, zachowując aktualizacji."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>Maszyna wirtualna w zachowaniu obsługi migracji maszyny Wirtualnej w miejscu

Podczas aktualizacji hello większość toohosted nie wpływu na maszynach wirtualnych, istnieją przypadki, w których toocomponents aktualizacji lub usług spowodować zakłócenia minimalnego toorunning maszyn wirtualnych (bez pełnego ponownego uruchomienia maszyny wirtualnej hello).

Te aktualizacje są realizowane za pomocą technologii, która umożliwia migrację na żywo w miejscu, nazywane również "zachowywania pamięci update". Podczas aktualizowania hosta hello, hello maszyny wirtualnej jest umieszczany w "" wstrzymana, zachowując hello pamięci RAM, hello hosting środowiska (np. system operacyjny) dotyczy hello niezbędne aktualizacje i poprawki.
Maszyna wirtualna Hello następnie zostanie wznowione w ciągu 30 sekund wstrzymywane.
Po wznowieniu pracy, zostanie automatycznie zsynchronizowana zegara hello hello maszyny wirtualnej.

Nie wszystkie aktualizacje można wdrożyć przy użyciu ten mechanizm, ale podany okres krótkiej przerwie wdrażania aktualizacji w ten sposób znacznie zmniejsza wpływ toovirtual maszyny.

Mająca wiele wystąpień aktualizacje (maszyn wirtualnych w zestawie dostępności) są stosowane jednej domeny aktualizacji w czasie.

Niektóre aplikacje może mieć wpływ na więcej niż inne aktualizacje. Aplikacje wykonujące przetwarzania zdarzeń w czasie rzeczywistym, przesyłania strumieniowego multimediów lub transkodowanie lub uzyskać wysoką przepustowość sieci scenariusze, na przykład nie można zaprojektowanego tootolerate 30 jednosekundową przerwę. Aplikacje działające na maszynie wirtualnej dowiedzieć się o nadchodzących aktualizacji przez wywołanie hello [zaplanowane zdarzenia](../virtual-machines-scheduled-events.md) API hello [Azure metadanych usługi](../virtual-machines-instancemetadataservice-overview.md).
