---
title: "aaaManaging rozwiązań partnerskich w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przeprowadzi Cię przez jaki Centrum zabezpieczeń Azure umożliwia monitorowanie stanu oka hello kondycji rozwiązań partnerskich zintegrowanych z subskrypcją platformy Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="db485-103">Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="db485-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="db485-104">Ten dokument przeprowadzi Cię przez jak toomonitor hello stanu kondycji rozwiązań partnerskich w Centrum zabezpieczeń Azure.</span><span class="sxs-lookup"><span data-stu-id="db485-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="db485-105">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="db485-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="db485-106">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="db485-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="db485-107">Monitorowanie rozwiązań partnerskich</span><span class="sxs-lookup"><span data-stu-id="db485-107">Monitoring partner solutions</span></span>
<span data-ttu-id="db485-108">Witaj **rozwiązania partnerskie** Kafelek na powitania **Centrum zabezpieczeń** bloku umożliwia monitorowanie stanu oka hello kondycji rozwiązań partnerskich zintegrowanych z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="db485-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Kafelek Rozwiązania partnerskie][1]

<span data-ttu-id="db485-110">Witaj **rozwiązania partnerskie** kafelka Wyświetla hello liczbę rozwiązań partnerskich zintegrowanych z subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="db485-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="db485-111">Jeśli nie masz rozwiązań zintegrowanych, kafelka hello Wyświetla hello liczby zero.</span><span class="sxs-lookup"><span data-stu-id="db485-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="db485-112">tooview hello kondycji rozwiązań partnerskich:</span><span class="sxs-lookup"><span data-stu-id="db485-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="db485-113">Wybierz hello **rozwiązania partnerskie** kafelka.</span><span class="sxs-lookup"><span data-stu-id="db485-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="db485-114">Witaj **rozwiązania partnerskie** tooSecurity Center połączona zostanie otwarty blok zawierający listę rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="db485-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Rozwiązania partnerskie][3]

   <span data-ttu-id="db485-116">Stan Hello rozwiązanie partnerskie może być:</span><span class="sxs-lookup"><span data-stu-id="db485-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="db485-117">Chronione (kolor zielony) — brak problemów dotyczących kondycji.</span><span class="sxs-lookup"><span data-stu-id="db485-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="db485-118">W złej kondycji (kolor czerwony) — istnieje problem z kondycją wymagający natychmiastowej uwagi.</span><span class="sxs-lookup"><span data-stu-id="db485-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="db485-119">Zatrzymano raportowania (kolor pomarańczowy) — Witaj rozwiązania zostało zatrzymane raportowanie dotyczące kondycji.</span><span class="sxs-lookup"><span data-stu-id="db485-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="db485-120">Nieznany stan ochrony (kolor pomarańczowy) — kondycja hello rozwiązania hello jest nieznany w tej chwili ukończenia procesu tooa nie powiodło się dodanie nowego zasobu toohello istniejącego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="db485-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="db485-121">Nie zgłoszono (kolor szary) — rozwiązanie hello nie zgłosił żadnych czynności, ale stan rozwiązania może zostać zgłoszony, jeśli został ostatnio podłączony i jego wdrażanie nadal trwa.</span><span class="sxs-lookup"><span data-stu-id="db485-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="db485-122">Wybierz rozwiązanie partnerskie.</span><span class="sxs-lookup"><span data-stu-id="db485-122">Select a partner solution.</span></span> <span data-ttu-id="db485-123">W tym przykładzie umożliwia wybierz hello **Qualys** rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="db485-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="db485-124">Zostanie otwarty blok, wyświetlając stan hello rozwiązaniem partnerskim hello i rozwiązania hello skojarzonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="db485-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="db485-125">Wybierz **Konsola rozwiązań** Zarządzanie partnerami hello tooopen środowisko dla tego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="db485-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Szczegóły rozwiązania partnerskiego][4]
3. <span data-ttu-id="db485-127">Przejdź wstecz toohello **Qualys** bloku, a następnie wybierz **wirtualna łącze**.</span><span class="sxs-lookup"><span data-stu-id="db485-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="db485-128">Witaj **łączenie aplikacji** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="db485-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="db485-129">Tutaj można połączyć z rozwiązaniem partnerskim toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="db485-129">Here you can connect resources toohello partner solution.</span></span>

   ![Łącze zasobów toopartner rozwiązania][5]

## <a name="next-steps"></a><span data-ttu-id="db485-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db485-131">Next steps</span></span>
<span data-ttu-id="db485-132">W tym dokumencie zostały wprowadzone toohello **rozwiązań partnerskich** kafelka w Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="db485-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="db485-133">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="db485-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="db485-134">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="db485-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="db485-135">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="db485-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="db485-136">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="db485-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="db485-137">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="db485-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="db485-138">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="db485-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="db485-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="db485-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
