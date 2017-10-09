---
title: aaaCreate niestandardowy pulpit nawigacyjny w Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Ten przewodnik pomaga zrozumieć, jak pulpity nawigacyjne analizy dzienników można Wizualizuj wszystkie dziennika zapisanych wyszukiwań, umożliwiając pojedynczy obiektywu tooview środowiska."
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
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a><span data-ttu-id="5f61e-103">Utwórz niestandardowy pulpit nawigacyjny do użycia w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="5f61e-103">Create a custom dashboard for use in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="5f61e-104">Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie nie można utworzyć nowe pulpity nawigacyjne lub edytowanie istniejących pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="5f61e-104">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you cannot create new dashboards or edit existing dashboards.</span></span> 

<span data-ttu-id="5f61e-105">Ten przewodnik pomaga zrozumieć, jak pulpity nawigacyjne analizy dzienników można Wizualizuj wszystkie dziennika zapisanych wyszukiwań, umożliwiając pojedynczy obiektywu tooview środowiska.</span><span class="sxs-lookup"><span data-stu-id="5f61e-105">This guide helps you understand how Log Analytics dashboards can visualize all of your saved log searches, giving you a single lens tooview your environment.</span></span>

![Przykład pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

<span data-ttu-id="5f61e-107">Wszystkie hello niestandardowych pulpitów nawigacyjnych utworzonych w portalu OMS hello są także dostępne w hello OMS aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="5f61e-107">All hello custom dashboards that you create in hello OMS portal are also available in hello OMS Mobile App.</span></span> <span data-ttu-id="5f61e-108">Zobacz następujące strony, aby uzyskać więcej informacji na temat aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="5f61e-108">See hello following pages for more information about hello apps.</span></span>

* [<span data-ttu-id="5f61e-109">OMS aplikacji mobilnej z hello Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="5f61e-109">OMS mobile app from hello Microsoft Store</span></span>](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [<span data-ttu-id="5f61e-110">OMS aplikacji mobilnej z iTunes firmy Apple</span><span class="sxs-lookup"><span data-stu-id="5f61e-110">OMS mobile app from Apple iTunes</span></span>](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobilnego pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a><span data-ttu-id="5f61e-112">Jak utworzyć mój pulpit nawigacyjny?</span><span class="sxs-lookup"><span data-stu-id="5f61e-112">How do I create my dashboard?</span></span>
<span data-ttu-id="5f61e-113">toobegin, przejdź toohello strony Przegląd OMS.</span><span class="sxs-lookup"><span data-stu-id="5f61e-113">toobegin, go toohello OMS Overview page.</span></span> <span data-ttu-id="5f61e-114">Zobaczysz hello **Mój pulpit nawigacyjny** kafelka powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="5f61e-114">You'll see hello **My Dashboard** tile on hello left.</span></span> <span data-ttu-id="5f61e-115">Kliknij go, toodrill w dół do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5f61e-115">Click it toodrill down into your dashboard.</span></span>

![Omówienie](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a><span data-ttu-id="5f61e-117">Dodawanie kafelka</span><span class="sxs-lookup"><span data-stu-id="5f61e-117">Adding a tile</span></span>
<span data-ttu-id="5f61e-118">W pulpitach nawigacyjnych Kafelki są obsługiwane przez zapisany dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="5f61e-118">In dashboards, tiles are powered by your saved log searches.</span></span> <span data-ttu-id="5f61e-119">OMS zawiera wiele wstępnie wprowadzone zapisany dziennik wyszukiwania, dzięki czemu będzie można od razu.</span><span class="sxs-lookup"><span data-stu-id="5f61e-119">OMS comes with many pre-made saved log searches, so you can begin right away.</span></span> <span data-ttu-id="5f61e-120">Użyj następujących hello kroki konspektu jak toobegin.</span><span class="sxs-lookup"><span data-stu-id="5f61e-120">Use hello following steps that outline how toobegin.</span></span>

<span data-ttu-id="5f61e-121">W widoku pulpitu nawigacyjnego Moje hello, wystarczy kliknąć **Dostosuj** tooenter trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="5f61e-121">In hello My Dashboard view, simply click **Customize** tooenter customize mode.</span></span>

![Obrazkami](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 <span data-ttu-id="5f61e-123">panel Hello, który zostanie otwarty po prawej stronie powitania hello strony są wyświetlane wszystkie obszaru roboczego zapisany dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="5f61e-123">hello panel that opens on hello right side of hello page shows all of your workspace's saved log searches.</span></span> <span data-ttu-id="5f61e-124">toovisualize zapisany dziennik wyszukiwania jako Kafelek, umieść kursor nad zapisanego kryterium wyszukiwania, a następnie kliknij przycisk hello **plus** symbolu.</span><span class="sxs-lookup"><span data-stu-id="5f61e-124">toovisualize a saved log search as a tile,  hover over a saved search and then click hello **plus** symbol.</span></span>

![Dodaj Kafelki 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

<span data-ttu-id="5f61e-126">Po kliknięciu hello **plus** symboli, fragment pojawia się w hello Wyświetl mój pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="5f61e-126">When you click hello **plus** symbol, a new tile appears in hello My Dashboard view.</span></span>

![Dodaj Kafelki 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a><span data-ttu-id="5f61e-128">Edytowanie kafelka</span><span class="sxs-lookup"><span data-stu-id="5f61e-128">Edit a tile</span></span>
<span data-ttu-id="5f61e-129">W widoku pulpitu nawigacyjnego Moje hello, wystarczy kliknąć **Dostosuj** tooenter trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="5f61e-129">In hello My Dashboard view, simply click  **Customize** tooenter customize mode.</span></span> <span data-ttu-id="5f61e-130">Kliknij Kafelek hello ma tooedit.</span><span class="sxs-lookup"><span data-stu-id="5f61e-130">Click hello tile you want tooedit.</span></span> <span data-ttu-id="5f61e-131">Prawy panel Hello zmiany tooedit i umożliwia wybranie opcji:</span><span class="sxs-lookup"><span data-stu-id="5f61e-131">hello right panel changes tooedit, and gives a selection of options:</span></span>

![Edytowanie kafelka](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Edytowanie kafelka](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a><span data-ttu-id="5f61e-134">Wizualizacje kafelka</span><span class="sxs-lookup"><span data-stu-id="5f61e-134">Tile visualizations</span></span>
<span data-ttu-id="5f61e-135">Istnieją trzy rodzaje toochoose wizualizacje kafelka z:</span><span class="sxs-lookup"><span data-stu-id="5f61e-135">There are three kinds of tile visualizations toochoose from:</span></span>

| <span data-ttu-id="5f61e-136">Typ wykresu</span><span class="sxs-lookup"><span data-stu-id="5f61e-136">chart type</span></span> | <span data-ttu-id="5f61e-137">jaką pełni funkcję</span><span class="sxs-lookup"><span data-stu-id="5f61e-137">what it does</span></span> |
| --- | --- |
| ![Wykres słupkowy](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |<span data-ttu-id="5f61e-139">Wyświetla oś czasu wyników wyszukiwania zapisany dziennik jako wykres słupkowy lub lista wyników według pola w zależności od, jeśli wyszukiwanie dziennika agreguje wyniki według pola, czy nie.</span><span class="sxs-lookup"><span data-stu-id="5f61e-139">Displays a timeline of your saved log search's results as a bar chart, or a list of results by a field depending on if your log search aggregates results by a field or not.</span></span> |
| ![Metryka](./media/log-analytics-dashboards/oms-dashboards-metric.png) |<span data-ttu-id="5f61e-141">Wyświetla trafień wynik wyszukiwania z całkowitej dziennika jako liczby na kafelku.</span><span class="sxs-lookup"><span data-stu-id="5f61e-141">Displays your total log search result hits as a number in a tile.</span></span> <span data-ttu-id="5f61e-142">Kafelki metryki pozwalają tooset wyróżnione kafelka powitania po osiągnięciu progu powitania od wartości progowej.</span><span class="sxs-lookup"><span data-stu-id="5f61e-142">Metric tiles allow you tooset a threshold that will highlight hello tile when hello threshold is reached.</span></span> |
| ![wiersz](./media/log-analytics-dashboards/oms-dashboards-line.png) |<span data-ttu-id="5f61e-144">Wyświetla wykres liniowy osi czasu z zapisany dziennik wyszukiwania wynik trafień wartościami.</span><span class="sxs-lookup"><span data-stu-id="5f61e-144">Displays a timeline of your saved log search result hits with values as a line chart.</span></span> |

### <a name="threshold"></a><span data-ttu-id="5f61e-145">Próg</span><span class="sxs-lookup"><span data-stu-id="5f61e-145">Threshold</span></span>
<span data-ttu-id="5f61e-146">Na kafelku, za pomocą wizualizacji metryki hello można utworzyć progu.</span><span class="sxs-lookup"><span data-stu-id="5f61e-146">You can create a threshold on a tile using hello Metric visualization.</span></span> <span data-ttu-id="5f61e-147">Wybierz na toocreate na kafelku hello wartość progową.</span><span class="sxs-lookup"><span data-stu-id="5f61e-147">Select on toocreate a threshold value on hello tile.</span></span> <span data-ttu-id="5f61e-148">Wybierz, czy toohighlight hello kafelka, gdy wartość hello jest powyżej lub poniżej progu hello wybrany następnie ustaw wartość progowa hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="5f61e-148">Choose whether toohighlight hello tile when hello value is over or under hello chosen threshold, then set hello threshold value below.</span></span>

## <a name="organizing-hello-dashboard"></a><span data-ttu-id="5f61e-149">Organizowanie hello pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="5f61e-149">Organizing hello dashboard</span></span>
<span data-ttu-id="5f61e-150">tooorganize pulpitu nawigacyjnego Przejdź toohello Wyświetl mój pulpit nawigacyjny i kliknij **Dostosuj** tooenter trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="5f61e-150">tooorganize your dashboard, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="5f61e-151">Kliknij i przeciągnij Kafelek hello toomove, a następnie przenieś go toowhere ma toobe Twojego kafelka.</span><span class="sxs-lookup"><span data-stu-id="5f61e-151">Click and drag hello tile you want toomove, and move it toowhere you want your tile toobe.</span></span>

![Organizowanie pulpitu nawigacyjnego](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a><span data-ttu-id="5f61e-153">Usuń Kafelek</span><span class="sxs-lookup"><span data-stu-id="5f61e-153">Remove a tile</span></span>
<span data-ttu-id="5f61e-154">tooremove kafelka, przejdź do widoku pulpitu nawigacyjnego Moje toohello i kliknij przycisk **Dostosuj** tooenter trybu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="5f61e-154">tooremove a tile, navigate toohello My Dashboard view and click **Customize** tooenter customize mode.</span></span> <span data-ttu-id="5f61e-155">Wybierz hello kafelka tooremove, a następnie w prawym panelu hello wybierz **usunąć kafelka**.</span><span class="sxs-lookup"><span data-stu-id="5f61e-155">Select hello tile you want tooremove, then on hello right panel select **Remove Tile**.</span></span>

![Usuń Kafelek](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a><span data-ttu-id="5f61e-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f61e-157">Next steps</span></span>
* <span data-ttu-id="5f61e-158">Utwórz [alerty](log-analytics-alerts.md) w powiadomieniach toogenerate analizy dzienników i tooremediate problemów.</span><span class="sxs-lookup"><span data-stu-id="5f61e-158">Create [alerts](log-analytics-alerts.md) in Log Analytics toogenerate notifications and tooremediate problems.</span></span>
