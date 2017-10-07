---
title: "aaaSupportability dodawania istniejącego zestawu dostępności maszyny wirtualne Azure tooan | Dokumentacja firmy Microsoft"
description: "Możliwość obsługi dodawania istniejącego zestawu dostępności tooan maszynach wirtualnych platformy Azure."
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
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Możliwość obsługi dodawania maszyn wirtualnych platformy Azure tooan istniejącego zestawu dostępności

Czasami mogą wystąpić ograniczenia, po dodaniu nowych maszynach wirtualnych (VM) tooan istniejącego zestawu dostępności. Witaj, poniższe informacje wykresu serii maszyn wirtualnych, które można łączyć w hello tego samego zestawu dostępności.

Oto hello obsługi macierzy toomix różne typy maszyn wirtualnych:

& Serii zestawu dostępności|Drugi maszyny Wirtualnej|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Pierwsza maszyna wirtualna|||||||
|A||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Wszystkie inne serii nie może być w hello tego samego zestawu danych o dostępności, ponieważ wymagają one konkretnego sprzętu.
