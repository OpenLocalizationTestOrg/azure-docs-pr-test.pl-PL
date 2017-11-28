---
title: "luki w zabezpieczeniach aaaRemediate systemu operacyjnego w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** luk w zabezpieczeniach ** skorygować systemu operacyjnego."
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="d5f68-103">Korygowanie luk w zabezpieczeniach systemu operacyjnego w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="d5f68-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="d5f68-104">Centrum zabezpieczeń Azure codziennie analizuje systemu operacyjnego maszyny wirtualnej (VM) (system operacyjny) dla maszyny Wirtualnej hello konfiguracje, które można utworzyć bardziej narażony konfiguracji tooattack i zaleca zmiany tooaddress te luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="d5f68-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="d5f68-105">Centrum zabezpieczeń zaleca się, Usuń luk w zabezpieczeniach, gdy konfiguracja systemu operacyjnego maszyny Wirtualnej jest niezgodna z hello zalecane reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d5f68-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="d5f68-106">Aby uzyskać więcej informacji na powitania określonych monitorowanych konfiguracji, zobacz hello [lista reguł zalecanych konfiguracji](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="d5f68-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="d5f68-107">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="d5f68-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="d5f68-108">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d5f68-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="d5f68-109">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="d5f68-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="d5f68-110">W hello **zalecenia** bloku, wybierz opcję **luk w zabezpieczeniach skorygować OS**.</span><span class="sxs-lookup"><span data-stu-id="d5f68-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="d5f68-111">![Koryguj luki w zabezpieczeniach systemu operacyjnego][1]</span><span class="sxs-lookup"><span data-stu-id="d5f68-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="d5f68-112">Witaj **luk w zabezpieczeniach skorygować OS** bloku otwiera i listy maszyn wirtualnych z konfiguracji systemu operacyjnego, które nie odpowiadają hello zalecane reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d5f68-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="d5f68-113">Dla każdej maszyny Wirtualnej identyfikuje bloku hello:</span><span class="sxs-lookup"><span data-stu-id="d5f68-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="d5f68-114">**REGUŁY nie powiodło się** — hello liczbę reguł, które hello Konfiguracja systemu operacyjnego maszyny Wirtualnej nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="d5f68-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="d5f68-115">**Czas ostatniego skanowania** — Witaj Data i czas ostatniego skanowania hello wirtualna Konfiguracja systemu operacyjnego czy Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d5f68-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="d5f68-116">**Stan** — Witaj bieżący stan hello luki w zabezpieczeniach:</span><span class="sxs-lookup"><span data-stu-id="d5f68-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="d5f68-117">Otwórz: Luka w zabezpieczeniach hello nie rozpoczęto jeszcze</span><span class="sxs-lookup"><span data-stu-id="d5f68-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="d5f68-118">W toku: Luka w zabezpieczeniach hello jest aktualnie stosowane, jest wymagana żadna akcja ze strony</span><span class="sxs-lookup"><span data-stu-id="d5f68-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="d5f68-119">Rozpoznać: Luka w zabezpieczeniach hello został objęty (gdy hello problem został rozwiązany, hello pozycja jest wyszarzona)</span><span class="sxs-lookup"><span data-stu-id="d5f68-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="d5f68-120">**WAŻNOŚĆ** — wszystkie luki w zabezpieczeniach są ustawione tooa ważność niski, co oznacza powinny być kierowane luka w zabezpieczeniach, ale nie wymaga natychmiastowej uwagi.</span><span class="sxs-lookup"><span data-stu-id="d5f68-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="d5f68-121">Wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="d5f68-121">Select a VM.</span></span> <span data-ttu-id="d5f68-122">Bloku dla tej maszyny Wirtualnej zostanie otwarty i wyświetla hello reguł, które nie powiodły.</span><span class="sxs-lookup"><span data-stu-id="d5f68-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="d5f68-123">![Reguły konfiguracji, które nie powiodło się][2]</span><span class="sxs-lookup"><span data-stu-id="d5f68-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="d5f68-124">Wybierz regułę.</span><span class="sxs-lookup"><span data-stu-id="d5f68-124">Select a rule.</span></span> <span data-ttu-id="d5f68-125">W tym przykładzie pozwala wybrać **hasło musi spełniać wymagania co do złożoności**.</span><span class="sxs-lookup"><span data-stu-id="d5f68-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="d5f68-126">Zostanie otwarty blok zawierająca opis wpływu reguły i hello hello nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="d5f68-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="d5f68-127">Przejrzyj szczegóły hello i należy wziąć pod uwagę sposób stosowania konfiguracji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d5f68-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="d5f68-128">![Opis hello reguły nie powiodło się][3]</span><span class="sxs-lookup"><span data-stu-id="d5f68-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="d5f68-129">Centrum zabezpieczeń używa typowych konfiguracji wyliczenie CCE () tooassign unikatowych identyfikatorów dla reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d5f68-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="d5f68-130">w tym bloku znajduje się Hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="d5f68-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="d5f68-131">Nazwa — Nazwa reguły</span><span class="sxs-lookup"><span data-stu-id="d5f68-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="d5f68-132">WAŻNOŚĆ — Wartości ważności CCE krytyczna ważne i ostrzeżenia</span><span class="sxs-lookup"><span data-stu-id="d5f68-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="d5f68-133">CCIED — Unikatowy identyfikator CCE Witaj reguły</span><span class="sxs-lookup"><span data-stu-id="d5f68-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="d5f68-134">OPIS — Opis reguły</span><span class="sxs-lookup"><span data-stu-id="d5f68-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="d5f68-135">Luki w zabezpieczeniach — Opis usterki lub ryzyko, gdy nie jest stosowana reguła</span><span class="sxs-lookup"><span data-stu-id="d5f68-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="d5f68-136">WPŁYW — Wpływ na prowadzoną działalność po zastosowaniu reguły</span><span class="sxs-lookup"><span data-stu-id="d5f68-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="d5f68-137">OCZEKIWANA wartość — Wartość oczekiwana w przypadku Centrum zabezpieczeń analizuje względem hello reguły konfiguracji systemu operacyjnego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d5f68-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="d5f68-138">— Reguła zasada operacji używane przez Centrum zabezpieczeń podczas analizy konfiguracji systemu operacyjnego maszyny Wirtualnej względem reguły hello</span><span class="sxs-lookup"><span data-stu-id="d5f68-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="d5f68-139">RZECZYWISTA wartość--Zwracana wartość po analizie względem hello reguły konfiguracji systemu operacyjnego maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d5f68-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="d5f68-140">WYNIK oceny —-wynik analizy: przekazywania błędów</span><span class="sxs-lookup"><span data-stu-id="d5f68-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="d5f68-141">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d5f68-141">See also</span></span>
<span data-ttu-id="d5f68-142">W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Skoryguj systemu operacyjnego luk w zabezpieczeniach."</span><span class="sxs-lookup"><span data-stu-id="d5f68-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="d5f68-143">Możesz przejrzeć hello zbiór reguł konfiguracji [tutaj](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="d5f68-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="d5f68-144">Centrum zabezpieczeń używa CCE (typowych konfiguracji wyliczenie) tooassign unikatowych identyfikatorów dla reguły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d5f68-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="d5f68-145">Odwiedź hello [CCE](https://nvd.nist.gov/cce/index.cfm) witryny, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d5f68-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="d5f68-146">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="d5f68-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="d5f68-147">[Obsługiwane platformy w Centrum zabezpieczeń Azure](security-center-os-coverage.md) — zawiera listę obsługiwanych systemu Windows i maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="d5f68-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="d5f68-148">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="d5f68-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d5f68-149">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5f68-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d5f68-150">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5f68-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="d5f68-151">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="d5f68-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d5f68-152">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="d5f68-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="d5f68-153">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="d5f68-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d5f68-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="d5f68-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
