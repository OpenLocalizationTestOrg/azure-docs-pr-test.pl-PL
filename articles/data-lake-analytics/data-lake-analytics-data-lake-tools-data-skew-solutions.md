---
title: "aaaResolve problemów zegara danych za pomocą usługi Azure Data Lake Tools dla programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Potencjalne rozwiązania problemów zegara danych za pomocą usługi Azure Data Lake Tools dla programu Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="1cde2-103">Rozwiązywanie problemów zegara danych za pomocą usługi Azure Data Lake Tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1cde2-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="1cde2-104">Co to są dane pochylanie?</span><span class="sxs-lookup"><span data-stu-id="1cde2-104">What is data skew?</span></span>

<span data-ttu-id="1cde2-105">Krótko już wspomniano, Pochylenie danych jest nadmiernie reprezentowanego wartością.</span><span class="sxs-lookup"><span data-stu-id="1cde2-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="1cde2-106">Załóżmy, że została przypisana 50 ekspertami podatku deklaracji podatkowych tooaudit, jeden egzaminator dla każdego stanu Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="1cde2-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="1cde2-107">Egzaminator Wyoming Hello, ponieważ hello wypełniania jest mały, ma małego toodo.</span><span class="sxs-lookup"><span data-stu-id="1cde2-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="1cde2-108">W Kalifornijskiej jednak egzaminator hello jest przechowywana bardzo zajęty z powodu dużej populacji hello stanu.</span><span class="sxs-lookup"><span data-stu-id="1cde2-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="1cde2-109">![Przykład danych zegara problemu](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="1cde2-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="1cde2-110">W naszym scenariuszu danych hello nierównomiernie obejmowała wszystkie ekspertami podatku, co oznacza, że niektóre ekspertami musi działać więcej niż inne.</span><span class="sxs-lookup"><span data-stu-id="1cde2-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="1cde2-111">W własne stanowisko często występują sytuacjach, takich jak hello egzaminator podatku w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1cde2-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="1cde2-112">W sposób bardziej technicznych jednego wierzchołka pobiera znacznie więcej danych niż jego elementów równorzędnych sytuacji, która sprawia, że wierzchołków hello działać więcej niż hello inne osoby i który ostatecznie spowalnia całego zadania.</span><span class="sxs-lookup"><span data-stu-id="1cde2-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="1cde2-113">Co to jest gorsza, hello zadania może się nie powieść, ponieważ wierzchołków może być, na przykład ograniczenie 5-godzinnym środowiska uruchomieniowego i ograniczenie 6 GB pamięci.</span><span class="sxs-lookup"><span data-stu-id="1cde2-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="1cde2-114">Rozwiązywanie problemów z danych zegara</span><span class="sxs-lookup"><span data-stu-id="1cde2-114">Resolving data-skew problems</span></span>

<span data-ttu-id="1cde2-115">Azure Data Lake Tools dla programu Visual Studio może pomóc wykryć, czy zadanie ma problem zegara danych.</span><span class="sxs-lookup"><span data-stu-id="1cde2-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="1cde2-116">Jeśli istnieje problem, można rozwiązać go za pomocą rozwiązań hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1cde2-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="1cde2-117">Rozwiązanie 1: Poprawić, Partycjonowanie tabel</span><span class="sxs-lookup"><span data-stu-id="1cde2-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="1cde2-118">Opcja 1: Hello filtru niesymetryczna wartość klucza z wyprzedzeniem</span><span class="sxs-lookup"><span data-stu-id="1cde2-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="1cde2-119">Jeśli nie ma ona wpływu na logice biznesowej, można filtrować hello wyższa częstotliwość wartości z wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="1cde2-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="1cde2-120">Na przykład jeśli istnieje wiele 000 000 000 w kolumnie identyfikator GUID, nie możesz tooaggregate tej wartości.</span><span class="sxs-lookup"><span data-stu-id="1cde2-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="1cde2-121">Przed agregacji, można wpisać "WHERE GUID! ="ruch 000 000 000"" toofilter hello wysokiej częstotliwości wartość.</span><span class="sxs-lookup"><span data-stu-id="1cde2-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="1cde2-122">Opcja 2: Wybierz inny klucz partycji lub dystrybucji</span><span class="sxs-lookup"><span data-stu-id="1cde2-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="1cde2-123">W hello poprzedzających przykład jeśli chcesz tylko toocheck hello inspekcji podatku obciążenia wszystkie za pośrednictwem hello kraju, hello danych dystrybucji można zwiększyć, wybierając numer identyfikacyjny hello jako klucz.</span><span class="sxs-lookup"><span data-stu-id="1cde2-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="1cde2-124">Pobrania różnych partycji lub klucza dystrybucji można czasami dystrybucji hello danych bardziej równomiernie, ale należy się upewnić, że ten wybór nie ma wpływu na logice biznesowej toomake.</span><span class="sxs-lookup"><span data-stu-id="1cde2-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="1cde2-125">Na przykład toocalculate hello podatku Suma dla każdego stanu może być toodesignate _stanu_ jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="1cde2-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="1cde2-126">Jeśli będziesz kontynuować tooexperience ten problem, spróbuj użyć opcja 3.</span><span class="sxs-lookup"><span data-stu-id="1cde2-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="1cde2-127">Opcja 3: Dodaj więcej partycji lub dystrybucji kluczy</span><span class="sxs-lookup"><span data-stu-id="1cde2-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="1cde2-128">Zamiast używać tylko _stanu_ jako klucza partycji, można użyć więcej niż jednego klucza do partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="1cde2-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="1cde2-129">Na przykład, Rozważ dodanie _kod POCZTOWY_ jako dodatkowa partycja partycji danych klucza tooreduce rozmiary i bardziej równomierne hello danych.</span><span class="sxs-lookup"><span data-stu-id="1cde2-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="1cde2-130">Opcja 4: Użycie rozdzielanie</span><span class="sxs-lookup"><span data-stu-id="1cde2-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="1cde2-131">Jeśli nie możesz znaleźć odpowiedniego klucza partycji i dystrybucji, można spróbować rozdzielaniem toouse.</span><span class="sxs-lookup"><span data-stu-id="1cde2-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="1cde2-132">Rozdzielanie traktuje wszystkie wiersze jednakowo i losowo umieszcza je w odpowiednich zasobników.</span><span class="sxs-lookup"><span data-stu-id="1cde2-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="1cde2-133">pobiera równomiernego Hello danych, ale utraty miejscowości informacji zwrotnych, może również zmniejszyć wydajność zadania dla niektórych operacji.</span><span class="sxs-lookup"><span data-stu-id="1cde2-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="1cde2-134">Ponadto, jeśli mimo to czynności agregacji dla klucza spowodowałoby zafałszowanie hello hello zegara danych problem zostanie będzie się powtarzał.</span><span class="sxs-lookup"><span data-stu-id="1cde2-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="1cde2-135">toolearn więcej informacji na temat rozdzielanie, zobacz dystrybucje tabeli U-SQL hello sekcji [CREATE TABLE (U-SQL): Tworzenie tabeli ze schematem](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="1cde2-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="1cde2-136">2 — rozwiązanie: Poprawy hello planu zapytania</span><span class="sxs-lookup"><span data-stu-id="1cde2-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="1cde2-137">Opcja 1: Użycie instrukcji CREATE STATISTICS hello</span><span class="sxs-lookup"><span data-stu-id="1cde2-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="1cde2-138">U-SQL zawiera instrukcję CREATE STATISTICS hello w tabelach.</span><span class="sxs-lookup"><span data-stu-id="1cde2-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="1cde2-139">Ta instrukcja daje więcej Optymalizator zapytań toohello informacji o hello właściwości danych, np. rozkład wartości, które są przechowywane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="1cde2-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="1cde2-140">Dla większości zapytań Optymalizator zapytań hello generuje już hello statystyki niezbędne dla planu zapytania wysokiej jakości.</span><span class="sxs-lookup"><span data-stu-id="1cde2-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="1cde2-141">Czasami może być konieczne tooimprove wydajność zapytań, tworząc dodatkowe statystyki z instrukcji CREATE STATISTICS lub modyfikując hello projektu zapytania.</span><span class="sxs-lookup"><span data-stu-id="1cde2-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="1cde2-142">Aby uzyskać więcej informacji, zobacz hello [instrukcji CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="1cde2-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="1cde2-143">Przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="1cde2-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="1cde2-144">Statystyki informacje nie są automatycznie aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="1cde2-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="1cde2-145">Po zaktualizowaniu hello dane w tabeli bez ponownego utworzenia statystyki hello może zmniejszyć wydajność kwerend hello.</span><span class="sxs-lookup"><span data-stu-id="1cde2-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="1cde2-146">Opcja 2: Użycie SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="1cde2-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="1cde2-147">Jeśli chcesz toosum hello podatkowych dla każdego stanu, należy użyć Grupuj według stanu, metody, która nie uniknąć hello zegara danych.</span><span class="sxs-lookup"><span data-stu-id="1cde2-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="1cde2-148">Jednak może podać wskazówkę danych w tooidentify Twojego zapytania, które danych pochylanie w kluczach, dzięki czemu Optymalizator hello można przygotować plan wykonania.</span><span class="sxs-lookup"><span data-stu-id="1cde2-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="1cde2-149">Zazwyczaj można ustawić parametru hello jako 0,5 i 1, 0,5 oznacza nie dużo zegara duże znaczenie pochylenia i 1.</span><span class="sxs-lookup"><span data-stu-id="1cde2-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="1cde2-150">Ponieważ wskazówka hello wpływa na plan wykonania optymalizacji dla bieżącej instrukcji hello i wszystkie podrzędne instrukcje, należy się wskazówka hello tooadd przed hello potencjalne niesymetryczna key-wise agregacji.</span><span class="sxs-lookup"><span data-stu-id="1cde2-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="1cde2-151">Przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="1cde2-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="1cde2-152">Opcja 3: Użycie ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="1cde2-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="1cde2-153">Ponadto tooSKEWFACTOR dla określonych niesymetryczna klucza join przypadków, jeśli wiadomo, że hello innych zestawu wierszy sprzężonych jest mały, można ustawić Optymalizator hello przez dodanie wskazówkę liczby wierszy w instrukcji U-SQL hello przed sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="1cde2-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="1cde2-154">W ten sposób Optymalizator można wybrać toohelp strategii emisji sprzężenia zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="1cde2-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="1cde2-155">Należy pamiętać, ROWCOUNT nie rozwiązania problemu zegara danych hello, że można zaoferować niektórych uzyskać dodatkową pomoc.</span><span class="sxs-lookup"><span data-stu-id="1cde2-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="1cde2-156">Przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="1cde2-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="1cde2-157">Rozwiązanie 3: Poprawa hello reduktor zdefiniowane przez użytkownika i łączenia</span><span class="sxs-lookup"><span data-stu-id="1cde2-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="1cde2-158">Czasami może zapisywać toodeal zdefiniowanego przez użytkownika, z logiką skomplikowany proces i dobrze napisane reduktor i łączenia może ograniczyć problem zegara danych w niektórych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="1cde2-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="1cde2-159">Opcja 1: Użycie reduktor rekursywny, jeśli to możliwe</span><span class="sxs-lookup"><span data-stu-id="1cde2-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="1cde2-160">Domyślnie reduktor zdefiniowane przez użytkownika jest uruchamiana w trybie niecykliczne, co oznacza, że zmniejszyć pracy dla klucza jest dystrybuowana do jednego wierzchołka.</span><span class="sxs-lookup"><span data-stu-id="1cde2-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="1cde2-161">Jednak jeśli danych jest niesymetryczna, hello dużych zestawów danych może być przetwarzane w jednym wierzchołka i uruchom przez długi czas.</span><span class="sxs-lookup"><span data-stu-id="1cde2-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="1cde2-162">wydajność tooimprove, można dodać atrybutu w Twojej kodu toodefine reduktor toorun w trybie cykliczne.</span><span class="sxs-lookup"><span data-stu-id="1cde2-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="1cde2-163">Następnie hello dużych zestawów danych można wierzchołków toomultiple rozproszone i uruchom równolegle, co przyspiesza swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="1cde2-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="1cde2-164">toochange toorecursive reduktor niecykliczne należy toomake się, że Twoje algorytm asocjacyjnej.</span><span class="sxs-lookup"><span data-stu-id="1cde2-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="1cde2-165">Na przykład Suma hello jest asocjacyjnej i medianę hello nie jest.</span><span class="sxs-lookup"><span data-stu-id="1cde2-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="1cde2-166">Należy się upewnić, że hello danych wejściowych i wyjściowych dla reduktor zachować hello toomake tego samego schematu.</span><span class="sxs-lookup"><span data-stu-id="1cde2-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="1cde2-167">Atrybut reduktor cykliczne:</span><span class="sxs-lookup"><span data-stu-id="1cde2-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="1cde2-168">Przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="1cde2-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="1cde2-169">Opcja 2: W trybie łączenia na poziomie wiersza, jeśli to możliwe</span><span class="sxs-lookup"><span data-stu-id="1cde2-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="1cde2-170">Wskazówki ROWCOUNT podobne toohello przypadków określonego klucza niesymetryczna sprzężenia, tryb łączenia próbuje toodistribute wartość klucza niesymetryczna ogromnych zestawów toomultiple wierzchołków tak, aby hello pracy mogą być wykonywane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="1cde2-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="1cde2-171">Tryb łączenia nie można rozpoznać danych zegara problemów, ale mogą oferować niektórych uzyskać dodatkową pomoc na wartość klucza niesymetryczna ogromnych zestawów.</span><span class="sxs-lookup"><span data-stu-id="1cde2-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="1cde2-172">Domyślnie tryb łączenia hello jest pełny, co oznacza, że hello pozostałych zestawu wierszy i prawego wiersza zestawu nie mogą być oddzielone.</span><span class="sxs-lookup"><span data-stu-id="1cde2-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="1cde2-173">Ustawianie trybu hello jako wewnętrzny/prawej/lewej umożliwia sprzężenia na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="1cde2-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="1cde2-174">Hello system oddziela hello odpowiednich zestawów wierszy i rozpowszechnia je do wielu wierzchołków, które są uruchamiane równolegle.</span><span class="sxs-lookup"><span data-stu-id="1cde2-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="1cde2-175">Jednak przed skonfigurowaniem trybie łączenia hello należy zachować ostrożność, że mogą być oddzielone tooensure, który hello odpowiednich zestawów wierszy.</span><span class="sxs-lookup"><span data-stu-id="1cde2-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="1cde2-176">przykład Witaj, który następuje zawiera zestaw rozdzielonych wiersza po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1cde2-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="1cde2-177">Każdy wiersz danych wyjściowych zależy pojedynczy wiersz wejściowych od lewej hello oraz potencjalnie zależy od wszystkich wierszy z hello prawo z hello takie same wartości klucza.</span><span class="sxs-lookup"><span data-stu-id="1cde2-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="1cde2-178">Po ustawieniu trybu łączenia powitania od lewej systemu hello oddziela hello ogromnych lewej-zestawu wierszy w małych sieci i przypisuje je toomultiple wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="1cde2-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Ilustracja trybie łączenia](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="1cde2-180">Jeśli ustawisz hello łączenia nieprawidłowy tryb kombinacja hello jest mniej wydajne i hello wyniki mogą być nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="1cde2-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="1cde2-181">Atrybuty trybu łączenia:</span><span class="sxs-lookup"><span data-stu-id="1cde2-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="1cde2-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): W pojedynczym wierszu wejściowych od lewej hello zależy od każdego wiersza danych wyjściowych (i potencjalnie wszystkie wiersze z tabeli hello prawo z hello sama wartość klucza).</span><span class="sxs-lookup"><span data-stu-id="1cde2-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="1cde2-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z prawej hello (i potencjalnie wszystkie wiersze z tabeli po lewej hello z hello sama wartość klucza).</span><span class="sxs-lookup"><span data-stu-id="1cde2-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="1cde2-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Każdy wiersz danych wyjściowych jest zależna od pojedynczy wiersz wejściowych z lewej hello i hello prawo z hello takie same wartości.</span><span class="sxs-lookup"><span data-stu-id="1cde2-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="1cde2-185">Przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="1cde2-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
