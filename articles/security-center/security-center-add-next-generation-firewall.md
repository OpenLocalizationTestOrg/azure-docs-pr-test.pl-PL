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
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="10ddc-103">Dodaj zaporę nowej generacji w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="10ddc-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="10ddc-104">Centrum zabezpieczeń Azure może zaleca dodanie zaporę nowej generacji (NGFW) z tooincrease partnera firmy Microsoft z ochrony zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="10ddc-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> <span data-ttu-id="10ddc-105">Ten dokument przeprowadzi Cię przez przykładowy sposób toodo to.</span><span class="sxs-lookup"><span data-stu-id="10ddc-105">This document walks you through an example of how toodo this.</span></span>

> [!NOTE]
> <span data-ttu-id="10ddc-106">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="10ddc-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="10ddc-107">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="10ddc-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="10ddc-108">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="10ddc-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="10ddc-109">W hello **zalecenia** bloku, wybierz opcję **dodać zaporę nowej generacji**.</span><span class="sxs-lookup"><span data-stu-id="10ddc-109">In hello **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="10ddc-110">![Dodawanie zapory nowej generacji][1]</span><span class="sxs-lookup"><span data-stu-id="10ddc-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="10ddc-111">W hello **dodać zaporę nowej generacji** bloku, wybierz punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="10ddc-111">In hello **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="10ddc-112">![Wybierz punkt końcowy][2]</span><span class="sxs-lookup"><span data-stu-id="10ddc-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="10ddc-113">Drugi **dodać zaporę nowej generacji** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="10ddc-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="10ddc-114">Można wybrać toouse istniejącego rozwiązania, a jeśli są dostępne lub można utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="10ddc-114">You can choose toouse an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="10ddc-115">W tym przykładzie nie dostępnych żadnych istniejących rozwiązań, utworzymy zapory nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="10ddc-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="10ddc-116">![Utwórz Zapora nowej generacji][3]</span><span class="sxs-lookup"><span data-stu-id="10ddc-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="10ddc-117">toocreate NGFW wybierz rozwiązanie z listy hello zintegrowane partnerów.</span><span class="sxs-lookup"><span data-stu-id="10ddc-117">toocreate an NGFW, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="10ddc-118">W tym przykładzie mamy wybierz **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="10ddc-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="10ddc-119">![Wybierz rozwiązanie Zapora nowej generacji][4]</span><span class="sxs-lookup"><span data-stu-id="10ddc-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="10ddc-120">Witaj **Check Point** zostanie otwarty blok informacjami o hello rozwiązaniem partnerskim.</span><span class="sxs-lookup"><span data-stu-id="10ddc-120">hello **Check Point** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="10ddc-121">Wybierz **Utwórz** w bloku informacji hello.</span><span class="sxs-lookup"><span data-stu-id="10ddc-121">Select **Create** in hello information blade.</span></span>
   <span data-ttu-id="10ddc-122">![Blok informacji zapory][5]</span><span class="sxs-lookup"><span data-stu-id="10ddc-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="10ddc-123">Witaj **tworzenia maszyny wirtualnej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="10ddc-123">hello **Create virtual machine** blade opens.</span></span> <span data-ttu-id="10ddc-124">Tutaj można wprowadzić informacje wymagane toospin maszyny wirtualnej (VM) uruchamia hello zapory nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="10ddc-124">Here you can enter information required toospin up a virtual machine (VM) that runs hello NGFW.</span></span> <span data-ttu-id="10ddc-125">Wykonaj kroki hello i podaj wymagane informacje NGFW hello.</span><span class="sxs-lookup"><span data-stu-id="10ddc-125">Follow hello steps and provide hello NGFW information required.</span></span> <span data-ttu-id="10ddc-126">Wybierz OK tooapply.</span><span class="sxs-lookup"><span data-stu-id="10ddc-126">Select OK tooapply.</span></span>
   <span data-ttu-id="10ddc-127">![Tworzenie maszyny wirtualnej toorun NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="10ddc-127">![Create virtual machine toorun NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="10ddc-128">Kieruj ruch tylko przez zaporę nowej generacji</span><span class="sxs-lookup"><span data-stu-id="10ddc-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="10ddc-129">Zwraca toohello **zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="10ddc-129">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="10ddc-130">Wygenerowano nowy wpis po dodaniu NGFW za pośrednictwem Centrum zabezpieczeń o nazwie **kierowania ruchu za pośrednictwem zapory nowej generacji**.</span><span class="sxs-lookup"><span data-stu-id="10ddc-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="10ddc-131">To zalecenie jest tworzony tylko w przypadku zainstalowania programu NGFW za pośrednictwem Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="10ddc-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="10ddc-132">Jeśli masz punkty końcowe skierowane do Internetu, Centrum zabezpieczeń zaleca, aby skonfigurować reguł sieciowej grupy zabezpieczeń, który wymusza ruch przychodzący tooyour maszyny Wirtualnej za pośrednictwem sieci NGFW.</span><span class="sxs-lookup"><span data-stu-id="10ddc-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic tooyour VM through your NGFW.</span></span>

1. <span data-ttu-id="10ddc-133">W hello **bloku zalecenia**, wybierz pozycję **kierowania ruchu za pośrednictwem zapory nowej generacji**.</span><span class="sxs-lookup"><span data-stu-id="10ddc-133">In hello **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="10ddc-134">![Kierowanie ruchu sieciowego tylko za pośrednictwem zapory następnej generacji][7]</span><span class="sxs-lookup"><span data-stu-id="10ddc-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="10ddc-135">Spowoduje to otwarcie bloku hello **kierowania ruchu za pośrednictwem zapory nowej generacji**, który zawiera listę maszyn wirtualnych, które może kierować ruchem do.</span><span class="sxs-lookup"><span data-stu-id="10ddc-135">This opens hello blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="10ddc-136">Wybierz maszynę Wirtualną z listy hello.</span><span class="sxs-lookup"><span data-stu-id="10ddc-136">Select a VM from hello list.</span></span>
   <span data-ttu-id="10ddc-137">![Wybierz maszynę Wirtualną][8]</span><span class="sxs-lookup"><span data-stu-id="10ddc-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="10ddc-138">Bloku hello wybrana maszyna wirtualna zostanie otwarta, wyświetlanie powiązanych reguł ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="10ddc-138">A blade for hello selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="10ddc-139">Opis zawiera więcej informacji na temat wykonać następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="10ddc-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="10ddc-140">Wybierz **edytowanie reguły ruchu przychodzącego** tooproceed z edytowanie reguły ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="10ddc-140">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span> <span data-ttu-id="10ddc-141">Witaj oczekuje się, że **źródła** nie ustawiono zbyt**żadnych** dla punktów końcowych internetowy hello połączone z hello zapory nowej generacji.</span><span class="sxs-lookup"><span data-stu-id="10ddc-141">hello expectation is that **Source** is not set too**Any** for hello Internet-facing endpoints linked with hello NGFW.</span></span> <span data-ttu-id="10ddc-142">toolearn więcej informacji na temat właściwości hello hello reguły dla ruchu przychodzącego, zobacz [reguły NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="10ddc-142">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="10ddc-143">![Konfigurowanie zasad dostępu toolimit][9]
   ![edycji reguły dla ruchu przychodzącego][10]</span><span class="sxs-lookup"><span data-stu-id="10ddc-143">![Configure rules toolimit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="10ddc-144">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="10ddc-144">See also</span></span>
<span data-ttu-id="10ddc-145">Ten dokument pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Dodaj zaporę nowej generacji".</span><span class="sxs-lookup"><span data-stu-id="10ddc-145">This document showed you how tooimplement hello Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="10ddc-146">toolearn więcej informacji na temat NGFWs i hello rozwiązaniem partnerskim Check Point, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="10ddc-146">toolearn more about NGFWs and hello Check Point partner solution, see hello following:</span></span>

* [<span data-ttu-id="10ddc-147">Zapora nowej generacji</span><span class="sxs-lookup"><span data-stu-id="10ddc-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="10ddc-148">Punkt wyboru vSEC</span><span class="sxs-lookup"><span data-stu-id="10ddc-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="10ddc-149">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="10ddc-149">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="10ddc-150">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="10ddc-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="10ddc-151">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10ddc-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="10ddc-152">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10ddc-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="10ddc-153">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="10ddc-153">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="10ddc-154">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="10ddc-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="10ddc-155">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="10ddc-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="10ddc-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="10ddc-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

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
