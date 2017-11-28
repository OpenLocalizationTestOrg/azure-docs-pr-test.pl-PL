---
title: "Stosowanie aktualizacji systemu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera implementowania zaleceń Centrum zabezpieczeń Azure ** zastosować aktualizacje systemu ** i ** ponowny rozruch po aktualizacji systemu **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="ff735-103">Stosowanie aktualizacji systemu w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="ff735-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="ff735-104">Centrum zabezpieczeń Azure codziennie monitoruje systemu Windows i Linux maszynach wirtualnych (VM) brakujących aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ff735-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="ff735-105">Centrum zabezpieczeń pobiera listę dostępnych zabezpieczeń i krytycznych aktualizacji z witryny Windows Update lub Windows Server Update Services (WSUS), w zależności od tego, który usługa jest skonfigurowana na maszynie Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ff735-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="ff735-106">Centrum zabezpieczeń sprawdza także najnowsze aktualizacje w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="ff735-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="ff735-107">Jeśli maszyna wirtualna jest Brak aktualizacji systemu, Centrum zabezpieczeń zaleca się zastosowanie aktualizacji systemu</span><span class="sxs-lookup"><span data-stu-id="ff735-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="ff735-108">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ff735-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="ff735-109">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="ff735-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="ff735-110">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="ff735-110">Implement the recommendation</span></span>
1. <span data-ttu-id="ff735-111">W **zalecenia** bloku, wybierz opcję **stosowanie aktualizacji systemu**.</span><span class="sxs-lookup"><span data-stu-id="ff735-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Zastosuj aktualizacje systemu][1]
2. <span data-ttu-id="ff735-113">**Stosowanie aktualizacji systemu** zostanie otwarty blok zawierający listę maszyn wirtualnych Brak aktualizacji systemu.</span><span class="sxs-lookup"><span data-stu-id="ff735-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="ff735-114">Wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ff735-114">Select a VM.</span></span>

   ![Wybierz maszynę Wirtualną][2]
3. <span data-ttu-id="ff735-116">Zostanie otwarty blok zawierający listę brakujących aktualizacji dla tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ff735-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="ff735-117">Wybierz aktualizację systemu.</span><span class="sxs-lookup"><span data-stu-id="ff735-117">Select a system update.</span></span> <span data-ttu-id="ff735-118">W tym przykładzie załóżmy wybierz KB3156016.</span><span class="sxs-lookup"><span data-stu-id="ff735-118">In this example, let’s select KB3156016.</span></span>

   ![Brakujące aktualizacje zabezpieczeń][3]

4. <span data-ttu-id="ff735-120">Postępuj zgodnie z instrukcjami **aktualizacji zabezpieczeń** bloku, aby zastosować brakujących aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ff735-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Aktualizacja zabezpieczeń][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="ff735-122">Uruchom ponownie po zaktualizowaniu systemu</span><span class="sxs-lookup"><span data-stu-id="ff735-122">Reboot after system updates</span></span>
1. <span data-ttu-id="ff735-123">Wróć do **zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="ff735-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="ff735-124">Wygenerowano nowy wpis, po zastosowaniu aktualizacji systemu, o nazwie **ponowny rozruch po aktualizacji systemu**.</span><span class="sxs-lookup"><span data-stu-id="ff735-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="ff735-125">Ten wpis informuje o tym, że należy przeprowadzić ponowny rozruch maszyny Wirtualnej, aby ukończyć proces stosowania aktualizacji systemu.</span><span class="sxs-lookup"><span data-stu-id="ff735-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Uruchom ponownie po zaktualizowaniu systemu][5]
2. <span data-ttu-id="ff735-127">Wybierz **ponowny rozruch po aktualizacji systemu**.</span><span class="sxs-lookup"><span data-stu-id="ff735-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="ff735-128">Spowoduje to otwarcie **oczekuje na ponowne uruchomienie do ukończenia aktualizacji systemu** blok zawierający listę maszyn wirtualnych, które należy ponownie przeprowadzić systemu Zastosuj aktualizacje procesu.</span><span class="sxs-lookup"><span data-stu-id="ff735-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Oczekiwanie na ponowne uruchomienie][6]

<span data-ttu-id="ff735-130">Uruchom ponownie maszynę Wirtualną z platformy Azure, aby ukończyć proces.</span><span class="sxs-lookup"><span data-stu-id="ff735-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff735-131">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ff735-131">See also</span></span>
<span data-ttu-id="ff735-132">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="ff735-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="ff735-133">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ff735-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ff735-134">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ff735-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ff735-135">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ff735-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ff735-136">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="ff735-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ff735-137">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="ff735-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ff735-138">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="ff735-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ff735-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="ff735-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
