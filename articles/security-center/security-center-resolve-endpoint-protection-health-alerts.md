---
title: "alerty kondycji aaaResolve programu endpoint protection w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** rozwiązania programu Endpoint Protection kondycji alerty **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="ac20d-103">Rozwiąż alerty kondycji programu endpoint protection w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="ac20d-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="ac20d-104">Centrum zabezpieczeń Azure zaleca rozwiązanie alerty dotyczące kondycji ochrony wykrytego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="ac20d-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="ac20d-105">Centrum zabezpieczeń umożliwia toosee maszyn wirtualnych (VM) mają błędy ochrony punktu końcowego i jak wiele błędów.</span><span class="sxs-lookup"><span data-stu-id="ac20d-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="ac20d-106">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ac20d-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="ac20d-107">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="ac20d-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ac20d-108">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="ac20d-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="ac20d-109">W hello **bloku zalecenia**, wybierz pozycję **alerty dotyczące kondycji rozwiązania programu Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="ac20d-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="ac20d-110">![Rozwiązywanie alertów dotyczących kondycji punktu końcowego][1]</span><span class="sxs-lookup"><span data-stu-id="ac20d-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="ac20d-111">Spowoduje to otwarcie bloku hello **awarii programu Endpoint Protection** zawierająca listę maszyn wirtualnych o awarii i hello liczby błędów dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ac20d-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="ac20d-112">Wybierz maszynę Wirtualną z listy hello.</span><span class="sxs-lookup"><span data-stu-id="ac20d-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="ac20d-113">![Błąd ochrony punktu końcowego][2]</span><span class="sxs-lookup"><span data-stu-id="ac20d-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="ac20d-114">A **listy błędów** zostanie otwarty blok dla hello wybranych maszyn wirtualnych, wyświetlanie listy błędów.</span><span class="sxs-lookup"><span data-stu-id="ac20d-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="ac20d-115">Wybierz awarii z toolearn listy hello więcej.</span><span class="sxs-lookup"><span data-stu-id="ac20d-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="ac20d-116">Spowoduje to otwarcie bloku z informacjami o niepowodzeniu hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="ac20d-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="ac20d-117">![Lista błędów][3]
   ![zdarzeń błędów][4]</span><span class="sxs-lookup"><span data-stu-id="ac20d-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="ac20d-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ac20d-118">See also</span></span>
<span data-ttu-id="ac20d-119">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ac20d-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ac20d-120">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md)— Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="ac20d-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ac20d-121">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — informacje o tym, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac20d-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ac20d-122">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md)— Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac20d-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ac20d-123">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md)— Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="ac20d-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ac20d-124">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="ac20d-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="ac20d-125">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="ac20d-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ac20d-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="ac20d-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
