---
title: "aktualizacje systemu aaaApply w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zaleceń Centrum zabezpieczeń Azure ** zastosować aktualizacje systemu ** i ** ponowny rozruch po aktualizacji systemu **."
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
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="495e7-103">Stosowanie aktualizacji systemu w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="495e7-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="495e7-104">Centrum zabezpieczeń Azure codziennie monitoruje systemu Windows i Linux maszynach wirtualnych (VM) brakujących aktualizacji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="495e7-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="495e7-105">Centrum zabezpieczeń pobiera listę dostępnych zabezpieczeń i krytycznych aktualizacji z witryny Windows Update lub Windows Server Update Services (WSUS), w zależności od tego, który usługa jest skonfigurowana na maszynie Wirtualnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="495e7-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="495e7-106">Centrum zabezpieczeń sprawdza również hello najnowsze aktualizacje w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="495e7-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="495e7-107">Jeśli maszyna wirtualna jest Brak aktualizacji systemu, Centrum zabezpieczeń zaleca się zastosowanie aktualizacji systemu</span><span class="sxs-lookup"><span data-stu-id="495e7-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="495e7-108">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="495e7-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="495e7-109">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="495e7-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="495e7-110">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="495e7-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="495e7-111">W hello **zalecenia** bloku, wybierz opcję **stosowanie aktualizacji systemu**.</span><span class="sxs-lookup"><span data-stu-id="495e7-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Zastosuj aktualizacje systemu][1]
2. <span data-ttu-id="495e7-113">Witaj **stosowanie aktualizacji systemu** zostanie otwarty blok zawierający listę maszyn wirtualnych Brak aktualizacji systemu.</span><span class="sxs-lookup"><span data-stu-id="495e7-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="495e7-114">Wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="495e7-114">Select a VM.</span></span>

   ![Wybierz maszynę Wirtualną][2]
3. <span data-ttu-id="495e7-116">Zostanie otwarty blok zawierający listę brakujących aktualizacji dla tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="495e7-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="495e7-117">Wybierz aktualizację systemu.</span><span class="sxs-lookup"><span data-stu-id="495e7-117">Select a system update.</span></span> <span data-ttu-id="495e7-118">W tym przykładzie załóżmy wybierz KB3156016.</span><span class="sxs-lookup"><span data-stu-id="495e7-118">In this example, let’s select KB3156016.</span></span>

   ![Brakujące aktualizacje zabezpieczeń][3]

4. <span data-ttu-id="495e7-120">Wykonaj kroki hello hello **aktualizacji zabezpieczeń** tooapply bloku hello brakujących aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="495e7-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Aktualizacja zabezpieczeń][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="495e7-122">Uruchom ponownie po zaktualizowaniu systemu</span><span class="sxs-lookup"><span data-stu-id="495e7-122">Reboot after system updates</span></span>
1. <span data-ttu-id="495e7-123">Zwraca toohello **zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="495e7-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="495e7-124">Wygenerowano nowy wpis, po zastosowaniu aktualizacji systemu, o nazwie **ponowny rozruch po aktualizacji systemu**.</span><span class="sxs-lookup"><span data-stu-id="495e7-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="495e7-125">Ten wpis informuje o tym, że należy tooreboot hello wirtualna toocomplete hello proces stosowania aktualizacji systemu.</span><span class="sxs-lookup"><span data-stu-id="495e7-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Uruchom ponownie po zaktualizowaniu systemu][5]
2. <span data-ttu-id="495e7-127">Wybierz **ponowny rozruch po aktualizacji systemu**.</span><span class="sxs-lookup"><span data-stu-id="495e7-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="495e7-128">Spowoduje to otwarcie **toocomplete oczekujące aktualizacje systemu jest ponowne uruchomienie** blok zawierający listę maszyn wirtualnych konieczność toorestart toocomplete hello zastosowania procesu aktualizacji systemu.</span><span class="sxs-lookup"><span data-stu-id="495e7-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Oczekiwanie na ponowne uruchomienie][6]

<span data-ttu-id="495e7-130">Uruchom ponownie hello maszyny Wirtualnej z platformy Azure toocomplete hello procesu.</span><span class="sxs-lookup"><span data-stu-id="495e7-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="495e7-131">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="495e7-131">See also</span></span>
<span data-ttu-id="495e7-132">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="495e7-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="495e7-133">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="495e7-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="495e7-134">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="495e7-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="495e7-135">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="495e7-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="495e7-136">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="495e7-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="495e7-137">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="495e7-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="495e7-138">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="495e7-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="495e7-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="495e7-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
