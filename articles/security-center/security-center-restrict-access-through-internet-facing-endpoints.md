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
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="4e0b6-103">Ogranicz dostęp za pośrednictwem punkty końcowe skierowane do Internetu w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="4e0b6-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="4e0b6-104">Centrum zabezpieczeń Azure zaleca ograniczyć dostęp za pośrednictwem punkty końcowe skierowane do Internetu, jeśli jakakolwiek z grup zabezpieczeń sieci (NSG) ma co najmniej jednej reguły dla ruchu przychodzącego zezwalających na dostęp z "dowolny" źródłowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="4e0b6-105">Otwieranie dostępu zbyt "any" mogą umożliwić tooaccess osoby atakujące zasobów.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="4e0b6-106">Centrum zabezpieczeń zaleca edytowanie tych reguł ruchu przychodzącego toorestrict dostępu toosource adresów IP, które faktycznie muszą mieć dostęp.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="4e0b6-107">To zalecenie jest generowany dla dowolnego portu sieci web zawierającej "dowolne" jako źródło.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0b6-108">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="4e0b6-109">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="4e0b6-110">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="4e0b6-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="4e0b6-111">W hello **bloku zalecenia**, wybierz pozycję **ograniczyć dostęp za pośrednictwem punktu końcowego internetowy**.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Ogranicz dostęp za pośrednictwem punktu końcowego mającego połączenie z Internetem][1]
2. <span data-ttu-id="4e0b6-113">Spowoduje to otwarcie bloku hello **ograniczyć dostęp za pośrednictwem punktu końcowego internetowy**.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="4e0b6-114">Ten blok list hello maszynach wirtualnych (VM) z reguł ruchu przychodzącego, które utworzyć potencjalny problem z zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="4e0b6-115">Wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-115">Select a VM.</span></span>

   ![Wybierz maszynę Wirtualną][2]
3. <span data-ttu-id="4e0b6-117">Witaj **NSG** bloku Wyświetla informacje sieciowej grupy zabezpieczeń, powiązanych reguł ruchu przychodzącego i hello skojarzonego VM.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="4e0b6-118">Wybierz **edytowanie reguły ruchu przychodzącego** tooproceed z edytowanie reguły ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Blok grupy zabezpieczeń sieci][3]
4. <span data-ttu-id="4e0b6-120">Na powitania **reguły zabezpieczeń dla ruchu przychodzącego** wybierz bloku hello tooedit reguły dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="4e0b6-121">W tym przykładzie załóżmy wybierz **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Reguły zabezpieczeń ruchu przychodzącego][4]

   <span data-ttu-id="4e0b6-123">Uwaga: Możesz też wybrać **domyślne zasady** toosee hello zestaw reguł domyślnych, które zawiera wszystkie grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="4e0b6-124">Nie można usunąć reguły domyślne Hello, ale ponieważ mają przypisany o niższym priorytecie, mogą być zastąpione przez hello utworzonych reguł.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="4e0b6-125">Dowiedz się więcej o [domyślne zasady](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="4e0b6-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Reguły domyślne][5]
5. <span data-ttu-id="4e0b6-127">Na powitania **AllowWeb** bloku, Edytuj właściwości hello hello przychodzącą regułę, która hello **źródła** jest adres IP lub blok adresów IP.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="4e0b6-128">toolearn więcej informacji na temat właściwości hello hello reguły dla ruchu przychodzącego, zobacz [reguły NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="4e0b6-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Edytowanie reguły ruchu przychodzącego][6]

## <a name="see-also"></a><span data-ttu-id="4e0b6-130">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4e0b6-130">See also</span></span>
<span data-ttu-id="4e0b6-131">W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Ogranicz dostęp za pośrednictwem internetowy punkt końcowy."</span><span class="sxs-lookup"><span data-stu-id="4e0b6-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="4e0b6-132">toolearn więcej informacji na temat włączania grup NSG i reguł, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4e0b6-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="4e0b6-133">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="4e0b6-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="4e0b6-134">Jak grupy NSG toomanage przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4e0b6-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="4e0b6-135">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4e0b6-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4e0b6-136">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md)— Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4e0b6-137">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — informacje o tym, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4e0b6-138">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md)— Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4e0b6-139">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md)— Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4e0b6-140">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="4e0b6-141">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4e0b6-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="4e0b6-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
