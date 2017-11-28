---
title: "Utwórz niestandardowy pulpit nawigacyjny w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Ten przewodnik pomaga zrozumieć, jak pulpity nawigacyjne analizy dzienników można Wizualizuj wszystkie dziennika zapisanych wyszukiwań, umożliwiając pojedynczego obiektyw, aby wyświetlić środowiska."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a90d9c620221bffbb225fb060b997af2f5e90390
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="d33dc-103">Utwórz niestandardowy pulpit nawigacyjny do użycia w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="d33dc-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="d33dc-104">Jeśli obszaru roboczego został uaktualniony do [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie nie można utworzyć nowe pulpity nawigacyjne lub edytowanie istniejących pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d33dc-104">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="d33dc-105">Ten przewodnik pomaga zrozumieć, jak pulpity nawigacyjne analizy dzienników można Wizualizuj wszystkie dziennika zapisanych wyszukiwań, umożliwiając pojedynczego obiektyw, aby wyświetlić środowiska.</span><span class="sxs-lookup"><span data-stu-id="d33dc-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens to view your environment.</span></span>

![Przykład pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="d33dc-107">Wszystkie niestandardowe pulpity nawigacyjne utworzone w portalu OMS są także dostępne w aplikacji mobilnej OMS.</span><span class="sxs-lookup"><span data-stu-id="d33dc-107">All the custom dashboards that you create in the OMS portal are also available in the OMS Mobile App.</span></span> <span data-ttu-id="d33dc-108">Zobacz następujące strony, aby uzyskać więcej informacji o aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="d33dc-108">See the following pages for more information about the apps.</span></span>

* [<span data-ttu-id="d33dc-109">OMS aplikacji mobilnej z Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="d33dc-109">OMS mobile app from the Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="d33dc-110">OMS aplikacji mobilnej z iTunes firmy Apple</span><span class="sxs-lookup"><span data-stu-id="d33dc-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobilnego pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="d33dc-112">Jak utworzyć mój pulpit nawigacyjny?</span><span class="sxs-lookup"><span data-stu-id="d33dc-112">How do I create my dashboard?</span></span>
<span data-ttu-id="d33dc-113">Aby rozpocząć, przejdź do strony Przegląd OMS.</span><span class="sxs-lookup"><span data-stu-id="d33dc-113">To begin, go to the OMS Overview page.</span></span> <span data-ttu-id="d33dc-114">Zobaczysz **Mój pulpit nawigacyjny** kafelka po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d33dc-114">You'll see the **My Dashboard** tile on the left.</span></span> <span data-ttu-id="d33dc-115">Kliknij go, aby przejść do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d33dc-115">Click it to drill down into your dashboard.</span></span>

![Omówienie](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="d33dc-117">Dodawanie kafelka</span><span class="sxs-lookup"><span data-stu-id="d33dc-117">Adding a tile</span></span>
<span data-ttu-id="d33dc-118">W pulpitach nawigacyjnych Kafelki są obsługiwane przez zapisany dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="d33dc-119">OMS zawiera wiele wstępnie wprowadzone zapisany dziennik wyszukiwania, dzięki czemu będzie można od razu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="d33dc-120">Wykonaj następujące kroki, które przedstawiają sposób rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="d33dc-120">Use the following steps that outline how to begin.</span></span>

<span data-ttu-id="d33dc-121">W widoku Mój pulpit nawigacyjny, wystarczy kliknąć **Dostosuj** wprowadzenia trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-121">In the My Dashboard view, simply click **Customize** to enter customize mode.</span></span>

![Obrazkami](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="d33dc-123">Panel, który zostanie otwarty w prawej części strony są wyświetlane wszystkie obszaru roboczego zapisany dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-123">The panel that opens on the right side of the page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="d33dc-124">Do wizualizacji wyszukiwania zapisany dziennik jako Kafelek, umieść kursor nad zapisanego kryterium wyszukiwania, a następnie kliknij przycisk **plus** symbolu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-124">To visualize a saved log search as a tile,  hover over a saved search and then click the **plus** symbol.</span></span>

![Dodaj Kafelki 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="d33dc-126">Po kliknięciu **plus** symboli, fragment pojawia się w widoku Mój pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="d33dc-126">When you click the **plus** symbol, a new tile appears in the My Dashboard view.</span></span>

![Dodaj Kafelki 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="d33dc-128">Edytowanie kafelka</span><span class="sxs-lookup"><span data-stu-id="d33dc-128">Edit a tile</span></span>
<span data-ttu-id="d33dc-129">W widoku Mój pulpit nawigacyjny, wystarczy kliknąć **Dostosuj** wprowadzenia trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-129">In the My Dashboard view, simply click  **Customize** to enter customize mode.</span></span> <span data-ttu-id="d33dc-130">Kliknij Kafelek, który chcesz edytować.</span><span class="sxs-lookup"><span data-stu-id="d33dc-130">Click the tile you want to edit.</span></span> <span data-ttu-id="d33dc-131">Zmiany prawym panelu, aby edytować i umożliwia wybranie opcji:</span><span class="sxs-lookup"><span data-stu-id="d33dc-131">The right panel changes to edit, and gives a selection of options:</span></span>

![Edytowanie kafelka](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Edytowanie kafelka](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="d33dc-134">Wizualizacje kafelka</span><span class="sxs-lookup"><span data-stu-id="d33dc-134">Tile visualizations</span></span>
<span data-ttu-id="d33dc-135">Istnieją trzy rodzaje wizualizacje kafelka do wyboru:</span><span class="sxs-lookup"><span data-stu-id="d33dc-135">There are three kinds of tile visualizations to choose from:</span></span>

| <span data-ttu-id="d33dc-136">Typ wykresu</span><span class="sxs-lookup"><span data-stu-id="d33dc-136">chart type</span></span> | <span data-ttu-id="d33dc-137">jaką pełni funkcję</span><span class="sxs-lookup"><span data-stu-id="d33dc-137">what it does</span></span> |
| --- | --- |
| ![Wykres słupkowy](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="d33dc-139">Wyświetla oś czasu wyników wyszukiwania zapisany dziennik jako wykres słupkowy lub lista wyników według pola w zależności od, jeśli wyszukiwanie dziennika agreguje wyniki według pola, czy nie.</span><span class="sxs-lookup"><span data-stu-id="d33dc-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![Metryka](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="d33dc-141">Wyświetla trafień wynik wyszukiwania z całkowitej dziennika jako liczby na kafelku.</span><span class="sxs-lookup"><span data-stu-id="d33dc-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="d33dc-142">Metryki kafelków umożliwiają ustawienie progu wyróżniane kafelka, po osiągnięciu progu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-142">Metric tiles allow you to set a threshold that will highlight the tile when the threshold is reached.</span></span> |
| ![wiersz](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="d33dc-144">Wyświetla wykres liniowy osi czasu z zapisany dziennik wyszukiwania wynik trafień wartościami.</span><span class="sxs-lookup"><span data-stu-id="d33dc-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="d33dc-145">Próg</span><span class="sxs-lookup"><span data-stu-id="d33dc-145">Threshold</span></span>
<span data-ttu-id="d33dc-146">Próg można utworzyć na kafelku, za pomocą metryki wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="d33dc-146">You can create a threshold on a tile using the Metric visualization.</span></span> <span data-ttu-id="d33dc-147">Wybierz na, aby utworzyć wartość progową na kafelku.</span><span class="sxs-lookup"><span data-stu-id="d33dc-147">Select on to create a threshold value on the tile.</span></span> <span data-ttu-id="d33dc-148">Wybierz opcję podświetlania kafelka, gdy wartość jest powyżej lub poniżej wybrany próg, a następnie ustaw poniżej wartości progowej.</span><span class="sxs-lookup"><span data-stu-id="d33dc-148">Choose whether to highlight the tile when the value is over or under the chosen threshold, then set the threshold value below.</span></span>

## <a name="organizing-the-dashboard"></a><span data-ttu-id="d33dc-149">Organizowanie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="d33dc-149">Organizing the dashboard</span></span>
<span data-ttu-id="d33dc-150">Aby zorganizować pulpitu nawigacyjnego, przejdź do widoku Mój pulpit nawigacyjny, a następnie kliknij przycisk **Dostosuj** wprowadzenia trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-150">To organize your dashboard, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="d33dc-151">Kliknij i przeciągnij Kafelek, który chcesz przenieść, a następnie przenieś go do której ma być kafelka.</span><span class="sxs-lookup"><span data-stu-id="d33dc-151">Click and drag the tile you want to move, and move it to where you want your tile to be.</span></span>

![Organizowanie pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="d33dc-153">Usuń Kafelek</span><span class="sxs-lookup"><span data-stu-id="d33dc-153">Remove a tile</span></span>
<span data-ttu-id="d33dc-154">Aby usunąć kafelka, przejdź do widoku Mój pulpit nawigacyjny, a następnie kliknij przycisk **Dostosuj** wprowadzenia trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-154">To remove a tile, navigate to the My Dashboard view and click **Customize** to enter customize mode.</span></span> <span data-ttu-id="d33dc-155">Wybierz Kafelek, który chcesz usunąć, a następnie w prawym okienku wybierz **usunąć kafelka**.</span><span class="sxs-lookup"><span data-stu-id="d33dc-155">Select the tile you want to remove, then on the right panel select **Remove Tile**.</span></span>

![Usuń Kafelek](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="d33dc-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d33dc-157">Next steps</span></span>
* <span data-ttu-id="d33dc-158">Utwórz [alerty](log-analytics-alerts.md) w analizy dzienników, aby generować powiadomienia i Korygowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="d33dc-158">Create [alerts](log-analytics-alerts.md) in Log Analytics to generate notifications and to remediate problems.</span></span>
