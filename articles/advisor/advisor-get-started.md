---
title: "wprowadzenie do usługi Advisor Azure aaaGet | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 30fc8b8f3823f6f047e46cb9000189f3ccb3d514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="5040d-103">Wprowadzenie do usługi Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="5040d-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="5040d-104">Dowiedz się, jak tooaccess Advisor za pośrednictwem hello portalu Azure, zalecenia get zaimplementować zalecenia, wyszukaj zalecenia i zalecenia dotyczące odświeżania.</span><span class="sxs-lookup"><span data-stu-id="5040d-104">Learn how tooaccess Advisor through hello Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="5040d-105">Uzyskuj zalecenia usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="5040d-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="5040d-106">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5040d-106">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="5040d-107">W okienku po lewej stronie powitania kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="5040d-107">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="5040d-108">W hello usługa okienku menu, w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="5040d-108">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="5040d-109">pulpit nawigacyjny usługi Advisor Hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="5040d-109">hello Advisor dashboard is displayed.</span></span>

   ![Klasyfikator Azure dostępu przy użyciu hello portalu Azure](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="5040d-111">Na pulpicie nawigacyjnym usługi Advisor hello Wybierz subskrypcję hello, dla której ma zostać tooreceive zalecenia.</span><span class="sxs-lookup"><span data-stu-id="5040d-111">On hello Advisor dashboard, select hello subscription for which you want tooreceive recommendations.</span></span>  
<span data-ttu-id="5040d-112">pulpit nawigacyjny usługi Advisor Hello wyświetla spersonalizowane zalecenia dla wybranej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5040d-112">hello Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="5040d-113">zalecenia dotyczące tooget dla określonej kategorii, kliknij jedną z kart hello: **wysokiej dostępności**, **zabezpieczeń**, **wydajności**, lub **koszt**.</span><span class="sxs-lookup"><span data-stu-id="5040d-113">tooget recommendations for a particular category, click one of hello tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="5040d-114">tooaccess zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor.</span><span class="sxs-lookup"><span data-stu-id="5040d-114">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="5040d-115">Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* powoduje uruchomienie hello Advisor hello pulpitu nawigacyjnego i klika przycisk **Uzyskaj zalecenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5040d-115">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="5040d-116">Jest to *jednorazowa operacja*.</span><span class="sxs-lookup"><span data-stu-id="5040d-116">This is a *one-time operation*.</span></span> <span data-ttu-id="5040d-117">Po zarejestrowaniu subskrypcji hello są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* subskrypcji, grupy zasobów, lub określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="5040d-117">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Azure Advisor pulpitu nawigacyjnego](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="5040d-119">Pobierz szczegóły zalecenia usługi Advisor i wdrożyć rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="5040d-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="5040d-120">Witaj **zalecenie** bloku klasyfikatora zawiera dodatkowe informacje na temat hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="5040d-120">hello **Recommendation** blade in Advisor offers additional information about hello recommendation.</span></span> 

1. <span data-ttu-id="5040d-121">Zaloguj się toohello [portalu Azure](https://portal.azure.com), a następnie uruchom [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="5040d-121">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="5040d-122">Na powitania **zalecenia doradcy w zakresie** pulpitu nawigacyjnego, kliknij przycisk **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="5040d-122">On hello **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="5040d-123">Kliknij zalecenie, które mają tooreview szczegółowo liście hello zaleceń.</span><span class="sxs-lookup"><span data-stu-id="5040d-123">In hello list of recommendations, click a recommendation that you want tooreview in detail.</span></span>  
<span data-ttu-id="5040d-124">Witaj **zalecenie** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="5040d-124">hello **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="5040d-125">Na powitania **zalecenia** bloku, przejrzyj informacje o akcjach, wykonaj tooresolve potencjalny problem, lub skorzystać z możliwości oszczędności.</span><span class="sxs-lookup"><span data-stu-id="5040d-125">On hello **Recommendations** blade, review information about actions that you can perform tooresolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Witaj bloku zalecenia usługi Advisor](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="5040d-127">Wyszukaj zalecenia doradcy w zakresie</span><span class="sxs-lookup"><span data-stu-id="5040d-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="5040d-128">Możesz wyszukać zalecenia dla określonej grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5040d-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="5040d-129">Możesz również wyszukać zaleceń według stanu.</span><span class="sxs-lookup"><span data-stu-id="5040d-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="5040d-130">Zaloguj się toohello [portalu Azure](https://portal.azure.com), a następnie uruchom [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="5040d-130">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="5040d-131">Wyszukaj zaleceń według filtrowania dla subskrypcji, grupy zasobów i stan zalecenie (**Active** lub **Snoozed**).</span><span class="sxs-lookup"><span data-stu-id="5040d-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="5040d-132">kliknij kryteria filtru wyszukiwania toodisplay listę zalecenia doradcy w zakresie oparte na **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="5040d-132">toodisplay a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Kryteria filtru wyszukiwania usługi Advisor](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="5040d-134">Odłóż lub odrzucić zalecenia doradcy w zakresie</span><span class="sxs-lookup"><span data-stu-id="5040d-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="5040d-135">Zaloguj się toohello [portalu Azure](https://portal.azure.com), a następnie uruchom [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="5040d-135">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="5040d-136">Kliknij przycisk **Uzyskaj zalecenia**, a następnie na liście hello zalecenia, kliknij zalecenie.</span><span class="sxs-lookup"><span data-stu-id="5040d-136">Click **Get recommendations**, and then, in hello list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="5040d-137">Na powitania **zalecenie** bloku, kliknij przycisk **Odłóż**.</span><span class="sxs-lookup"><span data-stu-id="5040d-137">On hello **Recommendation** blade, click **Snooze**.</span></span>  

   ![Przykład działania zalecenia usługi Advisor](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="5040d-139">Określ włączenia trybu czuwania przedziale czasu, lub wybierz **nigdy** toodismiss hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="5040d-139">Specify a snooze time period, or select **Never** toodismiss hello recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5040d-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5040d-140">Next steps</span></span>

<span data-ttu-id="5040d-141">toolearn więcej informacji o usłudze Advisor, zobacz:</span><span class="sxs-lookup"><span data-stu-id="5040d-141">toolearn more about Advisor, see:</span></span>
* [<span data-ttu-id="5040d-142">Wprowadzenie tooAzure Advisor</span><span class="sxs-lookup"><span data-stu-id="5040d-142">Introduction tooAzure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="5040d-143">Zalecenia doradcy w zakresie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="5040d-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="5040d-144">Zalecenia doradcy w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="5040d-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="5040d-145">Zalecenia doradcy w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="5040d-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="5040d-146">Zalecenia doradcy w zakresie koszt</span><span class="sxs-lookup"><span data-stu-id="5040d-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
