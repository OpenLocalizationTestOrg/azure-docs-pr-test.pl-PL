---
title: "szczegółowe informacje o wydajności aaaQuery bazy danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Monitorowanie wydajności kwerendy identyfikuje hello większości używające Procesora zapytań dla bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="c1ba9-103">Wgląd wydajności kwerendy bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="c1ba9-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="c1ba9-104">Zarządzanie i dostrajania wydajności hello relacyjnych baz danych jest trudne zadanie, które wymaga znaczących wiedzę i czas inwestycji.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="c1ba9-105">Szczegółowe informacje o wydajności zapytań pozwala toospend mniej czasu Rozwiązywanie problemów z wydajnością bazy danych podając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="c1ba9-106">Bardziej szczegółowe informacje na temat użycia zasobów (bazy danych DTU) bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="c1ba9-107">Witaj najważniejszych zapytań przez Procesor/czas trwania/wykonywania licznik, który może potencjalnie dostroić zwiększonej wydajności.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="c1ba9-108">Witaj toodrill możliwości w dół do szczegółów hello zapytania, Wyświetl tekst i historii wykorzystania zasobów.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="c1ba9-109">Adnotacje, które zawierają akcje wykonywane przez dostrajania wydajności [doradcy bazy danych SQL Azure](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="c1ba9-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="c1ba9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c1ba9-110">Prerequisites</span></span>
* <span data-ttu-id="c1ba9-111">Szczegółowe informacje o wydajności wymaga, aby zapytania [magazyn zapytań](https://msdn.microsoft.com/library/dn817826.aspx) jest aktywny w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="c1ba9-112">Jeśli Magazyn zapytań nie jest uruchomiona, hello portal monit tooturn go.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="c1ba9-113">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="c1ba9-113">Permissions</span></span>
<span data-ttu-id="c1ba9-114">następujące Hello [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md) uprawnienia są wymagane toouse szczegółowe informacje o wydajności zapytań:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="c1ba9-115">**Czytnik**, **właściciela**, **współautora**, **Współautor bazy danych SQL**, lub **programu SQL Server współautora** uprawnienia są Wymagany zasób najwyższego hello tooview wykorzystywanie kwerend i wykresy.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="c1ba9-116">**Właściciel**, **współautora**, **Współautor bazy danych SQL**, lub **programu SQL Server współautora** tekst zapytania tooview wymagane są uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="c1ba9-117">Przy użyciu szczegółowe informacje o wydajności zapytań</span><span class="sxs-lookup"><span data-stu-id="c1ba9-117">Using Query Performance Insight</span></span>
<span data-ttu-id="c1ba9-118">Szczegółowe informacje o wydajności zapytań jest łatwe toouse:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="c1ba9-119">Otwórz [portalu Azure](https://portal.azure.com/) i Znajdź bazy danych, które mają tooexamine.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="c1ba9-120">Z menu po lewej stronie, w ramach pomocy technicznej i rozwiązywania problemów wybierz opcję "Szybkie szczegółowe informacje o wydajności zapytań".</span><span class="sxs-lookup"><span data-stu-id="c1ba9-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="c1ba9-121">Na pierwszej karcie hello Przejrzyj listę hello najważniejszych zapytań korzystanie z zasobów.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="c1ba9-122">Wybierz tooview określone zapytanie jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="c1ba9-123">Otwórz [doradcy bazy danych SQL Azure](sql-database-advisor.md) i sprawdź, czy wszystkie zalecenia są dostępne.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="c1ba9-124">Za pomocą suwaków lub powiększenie toochange ikony obserwowanych interwału.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![pulpit nawigacyjny wydajności](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="c1ba9-126">Po kilku godzinach danych musi toobe przechwycone przez Magazyn zapytań dla zapytania SQL Database tooprovide szczegółowe informacje o wydajności.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="c1ba9-127">Jeśli hello bazy danych nie ma aktywności lub magazyn zapytań był nieaktywny w przedziale czasu, wykresy hello będzie pusta podczas wyświetlania tego okresu.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="c1ba9-128">Mogą włączyć magazyn zapytań w dowolnym momencie, jeśli nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="c1ba9-129">Przejrzyj górny Procesora korzystanie z zapytań</span><span class="sxs-lookup"><span data-stu-id="c1ba9-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="c1ba9-130">W hello [portal](http://portal.azure.com) hello następujące:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="c1ba9-131">Przeglądaj tooa bazy danych SQL, a następnie kliknij przycisk **wszystkie ustawienia** > **pomocy technicznej i rozwiązywania problemów** > **szczegółowe informacje o wydajności zapytań**.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Szczegółowe informacje o wydajności zapytań][1]
   
    <span data-ttu-id="c1ba9-133">Otwiera widok najważniejszych zapytań Hello i hello najważniejszych Procesora zapytań odbierająca komunikaty są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="c1ba9-134">Kliknij przycisk wokół hello wykresu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-134">Click around hello chart for details.</span></span><br><span data-ttu-id="c1ba9-135">Hello pierwszego wiersza wyświetlane ogólnej % jednostek dtu w warstwie hello bazy danych, podczas gdy paski hello Pokaż używane przez zapytania hello wybrane interwale wybranego hello procent użycia procesora CPU (na przykład, jeśli **ostatni tydzień** wybrano każdy pasek reprezentuje jeden dzień).</span><span class="sxs-lookup"><span data-stu-id="c1ba9-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![najważniejszych zapytań][2]
   
    <span data-ttu-id="c1ba9-137">Siatka dolnej Hello reprezentuje zagregowane informacje hello widoczne zapytań.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="c1ba9-138">Identyfikator zapytania — Unikatowy identyfikator zapytania w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="c1ba9-139">Procesor zapytań interwale zauważalne (zależy od funkcji agregacji tabeli).</span><span class="sxs-lookup"><span data-stu-id="c1ba9-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="c1ba9-140">Czas trwania jednego zapytania (zależy od funkcji agregacji tabeli).</span><span class="sxs-lookup"><span data-stu-id="c1ba9-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="c1ba9-141">Całkowita liczba wykonaniami dla określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="c1ba9-142">Wybierz lub wyczyść tooinclude poszczególnych kwerend lub wykluczyć je z wykresu hello przy użyciu pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="c1ba9-143">W przypadku danych starych, kliknij przycisk hello **Odśwież** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="c1ba9-144">Za pomocą suwaków i przedziałach obserwacji toochange przycisków powiększenia i zbadaj nagłego: ![ustawienia](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="c1ba9-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="c1ba9-145">Opcjonalnie, jeśli chcesz inny widok, możesz zaznaczyć **niestandardowy** kartę i ustawić:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="c1ba9-146">Metryka (CPU, czas trwania, liczba wykonań)</span><span class="sxs-lookup"><span data-stu-id="c1ba9-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="c1ba9-147">Interwał czasu (ostatni tydzień ostatni miesiąc ostatnich 24 godzin).</span><span class="sxs-lookup"><span data-stu-id="c1ba9-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="c1ba9-148">Liczba zapytań.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-148">Number of queries.</span></span>
   * <span data-ttu-id="c1ba9-149">Funkcją agregacji.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-149">Aggregation function.</span></span>
     
     ![settings](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="c1ba9-151">Wyświetlanie szczegółów pojedynczych zapytań</span><span class="sxs-lookup"><span data-stu-id="c1ba9-151">Viewing individual query details</span></span>
<span data-ttu-id="c1ba9-152">Szczegóły kwerendy tooview:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-152">tooview query details:</span></span>

1. <span data-ttu-id="c1ba9-153">Kliknij każde zapytanie operacji hello listę najważniejszych zapytań.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-153">Click any query in hello list of top queries.</span></span>
   
    ![Szczegóły](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="c1ba9-155">Otwiera widok szczegółów Hello i liczba zużycie/czas trwania/wykonania Procesora kwerend hello dzieli się wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="c1ba9-156">Kliknij przycisk wokół hello wykresu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="c1ba9-157">Górny wykres pokazuje wiersza z ogólną % jednostek dtu w warstwie bazy danych i paski hello są używane przez wybrane zapytanie hello procent użycia procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="c1ba9-158">Drugi wykres przedstawia całkowity czas trwania przez wybrane zapytanie hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="c1ba9-159">Wykres dolnej pokazuje łączna liczba wykonań przez wybrane zapytanie hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![Szczegóły kwerendy][3]
4. <span data-ttu-id="c1ba9-161">Opcjonalnie, za pomocą suwaków, przyciski powiększania lub kliknij przycisk **ustawienia** toocustomize sposób wyświetlania danych zapytania lub toopick w innym czasie.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="c1ba9-162">Przejrzyj najważniejszych zapytań na czas trwania</span><span class="sxs-lookup"><span data-stu-id="c1ba9-162">Review top queries per duration</span></span>
<span data-ttu-id="c1ba9-163">Witaj najnowszych aktualizacji szczegółowe informacje o wydajności zapytań, wprowadzono dwie nowe metryki, które mogą ułatwić identyfikację wąskich gardeł: liczba czas trwania i wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="c1ba9-164">Kwerend mają potencjalnie największy hello blokowanie zasobów dłużej, blokowania innych użytkowników i ograniczanie skalowalności.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="c1ba9-165">Są one również hello najbardziej odpowiednich do optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="c1ba9-166">tooidentify długo działające kwerendy:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="c1ba9-167">Otwórz **niestandardowy** karcie szczegółowe informacje o wydajności zapytań dla wybranej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c1ba9-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="c1ba9-168">Zmień toobe metryki **czas trwania**</span><span class="sxs-lookup"><span data-stu-id="c1ba9-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="c1ba9-169">Wybierz liczbę zapytań i przedziałach obserwacji</span><span class="sxs-lookup"><span data-stu-id="c1ba9-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="c1ba9-170">Wybierz funkcję agregacji</span><span class="sxs-lookup"><span data-stu-id="c1ba9-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="c1ba9-171">**Suma** dodaje wszystkie czasu wykonywania zapytania interwału obserwacji całego.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="c1ba9-172">**Maksymalna liczba** znajduje zapytań, które czas wykonywania był maksymalna w przedziałach obserwacji całego.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="c1ba9-173">**Średni** znajduje Średni czas wykonania wszystkich zapytań wykonaniami i wyświetlić hello top poza te wartości.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![czas trwania kwerendy][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="c1ba9-175">Przejrzyj najważniejszych zapytań na liczba wykonania</span><span class="sxs-lookup"><span data-stu-id="c1ba9-175">Review top queries per execution count</span></span>
<span data-ttu-id="c1ba9-176">Wysoka liczba wykonań nie może mieć wpływ sama baza danych i użycia zasobów może być niski, ale może spowodować, że aplikacja ogólna powolne.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="c1ba9-177">W niektórych przypadkach wykonanie bardzo dużej liczby może prowadzić tooincrease sieci rund.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="c1ba9-178">Rund znacznie wpłynąć na wydajność.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="c1ba9-179">Są one podmiotu toonetwork opóźnienia i toodownstream opóźnienia serwera.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="c1ba9-180">Wiele witryn sieci Web opartych na danych dostęp silnie hello bazy danych, dla każdego żądania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="c1ba9-181">Podczas buforowania pomaga, hello połączeń zwiększenie ruchu sieciowego i obciążenie przetwarzaniem na powitania serwera bazy danych może niekorzystnie wpłynąć na wydajność.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="c1ba9-182">Ogólne porady jest tookeep round rund tooan absolutne minimum.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="c1ba9-183">tooidentify często wykonywane zapytania zapytań ("chatty"):</span><span class="sxs-lookup"><span data-stu-id="c1ba9-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="c1ba9-184">Otwórz **niestandardowy** karcie szczegółowe informacje o wydajności zapytań dla wybranej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c1ba9-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="c1ba9-185">Zmień toobe metryki **liczba wykonania**</span><span class="sxs-lookup"><span data-stu-id="c1ba9-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="c1ba9-186">Wybierz liczbę zapytań i przedziałach obserwacji</span><span class="sxs-lookup"><span data-stu-id="c1ba9-186">Select number of queries and observation interval</span></span>
   
    ![Liczba wykonania zapytania][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="c1ba9-188">Opis adnotacje dostrajania wydajności</span><span class="sxs-lookup"><span data-stu-id="c1ba9-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="c1ba9-189">Podczas eksploracji obciążenie w szczegółowe informacje o wydajności zapytań, można zauważyć ikon z pionowym wierszem na powitania wykresu.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="c1ba9-190">Te ikony są adnotacje; reprezentują wydajności wpływających na akcje wykonywane przez [doradcy bazy danych SQL Azure](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="c1ba9-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="c1ba9-191">Dzięki aktywowania adnotacji możesz uzyskać podstawowe informacje o akcji hello:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-191">By hovering annotation, you get basic information about hello action:</span></span>

![Adnotacja zapytania][6]

<span data-ttu-id="c1ba9-193">Jeśli chcesz tooknow więcej lub zastosować zalecenia usługi advisor, kliknij ikonę hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="c1ba9-194">Zostanie otwarty szczegóły akcji.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-194">It will open details of action.</span></span> <span data-ttu-id="c1ba9-195">Jeśli jest aktywny zalecenia można zastosować razu za pomocą polecenia.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![Szczegóły adnotacji kwerendy][7]

### <a name="multiple-annotations"></a><span data-ttu-id="c1ba9-197">Wiele adnotacji.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-197">Multiple annotations.</span></span>
<span data-ttu-id="c1ba9-198">Jest to możliwe, że z powodu poziomu powiększenia adnotacje tooeach Zamknij inne będzie pobrać zwinięte do jednego.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="c1ba9-199">To będą reprezentowane przez specjalnej ikony, klikając go zostanie otwarty nowy blok, gdy lista pogrupowanych adnotacje będą wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="c1ba9-200">Korelowanie zapytań i akcji dostrajania wydajności mogą pomóc toobetter zrozumieć obciążenie.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="c1ba9-201">Optymalizowanie konfiguracji magazynu zapytań hello, aby uzyskać szczegółowe informacje o wydajności zapytań</span><span class="sxs-lookup"><span data-stu-id="c1ba9-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="c1ba9-202">Podczas korzystania z szczegółowe informacje o wydajności zapytań mogą wystąpić następujące magazynu zapytań wiadomości powitania:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="c1ba9-203">"Magazyn zapytań nie jest prawidłowo skonfigurowany na tę bazę danych.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="c1ba9-204">Kliknij tutaj toolearn więcej".</span><span class="sxs-lookup"><span data-stu-id="c1ba9-204">Click here toolearn more."</span></span>
* <span data-ttu-id="c1ba9-205">"Magazyn zapytań nie jest prawidłowo skonfigurowany na tę bazę danych.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="c1ba9-206">Kliknij tutaj ustawienia toochange".</span><span class="sxs-lookup"><span data-stu-id="c1ba9-206">Click here toochange settings."</span></span> 

<span data-ttu-id="c1ba9-207">Komunikaty te są zwykle widoczne, gdy magazyn zapytań nie jest możliwe toocollect nowych danych.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="c1ba9-208">Pierwszym przypadku się stanie, jeśli magazyn zapytań jest w stanie tylko do odczytu i parametry zostały ustawione optymalnie.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="c1ba9-209">Można temu zaradzić przez zwiększenie rozmiaru magazynu zapytań lub wyczyszczenie magazynu zapytań.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![przycisk qds][8]

<span data-ttu-id="c1ba9-211">Drugim przypadku się stanie, jeśli magazyn zapytań jest wyłączony lub parametry nie są ustawione optymalnie.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="c1ba9-212">Witaj przechowywania i przechwytywania zasad i Włącz magazyn zapytań można zmienić, wykonując poniższe polecenia lub bezpośrednio z portalu:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![przycisk qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="c1ba9-214">Zalecane zasady przechowywania i przechwytywania</span><span class="sxs-lookup"><span data-stu-id="c1ba9-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="c1ba9-215">Istnieją dwa typy zasad przechowywania:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="c1ba9-216">Na podstawie rozmiaru — po osiągnięciu tooAUTO zestaw zostanie czyszczenia automatycznie prawie maksymalny rozmiar danych.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="c1ba9-217">Czas na podstawie — domyślnie możemy zostanie ustawiony too30 dni, co oznacza, że, jeśli magazyn zapytań zabraknie miejsca, spowoduje to usunięcie zapytania o informacje o starsze niż 30 dni</span><span class="sxs-lookup"><span data-stu-id="c1ba9-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="c1ba9-218">Przechwyć można ustawić zasady:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="c1ba9-219">**Wszystkie** -przechwytuje wszystkie zapytania.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="c1ba9-220">**Automatycznie** -rzadkim zapytania i zapytania z nieznaczne czas trwania kompilacji i wykonywanie zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="c1ba9-221">Wewnętrznie zależą progi czas wykonywania liczby, kompilacji i środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="c1ba9-222">Jest to opcja domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-222">This is hello default option.</span></span>
* <span data-ttu-id="c1ba9-223">**Brak** — magazyn zapytań zatrzymuje przechwytywanie nowego zapytania, jednak Statystyka środowiska uruchomieniowego już przechwyconych zapytania są nadal zbierane.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="c1ba9-224">Firma Microsoft zaleca ustawienie wszystkich tooAUTO zasad i wyczyść zasad too30 dni:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="c1ba9-225">Zwiększ rozmiar magazynu zapytań.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-225">Increase size of Query Store.</span></span> <span data-ttu-id="c1ba9-226">Może to być wykonywane przez łączącego tooa bazę danych i wystawiających następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="c1ba9-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="c1ba9-227">Stosowanie tych ustawień spowoduje ostatecznie magazynu zapytań zbieranie nowego zapytania, jednak jeśli nie chcesz toowait można wyczyścić magazyn zapytań.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="c1ba9-228">Wykonywanie zapytania następujące spowoduje usunięcie wszystkich bieżących informacji w hello magazynu zapytań.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="c1ba9-229">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c1ba9-229">Summary</span></span>
<span data-ttu-id="c1ba9-230">Szczegółowe informacje o wydajności zapytań ułatwia zrozumienie wpływu hello obciążenia zapytania i jego powiązań toodatabase zużycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="c1ba9-231">W przypadku tej funkcji będzie informacje o hello zapytania zużywające najwięcej zasobów i łatwo zidentyfikować toofix hello z nich, zanim staną się problem.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1ba9-232">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1ba9-232">Next steps</span></span>
<span data-ttu-id="c1ba9-233">Aby uzyskać dodatkowe zalecenia dotyczące poprawy wydajności hello bazy danych SQL, kliknij [zalecenia](sql-database-advisor.md) na powitania **szczegółowe informacje o wydajności zapytań** bloku.</span><span class="sxs-lookup"><span data-stu-id="c1ba9-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

![Doradca wydajności](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

