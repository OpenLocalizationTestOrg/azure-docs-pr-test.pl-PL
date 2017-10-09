---
title: "aaaManaging rozwiązań partnerskich w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przeprowadzi Cię przez jaki Centrum zabezpieczeń Azure umożliwia monitorowanie stanu oka hello kondycji rozwiązań partnerskich zintegrowanych z subskrypcją platformy Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure
Ten dokument przeprowadzi Cię przez jak toomonitor hello stanu kondycji rozwiązań partnerskich w Centrum zabezpieczeń Azure.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia. Ten dokument nie jest przewodnik krok po kroku.
>
>

## <a name="monitoring-partner-solutions"></a>Monitorowanie rozwiązań partnerskich
Witaj **rozwiązania partnerskie** Kafelek na powitania **Centrum zabezpieczeń** bloku umożliwia monitorowanie stanu oka hello kondycji rozwiązań partnerskich zintegrowanych z subskrypcją platformy Azure.

![Kafelek Rozwiązania partnerskie][1]

Witaj **rozwiązania partnerskie** kafelka Wyświetla hello liczbę rozwiązań partnerskich zintegrowanych z subskrypcją. Jeśli nie masz rozwiązań zintegrowanych, kafelka hello Wyświetla hello liczby zero.

tooview hello kondycji rozwiązań partnerskich:

1. Wybierz hello **rozwiązania partnerskie** kafelka. Witaj **rozwiązania partnerskie** tooSecurity Center połączona zostanie otwarty blok zawierający listę rozwiązań partnerskich.

   ![Rozwiązania partnerskie][3]

   Stan Hello rozwiązanie partnerskie może być:

   * Chronione (kolor zielony) — brak problemów dotyczących kondycji.
   * W złej kondycji (kolor czerwony) — istnieje problem z kondycją wymagający natychmiastowej uwagi.
   * Zatrzymano raportowania (kolor pomarańczowy) — Witaj rozwiązania zostało zatrzymane raportowanie dotyczące kondycji.
   * Nieznany stan ochrony (kolor pomarańczowy) — kondycja hello rozwiązania hello jest nieznany w tej chwili ukończenia procesu tooa nie powiodło się dodanie nowego zasobu toohello istniejącego rozwiązania.
   * Nie zgłoszono (kolor szary) — rozwiązanie hello nie zgłosił żadnych czynności, ale stan rozwiązania może zostać zgłoszony, jeśli został ostatnio podłączony i jego wdrażanie nadal trwa.

2. Wybierz rozwiązanie partnerskie. W tym przykładzie umożliwia wybierz hello **Qualys** rozwiązania.  Zostanie otwarty blok, wyświetlając stan hello rozwiązaniem partnerskim hello i rozwiązania hello skojarzonych zasobów. Wybierz **Konsola rozwiązań** Zarządzanie partnerami hello tooopen środowisko dla tego rozwiązania.

   ![Szczegóły rozwiązania partnerskiego][4]
3. Przejdź wstecz toohello **Qualys** bloku, a następnie wybierz **wirtualna łącze**. Witaj **łączenie aplikacji** zostanie otwarty blok. Tutaj można połączyć z rozwiązaniem partnerskim toohello zasobów.

   ![Łącze zasobów toopartner rozwiązania][5]

## <a name="next-steps"></a>Następne kroki
W tym dokumencie zostały wprowadzone toohello **rozwiązań partnerskich** kafelka w Centrum zabezpieczeń. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące artykuły hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiada.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
