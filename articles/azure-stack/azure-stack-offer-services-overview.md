---
title: "Oferty usług w stosie Azure | Dokumentacja firmy Microsoft"
description: "Operator chmury mają możliwość oferowania usługi dla użytkowników."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 7a54771d99f2719fcc345496b152a5d3acc02121
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a>Przegląd oferty usług Azure stosu

*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*

[Microsoft Azure stosu](azure-stack-poc.md) platforma chmury hybrydowej, która umożliwia świadczenie usług z centrum danych. Dostawcy usług mają możliwość oferowania usług dzierżawcom. W firmie lub agencji rządowych Stanów Zjednoczonych możesz zaoferować lokalnych usług pracownikom. Usługi, które można dostarczać obejmują, ale nie są ograniczone do:

- Usługi aplikacji, aplikacje mobilne, aplikacje interfejsu API, funkcje interfejsu API, SQL, MySQL, takich jak platforma jako usługa (PaaS) usługi.

Można nawet łączyć usług integracji do tworzenia złożonych rozwiązań dla różnych użytkowników.

Aby dostarczyć te usługi dla użytkowników, należy utworzyć [planów, ofertami i przydziały](azure-stack-plan-offer-quota-overview.md). Użytkownicy mogą następnie subskrybować oferty korzystać z usług.

## <a name="plan-your-service-offers"></a>Planowanie oferty usługi

Podczas planujesz Twojej oferty, należy uwzględnić następujące kwestie:

**Próbnych**: próbnych umożliwia przyciągania nowych użytkowników, które następnie można uaktualnić do dodatkowych usług. Wersja próbna, utworzyć małą [planu podstawowego](azure-stack-plan-offer-quota-overview.md#base-plan) z większego planu dodatek opcjonalne.

**Planowanie pojemności**: może być użytkowników Przechwytywanie dużych ilości zasobów i zapychaniem systemu dla wszystkich użytkowników. Aby ułatwić wydajności, można [skonfigurować przydziały planów](azure-stack-plan-offer-quota-overview.md#plans) z użyciem centralnych zasad dostępu.

**Delegowane dostawców**: można przyznać innym możliwość tworzenia oferty w danym środowisku. Na przykład jeśli jesteś dostawcą usług, możesz [delegować](azure-stack-delegated-provider.md) możliwość Twojej odsprzedawców. Lub, w przypadku organizacji, możesz delegować do innych działów/zależnych.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o oferty, planów, przydziały i subskrypcji](azure-stack-plan-offer-quota-overview.md)

