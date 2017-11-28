---
title: "Włącz agenta maszyny Wirtualnej w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** włączyć VM Agent **."
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
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="2432e-103">Włącz agenta maszyny Wirtualnej w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="2432e-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="2432e-104">Agent maszyny Wirtualnej musi być zainstalowany na maszynach wirtualnych (VM) w celu [Włącz zbieranie danych](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="2432e-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="2432e-105">Centrum zabezpieczeń Azure umożliwia można zobaczyć, które maszyny wirtualne wymagają agenta maszyny Wirtualnej i zaleca włączenie agenta maszyny Wirtualnej na tych maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2432e-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="2432e-106">Agent maszyny wirtualnej jest instalowany domyślnie w przypadku maszyn wirtualnych wdrażanych z poziomu portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2432e-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="2432e-107">Informacje na temat instalowania agenta maszyny wirtualnej można znaleźć w artykule [Agent maszyny wirtualnej i rozszerzenia — część 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).</span><span class="sxs-lookup"><span data-stu-id="2432e-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="2432e-108">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2432e-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="2432e-109">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="2432e-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="2432e-110">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="2432e-110">Implement the recommendation</span></span>
1. <span data-ttu-id="2432e-111">W **bloku zalecenia**, wybierz pozycję **włączyć agenta maszyny Wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="2432e-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="2432e-112">![Włącz agenta maszyny wirtualnej][1]</span><span class="sxs-lookup"><span data-stu-id="2432e-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="2432e-113">Spowoduje to otwarcie bloku **VM Agent Brak lub nie odpowiada**.</span><span class="sxs-lookup"><span data-stu-id="2432e-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="2432e-114">Ten blok zawiera listę maszyn wirtualnych, które wymagają agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2432e-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="2432e-115">Postępuj zgodnie z instrukcjami w bloku, aby zainstalować agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2432e-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="2432e-116">![Brak agenta maszyny Wirtualnej][2]</span><span class="sxs-lookup"><span data-stu-id="2432e-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="2432e-117">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2432e-117">See also</span></span>
<span data-ttu-id="2432e-118">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="2432e-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="2432e-119">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2432e-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2432e-120">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — informacje o tym, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2432e-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="2432e-121">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje na temat monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2432e-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="2432e-122">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="2432e-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="2432e-123">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="2432e-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="2432e-124">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — odpowiedzi na najczęstsze pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="2432e-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="2432e-125">[Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — najnowsze informacje na temat zabezpieczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2432e-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
