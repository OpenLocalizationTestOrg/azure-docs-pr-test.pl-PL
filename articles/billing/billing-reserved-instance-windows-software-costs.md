---
title: "Azure koszty oprogramowania Windows wystąpień maszyny Wirtualnej rezerwy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, które liczniki są używane oprogramowania systemu Windows dla maszyny Wirtualnej systemu Windows, które kwalifikują się do wystąpienia zastrzeżone."
services: billing
documentationcenter: 
author: manish-shukla01
manager: manshuk
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/03/2017
ms.author: manshuk
ms.openlocfilehash: b985e6e9575ffeedcac5bcb3f94a43d23fdbb85e
ms.sourcegitcommit: 7d107bb9768b7f32ec5d93ae6ede40899cbaa894
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/16/2017
---
# <a name="windows-software-costs-not-included-with-reserved-instances"></a>Koszty oprogramowania systemu Windows nie jest dołączony do wystąpienia zastrzeżone

Jeśli nie masz korzyści Użyj hybrydowe platformy Azure na maszynie Wirtualnej zarezerwowana wystąpienia są naliczane dla liczników oprogramowania systemu Windows wymienionych w poniższej tabeli:

| meterId | MeterName w pliku użycia | Używane przez maszynę Wirtualną |
| ------- | ------------------------| --- |
| e7e152ac-f29c-4cce-ad6e-026192c01ef2 | Windows rezerwacji Svr serii (1 rdzeń) | Seria B |
| cac255a2-9f0f-4c62-8bd6-f0fa449c5f76 | Windows rezerwacji Svr serii (2 rdzenie) | Seria B |
| 09756b58-3fb5-4390-976d-9ddd14f9ed18 | Windows rezerwacji Svr serii (4 rdzenie) | Seria B |
| e828cb37-5920-4dc7-b30f-664e4dbcb6c7 | Windows rezerwacji Svr serii (8 rdzeni) | Seria B |
| f65a06cf-c9c3-47a2-8104-f17a8542215a | Windows rezerwacji Svr (1 rdzeń) | Wszystkie z wyjątkiem serii B |
| b99d40ae-41fe-4d1d-842b-56d72f3d15ee | Windows rezerwacji Svr (2 rdzenie) | Wszystkie z wyjątkiem serii B |
| 1cb88381-0905-4843-9ba2-7914066aabe5 | Windows rezerwacji Svr (4 rdzenie) | Wszystkie z wyjątkiem serii B |
| 07d9e10d-3e3e-4672-ac30-87f58ec4b00a | Windows rezerwacji Svr (6 rdzeni) | Wszystkie z wyjątkiem serii B |
| 603f58d1-1e96-460b-a933-ce3775ac7e2e | Windows rezerwacji Svr (8 rdzeni) | Wszystkie z wyjątkiem serii B |
| 36aaadda-da86-484a-b465-c8b5ab292d71 | Windows rezerwacji Svr (12 rdzeni) | Wszystkie z wyjątkiem serii B |
| 02968a6b-1654-4495-ada6-13f378ba7172 | Windows rezerwacji Svr (16 rdzeni) | Wszystkie z wyjątkiem serii B |
| 175434d8-75f9-474b-9906-5d151b6bed84 | Windows rezerwacji Svr (20 rdzeni) | Wszystkie z wyjątkiem serii B |
| 77eb6dd0-88f5-4a16-ab39-05d1742efb25 | Windows rezerwacji Svr (24 rdzenie) | Wszystkie z wyjątkiem serii B |
| 0d5bdf46-b719-4b1f-a780-b9bdfffd0591 | Windows rezerwacji Svr (32 rdzenie) | Wszystkie z wyjątkiem serii B |
| f1214b5c-cc16-445f-be6c-a3bb75f8395a | Windows rezerwacji Svr (40 rdzeni) | Wszystkie z wyjątkiem serii B |
| 637b7c77-65ad-4486-9cc7-dc7b3e9a8731 | Svr rezerwacji Windows (64 rdzenie) | Wszystkie z wyjątkiem serii B |
| da612742-e7cc-4ca3-9334-0fb7234059cd | Windows rezerwacji Svr (72 rdzeni) | Wszystkie z wyjątkiem serii B |
| a485cb8c-069b-4cf3-9a8e-ddd84b323da2 | Windows rezerwacji Svr (128 rdzeni) | Wszystkie z wyjątkiem serii B |
| 904c5c71-1eb7-43a6-961c-d305a9681624 | Windows rezerwacji Svr (256 rdzeni) | Wszystkie z wyjątkiem serii B |
| 6fdab81b-4284-4df9-8939-c237cc7462fe | Windows rezerwacji Svr (96 rdzeni) | Wszystkie z wyjątkiem serii B |

Koszt każdej z tych liczników można uzyskać za pośrednictwem interfejsu API RateCard Azure. Aby uzyskać informacje dotyczące sposobu uzyskania stawki miernika azure, zobacz [uzyskiwanie informacji o cenach i metadanych dla zasobów używanych w subskrypcji platformy Azure](https://msdn.microsoft.com/library/azure/mt219004).