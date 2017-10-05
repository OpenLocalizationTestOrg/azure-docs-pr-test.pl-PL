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
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="b60b3-103">Włącz sieciowych grup zabezpieczeń w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="b60b3-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="b60b3-104">Centrum zabezpieczeń Azure zaleca włączyć grupę zabezpieczeń sieci (NSG), jeśli nie jest jeszcze włączone.</span><span class="sxs-lookup"><span data-stu-id="b60b3-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="b60b3-105">Grupy NSG zawierają listę reguł listy kontroli dostępu (ACL), które akceptować lub odrzucać ruch sieciowy do wystąpień maszyn wirtualnych w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b60b3-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="b60b3-106">Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci.</span><span class="sxs-lookup"><span data-stu-id="b60b3-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="b60b3-107">Gdy sieciowa grupa zabezpieczeń jest skojarzona z podsiecią, reguły listy ACL dotyczą wszystkich wystąpień maszyn wirtualnych w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="b60b3-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="b60b3-108">Ponadto ruch do poszczególnych maszyn wirtualnych można ograniczyć jeszcze bardziej przez skojarzenie grupy NSG bezpośrednio z tą maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b60b3-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span> <span data-ttu-id="b60b3-109">Aby dowiedzieć się więcej, zobacz [co to jest grupa zabezpieczeń sieci (NSG)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="b60b3-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="b60b3-110">Jeśli nie ma włączone grup NSG, Centrum zabezpieczeń przedstawia dwa zaleceń możesz: Włącz grup zabezpieczeń sieci na podsieci i włączyć grup zabezpieczeń sieci na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b60b3-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="b60b3-111">Należy wybrać poziom, podsieć lub maszyny Wirtualnej, aby zastosować grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="b60b3-111">You choose which level, subnet or VM, to apply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="b60b3-112">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b60b3-112">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="b60b3-113">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="b60b3-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="b60b3-114">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="b60b3-114">Implement the recommendation</span></span>
1. <span data-ttu-id="b60b3-115">W **zalecenia** bloku, wybierz opcję **włączyć grup zabezpieczeń sieci** podsieci lub maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b60b3-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="b60b3-116">![Włączanie sieciowych grup zabezpieczeń][1]</span><span class="sxs-lookup"><span data-stu-id="b60b3-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="b60b3-117">Spowoduje to otwarcie bloku **Konfiguruj brakujące grupy zabezpieczeń sieci** dla podsieci lub dla maszyn wirtualnych, w zależności od wybranego zalecenia.</span><span class="sxs-lookup"><span data-stu-id="b60b3-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span></span> <span data-ttu-id="b60b3-118">Wybierz podsieć lub skonfigurować grupy NSG na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b60b3-118">Select a subnet or a virtual machine to configure an NSG on.</span></span>

   ![Skonfiguruj grupy NSG dla podsieci][2]

   ![Skonfiguruj grupy NSG dla maszyny Wirtualnej][3]
3. <span data-ttu-id="b60b3-121">Na **Wybieranie grupy zabezpieczeń sieci** bloku, wybierz istniejącą grupę NSG lub **Utwórz nowy** do utworzenia grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="b60b3-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span></span>

   ![Wybieranie grupy zabezpieczeń sieci][4]

<span data-ttu-id="b60b3-123">Jeśli utworzysz grupy NSG, postępuj zgodnie z instrukcjami [jak zarządzać przy użyciu portalu Azure grup NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) do utworzenia grupy NSG i ustawienia zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b60b3-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="b60b3-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b60b3-124">See also</span></span>
<span data-ttu-id="b60b3-125">W tym artykule pokazano sposób wykonania "Włącz sieciowe grupy zabezpieczeń" zalecenia Centrum zabezpieczeń dla podsieci maszyny wirtualnej lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b60b3-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="b60b3-126">Aby dowiedzieć się więcej na temat włączania grup NSG, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="b60b3-126">To learn more about enabling NSGs, see the following:</span></span>

* [<span data-ttu-id="b60b3-127">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="b60b3-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="b60b3-128">Jak zarządzać grup NSG przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b60b3-128">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="b60b3-129">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="b60b3-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="b60b3-130">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b60b3-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b60b3-131">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b60b3-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b60b3-132">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b60b3-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="b60b3-133">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="b60b3-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="b60b3-134">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="b60b3-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="b60b3-135">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="b60b3-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b60b3-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Uzyskaj najnowsze informacje zabezpieczeń platformy Azure i informacje.</span><span class="sxs-lookup"><span data-stu-id="b60b3-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
