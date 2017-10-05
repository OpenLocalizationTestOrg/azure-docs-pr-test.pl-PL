---
title: "Korygowanie luk w zabezpieczeniach systemu operacyjnego w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** luk w zabezpieczeniach ** skorygować systemu operacyjnego."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="9cf64-103">Korygowanie luk w zabezpieczeniach systemu operacyjnego w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="9cf64-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="9cf64-104">Centrum zabezpieczeń Azure codziennie analizuje systemu operacyjnego maszyny wirtualnej (VM) (system operacyjny) dla konfiguracji, które można utworzyć maszyny Wirtualnej bardziej narażony na ataki i zaleca zmiany konfiguracji, aby rozwiązać te luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="9cf64-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="9cf64-105">Centrum zabezpieczeń zaleca się, Usuń luk w zabezpieczeniach, gdy konfiguracja systemu operacyjnego maszyny Wirtualnej jest niezgodna z reguł zalecanych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9cf64-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf64-106">Aby uzyskać więcej informacji o określonych monitorowanych konfiguracji, zobacz [lista reguł zalecanych konfiguracji](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="9cf64-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="9cf64-107">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="9cf64-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="9cf64-108">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9cf64-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="9cf64-109">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="9cf64-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="9cf64-110">W **zalecenia** bloku, wybierz opcję **luk w zabezpieczeniach skorygować OS**.</span><span class="sxs-lookup"><span data-stu-id="9cf64-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="9cf64-111">![Koryguj luki w zabezpieczeniach systemu operacyjnego][1]</span><span class="sxs-lookup"><span data-stu-id="9cf64-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="9cf64-112">**Luk w zabezpieczeniach skorygować OS** bloku otwiera i listy maszyn wirtualnych z konfiguracji systemu operacyjnego, które nie są zgodne z reguł zalecanych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9cf64-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="9cf64-113">Dla każdej maszyny Wirtualnej identyfikuje bloku:</span><span class="sxs-lookup"><span data-stu-id="9cf64-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="9cf64-114">**REGUŁY nie powiodło się** — liczba reguł, których konfiguracja systemu operacyjnego maszyny Wirtualnej nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="9cf64-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="9cf64-115">**Czas ostatniego skanowania** — Data i godzina Centrum zabezpieczeń będzie ostatniego skanowania Konfiguracja systemu operacyjnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9cf64-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="9cf64-116">**Stan** — bieżący stan luki w zabezpieczeniach:</span><span class="sxs-lookup"><span data-stu-id="9cf64-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="9cf64-117">Otwórz: Lukę w zabezpieczeniach nie rozpoczęto jeszcze</span><span class="sxs-lookup"><span data-stu-id="9cf64-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="9cf64-118">W toku: Jest aktualnie stosowane lukę w zabezpieczeniach, jest wymagana żadna akcja ze strony</span><span class="sxs-lookup"><span data-stu-id="9cf64-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="9cf64-119">Rozpoznać: Usterka została już omówiona (gdy problem został rozwiązany, pozycja jest wyszarzona)</span><span class="sxs-lookup"><span data-stu-id="9cf64-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="9cf64-120">**WAŻNOŚĆ** — wszystkie luki w zabezpieczeniach są ustawione na ważność niski, co oznacza powinny być kierowane luka w zabezpieczeniach, ale nie wymaga natychmiastowej uwagi.</span><span class="sxs-lookup"><span data-stu-id="9cf64-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="9cf64-121">Wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="9cf64-121">Select a VM.</span></span> <span data-ttu-id="9cf64-122">Bloku dla tej maszyny Wirtualnej zostanie otwarty i wyświetla reguł, które nie powiodły.</span><span class="sxs-lookup"><span data-stu-id="9cf64-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="9cf64-123">![Reguły konfiguracji, które nie powiodło się][2]</span><span class="sxs-lookup"><span data-stu-id="9cf64-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="9cf64-124">Wybierz regułę.</span><span class="sxs-lookup"><span data-stu-id="9cf64-124">Select a rule.</span></span> <span data-ttu-id="9cf64-125">W tym przykładzie pozwala wybrać **hasło musi spełniać wymagania co do złożoności**.</span><span class="sxs-lookup"><span data-stu-id="9cf64-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="9cf64-126">Zostanie otwarty blok opisujące reguły nie powiodło się i wpływu.</span><span class="sxs-lookup"><span data-stu-id="9cf64-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="9cf64-127">Przejrzyj szczegóły i należy wziąć pod uwagę sposób stosowania konfiguracji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9cf64-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="9cf64-128">![Opis reguły nie powiodło się][3]</span><span class="sxs-lookup"><span data-stu-id="9cf64-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="9cf64-129">Centrum zabezpieczeń używane typowych konfiguracji wyliczenie CCE () do przypisywania unikatowych identyfikatorów dla reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9cf64-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="9cf64-130">Poniższe informacje są przekazywane w tym bloku:</span><span class="sxs-lookup"><span data-stu-id="9cf64-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="9cf64-131">Nazwa — Nazwa reguły</span><span class="sxs-lookup"><span data-stu-id="9cf64-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="9cf64-132">WAŻNOŚĆ — Wartości ważności CCE krytyczna ważne i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="9cf64-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="9cf64-133">CCIED — CCE Unikatowy identyfikator reguły</span><span class="sxs-lookup"><span data-stu-id="9cf64-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="9cf64-134">OPIS — Opis reguły</span><span class="sxs-lookup"><span data-stu-id="9cf64-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="9cf64-135">Luki w zabezpieczeniach — Opis usterki lub ryzyko, gdy nie jest stosowana reguła</span><span class="sxs-lookup"><span data-stu-id="9cf64-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="9cf64-136">WPŁYW — Wpływ na prowadzoną działalność po zastosowaniu reguły</span><span class="sxs-lookup"><span data-stu-id="9cf64-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="9cf64-137">OCZEKIWANA wartość — Wartość oczekiwana w przypadku Centrum zabezpieczeń analizuje względem reguły konfiguracji systemu operacyjnego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9cf64-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="9cf64-138">— Reguła zasada operacji używane przez Centrum zabezpieczeń podczas analizy konfiguracji systemu operacyjnego maszyny Wirtualnej względem reguły</span><span class="sxs-lookup"><span data-stu-id="9cf64-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="9cf64-139">RZECZYWISTA wartość--Zwracana wartość po analizie względem reguły konfiguracji systemu operacyjnego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9cf64-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="9cf64-140">WYNIK oceny —-wynik analizy: przekazywania błędów</span><span class="sxs-lookup"><span data-stu-id="9cf64-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="9cf64-141">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9cf64-141">See also</span></span>
<span data-ttu-id="9cf64-142">W tym artykule przedstawiono sposób wykonania zalecenia Centrum zabezpieczeń "Luk Skoryguj systemu operacyjnego".</span><span class="sxs-lookup"><span data-stu-id="9cf64-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="9cf64-143">Możesz przejrzeć zestaw reguł konfiguracji [tutaj](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="9cf64-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="9cf64-144">Centrum zabezpieczeń używane CCE (typowych konfiguracji wyliczenie) do przypisywania unikatowych identyfikatorów dla reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9cf64-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="9cf64-145">Odwiedź stronę [CCE](https://nvd.nist.gov/cce/index.cfm) witryny, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9cf64-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="9cf64-146">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="9cf64-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="9cf64-147">[Obsługiwane platformy w Centrum zabezpieczeń Azure](security-center-os-coverage.md) — zawiera listę obsługiwanych systemu Windows i maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9cf64-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="9cf64-148">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="9cf64-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9cf64-149">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf64-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9cf64-150">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf64-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9cf64-151">[Reagowanie na alerty zabezpieczeń w Centrum zabezpieczeń Azure i zarządzanie nimi](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="9cf64-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9cf64-152">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje o sposobie monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="9cf64-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="9cf64-153">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9cf64-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9cf64-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="9cf64-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
