---
title: "aaaAdd zaporę nowej generacji w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zaleceń Centrum zabezpieczeń Azure ** dodać następnej generacji zapory ** i ** traffice o trasy za pośrednictwem zapory nowej generacji tylko **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Dodaj zaporę nowej generacji w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure może zaleca dodanie zaporę nowej generacji (NGFW) z tooincrease partnera firmy Microsoft z ochrony zabezpieczeń. Ten dokument przeprowadzi Cię przez przykładowy sposób toodo to.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **dodać zaporę nowej generacji**.
   ![Dodawanie zapory nowej generacji][1]
2. W hello **dodać zaporę nowej generacji** bloku, wybierz punkt końcowy.
   ![Wybierz punkt końcowy][2]
3. Drugi **dodać zaporę nowej generacji** zostanie otwarty blok. Można wybrać toouse istniejącego rozwiązania, a jeśli są dostępne lub można utworzyć nowy. W tym przykładzie nie dostępnych żadnych istniejących rozwiązań, utworzymy zapory nowej generacji.
   ![Utwórz Zapora nowej generacji][3]
4. toocreate NGFW wybierz rozwiązanie z listy hello zintegrowane partnerów. W tym przykładzie mamy wybierz **Check Point**.
   ![Wybierz rozwiązanie Zapora nowej generacji][4]
5. Witaj **Check Point** zostanie otwarty blok informacjami o hello rozwiązaniem partnerskim. Wybierz **Utwórz** w bloku informacji hello.
   ![Blok informacji zapory][5]
6. Witaj **tworzenia maszyny wirtualnej** zostanie otwarty blok. Tutaj można wprowadzić informacje wymagane toospin maszyny wirtualnej (VM) uruchamia hello zapory nowej generacji. Wykonaj kroki hello i podaj wymagane informacje NGFW hello. Wybierz OK tooapply.
   ![Tworzenie maszyny wirtualnej toorun NGFW][6]

## <a name="route-traffic-through-ngfw-only"></a>Kieruj ruch tylko przez zaporę nowej generacji
Zwraca toohello **zalecenia** bloku. Wygenerowano nowy wpis po dodaniu NGFW za pośrednictwem Centrum zabezpieczeń o nazwie **kierowania ruchu za pośrednictwem zapory nowej generacji**. To zalecenie jest tworzony tylko w przypadku zainstalowania programu NGFW za pośrednictwem Centrum zabezpieczeń. Jeśli masz punkty końcowe skierowane do Internetu, Centrum zabezpieczeń zaleca, aby skonfigurować reguł sieciowej grupy zabezpieczeń, który wymusza ruch przychodzący tooyour maszyny Wirtualnej za pośrednictwem sieci NGFW.

1. W hello **bloku zalecenia**, wybierz pozycję **kierowania ruchu za pośrednictwem zapory nowej generacji**.
   ![Kierowanie ruchu sieciowego tylko za pośrednictwem zapory następnej generacji][7]
2. Spowoduje to otwarcie bloku hello **kierowania ruchu za pośrednictwem zapory nowej generacji**, który zawiera listę maszyn wirtualnych, które może kierować ruchem do. Wybierz maszynę Wirtualną z listy hello.
   ![Wybierz maszynę Wirtualną][8]
3. Bloku hello wybrana maszyna wirtualna zostanie otwarta, wyświetlanie powiązanych reguł ruchu przychodzącego. Opis zawiera więcej informacji na temat wykonać następujące czynności. Wybierz **edytowanie reguły ruchu przychodzącego** tooproceed z edytowanie reguły ruchu przychodzącego. Witaj oczekuje się, że **źródła** nie ustawiono zbyt**żadnych** dla punktów końcowych internetowy hello połączone z hello zapory nowej generacji. toolearn więcej informacji na temat właściwości hello hello reguły dla ruchu przychodzącego, zobacz [reguły NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Konfigurowanie zasad dostępu toolimit][9]
   ![edycji reguły dla ruchu przychodzącego][10]

## <a name="see-also"></a>Zobacz też
Ten dokument pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Dodaj zaporę nowej generacji". toolearn więcej informacji na temat NGFWs i hello rozwiązaniem partnerskim Check Point, zobacz następujące hello:

* [Zapora nowej generacji](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Punkt wyboru vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
