---
title: "zalecenia usługi Advisor koszt aaaAzure | Dokumentacja firmy Microsoft"
description: "Użyj Azure Advisor toooptimize hello koszt wdrożeń platformy Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="cef96-103">Zalecenia doradcy w zakresie koszt</span><span class="sxs-lookup"><span data-stu-id="cef96-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="cef96-104">Advisor pomaga zoptymalizować i zmniejszyć ogólną Azure wydatków, określając bezczynności i wyczerpaniu zasobów.</span><span class="sxs-lookup"><span data-stu-id="cef96-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="cef96-105">Zalecenia z hello mogą uzyskać kosztem **koszt** kartę na pulpicie nawigacyjnym usługi Advisor hello.</span><span class="sxs-lookup"><span data-stu-id="cef96-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Karta koszt usługi Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="cef96-107">Optymalizacja spędzają na zmieniając niedostatecznie wystąpień maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="cef96-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="cef96-108">Mimo że niektóre scenariusze aplikacji może spowodować niskiego poziomu wykorzystania zgodnie z projektem, można często zaoszczędzić, zarządzając hello rozmiaru i liczby maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cef96-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="cef96-109">Klasyfikator monitoruje użycie maszyny wirtualnej w ciągu ostatnich 14 dni, a następnie identyfikuje niskiego wykorzystania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cef96-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="cef96-110">Maszyny wirtualne, których użycie procesora CPU wynosi 5 procent lub mniej i użycie sieci jest 7 MB lub mniej przez cztery lub więcej dni są traktowane jako niskiego wykorzystania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cef96-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="cef96-111">Pokazuje Advisor hello szacowany koszt kontynuowanie toorun maszyny wirtualnej, dzięki czemu można wybrać tooshut w dół, lub zmienić jego rozmiar.</span><span class="sxs-lookup"><span data-stu-id="cef96-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Klasyfikator koszt zalecenia dotyczące zmiany rozmiaru maszyny wirtualne](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="cef96-113">Użyj ekonomiczne rozwiązanie toomanage cele dotyczące wydajności wielu baz danych serwera SQL</span><span class="sxs-lookup"><span data-stu-id="cef96-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="cef96-114">Klasyfikator identyfikuje wystąpienia programu SQL server, które mogą korzystać z tworzenie elastycznych pul baz danych.</span><span class="sxs-lookup"><span data-stu-id="cef96-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="cef96-115">Elastyczne pule baz danych Podaj toomanage proste i ekonomiczne rozwiązanie hello cele dotyczące wydajności z wieloma bazami danych, które mają różne wzorce użycia.</span><span class="sxs-lookup"><span data-stu-id="cef96-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="cef96-116">Aby uzyskać więcej informacji na temat Azure pule elastyczne, zobacz [co to jest pula elastyczna Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="cef96-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Klasyfikator koszt zalecenia dotyczące elastyczne pule baz danych](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="cef96-118">Jak tooaccess koszt zalecenia w programie Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="cef96-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="cef96-119">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cef96-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="cef96-120">W okienku po lewej stronie powitania kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="cef96-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="cef96-121">W hello usługa okienku menu, w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="cef96-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="cef96-122">pulpit nawigacyjny usługi Advisor Hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="cef96-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="cef96-123">Na pulpicie nawigacyjnym usługi Advisor hello, kliknij przycisk hello **koszt** kartę.</span><span class="sxs-lookup"><span data-stu-id="cef96-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="cef96-124">Wybierz subskrypcję hello, dla którego chcesz tooreceive zalecenia, a następnie kliknij **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="cef96-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="cef96-125">tooaccess zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor.</span><span class="sxs-lookup"><span data-stu-id="cef96-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="cef96-126">Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* powoduje uruchomienie hello Advisor hello pulpitu nawigacyjnego i klika przycisk **Uzyskaj zalecenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cef96-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="cef96-127">Jest to *jednorazowa operacja*.</span><span class="sxs-lookup"><span data-stu-id="cef96-127">This is a *one-time operation*.</span></span> <span data-ttu-id="cef96-128">Po zarejestrowaniu subskrypcji hello są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* subskrypcji, grupy zasobów, lub określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="cef96-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cef96-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cef96-129">Next steps</span></span>

<span data-ttu-id="cef96-130">toolearn więcej informacji na temat zalecenia doradcy w zakresie, zobacz:</span><span class="sxs-lookup"><span data-stu-id="cef96-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="cef96-131">Wprowadzenie tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="cef96-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="cef96-132">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="cef96-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="cef96-133">Zalecenia doradcy w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="cef96-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="cef96-134">Zalecenia doradcy w zakresie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="cef96-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="cef96-135">Zalecenia doradcy w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="cef96-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
