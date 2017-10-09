---
title: "aaaProtecting sieci w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten adres dokumentu zalecenia w Centrum zabezpieczeń Azure, które ułatwiają ochronę sieci platformy Azure i są aktualizowane zgodnie z zasadami zabezpieczeń."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Ochrona sieci w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure analizuje hello stan zabezpieczeń zasobów platformy Azure. Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania kontrolek hello potrzebne hello.  Zalecenia dotyczące zastosować tooAzure typy zasobów: maszynach wirtualnych (VM), sieci, SQL i aplikacji.

W tym artykule opisano zalecenia dotyczące sieci tooyour.  Centrum zalecenia dotyczące sieci wokół następnej generacji zapór, grup zabezpieczeń sieci, konfigurowanie reguł ruchu przychodzącego i.  Użyj hello poniższej tabeli jako toohelp odwołanie zrozumieć hello dostępnej sieci zalecenia i jak każdej z nich działa w przypadku zastosowania.

## <a name="available-network-recommendations"></a>Zalecenia dostępnej sieci
| Zalecenie | Opis |
| --- | --- |
| [Dodawanie zapory nowej generacji](security-center-add-next-generation-firewall.md) |Zaleca się, że dodasz dalej zapory generacji (NGFW) z tooincrease partnera firmy Microsoft z ochrony zabezpieczeń. |
| [Kierowanie ruchu sieciowego tylko za pośrednictwem zapory następnej generacji](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Zaleca się, aby skonfigurować reguły grupy (NSG) zabezpieczeń sieciowych, który wymusza ruch przychodzący tooyour maszyny Wirtualnej za pośrednictwem sieci NGFW. |
| [Włączenie grup zabezpieczeń sieci dla podsieci lub maszyny wirtualne](security-center-enable-network-security-groups.md) |Zaleca się włączenie grup NSG dla podsieci lub maszyn wirtualnych. |
| [Ogranicz dostęp za pośrednictwem internetowy punkt końcowy](security-center-restrict-access-through-internet-facing-endpoints.md) |Zaleca się, aby skonfigurować reguły ruchu przychodzącego dla grup NSG. |

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat zaleceń, które są stosowane tooother typów zasobów platformy Azure, zobacz następujące hello:

* [Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure](security-center-virtual-machine-recommendations.md)
* [Ochrona aplikacji w Centrum zabezpieczeń Azure](security-center-application-recommendations.md)
* [Ochrona usługi Azure SQL w Centrum zabezpieczeń Azure](security-center-sql-service-recommendations.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
