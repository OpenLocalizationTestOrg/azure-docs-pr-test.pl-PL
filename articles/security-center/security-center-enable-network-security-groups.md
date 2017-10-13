---
title: "Włącz sieciowych grup zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** włączyć sieci zabezpieczeń grupy **."
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
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Włącz sieciowych grup zabezpieczeń w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca włączyć grupę zabezpieczeń sieci (NSG), jeśli nie jest jeszcze włączone. Grupy NSG zawierają listę reguł listy kontroli dostępu (ACL), które akceptować lub odrzucać ruch sieciowy do wystąpień maszyn wirtualnych w sieci wirtualnej. Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci. Gdy sieciowa grupa zabezpieczeń jest skojarzona z podsiecią, reguły listy ACL dotyczą wszystkich wystąpień maszyn wirtualnych w tej podsieci. Ponadto ruch do poszczególnych maszyn wirtualnych można ograniczyć jeszcze bardziej przez skojarzenie grupy NSG bezpośrednio z tą maszyną Wirtualną. Aby dowiedzieć się więcej, zobacz [co to jest grupa zabezpieczeń sieci (NSG)?](../virtual-network/virtual-networks-nsg.md)

Jeśli nie ma włączone grup NSG, Centrum zabezpieczeń przedstawia dwa zaleceń możesz: Włącz grup zabezpieczeń sieci na podsieci i włączyć grup zabezpieczeń sieci na maszynach wirtualnych. Należy wybrać poziom, podsieć lub maszyny Wirtualnej, aby zastosować grupy NSG.

> [!NOTE]
> Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-the-recommendation"></a>Wykonania zalecenia
1. W **zalecenia** bloku, wybierz opcję **włączyć grup zabezpieczeń sieci** podsieci lub maszynach wirtualnych.
   ![Włączanie sieciowych grup zabezpieczeń][1]
2. Spowoduje to otwarcie bloku **Konfiguruj brakujące grupy zabezpieczeń sieci** dla podsieci lub dla maszyn wirtualnych, w zależności od wybranego zalecenia. Wybierz podsieć lub skonfigurować grupy NSG na maszynie wirtualnej.

   ![Skonfiguruj grupy NSG dla podsieci][2]

   ![Skonfiguruj grupy NSG dla maszyny Wirtualnej][3]
3. Na **Wybieranie grupy zabezpieczeń sieci** bloku, wybierz istniejącą grupę NSG lub **Utwórz nowy** do utworzenia grupy NSG.

   ![Wybieranie grupy zabezpieczeń sieci][4]

Jeśli utworzysz grupy NSG, postępuj zgodnie z instrukcjami [jak zarządzać przy użyciu portalu Azure grup NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) do utworzenia grupy NSG i ustawienia zasad zabezpieczeń.

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano sposób wykonania "Włącz sieciowe grupy zabezpieczeń" zalecenia Centrum zabezpieczeń dla podsieci maszyny wirtualnej lub maszyny wirtualnej. Aby dowiedzieć się więcej na temat włączania grup NSG, zobacz następujące tematy:

* [Co to jest sieciowa grupa zabezpieczeń?](../virtual-network/virtual-networks-nsg.md)
* [Jak zarządzać grup NSG przy użyciu portalu Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:

* [Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.
* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.
* [Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Uzyskaj najnowsze informacje zabezpieczeń platformy Azure i informacje.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
