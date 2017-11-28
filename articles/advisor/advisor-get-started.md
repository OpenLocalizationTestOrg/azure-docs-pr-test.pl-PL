---
title: "Wprowadzenie do usługi Advisor Azure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do usługi Advisor Azure."
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="02ac1-103">Wprowadzenie do usługi Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="02ac1-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="02ac1-104">Dowiedz się, jak dostęp do usługi Advisor za pośrednictwem portalu Azure, Uzyskaj zalecenia, zaimplementować zalecenia, wyszukaj zalecenia i zalecenia dotyczące odświeżania.</span><span class="sxs-lookup"><span data-stu-id="02ac1-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="02ac1-105">Uzyskuj zalecenia usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="02ac1-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="02ac1-106">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02ac1-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="02ac1-107">W okienku po lewej stronie kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="02ac1-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="02ac1-108">W okienku usługi menu w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="02ac1-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="02ac1-109">Zostanie wyświetlony pulpit nawigacyjny usługi Advisor.</span><span class="sxs-lookup"><span data-stu-id="02ac1-109">The Advisor dashboard is displayed.</span></span>

   ![Klasyfikator Azure dostępu przy użyciu portalu Azure](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="02ac1-111">Na pulpicie nawigacyjnym usługi Advisor Wybierz subskrypcję, dla którego chcesz otrzymywać zalecenia.</span><span class="sxs-lookup"><span data-stu-id="02ac1-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="02ac1-112">Pulpit nawigacyjny usługi Advisor wyświetla spersonalizowane zalecenia dla wybranej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="02ac1-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="02ac1-113">Aby uzyskać zalecenia dotyczące określonej kategorii, kliknij jedną z kart: **wysokiej dostępności**, **zabezpieczeń**, **wydajności**, lub **koszt**.</span><span class="sxs-lookup"><span data-stu-id="02ac1-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="02ac1-114">Aby uzyskać dostęp do zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor.</span><span class="sxs-lookup"><span data-stu-id="02ac1-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="02ac1-115">Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* uruchamia pulpitu nawigacyjnego usługi Advisor i klika pozycję **Uzyskaj zalecenia** przycisk.</span><span class="sxs-lookup"><span data-stu-id="02ac1-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="02ac1-116">Jest to *jednorazowa operacja*.</span><span class="sxs-lookup"><span data-stu-id="02ac1-116">This is a *one-time operation*.</span></span> <span data-ttu-id="02ac1-117">Po zarejestrowaniu subskrypcji są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* dla określonego zasobu, grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="02ac1-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Azure Advisor pulpitu nawigacyjnego](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="02ac1-119">Pobierz szczegóły zalecenia usługi Advisor i wdrożyć rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="02ac1-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="02ac1-120">**Zalecenie** bloku klasyfikatora zawiera dodatkowe informacje na temat zalecenia.</span><span class="sxs-lookup"><span data-stu-id="02ac1-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="02ac1-121">Zaloguj się do [portalu Azure](https://portal.azure.com), a następnie uruchom [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="02ac1-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="02ac1-122">Na **zalecenia doradcy w zakresie** pulpitu nawigacyjnego, kliknij przycisk **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="02ac1-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="02ac1-123">Na liście zalecenia kliknij zalecenie, którego chcesz przejrzeć szczegóły.</span><span class="sxs-lookup"><span data-stu-id="02ac1-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="02ac1-124">**Zalecenie** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="02ac1-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="02ac1-125">Na **zalecenia** bloku, przejrzyj informacje o akcjach wykonać, aby rozwiązać potencjalny problem, lub skorzystać z możliwości oszczędności.</span><span class="sxs-lookup"><span data-stu-id="02ac1-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![W bloku zalecenia usługi Advisor](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="02ac1-127">Wyszukaj zalecenia doradcy w zakresie</span><span class="sxs-lookup"><span data-stu-id="02ac1-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="02ac1-128">Możesz wyszukać zalecenia dla określonej grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="02ac1-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="02ac1-129">Możesz również wyszukać zaleceń według stanu.</span><span class="sxs-lookup"><span data-stu-id="02ac1-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="02ac1-130">Zaloguj się do [portalu Azure](https://portal.azure.com), a następnie uruchom [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="02ac1-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="02ac1-131">Wyszukaj zaleceń według filtrowania dla subskrypcji, grupy zasobów i stan zalecenie (**Active** lub **Snoozed**).</span><span class="sxs-lookup"><span data-stu-id="02ac1-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="02ac1-132">Aby wyświetlić listę zalecenia doradcy w zakresie oparte na kryteria filtru wyszukiwania, kliknij przycisk **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="02ac1-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Kryteria filtru wyszukiwania usługi Advisor](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="02ac1-134">Odłóż lub odrzucić zalecenia doradcy w zakresie</span><span class="sxs-lookup"><span data-stu-id="02ac1-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="02ac1-135">Zaloguj się do [portalu Azure](https://portal.azure.com), a następnie uruchom [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="02ac1-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="02ac1-136">Kliknij przycisk **Uzyskaj zalecenia**, a następnie na liście zalecenia, kliknij zalecenie.</span><span class="sxs-lookup"><span data-stu-id="02ac1-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="02ac1-137">Na **zalecenie** bloku, kliknij przycisk **Odłóż**.</span><span class="sxs-lookup"><span data-stu-id="02ac1-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Przykład działania zalecenia usługi Advisor](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="02ac1-139">Określ włączenia trybu czuwania przedziale czasu, lub wybierz **nigdy** aby odrzucić zalecenia.</span><span class="sxs-lookup"><span data-stu-id="02ac1-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="02ac1-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02ac1-140">Next steps</span></span>

<span data-ttu-id="02ac1-141">Aby dowiedzieć się więcej o usłudze Advisor, zobacz:</span><span class="sxs-lookup"><span data-stu-id="02ac1-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="02ac1-142">Wprowadzenie do usługi Advisor Azure</span><span class="sxs-lookup"><span data-stu-id="02ac1-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="02ac1-143">Zalecenia doradcy w zakresie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="02ac1-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="02ac1-144">Zalecenia doradcy w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="02ac1-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="02ac1-145">Zalecenia doradcy w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="02ac1-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="02ac1-146">Zalecenia doradcy w zakresie koszt</span><span class="sxs-lookup"><span data-stu-id="02ac1-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
