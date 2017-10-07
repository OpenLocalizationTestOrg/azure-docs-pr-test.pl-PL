---
title: "wersja systemu operacyjnego aaaUpdate w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooimplement hello zalecenia Centrum zabezpieczeń Azure ** wersji ** aktualizacji systemu operacyjnego."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: f3497d7266da40d3a965f9cb8e84392d2aaa28f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="94395-103">Zaktualizuj wersję systemu operacyjnego w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="94395-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="94395-104">Dla maszyn wirtualnych (VM) usług w chmurze Centrum zabezpieczeń Azure zaleca można zaktualizować tego systemu operacyjnego hello (systemu operacyjnego), jeśli jest dostępna nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="94395-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that hello operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="94395-105">Tylko chmury usługi sieci web i proces roboczy role uruchomione w środowisku produkcyjnym, które są monitorowane gniazda.</span><span class="sxs-lookup"><span data-stu-id="94395-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="94395-106">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="94395-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="94395-107">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="94395-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="94395-108">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="94395-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="94395-109">W hello **zalecenia** bloku, wybierz opcję **wersji systemu operacyjnego aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="94395-109">In hello **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="94395-110">![Aktualizacja wersji systemu operacyjnego][1]</span><span class="sxs-lookup"><span data-stu-id="94395-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="94395-111">Spowoduje to otwarcie bloku hello **wersji systemu operacyjnego aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="94395-111">This opens hello blade **Update OS version**.</span></span> <span data-ttu-id="94395-112">Wykonaj kroki hello w tej wersji systemu operacyjnego hello tooupdate bloku.</span><span class="sxs-lookup"><span data-stu-id="94395-112">Follow hello steps in this blade tooupdate hello OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="94395-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="94395-113">See also</span></span>
<span data-ttu-id="94395-114">W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "wersja aktualizacji systemu operacyjnego."</span><span class="sxs-lookup"><span data-stu-id="94395-114">This article showed you how tooimplement hello Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="94395-115">toolearn więcej informacji na temat usługi w chmurze i aktualizowania hello wersji systemu operacyjnego dla usługi w chmurze, zobacz:</span><span class="sxs-lookup"><span data-stu-id="94395-115">toolearn more about cloud services and updating hello OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="94395-116">Omówienie usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="94395-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="94395-117">Jak tooupdate usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="94395-117">How tooupdate a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="94395-118">W jaki sposób tooConfigure usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="94395-118">How tooConfigure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="94395-119">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="94395-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="94395-120">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="94395-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="94395-121">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94395-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="94395-122">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94395-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="94395-123">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="94395-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="94395-124">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="94395-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="94395-125">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="94395-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="94395-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="94395-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
