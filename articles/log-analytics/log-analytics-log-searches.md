---
title: aaaFind danych z dziennika wyszukiwania Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Dziennik wyszukiwania pozwalają toocombine i skorelowania danych dowolnego komputera z wielu źródeł w danym środowisku."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="34324-103">Wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="34324-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="34324-104">W tym artykule opisano dziennik wyszukiwania przy użyciu hello bieżący język zapytań w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="34324-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="34324-105">Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie należy zapoznać się zbyt[opis dziennika przeszukuje analizy dzienników (nowy)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="34324-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="34324-106">Na powitania najważniejsza część analizy dzienników jest funkcja wyszukiwania dziennika hello, dzięki czemu można toocombine i skorelowania danych dowolnego komputera z wielu źródeł w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="34324-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="34324-107">Rozwiązania są również obsługiwane przez dziennik wyszukiwania toobring metryki można przestawiać wokół obszaru określonego problemu.</span><span class="sxs-lookup"><span data-stu-id="34324-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="34324-108">Na stronie wyszukiwania hello można utworzyć kwerendę, a następnie podczas wyszukiwania, możesz filtrować wyniki hello za pomocą formantów zestawu reguł.</span><span class="sxs-lookup"><span data-stu-id="34324-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="34324-109">Można też utworzyć tootransform zaawansowanych zapytań, filtrować i raportu na wyniki.</span><span class="sxs-lookup"><span data-stu-id="34324-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="34324-110">Typowe zapytania wyszukiwania dziennika znajdują się na większości stronach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="34324-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="34324-111">W konsoli OMS hello możesz kliknąć Kafelki lub przejść do szczegółów w elementach tooother tooview szczegóły elementu hello za pomocą wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="34324-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="34324-112">W tym samouczku zostanie omówiony toocover przykłady wszystkie podstawy hello podczas wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="34324-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="34324-113">Firma Microsoft będzie rozpoczynać się od prostego, praktyczne przykłady i następnie ich tak, aby uzyskać opis praktycznych zastosowań o toouse hello składni tooextract hello insights sposób hello danych.</span><span class="sxs-lookup"><span data-stu-id="34324-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="34324-114">Po znasz zapoznać się z techniki wyszukiwania, można przejrzeć hello [analizy dzienników dziennika odwołanie wyszukiwania](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="34324-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="34324-115">Używanie filtrów podstawowych</span><span class="sxs-lookup"><span data-stu-id="34324-115">Use basic filters</span></span>
<span data-ttu-id="34324-116">Witaj po pierwsze tooknow jest pierwszym hello część zapytania wyszukiwania, przed każdą "|" znak kreski pionowej, jest zawsze *filtru*.</span><span class="sxs-lookup"><span data-stu-id="34324-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="34324-117">Należy go traktować jako klauzuli WHERE TSQL — Określa *co* podzbiór toopull danych z magazynu danych hello OMS.</span><span class="sxs-lookup"><span data-stu-id="34324-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="34324-118">Wyszukiwanie w magazynie danych hello dotyczy przede wszystkim określenie właściwości hello hello dane tooextract, dlatego jest naturalna, czy zapytanie może rozpoczynać się hello klauzuli WHERE.</span><span class="sxs-lookup"><span data-stu-id="34324-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="34324-119">Hello najbardziej podstawową można użyć są następujące filtry *słowa kluczowe*, na przykład "error" lub 'timeout' lub nazwę komputera.</span><span class="sxs-lookup"><span data-stu-id="34324-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="34324-120">Tego rodzaju prostego zapytania na ogół wraca kształtów różnych danych w ramach hello sam wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="34324-121">Analiza dzienników ma inną *typy* danych w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="34324-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="34324-122">tooconduct proste wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="34324-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="34324-123">W portalu OMS hello, kliknij przycisk **wyszukiwania dziennika**.</span><span class="sxs-lookup"><span data-stu-id="34324-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="34324-124">![Kafelek wyszukiwania](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="34324-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="34324-125">W polu zapytania hello wpisz `error` , a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="34324-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="34324-126">![Błąd wyszukiwania](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="34324-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="34324-127">Na przykład hello zapytanie dla `error` w hello poniższy obraz zwrócone 100 000 **zdarzeń** rekordy (zbierane przez zarządzanie dziennikiem) 18 **ConfigurationAlert** rekordów (wygenerowanych przez konfigurację Ocena) i 12 **Zmianakonfiguracji** rekordy (przechwycone przez hello śledzenia zmian).</span><span class="sxs-lookup"><span data-stu-id="34324-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="34324-128">![wyniki wyszukiwania](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="34324-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="34324-129">Te filtry nie są naprawdę klas typów obiektów.</span><span class="sxs-lookup"><span data-stu-id="34324-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="34324-130">*Typ* jest tylko tag lub właściwość lub ciąg/Nazwa/kategorii, który jest dołączony tooa część danych.</span><span class="sxs-lookup"><span data-stu-id="34324-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="34324-131">Niektóre dokumenty w systemie hello są oznaczone jako **typu: ConfigurationAlert** i niektóre są oznaczone jako **typu: wydajności**, lub **typu: zdarzenia**i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="34324-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="34324-132">Każdy wynik wyszukiwania, dokument, rekordu lub wpis zawiera wszystkie właściwości pierwotnych hello i ich wartości dla każdego z tych fragmentów danych i użyciem tych toospecify nazwy pól w filtrze hello tylko rekordy hello tooretrieve gdzie hello pole ma, czy wartość.</span><span class="sxs-lookup"><span data-stu-id="34324-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="34324-133">*Typ* jest naprawdę tylko pola, które mają wszystkie rekordy, nie jest inny niż inne pole.</span><span class="sxs-lookup"><span data-stu-id="34324-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="34324-134">Ustanowiono to oparta na wartości hello hello typ pola.</span><span class="sxs-lookup"><span data-stu-id="34324-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="34324-135">Ten rekord ma inny formularz lub kształtu.</span><span class="sxs-lookup"><span data-stu-id="34324-135">That record will have a different shape or form.</span></span> <span data-ttu-id="34324-136">Okazjonalnie **typu = wydajności**, lub **typu = zdarzeń** jest również hello składni konieczne toolearn tooquery danych wydajności lub zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="34324-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="34324-137">Po nazwie pola hello i przed wartością hello można użyć dwukropka (:) lub znakiem równości (=).</span><span class="sxs-lookup"><span data-stu-id="34324-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="34324-138">**Typ: zdarzenie** i **typu = zdarzeń** są równoważne w rozumieniu, możesz wybrać hello styl preferowane.</span><span class="sxs-lookup"><span data-stu-id="34324-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="34324-139">Tak, jeśli hello wpisz = wydajności rekordów pole o nazwie "CounterName", a następnie można pisać zapytania podobne `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="34324-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="34324-140">Zapewni to tylko dane dotyczące wydajności hello gdy nazwa licznika wydajności hello jest "% czasu procesora".</span><span class="sxs-lookup"><span data-stu-id="34324-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="34324-141">toosearch danych wydajności czas procesora</span><span class="sxs-lookup"><span data-stu-id="34324-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="34324-142">W polu zapytania wyszukiwania hello wpisz`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="34324-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="34324-143">Można również być bardziej szczegółowe i używać **InstanceName = _ "Ogółem"** w zapytaniu hello, która jest licznika wydajności systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="34324-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="34324-144">Możesz też wybrać zestaw reguł, a drugi **pola: wartość**.</span><span class="sxs-lookup"><span data-stu-id="34324-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="34324-145">Filtr Hello jest automatycznie dodawany filtru tooyour hello pasku zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="34324-146">Widać to w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="34324-146">You can see this in hello following image.</span></span> <span data-ttu-id="34324-147">Przedstawia on gdzie tooclick tooadd **InstanceName: "_łącznie"** toohello zapytań bez wprowadzania żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="34324-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![aspekt wyszukiwania](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="34324-149">Zapytanie staje się teraz`Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="34324-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="34324-150">W tym przykładzie, nie masz toospecify **typu = wydajności** tooget toothis wynik.</span><span class="sxs-lookup"><span data-stu-id="34324-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="34324-151">Ponieważ pola hello CounterName i InstanceName tylko istnieje dla rekordów typu = wydajności, zapytania hello jest wystarczająco konkretny tooreturn hello takie same wyniki hello dłużej, poprzednie jedną:</span><span class="sxs-lookup"><span data-stu-id="34324-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="34324-152">Jest to spowodowane wszystkie filtry hello w zapytaniu hello są oceniane jako *i* ze sobą.</span><span class="sxs-lookup"><span data-stu-id="34324-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="34324-153">Ostatecznie hello Dodaj kryteria toohello więcej pól, możesz uzyskać mniejszy, więcej określonych i precyzyjnych wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="34324-154">Na przykład hello zapytania `Type=Event EventLog="Windows PowerShell"` jest identyczny zbyt`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="34324-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="34324-155">Zwraca wszystkie zdarzenia, które zostały zarejestrowane w i zbierane z dziennika zdarzeń hello środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34324-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="34324-156">Jeśli dodasz filtr wielokrotnie wielokrotnie, wybierając hello jest tego samego zestawu reguł, następnie hello problem czysto bardzo drobny — może zajmowały hello pasek wyszukiwania, ale nadal zwraca hello takie same wyniki ponieważ niejawny operator AND hello są zawsze dostępne.</span><span class="sxs-lookup"><span data-stu-id="34324-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="34324-157">Niejawny operator AND hello można łatwo cofnąć za pomocą operatora NOT jawnie.</span><span class="sxs-lookup"><span data-stu-id="34324-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="34324-158">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-158">For example:</span></span>

<span data-ttu-id="34324-159">`Type:Event NOT(EventLog:"Windows PowerShell")`lub jego odpowiednik `Type=Event EventLog!="Windows PowerShell"` zwrócić wszystkie zdarzenia ze wszystkich dzienników, które nie są hello dziennika programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34324-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="34324-160">Można użyć innych operator logiczny takich jak "Lub".</span><span class="sxs-lookup"><span data-stu-id="34324-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="34324-161">Witaj następujące zapytanie zwraca rekordy, dla których hello EventLog znajduje albo aplikacji lub systemu.</span><span class="sxs-lookup"><span data-stu-id="34324-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="34324-162">Przy użyciu hello powyżej zapytania, otrzymasz wpisy dla obu dzienników w hello sam wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="34324-163">Jednak jeśli usuniesz hello lub pozostawić hello niejawne i w miejscu, następnie hello następujące zapytanie nie utworzy żadnych wyników, ponieważ nie istnieje wpis dziennika zdarzeń, który należy tooBOTH dzienniki.</span><span class="sxs-lookup"><span data-stu-id="34324-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="34324-164">Każdy wpis dziennika zdarzeń został napisany tooonly jedną z dwóch dzienniki hello.</span><span class="sxs-lookup"><span data-stu-id="34324-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="34324-165">Używanie filtrów dodatkowe</span><span class="sxs-lookup"><span data-stu-id="34324-165">Use additional filters</span></span>
<span data-ttu-id="34324-166">Witaj następujące zapytanie zwraca wpisy 2 dzienników zdarzeń dla wszystkich komputerów hello, które zostały wysłane dane.</span><span class="sxs-lookup"><span data-stu-id="34324-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![Wyniki wyszukiwania](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="34324-168">Wybranie jednego z pól hello lub filtry zostaną zawęzić hello zapytania tooa określonego komputera, z wyłączeniem innych protokołów.</span><span class="sxs-lookup"><span data-stu-id="34324-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="34324-169">Wynikowe zapytanie Hello czy przypominać następujące hello.</span><span class="sxs-lookup"><span data-stu-id="34324-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="34324-170">Czyli następujące toohello równoważne z powodu hello niejawne koniunkcji binarnej.</span><span class="sxs-lookup"><span data-stu-id="34324-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="34324-171">Każde zapytanie jest oceniane w powitania po jawnym kolejności.</span><span class="sxs-lookup"><span data-stu-id="34324-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="34324-172">Uwaga hello nawiasu.</span><span class="sxs-lookup"><span data-stu-id="34324-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="34324-173">Podobnie jak hello pola dziennika zdarzeń, można pobrać dane tylko w przypadku zestaw komputerów określonych przez dodanie lub.</span><span class="sxs-lookup"><span data-stu-id="34324-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="34324-174">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="34324-175">Podobnie, ten powitania po return zapytania **% czasu procesora CPU** dla hello wybranych tylko dwa komputery.</span><span class="sxs-lookup"><span data-stu-id="34324-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="34324-176">Typy pól</span><span class="sxs-lookup"><span data-stu-id="34324-176">Field types</span></span>
<span data-ttu-id="34324-177">Podczas tworzenia filtrów, należy poznać różnice hello w pracy z różnymi typami pól zwrócony przez dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="34324-178">**Pola z możliwością przeszukiwania** Pokaż na niebiesko w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="34324-179">Pola, w których można użyć w polu toohello określone warunki wyszukiwania takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="34324-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="34324-180">**Zwolnij pól z możliwością wyszukiwania tekstu** są wyświetlane w kolorze szarym w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="34324-181">Nie można ich używać z polem toohello określone warunki wyszukiwania jak pól z możliwością wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="34324-182">Są one tylko przeszukiwane, gdy wszystkie pola, takie jak następujące hello wykonywanie zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="34324-183">Operatory logiczne</span><span class="sxs-lookup"><span data-stu-id="34324-183">Boolean operators</span></span>
<span data-ttu-id="34324-184">Datetime i pól liczbowych, możesz wyszukać wartości przy użyciu *większe*, *mniejszym niż*, i *mniejsza lub równa*.</span><span class="sxs-lookup"><span data-stu-id="34324-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="34324-185">Można używać operatorów prosty przykład >, <>, =, < =,! = w pasku wyszukiwania hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="34324-186">Umożliwia wysyłanie zapytań określonego dziennika zdarzeń w określonym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="34324-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="34324-187">Na przykład hello ostatnich 24 godzinach jest wyrażona z powitania po wyrażeniu skrótu.</span><span class="sxs-lookup"><span data-stu-id="34324-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="34324-188">toosearch przy użyciu operatora logicznego</span><span class="sxs-lookup"><span data-stu-id="34324-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="34324-189">W polu zapytania wyszukiwania hello wpisz`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="34324-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="34324-190">![Wyszukiwanie z wartość logiczna](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="34324-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="34324-191">Mimo że można kontrolować graficznie hello interwał czasu, a większość czasu może być toodo, czy tooincluding zalety filtr czasu bezpośrednio do hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="34324-192">Na przykład, to rozwiązanie idealne za pomocą pulpitów nawigacyjnych, w którym można zastąpić hello czasu dla każdego kafelka, niezależnie od hello *globalne* selektor czas na powitania strony pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="34324-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="34324-193">Aby uzyskać więcej informacji, zobacz [sprawach czas na pulpicie nawigacyjnym](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="34324-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="34324-194">Filtrowanie według czasu, pamiętać uzyskać wyniki dla hello *przecięcia* z hello dwóch okresów: hello określona w portalu OMS hello (S1) i hello określona w zapytaniu hello (S2).</span><span class="sxs-lookup"><span data-stu-id="34324-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![część wspólną](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="34324-196">Oznacza to, że jeśli hello okresów nie intersect, na przykład w portalu OMS hello, którym można wybrać **ten tydzień** w hello kwerendy, gdzie został zdefiniowany **ostatniego tygodnia**, to nie ma żadnych przecięcia i użytkownik nie będzie otrzymywać żadnych wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="34324-197">Operatory porównania pola TimeGenerated hello są przydatne także w innych sytuacjach.</span><span class="sxs-lookup"><span data-stu-id="34324-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="34324-198">Na przykład w przypadku pól liczbowych.</span><span class="sxs-lookup"><span data-stu-id="34324-198">For example, with numeric fields.</span></span>

<span data-ttu-id="34324-199">Podane na przykład, że alerty oceny konfiguracji hello następujące wartości ważności:</span><span class="sxs-lookup"><span data-stu-id="34324-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="34324-200">0 = informacji</span><span class="sxs-lookup"><span data-stu-id="34324-200">0 = Information</span></span>
* <span data-ttu-id="34324-201">1 = Ostrzeżenie</span><span class="sxs-lookup"><span data-stu-id="34324-201">1 = Warning</span></span>
* <span data-ttu-id="34324-202">2 = krytyczne</span><span class="sxs-lookup"><span data-stu-id="34324-202">2 = Critical</span></span>

<span data-ttu-id="34324-203">Można wyszukać zarówno ostrzegawcze i krytyczne alerty i wykluczyć informacyjną sieci z hello następujące zapytanie:</span><span class="sxs-lookup"><span data-stu-id="34324-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="34324-204">Umożliwia także zakresu zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-204">You can also use range queries.</span></span> <span data-ttu-id="34324-205">Oznacza to, zapewniają hello początku i na końcu zakresu wartości w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="34324-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="34324-206">Na przykład jeśli zdarzenia z dziennika zdarzeń programu Operations Manager hello gdzie hello identyfikator zdarzenia jest większy lub równy too2100, ale nie jest większa niż 2199, następnie hello następujące kwerendy zwróci je.</span><span class="sxs-lookup"><span data-stu-id="34324-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="34324-207">należy użyć składni zakresu Hello jest hello dwukropka (:) pola: wartość separatora i *nie* hello znak równości (=).</span><span class="sxs-lookup"><span data-stu-id="34324-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="34324-208">Ujmij hello dolna i górna końca zakresu hello w nawiasach kwadratowych i oddziel dwie kropki (.).</span><span class="sxs-lookup"><span data-stu-id="34324-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="34324-209">Opracowanie wyników wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="34324-209">Manipulate search results</span></span>
<span data-ttu-id="34324-210">Jeśli szukasz danych zostanie mają toorefine zapytania wyszukiwania oraz mają dobrej poziom kontroli nad hello wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="34324-211">Pobierane są wyniki, można zastosować tootransform polecenia je.</span><span class="sxs-lookup"><span data-stu-id="34324-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="34324-212">Polecenia w wyszukiwaniach analizy dzienników *musi* należy wykonać po hello znaku kreski pionowej (|).</span><span class="sxs-lookup"><span data-stu-id="34324-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="34324-213">Filtr musi być zawsze hello pierwsza część ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="34324-214">Definiuje zestaw danych hello, w którym pracujesz z, a następnie "powoduje przekazanie w potoku" uzyskanych w poleceniu.</span><span class="sxs-lookup"><span data-stu-id="34324-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="34324-215">Następnie można użyć potoku hello tooadd dodatkowych poleceń.</span><span class="sxs-lookup"><span data-stu-id="34324-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="34324-216">To jest luźno podobne potoku środowiska Windows PowerShell toohello.</span><span class="sxs-lookup"><span data-stu-id="34324-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="34324-217">Ogólnie rzecz biorąc, hello język wyszukiwania analizy dzienników próbuje toomake styl i wskazówki dotyczące programu PowerShell toofollow it podobne toohello IT zalet i tooease hello naukę.</span><span class="sxs-lookup"><span data-stu-id="34324-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="34324-218">Polecenia mają nazwy zleceń, dzięki czemu można łatwo sprawdzić, co zrobić.</span><span class="sxs-lookup"><span data-stu-id="34324-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="34324-219">Sortuj</span><span class="sxs-lookup"><span data-stu-id="34324-219">Sort</span></span>
<span data-ttu-id="34324-220">polecenie sortowania Hello pozwala hello toodefine sortowanie według wielu pól.</span><span class="sxs-lookup"><span data-stu-id="34324-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="34324-221">Nawet jeśli nie używasz go, domyślna, czas, w kolejności malejącej jest wymuszana.</span><span class="sxs-lookup"><span data-stu-id="34324-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="34324-222">Najnowsze wyniki Hello są zawsze u góry hello wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="34324-223">Oznacza to, że po uruchomieniu wyszukiwania z `Type=Event EventID=1234` co naprawdę wykonaniu dla Ciebie jest:</span><span class="sxs-lookup"><span data-stu-id="34324-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="34324-224">To, ponieważ jest typem hello doświadczenia, które znasz w dziennikach.</span><span class="sxs-lookup"><span data-stu-id="34324-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="34324-225">Na przykład w Podglądzie zdarzeń systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="34324-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="34324-226">Możesz użyć sortowania toochange hello sposób są zwracane.</span><span class="sxs-lookup"><span data-stu-id="34324-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="34324-227">Witaj poniższych przykładach pokazano, jak to działa.</span><span class="sxs-lookup"><span data-stu-id="34324-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="34324-228">Hello proste powyższych przykładach można działanie polecenia — zmienia kształt hello hello wyników, które hello filtr zwrócił.</span><span class="sxs-lookup"><span data-stu-id="34324-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="34324-229">Limit i od góry</span><span class="sxs-lookup"><span data-stu-id="34324-229">Limit and top</span></span>
<span data-ttu-id="34324-230">Inne mniej znanych polecenie jest ograniczona.</span><span class="sxs-lookup"><span data-stu-id="34324-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="34324-231">Limit wynosi zlecenie przypominającej programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34324-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="34324-232">Limit jest funkcjonalnie identyczne toohello polecenie TOP.</span><span class="sxs-lookup"><span data-stu-id="34324-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="34324-233">Witaj następujące kwerendy zwracają hello takie same wyniki.</span><span class="sxs-lookup"><span data-stu-id="34324-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="34324-234">za pomocą górnej toosearch</span><span class="sxs-lookup"><span data-stu-id="34324-234">toosearch using top</span></span>
* <span data-ttu-id="34324-235">W polu zapytania wyszukiwania hello wpisz`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="34324-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="34324-236">![top wyszukiwania](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="34324-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="34324-237">W powyższy obraz powitania, istnieją tysiące 358 rekordy z EventID = 600.</span><span class="sxs-lookup"><span data-stu-id="34324-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="34324-238">Witaj pól, aspekty i filtry na powitania left zawsze Pokaż informacje o wynikach hello *przez część filtru hello* hello zapytania, który jest częścią hello przed znakiem potoku.</span><span class="sxs-lookup"><span data-stu-id="34324-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="34324-239">Witaj **wyniki** okienko tylko zwraca wynik hello najnowszych 1, ponieważ hello przykładowe polecenie w kształcie i przekształcić hello wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="34324-240">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="34324-240">Select</span></span>
<span data-ttu-id="34324-241">Wybierz polecenie Hello zachowuje się jak Select-Object w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34324-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="34324-242">Zwraca przefiltrowane wyniki, które nie ma wszystkich swoich oryginalnych właściwości.</span><span class="sxs-lookup"><span data-stu-id="34324-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="34324-243">Wybiera hello tylko te właściwości, które określisz.</span><span class="sxs-lookup"><span data-stu-id="34324-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="34324-244">toorun wyszukiwany przy użyciu polecenia select hello</span><span class="sxs-lookup"><span data-stu-id="34324-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="34324-245">W polu Wyszukaj wpisz `Type=Event` , a następnie kliknij przycisk **wyszukiwania**.</span><span class="sxs-lookup"><span data-stu-id="34324-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="34324-246">Kliknij przycisk **+ Pokaż więcej** w jednym z tooview wyniki hello ma wszystkie właściwości hello, które hello wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="34324-247">Wybierz tych jawnie i hello zmiany zapytań za`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="34324-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="34324-248">![Wybierz wyszukiwanie](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="34324-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="34324-249">To polecenie jest szczególnie przydatne, gdy mają toocontrol wyszukiwania wyjściowy i wybierz tylko hello części danych, który znaczenia naprawdę podróży często nie jest pełną dokumentację hello.</span><span class="sxs-lookup"><span data-stu-id="34324-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="34324-250">Umożliwia to również mieć rekordów o różnych typach *niektórych* wspólnych właściwości, ale nie *wszystkie* ich właściwości są wspólne.</span><span class="sxs-lookup"><span data-stu-id="34324-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="34324-251">Generowanie danych wyjściowych, który wygląda tabeli w naturalnie więcej lub działa dobrze w przypadku, gdy eksportowany plik CSV tooa, a następnie sprasowany w programie Excel.</span><span class="sxs-lookup"><span data-stu-id="34324-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="34324-252">Użyj polecenia miary hello</span><span class="sxs-lookup"><span data-stu-id="34324-252">Use hello measure command</span></span>
<span data-ttu-id="34324-253">MIARA jest jednym z najbardziej wszechstronny polecenia hello w wyszukiwaniach analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="34324-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="34324-254">Umożliwia on tooapply statystyczne *funkcje* tooyour danych i wyników agregacji pogrupowane według danego pola.</span><span class="sxs-lookup"><span data-stu-id="34324-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="34324-255">Istnieje wiele funkcji statystycznych, które obsługuje miary.</span><span class="sxs-lookup"><span data-stu-id="34324-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="34324-256">Miara count()</span><span class="sxs-lookup"><span data-stu-id="34324-256">Measure count()</span></span>
<span data-ttu-id="34324-257">Witaj pierwszy toowork funkcji statystycznych z, a jedną toounderstand najprostszym hello jest hello *count()* funkcji.</span><span class="sxs-lookup"><span data-stu-id="34324-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="34324-258">Wynikiem każde zapytanie operacji wyszukiwania, takie jak `Type=Event`, pokazuje filtrów, nazywane również aspekty na powitania po lewej stronie wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="34324-259">filtry Hello pokazują rozkład wartości przy użyciu danego pola hello wyników w hello wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![liczba miar wyszukiwania](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="34324-261">Na przykład w hello obrazu powyżej, które będzie widoczny hello **komputera** pola i informuje, że w zdarzeniach prawie 739 tysięcy hello w wynikach hello, umożliwiają 68 unikatowe i różne wartości hello **komputera** pole w tych rekordów.</span><span class="sxs-lookup"><span data-stu-id="34324-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="34324-262">Kafelek Hello przedstawia tylko hello 5 pierwszych, które są hello najbardziej typowych 5 wartości, które są zapisywane w hello **komputera** pól), są posortowane według hello liczby dokumentów, które zawierają tej określonej wartości w tym polu.</span><span class="sxs-lookup"><span data-stu-id="34324-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="34324-263">W obrazie hello widać, — czy wśród tych zdarzeń prawie 369 tysięcy — tysięcy 90 pochodzi z komputera OpsInsights04.contoso.com hello, tysięcy 83 z hello DB03.contoso.com komputera i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="34324-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="34324-264">Co zrobić, jeśli chcesz toosee wszystkie wartości, ponieważ Kafelek hello przedstawia tylko hello tylko 5 pierwszych?</span><span class="sxs-lookup"><span data-stu-id="34324-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="34324-265">To miara bazowa hello polecenia można wykonać za pomocą funkcji count() hello.</span><span class="sxs-lookup"><span data-stu-id="34324-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="34324-266">Ta funkcja nie używa żadnych parametrów.</span><span class="sxs-lookup"><span data-stu-id="34324-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="34324-267">Wystarczy określić pole hello za pomocą którego chcesz toogroup — Witaj **komputera** pola w tym przypadku:</span><span class="sxs-lookup"><span data-stu-id="34324-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![liczba miar wyszukiwania](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="34324-269">Jednak **komputera** jest to pole używane *w* każdego z nich dane — obejmuje nie relacyjnych baz danych i nie istnieje żadne oddzielne **komputera** obiektów w dowolnym miejscu.</span><span class="sxs-lookup"><span data-stu-id="34324-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="34324-270">Po prostu hello wartości *w* hello danych można opisać jakiej encji wygenerowany je oraz wiele innych właściwości aspekty hello danych — dlatego hello termin *aspektu*.</span><span class="sxs-lookup"><span data-stu-id="34324-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="34324-271">Jednak równie dobrze można grupować według innych pól.</span><span class="sxs-lookup"><span data-stu-id="34324-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="34324-272">Ponieważ oryginalne wyniki hello prawie 739 tysięcy zdarzeń, które są przekazywane w potoku do polecenia miary hello również ma pole o nazwie **EventID**, można zastosować hello tego samego toogroup technika według tego pola i Pobierz liczbę zdarzeń przez identyfikator zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="34324-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="34324-273">Jeśli użytkownik nie chce hello rzeczywistego rekordu liczba, która zawiera konkretną wartość, ale zamiast tego, jeśli chcesz tylko listę hello wartości samodzielnie, możesz dodać *wybierz* polecenia na końcu hello go i po prostu wybierz hello pierwszej kolumny:</span><span class="sxs-lookup"><span data-stu-id="34324-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="34324-274">Następnie można uzyskać w bardziej skomplikowanych i wstępnie sortowanie wyników hello w zapytaniu hello lub wystarczy kliknąć hello kolumn w siatce hello zbyt.</span><span class="sxs-lookup"><span data-stu-id="34324-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="34324-275">toosearch za pomocą liczby miary</span><span class="sxs-lookup"><span data-stu-id="34324-275">toosearch using measure count</span></span>
* <span data-ttu-id="34324-276">W polu zapytania wyszukiwania hello wpisz`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="34324-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="34324-277">Dołącz `| Select EventID` toohello koniec hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="34324-278">Na koniec Dołącz `| Sort EventID asc` toohello koniec hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="34324-279">Istnieje kilka ważnych kwestii toonotice i wyróżnienie:</span><span class="sxs-lookup"><span data-stu-id="34324-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="34324-280">Po pierwsze hello wyniki będą nie są oryginalne nieprzetworzone wyniki hello już.</span><span class="sxs-lookup"><span data-stu-id="34324-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="34324-281">Zamiast tego są one wyników zagregowany — zasadniczo grup wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="34324-282">Nie jest to problem, ale należy pamiętać, że w przypadku interakcji z kształtem bardzo różnych danych, która różni się od hello oryginalnego raw kształtu, który jest tworzony na bieżąco hello wyniku funkcji agregacji/statystyczne hello.</span><span class="sxs-lookup"><span data-stu-id="34324-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="34324-283">Drugi, **pomiaru liczby** obecnie zwraca tylko hello top 100 wyników distinct.</span><span class="sxs-lookup"><span data-stu-id="34324-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="34324-284">To ograniczenie nie dotyczy toohello innych funkcji statystycznych.</span><span class="sxs-lookup"><span data-stu-id="34324-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="34324-285">Tak zazwyczaj należy toouse dokładniejsze toosearch pierwszy filtr dla określonych elementów przed zastosowaniem funkcji count() miary.</span><span class="sxs-lookup"><span data-stu-id="34324-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="34324-286">Użyj funkcji max i min hello za pomocą polecenia miary hello</span><span class="sxs-lookup"><span data-stu-id="34324-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="34324-287">Istnieją różne scenariusze gdzie **Max() miary** i **Min() miary** są przydatne.</span><span class="sxs-lookup"><span data-stu-id="34324-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="34324-288">Jednak ponieważ każdej funkcji jest przeciwny od siebie, możemy ilustrują Max() i możesz eksperymentować z Min() samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="34324-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="34324-289">Po wykonaniu zapytania do zdarzenia zabezpieczeń mają **poziom** właściwość, która może się różnić.</span><span class="sxs-lookup"><span data-stu-id="34324-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="34324-290">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-290">For example:</span></span>

```
Type=SecurityEvent
```

![start liczba miar wyszukiwania](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="34324-292">Jeśli chcesz tooview hello najwyższej wartości dla wszystkich zabezpieczeń hello zdarzenia danego komputera z programem, hello Grupuj według pola, możesz użyć</span><span class="sxs-lookup"><span data-stu-id="34324-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![Wyszukiwanie miary maksymalnej komputera](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="34324-294">Który będzie wyświetlany dla hello komputerów, które ma **poziom** rekordów, większość z nich ma co najmniej poziom 8, ma wiele poziom 16.</span><span class="sxs-lookup"><span data-stu-id="34324-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![Maksymalny czas miar wyszukiwania wygenerowany komputera](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="34324-296">Ta funkcja działa prawidłowo w przypadku liczb, ale współdziała również z pól daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="34324-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="34324-297">Ostatnio jest przydatne toocheck dla hello lub sygnatura czasowa ostatniej dowolne dane indeksowanym dla każdego komputera.</span><span class="sxs-lookup"><span data-stu-id="34324-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="34324-298">Na przykład: gdy został hello najnowszych zabezpieczeń zgłoszone zdarzenie dla każdej maszyny?</span><span class="sxs-lookup"><span data-stu-id="34324-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="34324-299">Funkcja avg hello za pomocą polecenia miary hello</span><span class="sxs-lookup"><span data-stu-id="34324-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="34324-300">Hello Avg() funkcji statystycznych używane z miarą umożliwia toocalculate hello średnią wartość niektóre pola, a grupy wyniki za hello w tym samym lub innym polu.</span><span class="sxs-lookup"><span data-stu-id="34324-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="34324-301">Jest to użyteczne w wielu przypadkach, takich jak dane dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="34324-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="34324-302">Zaczniemy dane dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="34324-302">We'll start with performance data.</span></span> <span data-ttu-id="34324-303">Należy pamiętać, że OMS aktualnie zbiera dane liczników wydajności dla systemu Windows i Linux maszyny.</span><span class="sxs-lookup"><span data-stu-id="34324-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="34324-304">toosearch dla *wszystkie* dane dotyczące wydajności, zapytanie najprostsze hello jest:</span><span class="sxs-lookup"><span data-stu-id="34324-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![wyszukiwanie start Śr.](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="34324-306">Witaj pierwszą rzeczą, którą można zauważyć jest czy analizy dzienników przedstawiono trzy perspektyw: lista, na której przedstawiono przedstawiającego rekordy rzeczywiste hello za hello na wykresach. Tabela, która przedstawia widok tabelaryczny danych licznika wydajności. i metryki, który wskazuje wykresów dla hello liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="34324-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="34324-307">Powyższy obraz powitania istnieją dwa zestawy pola oznaczone wskazujące hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="34324-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="34324-308">pierwszy zestaw Hello identyfikuje nazwę licznika wydajności systemu Windows, nazwa obiektu i nazwę wystąpienia w hello zapytania filtru.</span><span class="sxs-lookup"><span data-stu-id="34324-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="34324-309">Są to hello pola prawdopodobnie będą najczęściej używane jako aspekty/filtrów</span><span class="sxs-lookup"><span data-stu-id="34324-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="34324-310">**Równowartości** jest wartość rzeczywista hello hello licznika.</span><span class="sxs-lookup"><span data-stu-id="34324-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="34324-311">W tym przykładzie wartość hello jest *75*.</span><span class="sxs-lookup"><span data-stu-id="34324-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="34324-312">**TimeGenerated** jest 12:51 w formacie 24-godzinnym.</span><span class="sxs-lookup"><span data-stu-id="34324-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="34324-313">Oto widoku metryki hello na wykresie.</span><span class="sxs-lookup"><span data-stu-id="34324-313">Here's a view of hello metrics in a graph.</span></span>

![wyszukiwanie start Śr.](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="34324-315">Po informacji o hello wydajności rekordu kształtu, a o przeczytaj informacje o innych technik wyszukiwania można użyć miary Avg() tooaggregate ten typ danych liczbowych.</span><span class="sxs-lookup"><span data-stu-id="34324-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="34324-316">Poniżej przedstawiono prosty przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Wyszukaj samplevalue Śr.](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="34324-318">W tym przykładzie wybierz licznik wydajności hello łączny czas procesora CPU i średnia przez komputer.</span><span class="sxs-lookup"><span data-stu-id="34324-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="34324-319">Chcesz toonarrow dół hello tooonly Twojego wyniki ostatniego 6 godzin, można formant filtru czasu hello lub określ kwerendy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="34324-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="34324-320">za pomocą funkcji AVG. hello za pomocą polecenia miary hello toosearch</span><span class="sxs-lookup"><span data-stu-id="34324-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="34324-321">W polu zapytania wyszukiwania hello wpisz `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="34324-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="34324-322">Można zagregować i skorelować danych *między* komputerów.</span><span class="sxs-lookup"><span data-stu-id="34324-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="34324-323">Na przykład, załóżmy, że masz zestawu hostów w jakieś farmy, gdzie każdy węzeł jest taki sam tooany, drugi i one tylko do tego samego typu pracy i obciążenia powinien uwzględniać około powitalne wszystkie.</span><span class="sxs-lookup"><span data-stu-id="34324-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="34324-324">Można pobrać ich liczniki, które go w jednym z hello następujących zapytań i uzyskać średnie hello całej farmy.</span><span class="sxs-lookup"><span data-stu-id="34324-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="34324-325">Można uruchomić, wybierając hello komputerów z hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="34324-326">Teraz, gdy masz hello komputery mają również tylko tooselect dwa kluczowe wskaźniki wydajności (KPI): % użycia procesora CPU i % wolnego miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="34324-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="34324-327">Tak staje się części zapytania hello:</span><span class="sxs-lookup"><span data-stu-id="34324-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="34324-328">Teraz można dodać komputery i liczniki z hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="34324-329">Masz bardzo określonego zaznaczenia, dlatego hello **miar Avg()** polecenia przywrócić średnia hello nie na komputerze, ale w farmie hello, grupując przez CounterName.</span><span class="sxs-lookup"><span data-stu-id="34324-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="34324-330">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="34324-331">Zapewnia widok compact przydatne kilka kluczowych wskaźników wydajności w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="34324-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![Grupowanie avg wyszukiwania](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="34324-333">Łatwo za pomocą zapytania wyszukiwania hello w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="34324-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="34324-334">Na przykład można zapisać kwerendę wyszukiwania hello i utworzyć pulpit nawigacyjny z niego o nazwie *kluczowych wskaźników wydajności sieci Web farmy*.</span><span class="sxs-lookup"><span data-stu-id="34324-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="34324-335">toolearn więcej informacji na temat korzystania z pulpitów nawigacyjnych, zobacz [utworzyć niestandardowy pulpit nawigacyjny w analizy dzienników](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="34324-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![pulpit nawigacyjny avg wyszukiwania](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="34324-337">Funkcja sum hello za pomocą polecenia miary hello</span><span class="sxs-lookup"><span data-stu-id="34324-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="34324-338">Funkcja sum Hello jest podobne funkcje tooother hello miary polecenia.</span><span class="sxs-lookup"><span data-stu-id="34324-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="34324-339">Można zobaczyć przykład o jak toouse hello funkcja sum [Wyszukaj dzienniki IIS W3C w Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="34324-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="34324-340">Można użyć Max() i Min() z liczb, daty i godziny oraz ciągów tekstowych.</span><span class="sxs-lookup"><span data-stu-id="34324-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="34324-341">Ciągi tekstowe są posortowane alfabetycznie i uzyskać pierwszy i ostatni.</span><span class="sxs-lookup"><span data-stu-id="34324-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="34324-342">Jednak nie można używać Sum() z wyjątkiem pól wartości liczbowych.</span><span class="sxs-lookup"><span data-stu-id="34324-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="34324-343">Dotyczy to również tooAvg().</span><span class="sxs-lookup"><span data-stu-id="34324-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="34324-344">Użyj funkcji percentylu hello za pomocą polecenia miary hello</span><span class="sxs-lookup"><span data-stu-id="34324-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="34324-345">funkcja PERCENTYL Hello jest podobne tooAvg() i Sum() można używać tylko jego pól wartości liczbowych.</span><span class="sxs-lookup"><span data-stu-id="34324-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="34324-346">Można użyć dowolnego percentyl między 1 too99 na pola liczbowego.</span><span class="sxs-lookup"><span data-stu-id="34324-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="34324-347">Możesz także używać ich obu **percentyl** i **pct** poleceń.</span><span class="sxs-lookup"><span data-stu-id="34324-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="34324-348">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="34324-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="34324-349">Używaj hello, gdzie jest to polecenie</span><span class="sxs-lookup"><span data-stu-id="34324-349">Use hello where command</span></span>
<span data-ttu-id="34324-350">Witaj, gdy polecenie działa jak filtr, ale mogą być stosowane w filtrze toofurther potoku hello agregowana wyniki oferowanych przez polecenie miary — jako min. tooraw wyniki, które zostały przefiltrowane na początku hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="34324-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="34324-351">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="34324-352">Można dodać inny potoku "|" znaków i hello, gdzie tooonly polecenia uzyskać komputerów, których średnie wykorzystanie Procesora jest powyżej 80% z hello następujący przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="34324-353">Jeśli znasz program Microsoft System Center — Operations Manager można traktować hello w przypadku, gdy polecenia w zakresie pakietu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="34324-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="34324-354">Przykład Witaj, gdyby regułę, pierwsza część zapytania hello hello będzie hello źródła danych i hello gdzie polecenie będzie hello wykrywanie warunku.</span><span class="sxs-lookup"><span data-stu-id="34324-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="34324-355">Można użyć zapytania hello jako Kafelek **Mój pulpit nawigacyjny**, jako monitor sortuje, toosee, gdy komputer procesorów jest nadmiernie używany.</span><span class="sxs-lookup"><span data-stu-id="34324-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="34324-356">toolearn więcej informacji na temat pulpitów nawigacyjnych, zobacz [utworzyć niestandardowy pulpit nawigacyjny w analizy dzienników](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="34324-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="34324-357">Można również tworzyć i korzystać z pulpitów nawigacyjnych przy użyciu aplikacji mobilnej hello.</span><span class="sxs-lookup"><span data-stu-id="34324-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="34324-358">Aby uzyskać więcej informacji, zobacz [aplikacji mobilnej OMS ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="34324-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="34324-359">Kafelkach dolnej dwa hello powitania po obrazu, zawiera hello monitor wyświetlane listy, a liczba.</span><span class="sxs-lookup"><span data-stu-id="34324-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="34324-360">Zasadniczo należy zawsze ma numer toobe hello zero i hello toobe lista jest pusta.</span><span class="sxs-lookup"><span data-stu-id="34324-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="34324-361">W przeciwnym razie oznacza warunek alertu.</span><span class="sxs-lookup"><span data-stu-id="34324-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="34324-362">W razie potrzeby można użyć tootake spojrzeć na komputery, które są wykorzystanie.</span><span class="sxs-lookup"><span data-stu-id="34324-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![mobilnego pulpitu nawigacyjnego](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="34324-364">Użyj hello w operatorze</span><span class="sxs-lookup"><span data-stu-id="34324-364">Use hello in operator</span></span>
<span data-ttu-id="34324-365">Witaj *IN* operatora, wraz z *NOT IN* pozwala subsearches toouse, które są wyszukiwania, które zawierają inne wyszukiwania jako argument.</span><span class="sxs-lookup"><span data-stu-id="34324-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="34324-366">Znajdują się w nawiasy {}, w innym *głównej* lub *zewnętrzne* wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="34324-367">wynik Hello subsearch, często listę różne wyniki, następnie jest używany jako argument w jego wyszukiwania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="34324-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="34324-368">Możesz użyć subsearches toomatch podzestawy danych nie opisywane bezpośrednio w wyrażeniu wyszukiwania, ale mogą być generowane z wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="34324-369">Na przykład, jeśli interesuje Cię przy użyciu jednego toofind Wyszukaj wszystkie zdarzenia z *komputerów brakujących aktualizacji zabezpieczeń*, wówczas należy toodesign subsearch, która najpierw określi, że *komputerów brakujących aktualizacji zabezpieczeń*  przed znajdzie zdarzenia należące toothose hostów.</span><span class="sxs-lookup"><span data-stu-id="34324-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="34324-370">Tak, można express *komputerów aktualnie brakuje wymaganych aktualizacji zabezpieczeń* z hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="34324-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![W przykładzie wyszukiwania](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="34324-372">Po utworzeniu listy hello hello wyszukiwania można używać jako wewnętrzne wyszukiwania toofeed hello listę komputerów w zewnętrznym wyszukiwania (podstawowe), który będzie szukać zdarzenia dla tych komputerów.</span><span class="sxs-lookup"><span data-stu-id="34324-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="34324-373">W tym celu otaczającej hello wewnętrzny wyszukiwania w nawiasach klamrowych i podawania wyniki jako możliwych wartości filtru/pola wyszukiwania zewnętrzne hello przy użyciu operatora IN hello.</span><span class="sxs-lookup"><span data-stu-id="34324-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="34324-374">Zapytanie Hello będzie wyglądać:</span><span class="sxs-lookup"><span data-stu-id="34324-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![W przykładzie wyszukiwania](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="34324-376">Również powiadomienie hello czasu używany w hello wewnętrzny wyszukiwania, ponieważ filtr hello oceny aktualizacji systemu wykonuje migawkę wszystkich komputerów, co 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="34324-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="34324-377">Możesz wprowadzić hello wewnętrzny zapytania więcej lekkie i precyzyjne przez wyszukiwanie tylko jeden dzień.</span><span class="sxs-lookup"><span data-stu-id="34324-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="34324-378">zewnętrzne wyszukiwania Hello użyje hello czasu wyboru w interfejsie użytkownika hello, pobierania zdarzeń z hello ostatnich 7 dni.</span><span class="sxs-lookup"><span data-stu-id="34324-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="34324-379">Zobacz [operatorów logicznych](#boolean-operators) uzyskać więcej informacji o czasie operatorów.</span><span class="sxs-lookup"><span data-stu-id="34324-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="34324-380">Ponieważ użytkownik naprawdę tylko wyniki wyszukiwania wewnętrzny hello jako wartość filtru dla hello Użyj hello jednego zewnętrznego, można nadal stosować poleceń w hello zewnętrzne wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="34324-381">Na przykład można nadal hello grupy powyżej zdarzenia za pomocą innego polecenia miary:</span><span class="sxs-lookup"><span data-stu-id="34324-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![W przykładzie wyszukiwania](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="34324-383">Ogólnie rzecz biorąc ma tooexecute Twojego zapytania wewnętrzny szybko ponieważ analizy dzienników ma przekroczeń limitu czasu po stronie serwera dla go, a także tooreturn niewielką ilość wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="34324-384">Jeśli hello wewnętrzny zapytanie zwraca więcej wyników, listy wyników hello obcinana, który może powodować tooreturn zewnętrzne wyszukiwania hello niepoprawnych wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="34324-385">Inna reguła jest tego Wyszukaj wewnętrzny hello musi obecnie tooprovide *zagregowane* wyników.</span><span class="sxs-lookup"><span data-stu-id="34324-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="34324-386">Innymi słowy, musi ona zawierać *miary* polecenia; nie można obecnie źródła danych pierwotnych wyników w zewnętrznym wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="34324-387">Ponadto może istnieć tylko jeden operator IN oraz musi być hello filtr w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="34324-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="34324-388">Nie może mieć wielu operatorów w lub czy to zasadniczo uniemożliwia uruchomiony wielu subsearches: hello punkt jest tego tylko jeden wyszukiwania sub/wewnętrzny ważne jest możliwe każdego zewnętrzne wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="34324-389">Nawet w przypadku tych granic w umożliwia wielu rodzajów skorelowane wyszukiwania i umożliwia toodefine coś podobnego toogroups, takich jak komputery, użytkowników lub pliki — niezależnie od hello danych zawierają.</span><span class="sxs-lookup"><span data-stu-id="34324-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="34324-390">Poniżej przedstawiono więcej przykładów:</span><span class="sxs-lookup"><span data-stu-id="34324-390">Here are more examples:</span></span>

<span data-ttu-id="34324-391">**Wszystkie aktualizacje Brak z komputerów z wyłączonym ustawienie automatycznej aktualizacji**</span><span class="sxs-lookup"><span data-stu-id="34324-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="34324-392">**Wszystkie zdarzenia błędów z komputerów z uruchomionym programem SQL Server (=, którym dysponuje oceny SQL)**</span><span class="sxs-lookup"><span data-stu-id="34324-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="34324-393">**Wszystkie zdarzenia zabezpieczeń z komputerów, które są kontrolerami domeny (=, którym dysponuje oceny AD)**</span><span class="sxs-lookup"><span data-stu-id="34324-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="34324-394">**Które inne konta zalogowanych toohello samych komputerach, na którym konto BACONLAND\jochan zalogował się na?**</span><span class="sxs-lookup"><span data-stu-id="34324-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="34324-395">Użyj polecenia różne hello</span><span class="sxs-lookup"><span data-stu-id="34324-395">Use hello distinct command</span></span>
<span data-ttu-id="34324-396">Jak nazwa hello sugeruje, to polecenie zawiera listę różnych wartości dla pola.</span><span class="sxs-lookup"><span data-stu-id="34324-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="34324-397">Jest zaskakująco proste, ale bardzo przydatne.</span><span class="sxs-lookup"><span data-stu-id="34324-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="34324-398">Witaj, które same może zostać osiągnięty przy polecenia count() miary również, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="34324-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![Przykład polecenia różne wyszukiwania](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="34324-400">Jednak w przypadku wszystkich interesuje Cię tylko listę różne wartości i nie hello liczby dokumentów, których tej wartości, następnie DISTINCT zapewniają czyszczący i łatwiejsze tooread danych wyjściowych i krótszy składni, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="34324-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![Przykład polecenia różne wyszukiwania](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="34324-402">Funkcja countdistinct hello za pomocą polecenia miary hello</span><span class="sxs-lookup"><span data-stu-id="34324-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="34324-403">Funkcja countdistinct Hello zlicza hello unikatowe wartości w każdej grupie.</span><span class="sxs-lookup"><span data-stu-id="34324-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="34324-404">Na przykład można użyć toocount hello liczba unikatowych komputerów raportowania dla każdego typu:</span><span class="sxs-lookup"><span data-stu-id="34324-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![OMS countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="34324-406">Polecenie interwał hello miary</span><span class="sxs-lookup"><span data-stu-id="34324-406">Use hello measure interval command</span></span>
<span data-ttu-id="34324-407">Z niemal zbierania danych wydajności w czasie rzeczywistym, można zbierać i wizualizować wszystkie licznika wydajności w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="34324-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="34324-408">Po prostu wprowadzanie zapytania hello **typu: wydajności** zwróci tysiące metryki wykresów na podstawie liczby hello liczników i serwerów w środowisku analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="34324-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="34324-409">Z agregacją metryki na żądanie, można przyjrzeć się hello ogólną metryki w środowisku w wysokiego poziomu, a nowości w bardziej szczegółowe dane na potrzeby.</span><span class="sxs-lookup"><span data-stu-id="34324-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="34324-410">Załóżmy, że chcesz tooknow, co to jest hello średnie wykorzystanie Procesora na wszystkich komputerach.</span><span class="sxs-lookup"><span data-stu-id="34324-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="34324-411">Spojrzenie na powitania średnie wykorzystanie Procesora dla każdego komputera, może nie być pomocne ponieważ może pobrać wygładzania wyników. toolook do bardziej szczegółowe informacje, można zagregować wyników czasu mniejsze fragmenty okna i wyglądu do szeregów czasowych w różnych wymiarach.</span><span class="sxs-lookup"><span data-stu-id="34324-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="34324-412">Na przykład można wykonywać hello średniej godzinowej użycia procesora CPU na wszystkich komputerach w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="34324-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![Interwał średni miary](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="34324-414">Domyślnie te wyniki zostaną wyświetlone na wykresie wiersz interakcyjne wielu serii.</span><span class="sxs-lookup"><span data-stu-id="34324-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="34324-415">Ten wykres obsługuje serii przełączanie (z ponowne skalowanie osi y), powiększanie i kursora myszy.</span><span class="sxs-lookup"><span data-stu-id="34324-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="34324-416">opcję wyświetlania tabeli Hello jest wciąż dostępna na potrzeby przeglądania danych pierwotnych hello w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="34324-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="34324-417">Można także grupować według innych pól.</span><span class="sxs-lookup"><span data-stu-id="34324-417">You can also group by other fields.</span></span> <span data-ttu-id="34324-418">W tym przykładzie wyświetlane wszystkie liczniki % hello jednego określonego komputera, i chcesz się tooknow co to jest hello percentylu co godzinę 70 co licznika:</span><span class="sxs-lookup"><span data-stu-id="34324-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="34324-419">Jeden element toonote są te zapytania nie liczniki tooperformance ograniczone.</span><span class="sxs-lookup"><span data-stu-id="34324-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="34324-420">Można je stosować tooany metryki.</span><span class="sxs-lookup"><span data-stu-id="34324-420">You can apply them tooany metric.</span></span> <span data-ttu-id="34324-421">W tym przykładzie wyświetlane dzienniki programu IIS W3C.</span><span class="sxs-lookup"><span data-stu-id="34324-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="34324-422">Chcę tooknow co to jest hello maksymalny czas, który przejmuje on 5 minut do przetwarzania każdego żądania:</span><span class="sxs-lookup"><span data-stu-id="34324-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="34324-423">Użyj wielu wartości zagregowanych w jednym zapytaniu</span><span class="sxs-lookup"><span data-stu-id="34324-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="34324-424">Można określić wiele klauzul agregacji w poleceniu miary.</span><span class="sxs-lookup"><span data-stu-id="34324-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="34324-425">Każdy z nich można używać z aliasem niezależnie.</span><span class="sxs-lookup"><span data-stu-id="34324-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="34324-426">Jeśli nie zostanie podany, hello alias co nazwa pola będzie hello funkcji agregującej, która została użyta (tj. "avg(CounterValue)" jak avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="34324-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="34324-428">Oto inny przykład:</span><span class="sxs-lookup"><span data-stu-id="34324-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="34324-429">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34324-429">Next steps</span></span>
<span data-ttu-id="34324-430">Aby uzyskać dodatkowe informacje dziennika wyszukiwania zobacz:</span><span class="sxs-lookup"><span data-stu-id="34324-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="34324-431">Użyj [pola niestandardowe w analizy dzienników](log-analytics-custom-fields.md) tooextend dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="34324-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="34324-432">Przejrzyj hello [analizy dzienników dziennika odwołanie wyszukiwania](log-analytics-search-reference.md) tooview wszystkie hello wyszukiwania pól i aspektów, które są dostępne w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="34324-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
