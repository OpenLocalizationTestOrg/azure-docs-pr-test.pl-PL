---
title: "Dodaj zaporę nowej generacji w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera implementowania zaleceń Centrum zabezpieczeń Azure ** dodać następnej generacji zapory ** i ** traffice o trasy za pośrednictwem zapory nowej generacji tylko **."
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
ms.openlocfilehash: 30589d0a943517c03394a3aae7c03c8094e78c1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="a6d8a-103">Dodaj zaporę nowej generacji w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="a6d8a-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="a6d8a-104">Centrum zabezpieczeń Azure może zaleca dodanie zaporę nowej generacji (NGFW) od partnera firmy Microsoft w celu zwiększenia z ochrony zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> <span data-ttu-id="a6d8a-105">Ten dokument przeprowadzi Cię przez przykładowy jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-105">This document walks you through an example of how to do this.</span></span>

> [!NOTE]
> <span data-ttu-id="a6d8a-106">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="a6d8a-107">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="a6d8a-108">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="a6d8a-108">Implement the recommendation</span></span>
1. <span data-ttu-id="a6d8a-109">W **zalecenia** bloku, wybierz opcję **dodać zaporę nowej generacji**.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-109">In the **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="a6d8a-110">![Dodawanie zapory nowej generacji][1]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="a6d8a-111">W **dodać zaporę nowej generacji** bloku, wybierz punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-111">In the **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="a6d8a-112">![Wybierz punkt końcowy][2]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="a6d8a-113">Drugi **dodać zaporę nowej generacji** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="a6d8a-114">Możesz użyć istniejącego rozwiązania, jeśli jest dostępny, lub można utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-114">You can choose to use an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="a6d8a-115">W tym przykładzie nie dostępnych żadnych istniejących rozwiązań, utworzymy zapory nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="a6d8a-116">![Utwórz Zapora nowej generacji][3]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="a6d8a-117">Utworzyć NGFW, należy wybrać z listy partnerów zintegrowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-117">To create an NGFW, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="a6d8a-118">W tym przykładzie mamy wybierz **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="a6d8a-119">![Wybierz rozwiązanie Zapora nowej generacji][4]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="a6d8a-120">**Check Point** zostanie otwarty blok informacjami o rozwiązaniem partnerskim.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-120">The **Check Point** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="a6d8a-121">Wybierz **Utwórz** w bloku informacji.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-121">Select **Create** in the information blade.</span></span>
   <span data-ttu-id="a6d8a-122">![Blok informacji zapory][5]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="a6d8a-123">**Tworzenia maszyny wirtualnej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-123">The **Create virtual machine** blade opens.</span></span> <span data-ttu-id="a6d8a-124">Tutaj można wprowadzić informacje wymagane do pokrętła maszyny wirtualnej (VM), który uruchamia zapory nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-124">Here you can enter information required to spin up a virtual machine (VM) that runs the NGFW.</span></span> <span data-ttu-id="a6d8a-125">Postępuj zgodnie z instrukcjami i podaj wymagane informacje zapory nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-125">Follow the steps and provide the NGFW information required.</span></span> <span data-ttu-id="a6d8a-126">Wybierz OK, aby zastosować.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-126">Select OK to apply.</span></span>
   <span data-ttu-id="a6d8a-127">![Utwórz maszynę wirtualną, aby uruchomić NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-127">![Create virtual machine to run NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="a6d8a-128">Kieruj ruch tylko przez zaporę nowej generacji</span><span class="sxs-lookup"><span data-stu-id="a6d8a-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="a6d8a-129">Wróć do **zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-129">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="a6d8a-130">Wygenerowano nowy wpis po dodaniu NGFW za pośrednictwem Centrum zabezpieczeń o nazwie **kierowania ruchu za pośrednictwem zapory nowej generacji**.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="a6d8a-131">To zalecenie jest tworzony tylko w przypadku zainstalowania programu NGFW za pośrednictwem Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="a6d8a-132">Jeśli masz punkty końcowe skierowane do Internetu, Centrum zabezpieczeń zaleca, aby skonfigurować reguł sieciowej grupy zabezpieczeń, który wymusza ruch przychodzący do maszyny Wirtualnej za pośrednictwem sieci NGFW.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic to your VM through your NGFW.</span></span>

1. <span data-ttu-id="a6d8a-133">W **bloku zalecenia**, wybierz pozycję **kierowania ruchu za pośrednictwem zapory nowej generacji**.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-133">In the **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="a6d8a-134">![Kierowanie ruchu sieciowego tylko za pośrednictwem zapory następnej generacji][7]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="a6d8a-135">Spowoduje to otwarcie bloku **kierowania ruchu za pośrednictwem zapory nowej generacji**, który zawiera listę maszyn wirtualnych, które może kierować ruchem do.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-135">This opens the blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="a6d8a-136">Wybierz maszynę Wirtualną z listy.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-136">Select a VM from the list.</span></span>
   <span data-ttu-id="a6d8a-137">![Wybierz maszynę Wirtualną][8]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="a6d8a-138">Zostanie otwarty blok dla wybranej maszyny Wirtualnej, wyświetlanie powiązanych reguł ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-138">A blade for the selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="a6d8a-139">Opis zawiera więcej informacji na temat wykonać następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="a6d8a-140">Wybierz **edytowanie reguły ruchu przychodzącego** kontynuować edytowanie reguły ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-140">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span> <span data-ttu-id="a6d8a-141">Oczekuje się, że **źródła** nie jest ustawiony na **żadnych** dla punktów końcowych internetowy połączone z zapory nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-141">The expectation is that **Source** is not set to **Any** for the Internet-facing endpoints linked with the NGFW.</span></span> <span data-ttu-id="a6d8a-142">Aby dowiedzieć się więcej o właściwościach reguły ruchu przychodzącego, zobacz [reguły NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="a6d8a-142">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="a6d8a-143">![Konfigurowanie reguł, aby ograniczyć dostęp do][9]
   ![edycji reguły dla ruchu przychodzącego][10]</span><span class="sxs-lookup"><span data-stu-id="a6d8a-143">![Configure rules to limit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="a6d8a-144">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a6d8a-144">See also</span></span>
<span data-ttu-id="a6d8a-145">Ten dokument pokazano sposób wykonania zalecenia Centrum zabezpieczeń "Dodaj zaporę nowej generacji".</span><span class="sxs-lookup"><span data-stu-id="a6d8a-145">This document showed you how to implement the Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="a6d8a-146">Aby dowiedzieć się więcej na temat NGFWs i rozwiązaniem partnerskim Check Point, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="a6d8a-146">To learn more about NGFWs and the Check Point partner solution, see the following:</span></span>

* [<span data-ttu-id="a6d8a-147">Zapora nowej generacji</span><span class="sxs-lookup"><span data-stu-id="a6d8a-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="a6d8a-148">Punkt wyboru vSEC</span><span class="sxs-lookup"><span data-stu-id="a6d8a-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="a6d8a-149">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="a6d8a-149">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="a6d8a-150">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="a6d8a-151">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a6d8a-152">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="a6d8a-153">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-153">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="a6d8a-154">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="a6d8a-155">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="a6d8a-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="a6d8a-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

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
