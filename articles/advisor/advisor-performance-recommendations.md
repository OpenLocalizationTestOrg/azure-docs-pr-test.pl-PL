---
title: "Azure zalecenia usługi Advisor wydajności | Dokumentacja firmy Microsoft"
description: "Użyj usługi Advisor w celu zoptymalizowania wydajności wdrożeń platformy Azure."
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
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="416db-103">Zalecenia doradcy w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="416db-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="416db-104">Azure zalecenia wydajności doradcy w zakresie zwiększyć szybkość i czas odpowiedzi aplikacji biznesowych o znaczeniu krytycznym.</span><span class="sxs-lookup"><span data-stu-id="416db-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="416db-105">Zalecenia dotyczące wydajności z usługi Advisor można uzyskać **wydajności** pulpitu nawigacyjnego usługi Advisor.</span><span class="sxs-lookup"><span data-stu-id="416db-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Karta wydajność usługi Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="416db-107">Poprawić wydajność bazy danych w usłudze Advisor bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="416db-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="416db-108">Advisor zapewnia spójne, skonsolidowanego widoku zaleceń dla wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="416db-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="416db-109">Umożliwia integrację z Doradcę bazy danych SQL, aby wyświetlić zalecenia dotyczące poprawy wydajności bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="416db-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="416db-110">Doradca bazy danych programu SQL ocenia wydajności baz danych SQL Azure, analizując Twojej historii użycia.</span><span class="sxs-lookup"><span data-stu-id="416db-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="416db-111">Oferuje zaleceń, które są najbardziej odpowiednie do uruchamiania typowych zadań bazy danych.</span><span class="sxs-lookup"><span data-stu-id="416db-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="416db-112">Aby uzyskać zalecenia, bazy danych musi mieć o tydzień użycia, a w ciągu tygodnia musi być pewne spójnej działania.</span><span class="sxs-lookup"><span data-stu-id="416db-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="416db-113">Doradca bazy danych SQL można zoptymalizować łatwiej wzorców zapytania spójna niż dla losowych seria działań.</span><span class="sxs-lookup"><span data-stu-id="416db-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="416db-114">Aby uzyskać więcej informacji o usłudze Advisor bazy danych SQL, zobacz [doradcy bazy danych SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="416db-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Zalecenia dotyczące bazy danych SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="416db-116">Zwiększyć wydajność pamięci podręcznej Redis i niezawodności</span><span class="sxs-lookup"><span data-stu-id="416db-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="416db-117">Klasyfikator identyfikuje wystąpienia pamięci podręcznej Redis, gdzie mogą być niekorzystny wpływ na wydajność wysokie użycie pamięci, obciążenie serwera, przepustowości sieci lub dużej liczby połączeń klientów.</span><span class="sxs-lookup"><span data-stu-id="416db-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="416db-118">Klasyfikator także najlepsze rozwiązania w zakresie zalecenia, aby uniknąć potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="416db-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="416db-119">Aby uzyskać więcej informacji o pamięci podręcznej Redis, zobacz [Advisor pamięci podręcznej Redis](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="416db-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="416db-120">Zwiększyć wydajność aplikacji usługi i niezawodności</span><span class="sxs-lookup"><span data-stu-id="416db-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="416db-121">Klasyfikator Azure integruje się poniżej rekomendowane najlepsze rozwiązania dla poprawy środowiska usługi aplikacji i wykrywania możliwości odpowiednie platformy.</span><span class="sxs-lookup"><span data-stu-id="416db-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="416db-122">Przykłady zalecenia usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="416db-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="416db-123">Wykrywanie wystąpień, w którym na wyczerpaniu pamięci lub zasobów procesora CPU przez środowisk uruchomieniowych aplikacji z opcjami środki zaradcze.</span><span class="sxs-lookup"><span data-stu-id="416db-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="416db-124">Wykrywanie wystąpień, w którym collocating zasoby, takie jak aplikacje sieci web i baz danych można zwiększyć wydajność i tańsze.</span><span class="sxs-lookup"><span data-stu-id="416db-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="416db-125">Aby uzyskać więcej informacji na temat zalecenia usługi aplikacji, zobacz [najlepsze rozwiązania dotyczące usługi Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="416db-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="416db-126">![Zalecenia dotyczące usług aplikacji](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="416db-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="416db-127">Jak uzyskać dostęp zalecenia dotyczące wydajności w usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="416db-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="416db-128">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="416db-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="416db-129">W okienku po lewej stronie kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="416db-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="416db-130">W okienku usługi menu w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="416db-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="416db-131">Zostanie wyświetlony pulpit nawigacyjny usługi Advisor.</span><span class="sxs-lookup"><span data-stu-id="416db-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="416db-132">Na pulpicie nawigacyjnym usługi Advisor, kliknij przycisk **wydajności** kartę.</span><span class="sxs-lookup"><span data-stu-id="416db-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="416db-133">Wybierz subskrypcję, dla którego chcesz otrzymywać zalecenia, a następnie kliknij przycisk **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="416db-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="416db-134">Aby uzyskać dostęp do zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor.</span><span class="sxs-lookup"><span data-stu-id="416db-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="416db-135">Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* uruchamia pulpitu nawigacyjnego usługi Advisor i klika pozycję **Uzyskaj zalecenia** przycisk.</span><span class="sxs-lookup"><span data-stu-id="416db-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="416db-136">Jest to *jednorazowa operacja*.</span><span class="sxs-lookup"><span data-stu-id="416db-136">This is a *one-time operation*.</span></span> <span data-ttu-id="416db-137">Po zarejestrowaniu subskrypcji są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* dla określonego zasobu, grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="416db-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="416db-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="416db-138">Next steps</span></span>

<span data-ttu-id="416db-139">Aby dowiedzieć się więcej na temat zalecenia doradcy w zakresie, zobacz:</span><span class="sxs-lookup"><span data-stu-id="416db-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="416db-140">Wprowadzenie do usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="416db-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="416db-141">Wprowadzenie do usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="416db-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="416db-142">Zalecenia doradcy w zakresie koszt</span><span class="sxs-lookup"><span data-stu-id="416db-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="416db-143">Zalecenia doradcy w zakresie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="416db-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="416db-144">Zalecenia doradcy w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="416db-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

