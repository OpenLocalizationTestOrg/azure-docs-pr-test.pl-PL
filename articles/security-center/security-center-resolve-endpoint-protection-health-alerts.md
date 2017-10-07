---
title: "alerty kondycji aaaResolve programu endpoint protection w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** rozwiązania programu Endpoint Protection kondycji alerty **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Rozwiąż alerty kondycji programu endpoint protection w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca rozwiązanie alerty dotyczące kondycji ochrony wykrytego punktu końcowego.  Centrum zabezpieczeń umożliwia toosee maszyn wirtualnych (VM) mają błędy ochrony punktu końcowego i jak wiele błędów.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia. Nie jest to przewodnik krok po kroku.
> 
> 

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **bloku zalecenia**, wybierz pozycję **alerty dotyczące kondycji rozwiązania programu Endpoint Protection**.
   ![Rozwiązywanie alertów dotyczących kondycji punktu końcowego][1]
2. Spowoduje to otwarcie bloku hello **awarii programu Endpoint Protection** zawierająca listę maszyn wirtualnych o awarii i hello liczby błędów dla każdej maszyny Wirtualnej. Wybierz maszynę Wirtualną z listy hello.
   ![Błąd ochrony punktu końcowego][2]
3. A **listy błędów** zostanie otwarty blok dla hello wybranych maszyn wirtualnych, wyświetlanie listy błędów. Wybierz awarii z toolearn listy hello więcej. Spowoduje to otwarcie bloku z informacjami o niepowodzeniu hello wybrane.
   ![Lista błędów][3]
   ![zdarzeń błędów][4]

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
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
