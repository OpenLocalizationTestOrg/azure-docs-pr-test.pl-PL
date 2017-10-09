---
title: "aaaEnable sieciowych grup zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** włączyć sieci zabezpieczeń grupy **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Włącz sieciowych grup zabezpieczeń w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca włączyć grupę zabezpieczeń sieci (NSG), jeśli nie jest jeszcze włączone. Grupy NSG zawierają listę reguł listy kontroli dostępu (ACL), które akceptować lub odrzucać ruch sieciowy tooyour wystąpień maszyn wirtualnych w sieci wirtualnej. Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci. Gdy grupa NSG jest skojarzona z podsiecią, reguły listy ACL hello zastosować wystąpień maszyn wirtualnych hello tooall w tej podsieci. Ponadto ruch tooan poszczególnych maszyn wirtualnych można ograniczyć jeszcze bardziej przez skojarzenie grupy NSG bezpośrednio toothat maszyny Wirtualnej. toolearn więcej zobacz [co to jest grupa zabezpieczeń sieci (NSG)?](../virtual-network/virtual-networks-nsg.md)

Jeśli nie ma włączone grup NSG, Centrum zabezpieczeń będzie zawierał dwóch tooyou zalecenia: Włącz grup zabezpieczeń sieci na podsieci i włączyć grup zabezpieczeń sieci na maszynach wirtualnych. Należy wybrać poziom, podsieć lub maszyny Wirtualnej, tooapply grup NSG.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **włączyć grup zabezpieczeń sieci** podsieci lub maszynach wirtualnych.
   ![Włączanie sieciowych grup zabezpieczeń][1]
2. Spowoduje to otwarcie bloku hello **Konfiguruj brakujące grupy zabezpieczeń sieci** dla podsieci lub dla maszyn wirtualnych, w zależności od zalecenie hello, które wybrano. Wybierz podsieć lub maszyny wirtualnej tooconfigure grupy NSG na.

   ![Skonfiguruj grupy NSG dla podsieci][2]

   ![Skonfiguruj grupy NSG dla maszyny Wirtualnej][3]
3. Na powitania **Wybieranie grupy zabezpieczeń sieci** bloku, wybierz istniejącą grupę NSG lub **Utwórz nowy** toocreate grupy NSG.

   ![Wybieranie grupy zabezpieczeń sieci][4]

Jeśli utworzysz grupy NSG, wykonaj kroki hello w [jak grupy NSG toomanage przy użyciu hello portalu Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate grupy NSG i ustawić zasady zabezpieczeń.

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Włącz grup zabezpieczeń sieci" dla podsieci maszyny wirtualnej lub maszyny wirtualnej. toolearn więcej informacji na temat włączania grup NSG, zobacz następujące hello:

* [Co to jest sieciowa grupa zabezpieczeń?](../virtual-network/virtual-networks-nsg.md)
* [Jak grupy NSG toomanage przy użyciu hello portalu Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
