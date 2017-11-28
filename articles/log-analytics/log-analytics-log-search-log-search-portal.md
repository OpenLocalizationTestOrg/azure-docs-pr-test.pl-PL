---
title: "Za pomocą portalu wyszukiwania dziennika w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera samouczek, który opisuje sposób tworzenia dziennik wyszukiwania i analizowania danych przechowywanych w obszarze roboczym analizy dzienników przy użyciu portalu wyszukiwania dziennika.  Samouczek obejmuje uruchamiania niektórych zapytań proste być zwracanie różnych typów danych i analiza wyników."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="43789-104">Tworzenie wyszukiwań dziennika w Analiza dzienników Azure przy użyciu portalu wyszukiwania dziennika</span><span class="sxs-lookup"><span data-stu-id="43789-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="43789-105">W tym artykule opisano portalu wyszukiwania dziennika w przy użyciu nowego języka zapytań usługi Analiza dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="43789-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="43789-106">Możesz dowiedzieć się więcej o nowy język i uzyskać Procedura uaktualniania obszaru roboczego na [uaktualnienia obszaru roboczego analizy dzienników Azure do nowego wyszukiwania dziennika](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="43789-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="43789-107">Jeśli nowy język kwerendy nie została ona uaktualniona obszaru roboczego, należy zapoznać się [wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników](log-analytics-log-searches.md) Aby uzyskać informacje o bieżącej wersji portalu wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="43789-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="43789-108">Ten artykuł zawiera samouczek, który opisuje sposób tworzenia dziennik wyszukiwania i analizowania danych przechowywanych w obszarze roboczym analizy dzienników przy użyciu portalu wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="43789-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="43789-109">Samouczek obejmuje uruchamiania niektórych zapytań proste być zwracanie różnych typów danych i analiza wyników.</span><span class="sxs-lookup"><span data-stu-id="43789-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="43789-110">Głównie funkcji w portalu wyszukiwania dziennika modyfikowania zapytania, a nie ich modyfikować.</span><span class="sxs-lookup"><span data-stu-id="43789-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="43789-111">Aby uzyskać więcej informacji dotyczących bezpośredniego edytowania zapytania, zobacz [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="43789-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="43789-112">Aby utworzyć wyszukiwania w portalu analityka zaawansowane zamiast portalu wyszukiwania dziennika, zobacz [wprowadzenie do korzystania z portalu usługi analiza](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="43789-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="43789-113">Obu portalach używany ten sam język kwerendy można uzyskać dostępu do tych samych danych, w obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43789-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43789-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="43789-114">Prerequisites</span></span>
<span data-ttu-id="43789-115">Ten samouczek zakłada, że masz już obszar roboczy analizy dzienników z co najmniej jedno źródło połączonych, który generuje dane dla zapytań do analizowania.</span><span class="sxs-lookup"><span data-stu-id="43789-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="43789-116">Jeśli nie masz obszaru roboczego, możesz utworzyć bezpłatne przy użyciu procedury na [Rozpoczynanie pracy z obszaru roboczego analizy dzienników](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="43789-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="43789-117">Co najmniej jednego połączenia [agenta Windows](log-analytics-windows-agents.md) lub [agenta systemu Linux](log-analytics-linux-agents.md) do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="43789-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="43789-118">Otwórz portal wyszukiwania dziennika</span><span class="sxs-lookup"><span data-stu-id="43789-118">Open the Log Search portal</span></span>
<span data-ttu-id="43789-119">Uruchom, otwierając portal wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="43789-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="43789-120">Można do niego dostęp w portalu Azure lub w portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="43789-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="43789-121">Otwórz Azure portal.</span><span class="sxs-lookup"><span data-stu-id="43789-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="43789-122">Przejdź do analizy dzienników i wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="43789-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="43789-123">Wybierz opcję **wyszukiwania dziennika** pozostanie w portalu Azure, czy portalu OMS wybierając **portalu OMS** , a następnie klikając przycisk wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="43789-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![Przycisk wyszukiwania dziennika](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="43789-125">Tworzenie prostego wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="43789-125">Create a simple search</span></span>
<span data-ttu-id="43789-126">Najszybszy sposób pobrać niektórych danych do pracy z jest proste zapytanie zwracające wszystkie rekordy w tabeli.</span><span class="sxs-lookup"><span data-stu-id="43789-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="43789-127">Jeśli masz połączone żadnych klientów z systemem Windows lub Linux do swojego obszaru roboczego, a następnie należy dane zdarzenie (system Windows) lub w tabeli dziennika systemowego (Linux).</span><span class="sxs-lookup"><span data-stu-id="43789-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="43789-128">Wpisz jedno następujące kwerendy w polu wyszukiwania, a następnie kliknij przycisk wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="43789-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="43789-129">Dane są zwracane w domyślny widok listy, a widać, ile całkowita liczba rekordów zostały zwrócone.</span><span class="sxs-lookup"><span data-stu-id="43789-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Prostego zapytania](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="43789-131">Wyświetlane są tylko pierwszy kilka właściwości każdego rekordu.</span><span class="sxs-lookup"><span data-stu-id="43789-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="43789-132">Kliknij przycisk **Pokaż więcej** do wyświetlenia wszystkich właściwości dla określonego rekordu.</span><span class="sxs-lookup"><span data-stu-id="43789-132">Click **show more** to display all properties for a particular record.</span></span>

![Szczegóły rekordu](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="43789-134">Ustaw zakres czasu</span><span class="sxs-lookup"><span data-stu-id="43789-134">Set the time scope</span></span>
<span data-ttu-id="43789-135">Każdy rekord zebrane przez analizy dzienników ma **TimeGenerated** właściwość, która zawiera Data i godzina utworzenia rekordu.</span><span class="sxs-lookup"><span data-stu-id="43789-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="43789-136">Zapytania w portalu wyszukiwania dziennika zwraca tylko rekordy z **TimeGenerated** w zakresie czasu, który jest wyświetlany po lewej stronie ekranu.</span><span class="sxs-lookup"><span data-stu-id="43789-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="43789-137">Filtr czasu można zmienić, wybierając z menu rozwijanego albo modyfikując suwaka.</span><span class="sxs-lookup"><span data-stu-id="43789-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="43789-138">Suwak Wyświetla wykres słupkowy przedstawiający względną liczbę rekordów dla każdego segmentu czasu w zakresie.</span><span class="sxs-lookup"><span data-stu-id="43789-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="43789-139">Ten segment będą się różnić w zależności od zakresu.</span><span class="sxs-lookup"><span data-stu-id="43789-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="43789-140">Domyślny zakres czasu to **1 dzień**.</span><span class="sxs-lookup"><span data-stu-id="43789-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="43789-141">Zmień tę wartość na **7 dni**, i zwiększyć całkowita liczba rekordów.</span><span class="sxs-lookup"><span data-stu-id="43789-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Zakres czasu daty](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="43789-143">Filtrowanie wyników zapytania</span><span class="sxs-lookup"><span data-stu-id="43789-143">Filter results of the query</span></span>
<span data-ttu-id="43789-144">Po lewej stronie ekranu jest okienko filtru, dzięki czemu można dodać filtrowanie do zapytania bez modyfikowania jej bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="43789-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="43789-145">Kilka właściwości zwracanych rekordów są wyświetlane z wartościami pierwszych dziesięciu z ich liczba rekordów.</span><span class="sxs-lookup"><span data-stu-id="43789-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="43789-146">Jeśli pracujesz z **zdarzeń**, zaznacz pole wyboru obok pozycji **błąd** w obszarze **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="43789-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="43789-147">Jeśli pracujesz z **Syslog**, zaznacz pole wyboru obok pozycji **błąd** w obszarze **poziom ważności**.</span><span class="sxs-lookup"><span data-stu-id="43789-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="43789-148">Spowoduje to zmianę zapytanie do jednego z następujących czynności, aby ograniczyć wyniki do zdarzenia błędów.</span><span class="sxs-lookup"><span data-stu-id="43789-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtr](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="43789-150">Dodawanie właściwości do okienka filtru, wybierając **dodać do filtrów** z menu właściwości na jednym z nich.</span><span class="sxs-lookup"><span data-stu-id="43789-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Dodawanie do menu filtrowania](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="43789-152">Ten sam filtr można ustawić, wybierając **filtru** z menu właściwości rekordu o wartości do filtrowania.</span><span class="sxs-lookup"><span data-stu-id="43789-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="43789-153">Masz tylko **filtru** opcji dla właściwości o nazwie ich w kolorze niebieskim.</span><span class="sxs-lookup"><span data-stu-id="43789-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="43789-154">Są to *wyszukiwanie* pola, które są indeksowane dla warunki wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="43789-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="43789-155">Pola w kolorze szarym są *wolne tekst można wyszukiwać* pola, które mają tylko **Pokaż odwołania** opcji.</span><span class="sxs-lookup"><span data-stu-id="43789-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="43789-156">Ta opcja zwraca rekordy, które mają tę wartość w dowolnej właściwości.</span><span class="sxs-lookup"><span data-stu-id="43789-156">This option returns records that have that value in any property.</span></span>

![Menu filtrowania](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="43789-158">W przypadku grupowania wyników dla jednej właściwości wybierając **Grupuj według** opcji z menu rekordu.</span><span class="sxs-lookup"><span data-stu-id="43789-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="43789-159">Spowoduje to dodanie [Podsumuj](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operatora w kwerendzie wyświetli wyniki na wykresie.</span><span class="sxs-lookup"><span data-stu-id="43789-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="43789-160">Można grupować w więcej niż jedną właściwość, ale trzeba edytować zapytanie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="43789-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="43789-161">Następnie wybierz menu rekordu **komputera** właściwości i wybierz **Grupuj według "Komputer"**.</span><span class="sxs-lookup"><span data-stu-id="43789-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Grupuj według komputera](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="43789-163">Praca z wynikami</span><span class="sxs-lookup"><span data-stu-id="43789-163">Work with results</span></span>
<span data-ttu-id="43789-164">Portal wyszukiwania dziennika ma wiele funkcji do pracy z wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="43789-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="43789-165">Można sortować, filtr i wyniki grupy do analizowania danych bez modyfikowania zapytania rzeczywistego.</span><span class="sxs-lookup"><span data-stu-id="43789-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="43789-166">Domyślnie nie są sortowane wyniki zapytania.</span><span class="sxs-lookup"><span data-stu-id="43789-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="43789-167">Aby wyświetlić dane w postaci tabeli, która zapewnia dodatkowe opcje filtrowania i sortowania, kliknij przycisk **tabeli**.</span><span class="sxs-lookup"><span data-stu-id="43789-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Widok tabeli](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="43789-169">Kliknij strzałkę przez rekord, aby wyświetlić szczegóły dla tego rekordu.</span><span class="sxs-lookup"><span data-stu-id="43789-169">Click the arrow by a record to view the details for that record.</span></span>

![Sortowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="43789-171">Sortuj według dowolnego pola, klikając jej nagłówek kolumny.</span><span class="sxs-lookup"><span data-stu-id="43789-171">Sort on any field by clicking on its column header.</span></span>

![Sortowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="43789-173">Filtrować wyniki na określoną wartość w kolumnie, klikając przycisk filtru i zapewnianie warunek filtru.</span><span class="sxs-lookup"><span data-stu-id="43789-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Filtrowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="43789-175">Grupy dla kolumny przez przeciągnięcie jego nagłówka kolumny na początku wyników.</span><span class="sxs-lookup"><span data-stu-id="43789-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="43789-176">Można grupować według wielu pól, przeciągając wiele kolumn do góry.</span><span class="sxs-lookup"><span data-stu-id="43789-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Wyniki grupy](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="43789-178">Praca z danych wydajności</span><span class="sxs-lookup"><span data-stu-id="43789-178">Work with performance data</span></span>
<span data-ttu-id="43789-179">Dane wydajności dla agentów systemów Windows i Linux są przechowywane w obszarze roboczym analizy dzienników w **wydajności** tabeli.</span><span class="sxs-lookup"><span data-stu-id="43789-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="43789-180">Rejestruje wydajności wyglądać podobnie jak dowolny inny rekord i firma Microsoft może zapisywać prostego zapytania, która zwraca wszystkie rekordy wydajności, podobnie jak ze zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="43789-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Dane dotyczące wydajności](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="43789-182">Mimo że zwracanie miliony rekordów wszystkie obiekty i liczniki wydajności nie jest bardzo przydatne.</span><span class="sxs-lookup"><span data-stu-id="43789-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="43789-183">Można użyć tych samych metod używanych powyżej przefiltruj dane lub po prostu wpisz poniższe zapytanie bezpośrednio w polu wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="43789-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="43789-184">To polecenie zwróci tylko procesor rekordów użycia dla komputerów z systemami Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="43789-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Użycie procesora](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="43789-186">To ogranicza dane do określonego licznika, ale jego nadal nie umieszcza je w postaci jest szczególnie przydatne.</span><span class="sxs-lookup"><span data-stu-id="43789-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="43789-187">Możesz wyświetlić dane w wykres liniowy, ale najpierw należy go Grupuj według komputera i TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="43789-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="43789-188">Aby grupować według wielu pól, należy bezpośrednio zmodyfikować zapytanie, tak zmodyfikuj zapytanie do następującego.</span><span class="sxs-lookup"><span data-stu-id="43789-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="43789-189">Ta metoda korzysta [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) działać na **równowartości** właściwości do obliczenia średniej wartości ciągu każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="43789-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Wykres danych wydajności](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="43789-191">Teraz, gdy dane są odpowiednio grupowane, można je wyświetlić na wykresie visual przez dodanie [renderowania](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operatora.</span><span class="sxs-lookup"><span data-stu-id="43789-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Wykres liniowy](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="43789-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43789-193">Next steps</span></span>

- <span data-ttu-id="43789-194">Dowiedz się więcej o język zapytań usługi Analiza dzienników w [wprowadzenie do korzystania z portalu usługi analiza](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="43789-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="43789-195">Przewodnik po użyciu samouczka [portal analityka zaawansowane](https://go.microsoft.com/fwlink/?linkid=856587) co pozwala na tej samej kwerend i dostęp do tych samych danych jako portal wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="43789-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
