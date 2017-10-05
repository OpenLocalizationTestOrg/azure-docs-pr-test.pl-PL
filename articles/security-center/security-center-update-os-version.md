---
title: "Wersja aktualizacji systemu operacyjnego w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób wykonania zalecenia Centrum zabezpieczeń Azure ** wersji ** aktualizacji systemu operacyjnego."
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
ms.openlocfilehash: ce0d178914907750e5da59f223a4b1e04b9bb6fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="226a2-103">Zaktualizuj wersję systemu operacyjnego w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="226a2-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="226a2-104">Dla maszyn wirtualnych (VM) usług w chmurze Centrum zabezpieczeń Azure zaleca czy systemu operacyjnego (OS) można zaktualizować, jeśli jest dostępna nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="226a2-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="226a2-105">Tylko chmury usługi sieci web i proces roboczy role uruchomione w środowisku produkcyjnym, które są monitorowane gniazda.</span><span class="sxs-lookup"><span data-stu-id="226a2-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="226a2-106">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="226a2-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="226a2-107">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="226a2-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="226a2-108">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="226a2-108">Implement the recommendation</span></span>
1. <span data-ttu-id="226a2-109">W **zalecenia** bloku, wybierz opcję **wersji systemu operacyjnego aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="226a2-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="226a2-110">![Aktualizacja wersji systemu operacyjnego][1]</span><span class="sxs-lookup"><span data-stu-id="226a2-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="226a2-111">Spowoduje to otwarcie bloku **wersji systemu operacyjnego aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="226a2-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="226a2-112">Wykonaj kroki opisane w tym bloku, aby zaktualizować wersję systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="226a2-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="226a2-113">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="226a2-113">See also</span></span>
<span data-ttu-id="226a2-114">W tym artykule przedstawiono sposób wykonania zalecenia Centrum zabezpieczeń "Wersja aktualizacji systemu operacyjnego".</span><span class="sxs-lookup"><span data-stu-id="226a2-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="226a2-115">Aby dowiedzieć się więcej na temat usługi w chmurze i aktualizowanie wersji systemu operacyjnego dla usługi w chmurze, zobacz:</span><span class="sxs-lookup"><span data-stu-id="226a2-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="226a2-116">Omówienie usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="226a2-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="226a2-117">Jak zaktualizować usługa w chmurze</span><span class="sxs-lookup"><span data-stu-id="226a2-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="226a2-118">Jak skonfigurować usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="226a2-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="226a2-119">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="226a2-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="226a2-120">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="226a2-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="226a2-121">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="226a2-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="226a2-122">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="226a2-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="226a2-123">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="226a2-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="226a2-124">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="226a2-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="226a2-125">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="226a2-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="226a2-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Uzyskaj najnowsze informacje zabezpieczeń platformy Azure i informacje.</span><span class="sxs-lookup"><span data-stu-id="226a2-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
