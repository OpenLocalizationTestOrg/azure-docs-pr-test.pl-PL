---
title: "aaaEnable agenta maszyny Wirtualnej w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** włączyć VM Agent **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>Włącz agenta maszyny Wirtualnej w Centrum zabezpieczeń Azure
Witaj maszyny Wirtualnej musi być zainstalowany Agent na maszynach wirtualnych (VM) w kolejności zbyt[Włącz zbieranie danych](security-center-enable-data-collection.md).  Centrum zabezpieczeń Azure umożliwia toosee możesz maszyny wirtualne wymagające hello agenta maszyny Wirtualnej i zaleca włączenie hello agenta maszyny Wirtualnej na tych maszynach wirtualnych.

Witaj agenta maszyny Wirtualnej jest instalowany domyślnie dla maszyn wirtualnych, które zostały wdrożone z hello Azure Marketplace. Artykuł Hello [agenta maszyny Wirtualnej i rozszerzenia — część 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) zawiera informacje na temat sposobu tooinstall hello agenta maszyny Wirtualnej.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia. Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **bloku zalecenia**, wybierz pozycję **włączyć agenta maszyny Wirtualnej**.
   ![Włącz agenta maszyny wirtualnej][1]
2. Spowoduje to otwarcie bloku hello **VM Agent Brak lub nie odpowiada**. Ten blok zawiera hello maszyn wirtualnych, które wymagają hello agenta maszyny Wirtualnej. Postępuj zgodnie instrukcje hello na agenta hello bloku tooinstall hello maszyny Wirtualnej.
   ![Brak agenta maszyny Wirtualnej][2]

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md)— Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — informacje o tym, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md)— Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md)— Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
