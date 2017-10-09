---
title: "aaaRestrict dostęp za pośrednictwem punkty końcowe skierowane do Internetu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** ograniczyć dostęp za pośrednictwem internetowy punkt końcowy **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Ogranicz dostęp za pośrednictwem punkty końcowe skierowane do Internetu w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca ograniczyć dostęp za pośrednictwem punkty końcowe skierowane do Internetu, jeśli jakakolwiek z grup zabezpieczeń sieci (NSG) ma co najmniej jednej reguły dla ruchu przychodzącego zezwalających na dostęp z "dowolny" źródłowy adres IP. Otwieranie dostępu zbyt "any" mogą umożliwić tooaccess osoby atakujące zasobów. Centrum zabezpieczeń zaleca edytowanie tych reguł ruchu przychodzącego toorestrict dostępu toosource adresów IP, które faktycznie muszą mieć dostęp.

To zalecenie jest generowany dla dowolnego portu sieci web zawierającej "dowolne" jako źródło.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia. Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **bloku zalecenia**, wybierz pozycję **ograniczyć dostęp za pośrednictwem punktu końcowego internetowy**.

   ![Ogranicz dostęp za pośrednictwem punktu końcowego mającego połączenie z Internetem][1]
2. Spowoduje to otwarcie bloku hello **ograniczyć dostęp za pośrednictwem punktu końcowego internetowy**. Ten blok list hello maszynach wirtualnych (VM) z reguł ruchu przychodzącego, które utworzyć potencjalny problem z zabezpieczeniami. Wybierz maszynę Wirtualną.

   ![Wybierz maszynę Wirtualną][2]
3. Witaj **NSG** bloku Wyświetla informacje sieciowej grupy zabezpieczeń, powiązanych reguł ruchu przychodzącego i hello skojarzonego VM. Wybierz **edytowanie reguły ruchu przychodzącego** tooproceed z edytowanie reguły ruchu przychodzącego.

   ![Blok grupy zabezpieczeń sieci][3]
4. Na powitania **reguły zabezpieczeń dla ruchu przychodzącego** wybierz bloku hello tooedit reguły dla ruchu przychodzącego. W tym przykładzie załóżmy wybierz **AllowWeb**.

   ![Reguły zabezpieczeń ruchu przychodzącego][4]

   Uwaga: Możesz też wybrać **domyślne zasady** toosee hello zestaw reguł domyślnych, które zawiera wszystkie grupy NSG. Nie można usunąć reguły domyślne Hello, ale ponieważ mają przypisany o niższym priorytecie, mogą być zastąpione przez hello utworzonych reguł. Dowiedz się więcej o [domyślne zasady](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Reguły domyślne][5]
5. Na powitania **AllowWeb** bloku, Edytuj właściwości hello hello przychodzącą regułę, która hello **źródła** jest adres IP lub blok adresów IP. toolearn więcej informacji na temat właściwości hello hello reguły dla ruchu przychodzącego, zobacz [reguły NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Edytowanie reguły ruchu przychodzącego][6]

## <a name="see-also"></a>Zobacz też
W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Ogranicz dostęp za pośrednictwem internetowy punkt końcowy." toolearn więcej informacji na temat włączania grup NSG i reguł, zobacz następujące hello:

* [Co to jest sieciowa grupa zabezpieczeń?](../virtual-network/virtual-networks-nsg.md)
* [Jak grupy NSG toomanage przy użyciu hello portalu Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md)— Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — informacje o tym, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md)— Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md)— Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
