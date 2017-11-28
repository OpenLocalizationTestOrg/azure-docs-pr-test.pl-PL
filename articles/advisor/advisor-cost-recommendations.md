---
title: "Azure zalecenia usługi Advisor koszt | Dokumentacja firmy Microsoft"
description: "Optymalizowanie koszt wdrożeń platformy Azure przy użyciu klasyfikatora Azure."
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="879da-103">Zalecenia doradcy w zakresie koszt</span><span class="sxs-lookup"><span data-stu-id="879da-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="879da-104">Advisor pomaga zoptymalizować i zmniejszyć ogólną Azure wydatków, określając bezczynności i wyczerpaniu zasobów.</span><span class="sxs-lookup"><span data-stu-id="879da-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="879da-105">Zalecenia można uzyskać koszt **koszt** na pulpicie nawigacyjnym usługi Advisor.</span><span class="sxs-lookup"><span data-stu-id="879da-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Karta koszt usługi Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="879da-107">Optymalizacja spędzają na zmieniając niedostatecznie wystąpień maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="879da-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="879da-108">Mimo że niektóre scenariusze aplikacji może spowodować niskiego poziomu wykorzystania zgodnie z projektem, można często zaoszczędzić, zarządzając rozmiaru i liczby maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="879da-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="879da-109">Klasyfikator monitoruje użycie maszyny wirtualnej w ciągu ostatnich 14 dni, a następnie identyfikuje niskiego wykorzystania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="879da-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="879da-110">Maszyny wirtualne, których użycie procesora CPU wynosi 5 procent lub mniej i użycie sieci jest 7 MB lub mniej przez cztery lub więcej dni są traktowane jako niskiego wykorzystania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="879da-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="879da-111">Klasyfikator pokazuje szacowany koszt kontynuowania działania maszyny wirtualnej, dzięki czemu można zamknąć lub zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="879da-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![Klasyfikator koszt zalecenia dotyczące zmiany rozmiaru maszyny wirtualne](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="879da-113">Używanie ekonomiczne rozwiązanie do zarządzania cele dotyczące wydajności wielu baz danych serwera SQL</span><span class="sxs-lookup"><span data-stu-id="879da-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="879da-114">Klasyfikator identyfikuje wystąpienia programu SQL server, które mogą korzystać z tworzenie elastycznych pul baz danych.</span><span class="sxs-lookup"><span data-stu-id="879da-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="879da-115">Elastyczne pule baz danych zapewniają proste i ekonomiczne rozwiązanie do zarządzania cele wydajności wielu baz danych, które mają różnych wzorców użycia.</span><span class="sxs-lookup"><span data-stu-id="879da-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="879da-116">Aby uzyskać więcej informacji na temat Azure pule elastyczne, zobacz [co to jest pula elastyczna Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="879da-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Klasyfikator koszt zalecenia dotyczące elastyczne pule baz danych](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="879da-118">Jak zalecenia kosztem dostępu w programie Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="879da-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="879da-119">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="879da-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="879da-120">W okienku po lewej stronie kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="879da-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="879da-121">W okienku usługi menu w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="879da-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="879da-122">Zostanie wyświetlony pulpit nawigacyjny usługi Advisor.</span><span class="sxs-lookup"><span data-stu-id="879da-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="879da-123">Na pulpicie nawigacyjnym usługi Advisor, kliknij przycisk **koszt** kartę.</span><span class="sxs-lookup"><span data-stu-id="879da-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="879da-124">Wybierz subskrypcję, dla którego chcesz otrzymywać zalecenia, a następnie kliknij przycisk **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="879da-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="879da-125">Aby uzyskać dostęp do zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor.</span><span class="sxs-lookup"><span data-stu-id="879da-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="879da-126">Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* uruchamia pulpitu nawigacyjnego usługi Advisor i klika pozycję **Uzyskaj zalecenia** przycisk.</span><span class="sxs-lookup"><span data-stu-id="879da-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="879da-127">Jest to *jednorazowa operacja*.</span><span class="sxs-lookup"><span data-stu-id="879da-127">This is a *one-time operation*.</span></span> <span data-ttu-id="879da-128">Po zarejestrowaniu subskrypcji są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* dla określonego zasobu, grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="879da-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="879da-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="879da-129">Next steps</span></span>

<span data-ttu-id="879da-130">Aby dowiedzieć się więcej na temat zalecenia doradcy w zakresie, zobacz:</span><span class="sxs-lookup"><span data-stu-id="879da-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="879da-131">Wprowadzenie do usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="879da-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="879da-132">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="879da-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="879da-133">Zalecenia doradcy w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="879da-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="879da-134">Zalecenia doradcy w zakresie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="879da-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="879da-135">Zalecenia doradcy w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="879da-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
