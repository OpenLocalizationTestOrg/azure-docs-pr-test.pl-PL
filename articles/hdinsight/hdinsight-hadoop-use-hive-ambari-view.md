---
title: "toowork widoków Ambari aaaUse z Hive w usłudze Azure HDInsight (Hadoop) - | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Hive View zapytań Hive toosubmit przeglądarki sieci web. Witaj Hive View jest częścią hello podane w interfejsie użytkownika sieci Web Ambari z klastrem usługi HDInsight opartej na systemie Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="3c609-104">Użyj hello widoku Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c609-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="3c609-105">Dowiedz się, jak toorun Hive zapytania przy użyciu widoku Hive narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="3c609-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="3c609-106">Ambari to zarządzania i monitorowania narzędzia dostarczanego z klastrami HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="3c609-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="3c609-107">Jedną z funkcji hello zapewniana za pomocą narzędzia Ambari jest interfejsem użytkownika sieci Web, które mogą być używane toorun zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3c609-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="3c609-108">Ambari ma wiele funkcji, które nie zostały omówione w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="3c609-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="3c609-109">Aby uzyskać więcej informacji, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari hello](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="3c609-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c609-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3c609-110">Prerequisites</span></span>

* <span data-ttu-id="3c609-111">Klaster usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="3c609-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="3c609-112">Aby uzyskać informacje dotyczące tworzenia klastra, zobacz [Rozpoczynanie pracy z opartą na systemie Linux usługą HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3c609-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c609-113">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="3c609-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3c609-114">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3c609-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3c609-115">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="3c609-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="3c609-116">Otwórz widok Hive hello</span><span class="sxs-lookup"><span data-stu-id="3c609-116">Open hello Hive view</span></span>

<span data-ttu-id="3c609-117">Można widoków Ambari z hello portal Azure. Wybierz z klastrem usługi HDInsight, a następnie wybierz **widoków Ambari** z hello **szybkie linki** sekcji.</span><span class="sxs-lookup"><span data-stu-id="3c609-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![Sekcja Szybkie linki hello portalu](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="3c609-119">Z listy hello widoków, wybierz hello __Hive View__.</span><span class="sxs-lookup"><span data-stu-id="3c609-119">From hello list of views, select hello __Hive View__.</span></span>

![Witaj wybrany widok gałęzi](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="3c609-121">Podczas uzyskiwania dostępu do Ambari, to zostanie wyświetlony monit o tooauthenticate toohello lokacji.</span><span class="sxs-lookup"><span data-stu-id="3c609-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="3c609-122">Wprowadź Witaj, Administratorze (domyślna `admin`) konta, nazwę i hasło używane podczas tworzenia hello klastra.</span><span class="sxs-lookup"><span data-stu-id="3c609-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="3c609-123">Powinny pojawić się Strona toohello podobne, po obrazu:</span><span class="sxs-lookup"><span data-stu-id="3c609-123">You should see a page similar toohello following image:</span></span>

![Obraz powitania zapytania arkusza hello Hive widoku](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="3c609-125"><a name="hivequery"></a>Uruchamianie zapytania</span><span class="sxs-lookup"><span data-stu-id="3c609-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="3c609-126">toorun zapytań programu hive za pomocą poniższych kroków z widoku Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="3c609-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="3c609-127">Z hello __zapytania__ karcie, Wklej hello następujące instrukcje HiveQL do arkusza hello:</span><span class="sxs-lookup"><span data-stu-id="3c609-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="3c609-128">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="3c609-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="3c609-129">`DROP TABLE`— Usuwa tabeli hello i hello pliku danych, w przypadku, gdy tabela hello już istnieje.</span><span class="sxs-lookup"><span data-stu-id="3c609-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="3c609-130">`CREATE EXTERNAL TABLE`-Tworzy nową tabelę "external" w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="3c609-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="3c609-131">Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="3c609-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="3c609-132">Hello danych pozostaje w hello oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3c609-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="3c609-133">`ROW FORMAT`— Sposób formatowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="3c609-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="3c609-134">W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="3c609-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="3c609-135">`STORED AS TEXTFILE LOCATION`-Miejsce przechowywania danych hello i że jest przechowywane jako tekst.</span><span class="sxs-lookup"><span data-stu-id="3c609-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="3c609-136">`SELECT`-Wybiera liczbę wszystkich wierszy, gdzie t4 kolumna zawiera wartość hello [Błąd].</span><span class="sxs-lookup"><span data-stu-id="3c609-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="3c609-137">Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="3c609-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="3c609-138">Na przykład automatyczne przekazywanie danych proces, lub przez inną operację MapReduce.</span><span class="sxs-lookup"><span data-stu-id="3c609-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="3c609-139">Usunięcie tabeli zewnętrznej jest *nie* usunąć dane hello, tylko hello definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="3c609-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3c609-140">Pozostaw hello __bazy danych__ zaznaczenie na __domyślne__.</span><span class="sxs-lookup"><span data-stu-id="3c609-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="3c609-141">Przykłady Hello w tym dokumencie Użyj hello domyślna baza danych uwzględnionych w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c609-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="3c609-142">toostart hello zapytania, użyj hello **Execute** znajdujący się poniżej hello arkusza.</span><span class="sxs-lookup"><span data-stu-id="3c609-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="3c609-143">Monitor przechodzi w stan pomarańczowy i hello tekst zostanie zmieniony zbyt**zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="3c609-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="3c609-144">Po zakończeniu hello zapytania, hello **wyniki** karcie są wyświetlane wyniki hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="3c609-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="3c609-145">powitania po tekst jest wynikiem hello hello zapytania:</span><span class="sxs-lookup"><span data-stu-id="3c609-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="3c609-146">Witaj **dzienniki** karty mogą być używane tooview hello rejestrowanie informacji o utworzonych przez zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="3c609-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="3c609-147">Witaj **Zapisz wyniki** okno dialogowe listy rozwijanej w hello górnym lewym rogu hello **wyniki przetwarzania zapytania** sekcji pozwala toodownload lub zapisać wyniki.</span><span class="sxs-lookup"><span data-stu-id="3c609-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="3c609-148">Wybierz hello pierwsze cztery wiersze tego zapytania, następnie wybierz **Execute**.</span><span class="sxs-lookup"><span data-stu-id="3c609-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="3c609-149">Zwróć uwagę, że nie ma żadnych wyników po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="3c609-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="3c609-150">Przy użyciu hello **Execute** gdy część zapytania hello zaznaczona jest tylko uruchamia hello wybranego instrukcje.</span><span class="sxs-lookup"><span data-stu-id="3c609-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="3c609-151">W takim przypadku hello zaznaczenia nie włączono hello końcowej instrukcji, która pobiera wiersze z tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="3c609-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="3c609-152">Po wybraniu tylko ten wiersz i użyj **Execute**, powinny pojawić się hello oczekiwano wyników.</span><span class="sxs-lookup"><span data-stu-id="3c609-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="3c609-153">tooadd arkusza, użyj hello **nowy arkusz** u dołu hello hello **edytora zapytań**.</span><span class="sxs-lookup"><span data-stu-id="3c609-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="3c609-154">W nowym arkuszu hello wprowadź następujące instrukcje HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="3c609-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="3c609-155">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="3c609-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="3c609-156">**Utwórz Tabela Jeśli nie ISTNIEJE** — tworzy tabelę, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="3c609-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="3c609-157">Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używana, jest tworzony wewnętrznej tabeli.</span><span class="sxs-lookup"><span data-stu-id="3c609-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="3c609-158">Wewnętrznej tabeli są przechowywane w magazynie danych Hive hello i zarządza całkowicie Hive.</span><span class="sxs-lookup"><span data-stu-id="3c609-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="3c609-159">W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli usuwa hello również danych źródłowych.</span><span class="sxs-lookup"><span data-stu-id="3c609-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="3c609-160">**ORC AS PRZECHOWYWANE** -przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC).</span><span class="sxs-lookup"><span data-stu-id="3c609-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="3c609-161">ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.</span><span class="sxs-lookup"><span data-stu-id="3c609-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="3c609-162">**ZASTĄP INSERT... Wybierz** -wybiera wiersze z hello **log4jLogs** tabeli, która zawiera `[ERROR]`, a następnie hello wstawia dane do hello **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="3c609-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="3c609-163">Użyj hello **Execute** przycisk toorun tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="3c609-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="3c609-164">Witaj **wyniki** karta nie zawiera żadnych informacji po hello zapytanie zwraca zero wierszy.</span><span class="sxs-lookup"><span data-stu-id="3c609-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="3c609-165">Stan Hello powinny być widoczne jako **zakończyło się pomyślnie** po zakończeniu hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="3c609-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="3c609-166">Wyjaśnić Visual</span><span class="sxs-lookup"><span data-stu-id="3c609-166">Visual explain</span></span>

<span data-ttu-id="3c609-167">toodisplay wizualizacji hello planu zapytania, wybierz hello **wyjaśnić Visual** kartę poniżej hello arkusza.</span><span class="sxs-lookup"><span data-stu-id="3c609-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="3c609-168">Witaj **wyjaśnić Visual** widoku hello zapytania mogą być pomocne w opis przepływu hello złożonych zapytań.</span><span class="sxs-lookup"><span data-stu-id="3c609-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="3c609-169">Odpowiednika tekstową tego widoku można wyświetlić przy użyciu hello **Wyjaśnij** przycisku na powitania edytora zapytań.</span><span class="sxs-lookup"><span data-stu-id="3c609-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="3c609-170">Interfejs użytkownika aplikacji tez</span><span class="sxs-lookup"><span data-stu-id="3c609-170">Tez UI</span></span>

<span data-ttu-id="3c609-171">toodisplay hello Tez interfejsu użytkownika dla zapytania hello, wybierz hello **Tez** kartę poniżej hello arkusza.</span><span class="sxs-lookup"><span data-stu-id="3c609-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c609-172">Tez jest nieużywane tooresolve wszystkie zapytania.</span><span class="sxs-lookup"><span data-stu-id="3c609-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="3c609-173">Wiele zapytań można rozpoznawać bez korzystania z aplikacji Tez.</span><span class="sxs-lookup"><span data-stu-id="3c609-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="3c609-174">Jeśli Tez była używana tooresolve hello zapytania, zostanie wyświetlony hello wykresu acyklicznego wskazówkami (DAG).</span><span class="sxs-lookup"><span data-stu-id="3c609-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="3c609-175">Witaj tooview DAG dla zapytania, które zostały uruchomione w ostatnich hello, lub debugowania hello Tez proces, należy użyć hello [widoku Tez](hdinsight-debug-ambari-tez-view.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="3c609-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="3c609-176">Wyświetlanie historii zadań</span><span class="sxs-lookup"><span data-stu-id="3c609-176">View job history</span></span>

<span data-ttu-id="3c609-177">Witaj __zadania__ kartę Wyświetla historię zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3c609-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Obraz powitania historii zadań](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="3c609-179">Tabele bazy danych</span><span class="sxs-lookup"><span data-stu-id="3c609-179">Database tables</span></span>

<span data-ttu-id="3c609-180">Można użyć hello __tabel__ karcie toowork z tabelami w bazie danych Hive.</span><span class="sxs-lookup"><span data-stu-id="3c609-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Obraz powitania karty tabele](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="3c609-182">Zapisane kwerendy</span><span class="sxs-lookup"><span data-stu-id="3c609-182">Saved queries</span></span>

<span data-ttu-id="3c609-183">Na karcie zapytania hello Opcjonalnie można zapisać zapytania.</span><span class="sxs-lookup"><span data-stu-id="3c609-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="3c609-184">Po zapisaniu, można ponownie użyć kwerendy hello z hello __zapisane kwerendy__ kartę.</span><span class="sxs-lookup"><span data-stu-id="3c609-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Obraz karty zapisane kwerendy](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="3c609-186">Funkcje zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="3c609-186">User-defined functions</span></span>

<span data-ttu-id="3c609-187">Można również rozszerzać hive za pomocą funkcji zdefiniowanej przez użytkownika (UDF).</span><span class="sxs-lookup"><span data-stu-id="3c609-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="3c609-188">UDF umożliwia funkcjonalności tooimplement lub logikę, która nie jest łatwo uformowana w HiveQL.</span><span class="sxs-lookup"><span data-stu-id="3c609-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="3c609-189">Hello kartę UDF u góry hello hello Hive View pozwala toodeclare i Zapisywanie zestawu funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="3c609-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="3c609-190">Te funkcje UDF mogą być używane z hello **edytora zapytań**.</span><span class="sxs-lookup"><span data-stu-id="3c609-190">These UDFs can be used with hello **Query Editor**.</span></span>

![Obraz karty funkcji zdefiniowanej przez użytkownika](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="3c609-192">Po dodaniu toohello UDF Hive View **Wstaw funkcje UDF** u dołu hello hello pojawi się przycisk **edytora zapytań**.</span><span class="sxs-lookup"><span data-stu-id="3c609-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="3c609-193">Wybranie tego wpisu powoduje wyświetlenie listy rozwijanej hello funkcji UDF zdefiniowane w hello Hive widoku.</span><span class="sxs-lookup"><span data-stu-id="3c609-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="3c609-194">Wybieranie funkcji zdefiniowanej przez użytkownika dodaje HiveQL instrukcje tooyour zapytania tooenable hello funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3c609-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="3c609-195">Na przykład, jeśli zdefiniowano UDF z hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3c609-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="3c609-196">Nazwa zasobu: myudfs</span><span class="sxs-lookup"><span data-stu-id="3c609-196">Resource name: myudfs</span></span>

* <span data-ttu-id="3c609-197">Ścieżka zasobu: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="3c609-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="3c609-198">Nazwa funkcji zdefiniowanej przez użytkownika: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="3c609-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="3c609-199">Nazwa klasy funkcji zdefiniowanej przez użytkownika: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="3c609-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="3c609-200">Przy użyciu hello **Wstaw funkcje UDF** przycisk zawiera wpis o nazwie **myudfs**, z innej listy rozwijanej dla każdej funkcji zdefiniowanej przez użytkownika zdefiniowany dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="3c609-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="3c609-201">W takim przypadku **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="3c609-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="3c609-202">Wybranie tego wpisu dodaje powitania od początku toohello hello zapytania:</span><span class="sxs-lookup"><span data-stu-id="3c609-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="3c609-203">Następnie można hello UDF w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="3c609-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="3c609-204">Na przykład `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="3c609-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="3c609-205">Aby uzyskać więcej informacji o korzystaniu z funkcji UDF z Hive w usłudze HDInsight Zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="3c609-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="3c609-206">Przy użyciu języka Python z Hive i Pig w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c609-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="3c609-207">Jak tooadd niestandardowych tooHDInsight Hive funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="3c609-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="3c609-208">Gałąź, ustawienia</span><span class="sxs-lookup"><span data-stu-id="3c609-208">Hive settings</span></span>

<span data-ttu-id="3c609-209">Ustawienia mogą być używane toochange różne ustawienia Hive.</span><span class="sxs-lookup"><span data-stu-id="3c609-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="3c609-210">Na przykład zmiana aparat wykonywania hello gałęzi z tooMapReduce Tez (domyślnie: hello).</span><span class="sxs-lookup"><span data-stu-id="3c609-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="3c609-211"><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3c609-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3c609-212">Ogólne informacje na temat Hive w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3c609-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="3c609-213">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c609-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="3c609-214">Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3c609-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3c609-215">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c609-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="3c609-216">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c609-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
