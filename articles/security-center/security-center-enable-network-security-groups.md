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
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="4e364-103">Włącz sieciowych grup zabezpieczeń w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="4e364-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="4e364-104">Centrum zabezpieczeń Azure zaleca włączyć grupę zabezpieczeń sieci (NSG), jeśli nie jest jeszcze włączone.</span><span class="sxs-lookup"><span data-stu-id="4e364-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="4e364-105">Grupy NSG zawierają listę reguł listy kontroli dostępu (ACL), które akceptować lub odrzucać ruch sieciowy tooyour wystąpień maszyn wirtualnych w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e364-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="4e364-106">Grupy NSG można kojarzyć z podsieciami lub poszczególnymi wystąpieniami maszyn wirtualnych w danej podsieci.</span><span class="sxs-lookup"><span data-stu-id="4e364-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="4e364-107">Gdy grupa NSG jest skojarzona z podsiecią, reguły listy ACL hello zastosować wystąpień maszyn wirtualnych hello tooall w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="4e364-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="4e364-108">Ponadto ruch tooan poszczególnych maszyn wirtualnych można ograniczyć jeszcze bardziej przez skojarzenie grupy NSG bezpośrednio toothat maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e364-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="4e364-109">toolearn więcej zobacz [co to jest grupa zabezpieczeń sieci (NSG)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="4e364-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="4e364-110">Jeśli nie ma włączone grup NSG, Centrum zabezpieczeń będzie zawierał dwóch tooyou zalecenia: Włącz grup zabezpieczeń sieci na podsieci i włączyć grup zabezpieczeń sieci na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4e364-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="4e364-111">Należy wybrać poziom, podsieć lub maszyny Wirtualnej, tooapply grup NSG.</span><span class="sxs-lookup"><span data-stu-id="4e364-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="4e364-112">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4e364-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="4e364-113">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="4e364-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="4e364-114">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="4e364-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="4e364-115">W hello **zalecenia** bloku, wybierz opcję **włączyć grup zabezpieczeń sieci** podsieci lub maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4e364-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="4e364-116">![Włączanie sieciowych grup zabezpieczeń][1]</span><span class="sxs-lookup"><span data-stu-id="4e364-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="4e364-117">Spowoduje to otwarcie bloku hello **Konfiguruj brakujące grupy zabezpieczeń sieci** dla podsieci lub dla maszyn wirtualnych, w zależności od zalecenie hello, które wybrano.</span><span class="sxs-lookup"><span data-stu-id="4e364-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="4e364-118">Wybierz podsieć lub maszyny wirtualnej tooconfigure grupy NSG na.</span><span class="sxs-lookup"><span data-stu-id="4e364-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![Skonfiguruj grupy NSG dla podsieci][2]

   ![Skonfiguruj grupy NSG dla maszyny Wirtualnej][3]
3. <span data-ttu-id="4e364-121">Na powitania **Wybieranie grupy zabezpieczeń sieci** bloku, wybierz istniejącą grupę NSG lub **Utwórz nowy** toocreate grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="4e364-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Wybieranie grupy zabezpieczeń sieci][4]

<span data-ttu-id="4e364-123">Jeśli utworzysz grupy NSG, wykonaj kroki hello w [jak grupy NSG toomanage przy użyciu hello portalu Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate grupy NSG i ustawić zasady zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4e364-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="4e364-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4e364-124">See also</span></span>
<span data-ttu-id="4e364-125">W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Włącz grup zabezpieczeń sieci" dla podsieci maszyny wirtualnej lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e364-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="4e364-126">toolearn więcej informacji na temat włączania grup NSG, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4e364-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="4e364-127">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="4e364-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="4e364-128">Jak grupy NSG toomanage przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4e364-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="4e364-129">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4e364-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4e364-130">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="4e364-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4e364-131">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4e364-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4e364-132">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4e364-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4e364-133">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="4e364-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4e364-134">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="4e364-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="4e364-135">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="4e364-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4e364-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="4e364-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
