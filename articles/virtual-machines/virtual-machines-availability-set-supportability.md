---
title: "Ustaw obsługi dodawania maszyn wirtualnych platformy Azure do istniejących dostępności | Dokumentacja firmy Microsoft"
description: "Możliwość obsługi dodawania maszyn wirtualnych platformy Azure do istniejącego zestawu dostępności."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a>Możliwość obsługi dodawania maszyn wirtualnych platformy Azure do istniejącego zestawu dostępności

Można czasami napotkać ograniczenia podczas dodawania nowych maszyn wirtualnych (VM) do istniejącego zestawu dostępności. Poniższy schemat zawiera szczegóły serii maszyn wirtualnych, które można łączyć w tym samym zestawie dostępności.

Oto macierz obsługi mieszać różnego rodzaju maszyn wirtualnych:

& Serii zestawu dostępności|Drugi maszyny Wirtualnej|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Pierwsza maszyna wirtualna|||||||
|A||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Wszystkie inne serii nie można w tym samym zestawie, ponieważ wymagają one konkretnego sprzętu dostępności.