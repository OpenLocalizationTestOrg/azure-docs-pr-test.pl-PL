---
title: "aaaMonitor i zwiększyć wydajność — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Azure SQL Database zapewnia wydajność powitalne narzędzi toohelp identyfikacji obszarów, które może poprawić wydajność kwerend bieżącej."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: a60b75ac-cf27-4d73-8322-ee4d4c448aa2
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2016
ms.author: sstein
ms.openlocfilehash: 84b8a1bc62698a29deb49e765f208bd7e14d0870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-improve-performance"></a><span data-ttu-id="4f37e-103">Monitorowanie i poprawianie wydajności</span><span class="sxs-lookup"><span data-stu-id="4f37e-103">Monitor and improve performance</span></span>
<span data-ttu-id="4f37e-104">Baza danych SQL Azure identyfikuje potencjalne problemy w bazie danych i zalecane akcje, które może poprawić wydajność obciążenia przez podanie inteligentnego akcje dostosowywania i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="4f37e-104">Azure SQL Database identifies potential problems in your database and recommends actions that can improve performance of your workload by providing intelligent tuning actions and recommendations.</span></span>

<span data-ttu-id="4f37e-105">tooreview Twojego wydajność bazy danych, użyj hello **wydajności** kafelka na stronie Przegląd hello lub zbyt przechodzenia "Obsługa + Rozwiązywanie problemów" sekcji:</span><span class="sxs-lookup"><span data-stu-id="4f37e-105">tooreview your database performance, use hello **Performance** tile on hello Overview page, or navigate down too"Support + troubleshooting" section:</span></span>

   ![Widok wydajności](./media/sql-database-performance/entries.png)

<span data-ttu-id="4f37e-107">W sekcji hello "Obsługa + Rozwiązywanie problemów" można użyć hello następujące strony:</span><span class="sxs-lookup"><span data-stu-id="4f37e-107">In hello "Support + troubleshooting" section, you can use hello following pages:</span></span>


1. <span data-ttu-id="4f37e-108">[Omówienie wydajności](#performance-overview) toomonitor wydajność bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4f37e-108">[Performance overview](#performance-overview) toomonitor performance of your database.</span></span> 
2. <span data-ttu-id="4f37e-109">[Zalecenia dotyczące wydajności](#performance-recommendations) toofind zalecenia dotyczące wydajności, które może poprawić wydajność obciążenia.</span><span class="sxs-lookup"><span data-stu-id="4f37e-109">[Performance recommendations](#performance-recommendations) toofind performance recommendations that can improve performance of your workload.</span></span>
3. <span data-ttu-id="4f37e-110">[Szczegółowe informacje o wydajności zapytań](#query-performance-insight) toofind zasobu najwyższego korzystanie z zapytania.</span><span class="sxs-lookup"><span data-stu-id="4f37e-110">[Query Performance Insight](#query-performance-insight) toofind top resource consuming queries.</span></span>
4. <span data-ttu-id="4f37e-111">[Automatycznego dostrajania](#automatic-tuning) toolet bazy danych SQL Azure automatycznie zoptymalizować bazę danych.</span><span class="sxs-lookup"><span data-stu-id="4f37e-111">[Automatic tuning](#automatic-tuning) toolet Azure SQL Database automatically optimize your database.</span></span>

## <a name="performance-overview"></a><span data-ttu-id="4f37e-112">Wydajności — omówienie</span><span class="sxs-lookup"><span data-stu-id="4f37e-112">Performance Overview</span></span>
<span data-ttu-id="4f37e-113">Ten widok zawiera podsumowanie wydajność bazy danych i pomaga wydajności dostrajanie i rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="4f37e-113">This view provides a summary of your database performance, and helps you with performance tuning and troubleshooting.</span></span> 

![Wydajność](./media/sql-database-performance/performance.png)

* <span data-ttu-id="4f37e-115">Witaj **zalecenia** Kafelek zawiera podział dostrajanie zalecenia dotyczące bazy danych (trzy najważniejsze zalecenia są wyświetlane czy więcej).</span><span class="sxs-lookup"><span data-stu-id="4f37e-115">hello **Recommendations** tile provides a breakdown of tuning recommendations for your database (top three recommendations are shown if there are more).</span></span> <span data-ttu-id="4f37e-116">Kliknięcie tego kafelka przejście zbyt**[zaleceń](#performance-recommendations)**.</span><span class="sxs-lookup"><span data-stu-id="4f37e-116">Clicking this tile takes you too**[Performance recommendations](#performance-recommendations)**.</span></span> 
* <span data-ttu-id="4f37e-117">Witaj **dostrajanie działania** kafelka zawiera podsumowanie hello bieżących i zakończonych, dostrajanie akcji dla bazy danych, umożliwiając zapewnia szybki wgląd w historię hello dostrajanie działania.</span><span class="sxs-lookup"><span data-stu-id="4f37e-117">hello **Tuning activity** tile provides a summary of hello ongoing and completed tuning actions for your database, giving you a quick view into hello history of tuning activity.</span></span> <span data-ttu-id="4f37e-118">Kliknięcie tego kafelka przyjmuje toohello pełne, dostrajanie widoku Historia dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4f37e-118">Clicking this tile takes you toohello full tuning history view for your database.</span></span>
* <span data-ttu-id="4f37e-119">Witaj **autostrojenie** kafelka zawiera hello [automatycznego dostrajania konfiguracji](sql-database-automatic-tuning-enable.md) bazy danych (dostrajanie opcje, które są automatycznie stosowane tooyour bazy danych).</span><span class="sxs-lookup"><span data-stu-id="4f37e-119">hello **Auto-tuning** tile shows hello [auto-tuning configuration](sql-database-automatic-tuning-enable.md) for your database (tuning options that are automatically applied tooyour database).</span></span> <span data-ttu-id="4f37e-120">Kliknięcie tego kafelka otwiera okno dialogowe konfiguracji automatyzacji hello.</span><span class="sxs-lookup"><span data-stu-id="4f37e-120">Clicking this tile opens hello automation configuration dialog.</span></span>
* <span data-ttu-id="4f37e-121">Witaj **zapytań bazy danych** kafelka przedstawia hello podsumowanie hello wydajność zapytań dla bazy danych (ogólną jednostek dtu w warstwie użycia i od góry zasobów korzystających z kwerendy).</span><span class="sxs-lookup"><span data-stu-id="4f37e-121">hello **Database queries** tile shows hello summary of hello query performance for your database (overall DTU usage and top resource consuming queries).</span></span> <span data-ttu-id="4f37e-122">Kliknięcie tego kafelka przejście zbyt**[szczegółowe informacje o wydajności zapytań](#query-performance-insight)**.</span><span class="sxs-lookup"><span data-stu-id="4f37e-122">Clicking this tile takes you too**[Query Performance Insight](#query-performance-insight)**.</span></span>

## <a name="performance-recommendations"></a><span data-ttu-id="4f37e-123">Zalecenia dotyczące wydajności</span><span class="sxs-lookup"><span data-stu-id="4f37e-123">Performance recommendations</span></span>
<span data-ttu-id="4f37e-124">Ta strona zawiera inteligentnego [dostrajanie zalecenia](sql-database-advisor.md) które może poprawić wydajność bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4f37e-124">This page provides intelligent [tuning recommendations](sql-database-advisor.md) that can improve your database's performance.</span></span> <span data-ttu-id="4f37e-125">następujące typy zalecenia Hello są wyświetlane na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="4f37e-125">hello following types of recommendations are shown on this page:</span></span>

* <span data-ttu-id="4f37e-126">Zalecenia, na które toocreate indeksy lub Usuń.</span><span class="sxs-lookup"><span data-stu-id="4f37e-126">Recommendations on which indexes toocreate or drop.</span></span>
* <span data-ttu-id="4f37e-127">Zalecenia dotyczące problemów schematu są identyfikowane w hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4f37e-127">Recommendations when schema issues are identified in hello database.</span></span>
* <span data-ttu-id="4f37e-128">Zalecenia dotyczące zapytań mogą korzystać z zapytania parametrycznego.</span><span class="sxs-lookup"><span data-stu-id="4f37e-128">Recommendations when queries can benefit from parameterized queries.</span></span>

![Wydajność](./media/sql-database-performance/recommendations.png)

<span data-ttu-id="4f37e-130">Można również znaleźć dostrajanie akcje, które zostały zastosowane w przeszłości hello pełnej historii.</span><span class="sxs-lookup"><span data-stu-id="4f37e-130">You can also find complete history of tuning actions that were applied in hello past.</span></span>

<span data-ttu-id="4f37e-131">Dowiedz się, jak toofind Zastosuj zalecenia dotyczące wydajności w [Znajdowanie i stosować zalecenia wydajności](sql-database-advisor-portal.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="4f37e-131">Learn how toofind an apply performance recommendations in [Find and apply performance recommendations](sql-database-advisor-portal.md) article.</span></span>

## <a name="automatic-tuning"></a><span data-ttu-id="4f37e-132">Automatyczne dostrajanie</span><span class="sxs-lookup"><span data-stu-id="4f37e-132">Automatic tuning</span></span>
<span data-ttu-id="4f37e-133">Bazy danych SQL Azure mogą automatycznie dostrajania wydajności bazy danych poprzez zastosowanie [zaleceń](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="4f37e-133">Azure SQL Databases can automatically tune database performance by applying [performance recommendations](sql-database-advisor.md).</span></span> <span data-ttu-id="4f37e-134">toolearn, przeczytaj [automatycznego dostrajania artykułu](sql-database-automatic-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="4f37e-134">toolearn more, read [Automatic tuning article](sql-database-automatic-tuning.md).</span></span> <span data-ttu-id="4f37e-135">tooenable, przeczytaj [sposób automatycznego dostrajania tooenable](sql-database-automatic-tuning-enable.md).</span><span class="sxs-lookup"><span data-stu-id="4f37e-135">tooenable it, read [how tooenable automatic tuning](sql-database-automatic-tuning-enable.md).</span></span>

## <a name="query-performance-insight"></a><span data-ttu-id="4f37e-136">Szczegółowe informacje o wydajności zapytań</span><span class="sxs-lookup"><span data-stu-id="4f37e-136">Query Performance Insight</span></span>
<span data-ttu-id="4f37e-137">[Szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) pozwala toospend mniej czasu Rozwiązywanie problemów z wydajnością bazy danych przez zapewnienie:</span><span class="sxs-lookup"><span data-stu-id="4f37e-137">[Query Performance Insight](sql-database-query-performance.md) allows you toospend less time troubleshooting database performance by providing:</span></span>

* <span data-ttu-id="4f37e-138">Bardziej szczegółowe informacje na temat użycia zasobów (bazy danych DTU) bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4f37e-138">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="4f37e-139">Korzystanie z zapytań, które potencjalnie dostrajania dla procesora CPU top Hello wyższą wydajność.</span><span class="sxs-lookup"><span data-stu-id="4f37e-139">hello top CPU consuming queries, which can potentially be tuned for improved performance.</span></span> 
* <span data-ttu-id="4f37e-140">Witaj toodrill możliwości w dół do szczegółów hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="4f37e-140">hello ability toodrill down into hello details of a query.</span></span> 

  ![pulpit nawigacyjny wydajności](./media/sql-database-query-performance/performance.png)

<span data-ttu-id="4f37e-142">Więcej informacji dotyczących tej strony można znaleźć w artykule hello  **[jak toouse szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md)**.</span><span class="sxs-lookup"><span data-stu-id="4f37e-142">Find more information about this page in hello article **[How toouse Query Performance Insight](sql-database-query-performance.md)**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4f37e-143">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4f37e-143">Additional resources</span></span>
* [<span data-ttu-id="4f37e-144">Azure wytyczne dotyczące wydajności bazy danych SQL dla pojedynczych baz danych</span><span class="sxs-lookup"><span data-stu-id="4f37e-144">Azure SQL Database performance guidance for single databases</span></span>](sql-database-performance-guidance.md)
* [<span data-ttu-id="4f37e-145">Kiedy należy użyć puli elastycznej?</span><span class="sxs-lookup"><span data-stu-id="4f37e-145">When should an elastic pool be used?</span></span>](sql-database-elastic-pool-guidance.md)

