---
title: aaaUsing hello wyszukiwania dziennika portal Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera samouczek, który opisuje sposób toocreate dziennika wyszukiwania i analizowanie danych przechowywanych w obszarze roboczym analizy dzienników przy użyciu hello dziennik wyszukiwania portalu.  Samouczek Hello obejmuje uruchamiania niektórych zapytań proste tooreturn różnych typów danych oraz analizowanie wyników."
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
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a><span data-ttu-id="fd023-104">Tworzenie wyszukiwań dziennika w przy użyciu hello dziennik wyszukiwania portalu usługi Analiza dzienników Azure</span><span class="sxs-lookup"><span data-stu-id="fd023-104">Create log searches in Azure Log Analytics using hello Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="fd023-105">W tym artykule opisano hello portal wyszukiwania dziennika przy użyciu hello nowego języka zapytań usługi Analiza dzienników Azure.</span><span class="sxs-lookup"><span data-stu-id="fd023-105">This article describes hello Log Search portal in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="fd023-106">Możesz dowiedzieć się więcej o nowy język hello i uzyskać hello procedury tooupgrade obszaru roboczego na [uaktualnienia wyszukiwania dziennika toonew roboczym usługi Analiza dzienników Azure](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="fd023-106">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="fd023-107">Jeśli obszar roboczy nie został uaktualniony toohello nowy język zapytań, należy zapoznać się zbyt[wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników](log-analytics-log-searches.md) Aby uzyskać informacje o bieżącej wersji hello hello dziennik wyszukiwania portalu.</span><span class="sxs-lookup"><span data-stu-id="fd023-107">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="fd023-108">Ten artykuł zawiera samouczek, który opisuje sposób toocreate dziennika wyszukiwania i analizowanie danych przechowywanych w obszarze roboczym analizy dzienników przy użyciu hello dziennik wyszukiwania portalu.</span><span class="sxs-lookup"><span data-stu-id="fd023-108">This article includes a tutorial that describes how toocreate log searches and analyze data stored in your Log Analytics workspace using hello Log Search portal.</span></span>  <span data-ttu-id="fd023-109">Samouczek Hello obejmuje uruchamiania niektórych zapytań proste tooreturn różnych typów danych oraz analizowanie wyników.</span><span class="sxs-lookup"><span data-stu-id="fd023-109">hello tutorial includes running some simple queries tooreturn different types of data and analyzing results.</span></span>  <span data-ttu-id="fd023-110">Głównie funkcji w portalu wyszukiwania dziennika hello modyfikowanie hello zapytanie, zamiast bezpośrednie modyfikowanie.</span><span class="sxs-lookup"><span data-stu-id="fd023-110">It focuses on features in hello Log Search portal for modifying hello query rather than modifying it directly.</span></span>  <span data-ttu-id="fd023-111">Szczegółowe informacje dotyczące bezpośredniego edytowania hello zapytania, zobacz hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="fd023-111">For details on directly editing hello query, see hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="fd023-112">Wyszukiwanie toocreate w portalu analityka zaawansowane hello zamiast hello dziennik wyszukiwania portalu, zobacz [wprowadzenie hello Portal analityka](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="fd023-112">toocreate searches in hello Advanced Analytics portal instead of hello Log Search portal, see [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="fd023-113">Obu portalach Użyj hello tego samego zapytania języka tooaccess hello tych samych danych, w obszarze roboczym analizy dzienników hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-113">Both portals use hello same query language tooaccess hello same data in hello Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd023-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fd023-114">Prerequisites</span></span>
<span data-ttu-id="fd023-115">W tym samouczku założono, że już obszar roboczy analizy dzienników z co najmniej jeden połączone źródła, które generuje dane dotyczące hello tooanalyze zapytania.</span><span class="sxs-lookup"><span data-stu-id="fd023-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for hello queries tooanalyze.</span></span>  

- <span data-ttu-id="fd023-116">Jeśli nie masz obszaru roboczego, możesz utworzyć wolnego przy użyciu procedury hello na [Rozpoczynanie pracy z obszaru roboczego analizy dzienników](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fd023-116">If you don't have a workspace, you can create a free one using hello procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="fd023-117">Co najmniej jednego połączenia [agenta Windows](log-analytics-windows-agents.md) lub [agenta systemu Linux](log-analytics-linux-agents.md) toohello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="fd023-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) toohello workspace.</span></span>  

## <a name="open-hello-log-search-portal"></a><span data-ttu-id="fd023-118">Otwórz hello dziennik wyszukiwania portalu</span><span class="sxs-lookup"><span data-stu-id="fd023-118">Open hello Log Search portal</span></span>
<span data-ttu-id="fd023-119">Rozpocznij od otwierania hello dziennik wyszukiwania portalu.</span><span class="sxs-lookup"><span data-stu-id="fd023-119">Start by opening hello Log Search portal.</span></span>  <span data-ttu-id="fd023-120">Można do niego dostęp w portalu OMS hello albo hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fd023-120">You can access it in either hello Azure portal or hello OMS portal.</span></span>

1. <span data-ttu-id="fd023-121">Otwórz hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fd023-121">Open hello Azure portal.</span></span>
2. <span data-ttu-id="fd023-122">Przejdź tooLog Analytics i wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="fd023-122">Navigate tooLog Analytics and select your workspace.</span></span>
3. <span data-ttu-id="fd023-123">Wybierz opcję **wyszukiwania dziennika** toostay w portalu lub uruchamiania hello OMS portalu Azure, wybierając hello **portalu OMS** , a następnie klikając przycisk wyszukiwania dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-123">Either select **Log Search** toostay in hello Azure portal or launch hello OMS portal by selecting **OMS Portal** and then clicking hello Log Search button.</span></span>

![Przycisk wyszukiwania dziennika](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="fd023-125">Tworzenie prostego wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="fd023-125">Create a simple search</span></span>
<span data-ttu-id="fd023-126">Witaj najszybszy sposób tooretrieve toowork niektóre dane z jest proste zapytanie zwracające wszystkie rekordy w tabeli.</span><span class="sxs-lookup"><span data-stu-id="fd023-126">hello quickest way tooretrieve some data toowork with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="fd023-127">Jeśli masz obszar roboczy dowolnego systemu Windows lub Linux klientów połączonych tooyour, będziesz mieć danych albo hello zdarzenia (system Windows) lub tabeli dziennika systemowego (Linux).</span><span class="sxs-lookup"><span data-stu-id="fd023-127">If you have any Windows or Linux clients connected tooyour workspace, then you'll have data in either hello Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="fd023-128">Wpisz jeden hello następującego zapytania w polu wyszukiwania hello i kliknij przycisk Wyszukaj hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-128">Type one hello following queries in hello search box and click hello search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="fd023-129">Dane są zwracane w hello domyślny widok listy, a widać, ile całkowita liczba rekordów zostały zwrócone.</span><span class="sxs-lookup"><span data-stu-id="fd023-129">Data is returned in hello default list view, and you can see how many total records were returned.</span></span>

![Prostego zapytania](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="fd023-131">Tylko hello pierwszy kilka właściwości każdego rekordu są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="fd023-131">Only hello first few properties of each record are displayed.</span></span>  <span data-ttu-id="fd023-132">Kliknij przycisk **Pokaż więcej** toodisplay wszystkie właściwości dla określonego rekordu.</span><span class="sxs-lookup"><span data-stu-id="fd023-132">Click **show more** toodisplay all properties for a particular record.</span></span>

![Szczegóły rekordu](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a><span data-ttu-id="fd023-134">Ustaw zakres czasu hello</span><span class="sxs-lookup"><span data-stu-id="fd023-134">Set hello time scope</span></span>
<span data-ttu-id="fd023-135">Każdy rekord zebrane przez analizy dzienników ma **TimeGenerated** właściwość, która zawiera hello Data i godzina utworzenia tego rekordu hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains hello date and time that hello record was created.</span></span>  <span data-ttu-id="fd023-136">Zapytania w portalu wyszukiwania dziennika hello zwraca tylko rekordy z **TimeGenerated** w zakresie czasu hello, który jest wyświetlany na powitania po lewej stronie ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-136">A query in hello Log Search portal only returns records with a **TimeGenerated** within hello time scope that's displayed on hello left side of hello screen.</span></span>  

<span data-ttu-id="fd023-137">Filtr czasu hello można zmienić, wybierając z listy rozwijanej hello lub modyfikując hello suwaka.</span><span class="sxs-lookup"><span data-stu-id="fd023-137">You can change hello time filter either by selecting hello dropdown or by modifying hello slider.</span></span>  <span data-ttu-id="fd023-138">Witaj suwak Wyświetla wykres słupkowy przedstawiający hello względną liczbę rekordów dla każdego segmentu czasu w zakresie hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-138">hello slider displays a bar graph that shows hello relative number of records for each time segment within hello range.</span></span>  <span data-ttu-id="fd023-139">Ten segment będą się różnić w zależności od zakresu hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-139">This segment will vary depending on hello range.</span></span>

<span data-ttu-id="fd023-140">zakres czasu domyślny Hello jest **1 dzień**.</span><span class="sxs-lookup"><span data-stu-id="fd023-140">hello default time scope is **1 day**.</span></span>  <span data-ttu-id="fd023-141">Zmień tę wartość za**7 dni**, i zwiększyć hello całkowita liczba rekordów.</span><span class="sxs-lookup"><span data-stu-id="fd023-141">Change this value too**7 days**, and hello total number of records should increase.</span></span>

![Zakres czasu daty](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a><span data-ttu-id="fd023-143">Filtrowanie wyników zapytania hello</span><span class="sxs-lookup"><span data-stu-id="fd023-143">Filter results of hello query</span></span>
<span data-ttu-id="fd023-144">Na powitania lewej części ekranu hello jest okienko filtru hello, dzięki czemu można tooadd filtrowania toohello zapytań bez modyfikowania jej bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="fd023-144">On hello left side of hello screen is hello filter pane which allows you tooadd filtering toohello query without modifying it directly.</span></span>  <span data-ttu-id="fd023-145">Kilka właściwości zwracanych rekordów hello są wyświetlane z najwyższym dziesięć wartościami z ich liczba rekordów.</span><span class="sxs-lookup"><span data-stu-id="fd023-145">Several properties of hello records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="fd023-146">Jeśli pracujesz z **zdarzeń**, wybierz hello pole wyboru obok zbyt**błąd** w obszarze **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="fd023-146">If you're working with **Event**, select hello checkbox next too**Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="fd023-147">Jeśli pracujesz z **Syslog**, wybierz hello pole wyboru obok zbyt**błąd** w obszarze **poziom ważności**.</span><span class="sxs-lookup"><span data-stu-id="fd023-147">If you're working with **Syslog**, select hello checkbox next too**err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="fd023-148">Spowoduje to zmianę zapytań hello tooone powitania po toolimit hello powoduje tooerror zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="fd023-148">This changes hello query tooone of hello following toolimit hello results tooerror events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtr](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="fd023-150">Okienko filtru toohello Dodaj właściwości, wybierając **dodać toofilters** z menu właściwości hello na jednym hello rekordów.</span><span class="sxs-lookup"><span data-stu-id="fd023-150">Add properties toohello filter pane by selecting **Add toofilters** from hello property menu on one of hello records.</span></span>

![Dodawanie toofilter menu](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="fd023-152">Można ustawić hello samego filtru, wybierając **filtru** menu właściwości hello rekord z wartością hello ma toofilter.</span><span class="sxs-lookup"><span data-stu-id="fd023-152">You can set hello same filter by selecting **Filter** from hello property menu for a record with hello value you want toofilter.</span></span>  

<span data-ttu-id="fd023-153">Masz tylko hello **filtru** opcji dla właściwości o nazwie ich w kolorze niebieskim.</span><span class="sxs-lookup"><span data-stu-id="fd023-153">You only have hello **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="fd023-154">Są to *wyszukiwanie* pola, które są indeksowane dla warunki wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="fd023-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="fd023-155">Pola w kolorze szarym są *wolne tekst można wyszukiwać* pola o tylko hello **Pokaż odwołania** opcji.</span><span class="sxs-lookup"><span data-stu-id="fd023-155">Fields in grey are *free text searchable* fields which only have hello **Show references** option.</span></span>  <span data-ttu-id="fd023-156">Ta opcja zwraca rekordy, które mają tę wartość w dowolnej właściwości.</span><span class="sxs-lookup"><span data-stu-id="fd023-156">This option returns records that have that value in any property.</span></span>

![Menu filtrowania](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="fd023-158">Można grupować hello wyników dla jednej właściwości, wybierając hello **Grupuj według** opcję w menu rekord hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-158">You can group hello results on a single property by selecting hello **Group by** option in hello record menu.</span></span>  <span data-ttu-id="fd023-159">Spowoduje to dodanie [Podsumuj](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour kwerendę, która wyświetla wyniki hello na wykresie.</span><span class="sxs-lookup"><span data-stu-id="fd023-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour query that displays hello results in a chart.</span></span>  <span data-ttu-id="fd023-160">Można grupować w więcej niż jedną właściwość, ale będzie potrzebny tooedit hello zapytania bezpośredniego.</span><span class="sxs-lookup"><span data-stu-id="fd023-160">You can group on more than one property, but you would need tooedit hello query directly.</span></span>  <span data-ttu-id="fd023-161">Wybierz hello rekordów menu dalej Witaj Witaj **komputera** właściwości i wybierz **Grupuj według "Komputer"**.</span><span class="sxs-lookup"><span data-stu-id="fd023-161">Select hello record menu next hello hello **Computer** property and select **Group by 'Computer'**.</span></span>  

![Grupuj według komputera](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="fd023-163">Praca z wynikami</span><span class="sxs-lookup"><span data-stu-id="fd023-163">Work with results</span></span>
<span data-ttu-id="fd023-164">portal wyszukiwania dziennika Hello ma wiele funkcji do pracy z hello wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="fd023-164">hello Log Search portal has a variety of features for working with hello results of a query.</span></span>  <span data-ttu-id="fd023-165">Można sortować, filtr i grupa powoduje tooanalyze hello danych bez modyfikowania zapytania rzeczywiste hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-165">You can sort, filter, and group results tooanalyze hello data without modifying hello actual query.</span></span>  <span data-ttu-id="fd023-166">Domyślnie nie są sortowane wyniki zapytania.</span><span class="sxs-lookup"><span data-stu-id="fd023-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="fd023-167">tooview hello danych w formie tabeli, która zapewnia dodatkowe opcje filtrowania i sortowania, kliknij przycisk **tabeli**.</span><span class="sxs-lookup"><span data-stu-id="fd023-167">tooview hello data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Widok tabeli](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="fd023-169">Kliknij strzałkę hello przez szczegóły hello tooview rekordów dla tego rekordu.</span><span class="sxs-lookup"><span data-stu-id="fd023-169">Click hello arrow by a record tooview hello details for that record.</span></span>

![Sortowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="fd023-171">Sortuj według dowolnego pola, klikając jej nagłówek kolumny.</span><span class="sxs-lookup"><span data-stu-id="fd023-171">Sort on any field by clicking on its column header.</span></span>

![Sortowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="fd023-173">Filtrowanie wyników hello na określoną wartość w kolumnie hello, klikając przycisk Filtr hello i podając warunek filtru.</span><span class="sxs-lookup"><span data-stu-id="fd023-173">Filter hello results on a specific value in hello column by clicking hello filter button and providing a filter condition.</span></span>

![Filtrowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="fd023-175">Grupy dla kolumny przez przeciągnięcie nagłówka kolumny toohello górnym hello wyników.</span><span class="sxs-lookup"><span data-stu-id="fd023-175">Group on a column by dragging its column header toohello top of hello results.</span></span>  <span data-ttu-id="fd023-176">Można grupować według wielu pól przeciągając wiele kolumn toohello top.</span><span class="sxs-lookup"><span data-stu-id="fd023-176">You can group on multiple fields by dragging multiple columns toohello top.</span></span>

![Wyniki grupy](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="fd023-178">Praca z danych wydajności</span><span class="sxs-lookup"><span data-stu-id="fd023-178">Work with performance data</span></span>
<span data-ttu-id="fd023-179">Dane wydajności dla agentów systemów Windows i Linux są przechowywane w obszarze roboczym analizy dzienników hello w hello **wydajności** tabeli.</span><span class="sxs-lookup"><span data-stu-id="fd023-179">Performance data for both Windows and Linux agents is stored in hello Log Analytics workspace in hello **Perf** table.</span></span>  <span data-ttu-id="fd023-180">Rejestruje wydajności wyglądać podobnie jak dowolny inny rekord i firma Microsoft może zapisywać prostego zapytania, która zwraca wszystkie rekordy wydajności, podobnie jak ze zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="fd023-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Dane dotyczące wydajności](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="fd023-182">Mimo że zwracanie miliony rekordów wszystkie obiekty i liczniki wydajności nie jest bardzo przydatne.</span><span class="sxs-lookup"><span data-stu-id="fd023-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="fd023-183">Można użyć hello tych samych metod używanych powyżej toofilter hello danych lub po prostu wpisz hello następujące zapytanie bezpośrednio do pola wyszukiwania hello dziennika.</span><span class="sxs-lookup"><span data-stu-id="fd023-183">You can use hello same methods you used above toofilter hello data or just type hello following query directly into hello log search box.</span></span>  <span data-ttu-id="fd023-184">To polecenie zwróci tylko procesor rekordów użycia dla komputerów z systemami Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="fd023-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Użycie procesora](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="fd023-186">To ogranicza hello danych tooa określonego licznika, ale jego nadal nie umieszcza je w postaci jest szczególnie przydatne.</span><span class="sxs-lookup"><span data-stu-id="fd023-186">This limits hello data tooa particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="fd023-187">Wyświetlanie danych hello w wykres liniowy, ale najpierw należy toogroup go przez komputer i TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="fd023-187">You can display hello data in a line chart, but first need toogroup it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="fd023-188">toogroup według wielu pól, należy toomodify hello zapytania bezpośrednio, więc modyfikować hello zapytania toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="fd023-188">toogroup on multiple fields, you need toomodify hello query directly, so modify hello query toohello following.</span></span>  <span data-ttu-id="fd023-189">Używa hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) funkcja na powitania **równowartości** właściwości toocalculate hello średnią wartość ciągu każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="fd023-189">This uses hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on hello **CounterValue** property toocalculate hello average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Wykres danych wydajności](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="fd023-191">Teraz, gdy dane hello odpowiednio są grupowane, można je wyświetlić na wykresie visual przez dodanie hello [renderowania](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operatora.</span><span class="sxs-lookup"><span data-stu-id="fd023-191">Now that hello data is suitably grouped, you can display it in a visual chart by adding hello [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Wykres liniowy](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="fd023-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd023-193">Next steps</span></span>

- <span data-ttu-id="fd023-194">Dowiedz się więcej o język zapytań usługi Analiza dzienników hello na [wprowadzenie hello Portal analityka](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="fd023-194">Learn more about hello Log Analytics query language at [Getting Started with hello Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="fd023-195">Zapoznaj się z artykułem samouczek przy użyciu hello [portal analityka zaawansowane](https://go.microsoft.com/fwlink/?linkid=856587) co pozwala toorun hello tego samego zapytania i dostęp do tych samych danych co hello dziennik wyszukiwania portalu hello.</span><span class="sxs-lookup"><span data-stu-id="fd023-195">Walk through a tutorial using hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you toorun hello same queries and access hello same data as hello Log Search portal.</span></span>
