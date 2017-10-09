---
title: "wydajność aaaTroubleshoot problemy i zoptymalizować bazę danych | Dokumentacja firmy Microsoft"
description: "Zastosuj tooyour zalecenia dotyczące wydajności bazy danych SQL, a także czyść jak wgląd w toogain hello wydajność kwerend hello uruchamiania bazy danych"
metakeywords: azure sql database performance monitoring recommendation
services: sql-database
documentationcenter: 
manager: jhubbard
author: jan-eng
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,monitor & tune
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: janeng
ms.openlocfilehash: e948d30ac74eecf45420d5d77ef55e3c0b6f3f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-performance-issues-and-optimize-your-database"></a><span data-ttu-id="df5db-103">Rozwiązywanie problemów z wydajnością i zoptymalizować bazę danych</span><span class="sxs-lookup"><span data-stu-id="df5db-103">Troubleshoot performance issues and optimize your database</span></span>

<span data-ttu-id="df5db-104">Częstymi przyczynami słabej wydajności bazy danych są brakujące indeksy i nieprawidłowo zoptymalizowane zapytania.</span><span class="sxs-lookup"><span data-stu-id="df5db-104">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="df5db-105">W tym samouczku dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="df5db-105">In this tutorial you learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="df5db-106">Przejrzyj i Zastosuj przywrócić zalecenia dotyczące poprawy wydajności</span><span class="sxs-lookup"><span data-stu-id="df5db-106">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="df5db-107">Znajdź zapytania z wykorzystania zasobów wysoka</span><span class="sxs-lookup"><span data-stu-id="df5db-107">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="df5db-108">Znajdź zapytania długo działające</span><span class="sxs-lookup"><span data-stu-id="df5db-108">Find long running queries</span></span>

> <span data-ttu-id="df5db-109">Należy ciągłe obciążenie bazy danych z problemów z wydajnością — Brak indeksu na przykład tooreceive zalecenia.</span><span class="sxs-lookup"><span data-stu-id="df5db-109">You need a continuous workload on a database with performance issues – missing an index for example tooreceive a recommendation.</span></span>
>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="df5db-110">Zaloguj się za toohello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="df5db-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="df5db-111">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="df5db-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="review-and-apply-a-recommendation"></a><span data-ttu-id="df5db-112">Przejrzyj i Zastosuj zalecenia</span><span class="sxs-lookup"><span data-stu-id="df5db-112">Review and apply a recommendation</span></span>

<span data-ttu-id="df5db-113">Wykonaj te kroki tooapply zalecenie z systemu hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="df5db-113">Follow these steps tooapply a recommendation from hello system for your database:</span></span>

1. <span data-ttu-id="df5db-114">Kliknij przycisk hello **zaleceń** w bloku bazy danych hello menu.</span><span class="sxs-lookup"><span data-stu-id="df5db-114">Click hello **Performance recommendations** menu in hello database blade.</span></span>

    ![zalecenie dotyczące wydajności](./media/sql-database-performance-tutorial/perf_recommendations.png)

2. <span data-ttu-id="df5db-116">Z listy hello zalecenia wybierz active zalecenia.</span><span class="sxs-lookup"><span data-stu-id="df5db-116">From hello list of recommendations, select an active recommendation.</span></span> <span data-ttu-id="df5db-117">W tym przykładzie Create Index.</span><span class="sxs-lookup"><span data-stu-id="df5db-117">In this example, Create Index.</span></span>

    ![Wybierz zalecenia](./media/sql-database-performance-tutorial/create_index.png)

3. <span data-ttu-id="df5db-119">Zastosuj hello zalecenie, klikając hello **Zastosuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="df5db-119">Apply hello recommendation by clicking hello **Apply** button.</span></span> <span data-ttu-id="df5db-120">Opcjonalnie, przejrzyj szczegóły zalecenia hello i zawiera skrypt hello T-SQL zbyt można wykonać, klikając **Wyświetl skrypt** przycisku.</span><span class="sxs-lookup"><span data-stu-id="df5db-120">Optionally, review hello recommendation details and see hello T-SQL script too be executed by clicking on **View Script** button.</span></span>

    ![Zastosuj zalecenia](./media/sql-database-performance-tutorial/apply.png)

4. <span data-ttu-id="df5db-122">[Opcjonalnie] Włączanie automatycznego dostrajania dla toobe zalecenia stosowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="df5db-122">[Optional] Enable automatic tuning for recommendations toobe applied automatically.</span></span>

    ![automatycznego dostrajania](./media/sql-database-performance-tutorial/auto_tuning.png)

## <a name="revert-a-recommendation"></a><span data-ttu-id="df5db-124">Przywróć zalecenia</span><span class="sxs-lookup"><span data-stu-id="df5db-124">Revert a recommendation</span></span>

<span data-ttu-id="df5db-125">Witaj doradcy bazy danych monitoruje każdy zalecenie zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="df5db-125">hello Database Advisor monitors every recommendation implemented.</span></span> <span data-ttu-id="df5db-126">Jeśli zalecenia nie poprawi obciążenia hello zostanie automatycznie przywrócony.</span><span class="sxs-lookup"><span data-stu-id="df5db-126">If a recommendation doesn't improve hello workload it will be automatically reverted.</span></span> <span data-ttu-id="df5db-127">Ręczne przywracanie zalecenie jest możliwe, ale nie jest konieczna w większości przypadków.</span><span class="sxs-lookup"><span data-stu-id="df5db-127">Manually reverting a recommendation is possible, but not necessary in most cases.</span></span> <span data-ttu-id="df5db-128">toorevert zalecenia:</span><span class="sxs-lookup"><span data-stu-id="df5db-128">toorevert a recommendation:</span></span>

1. <span data-ttu-id="df5db-129">Przejdź do menu zalecenia dotyczące wydajności toohello i wybierz jedną z hello stosowane zalecenia.</span><span class="sxs-lookup"><span data-stu-id="df5db-129">Go toohello performance recommendations menu and select one of hello applied recommendations.</span></span>

    ![Wybierz zalecenia](./media/sql-database-performance-tutorial/select.png)

2. <span data-ttu-id="df5db-131">W widoku szczegółów powitania kliknij **Przywróć**.</span><span class="sxs-lookup"><span data-stu-id="df5db-131">In hello details view, click **Revert**.</span></span>

    ![Przywróć zalecenia](./media/sql-database-performance-tutorial/revert.png)

## <a name="find-hello-query-that-consumes-hello-most-resources"></a><span data-ttu-id="df5db-133">Znajdź zapytania hello, który wykorzystuje hello najwięcej zasobów</span><span class="sxs-lookup"><span data-stu-id="df5db-133">Find hello query that consumes hello most resources</span></span>

<span data-ttu-id="df5db-134">Wykonaj te kroki toofind hello zapytania zużywające hello najwięcej zasobów:</span><span class="sxs-lookup"><span data-stu-id="df5db-134">Follow these steps toofind hello query consuming hello most resources:</span></span>

1. <span data-ttu-id="df5db-135">Polecenie hello **szczegółowe informacje o wydajności zapytań** w bloku bazy danych hello menu.</span><span class="sxs-lookup"><span data-stu-id="df5db-135">Click on hello **Query Performance Insight** menu in hello database blade.</span></span>

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/query_perf_insights.png)

2. <span data-ttu-id="df5db-137">Wybierz typ zasobu.</span><span class="sxs-lookup"><span data-stu-id="df5db-137">Select a resource type.</span></span>

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/select_resource_type.png)

3. <span data-ttu-id="df5db-139">Wybierz hello pierwszego zapytania w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="df5db-139">Select hello first query in hello table.</span></span>

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/select_query.png)

4. <span data-ttu-id="df5db-141">Przejrzyj szczegóły zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="df5db-141">Review hello query details.</span></span>

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/query_details.png)

## <a name="find-hello-longest-running-query"></a><span data-ttu-id="df5db-143">Znajdź hello najdłuższym uruchomione zapytania</span><span class="sxs-lookup"><span data-stu-id="df5db-143">Find hello longest running query</span></span>

1. <span data-ttu-id="df5db-144">Przejdź tooQuery szczegółowe informacje o wydajności i wybierz hello **długo działające kwerendy** kartę.</span><span class="sxs-lookup"><span data-stu-id="df5db-144">Go tooQuery Performance Insight and select hello **Long running queries** tab.</span></span>

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/long_running.png)

3. <span data-ttu-id="df5db-146">Wybierz hello pierwszego zapytania w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="df5db-146">Select hello first query in hello table.</span></span>

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/select_first_query.png)

4. <span data-ttu-id="df5db-148">Przejrzyj szczegóły zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="df5db-148">Review hello query details.</span></span>

    ![szczegółowe informacje o zapytań](./media/sql-database-performance-tutorial/review_query_details.png)



## <a name="next-steps"></a><span data-ttu-id="df5db-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df5db-150">Next steps</span></span> 
<span data-ttu-id="df5db-151">Częstymi przyczynami słabej wydajności bazy danych są brakujące indeksy i nieprawidłowo zoptymalizowane zapytania.</span><span class="sxs-lookup"><span data-stu-id="df5db-151">Missing indexes and poorly optimized queries are common reasons for poor database performance.</span></span> <span data-ttu-id="df5db-152">W tym samouczku przedstawiono do:</span><span class="sxs-lookup"><span data-stu-id="df5db-152">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="df5db-153">Przejrzyj i Zastosuj przywrócić zalecenia dotyczące poprawy wydajności</span><span class="sxs-lookup"><span data-stu-id="df5db-153">Review, apply and revert performance improvement recommendations</span></span>
> * <span data-ttu-id="df5db-154">Znajdź zapytania z wykorzystania zasobów wysoka</span><span class="sxs-lookup"><span data-stu-id="df5db-154">Find queries with high resource utilization</span></span>
> * <span data-ttu-id="df5db-155">Znajdź zapytania długo działające</span><span class="sxs-lookup"><span data-stu-id="df5db-155">Find long running queries</span></span>

[<span data-ttu-id="df5db-156">Wskazówki dotyczące dostrajania wydajności bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="df5db-156">SQL Database performance tuning tips</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-performance)
