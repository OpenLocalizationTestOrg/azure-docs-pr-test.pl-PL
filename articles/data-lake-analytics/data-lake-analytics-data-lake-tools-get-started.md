---
title: "skrypty aaaDevelop U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Data Lake Tools dla programu Visual Studio i jak toodevelop i testowania skryptów U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="21c4d-103">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21c4d-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="21c4d-104">Dowiedz się, jak toouse Visual Studio toocreate kont usługi Azure Data Lake Analytics, definiowania zadań w [U-SQL](data-lake-analytics-u-sql-get-started.md)i przesyłanie usługi Data Lake Analytics toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="21c4d-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="21c4d-105">Więcej informacji na temat usługi Data Lake Analytics można znaleźć w artykule [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="21c4d-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="21c4d-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="21c4d-106">Prerequisites</span></span>

* <span data-ttu-id="21c4d-107">**Visual Studio**: obsługiwane są wszystkie wersje z wyjątkiem Express.</span><span class="sxs-lookup"><span data-stu-id="21c4d-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="21c4d-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="21c4d-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="21c4d-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="21c4d-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="21c4d-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="21c4d-110">Visual Studio 2013</span></span>
* <span data-ttu-id="21c4d-111">**Zestaw Microsoft Azure SDK dla platformy .NET** w wersji 2.7.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="21c4d-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="21c4d-112">Zainstalować go za pomocą hello [Instalatora platformy sieci Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="21c4d-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="21c4d-113">Konto usługi **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="21c4d-114">toocreate konto, zobacz [wprowadzenie do usługi Azure Data Lake Analytics przy użyciu portalu Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21c4d-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="21c4d-115">Instalowanie narzędzi Azure Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21c4d-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="21c4d-116">Pobierz i zainstaluj usługi Azure Data Lake Tools dla Visual Studio [z Centrum pobierania hello](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="21c4d-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="21c4d-117">Po instalacji pamiętaj, że:</span><span class="sxs-lookup"><span data-stu-id="21c4d-117">After installation, note that:</span></span>
* <span data-ttu-id="21c4d-118">Witaj **Eksploratora serwera** > **Azure** zawiera węzeł **usługi Data Lake Analytics** węzła.</span><span class="sxs-lookup"><span data-stu-id="21c4d-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="21c4d-119">Witaj **narzędzia** menu ma **usługi Data Lake** elementu.</span><span class="sxs-lookup"><span data-stu-id="21c4d-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="21c4d-120">Połącz tooan konta usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="21c4d-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="21c4d-121">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21c4d-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="21c4d-122">Otwórz Eksplorator serwera, wybierając pozycje **Widok** > **Eksplorator serwera**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="21c4d-123">Kliknij prawym przyciskiem myszy pozycję **Azure**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-123">Right-click **Azure**.</span></span> <span data-ttu-id="21c4d-124">Następnie wybierz **połączyć tooMicrosoft subskrypcji Azure** i postępuj zgodnie z instrukcjami hello.</span><span class="sxs-lookup"><span data-stu-id="21c4d-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="21c4d-125">W Eksploratorze serwera wybierz pozycje **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="21c4d-126">Zobaczysz listę swoich kont usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="21c4d-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="21c4d-127">Pisanie pierwszego skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="21c4d-127">Write your first U-SQL script</span></span>

<span data-ttu-id="21c4d-128">powitania po tekst jest prosty skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="21c4d-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="21c4d-129">Definiuje małym zestawie danych i operacji zapisu, które dataset toohello domyślne Data Lake Store jako plik o nazwie `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="21c4d-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="21c4d-130">Przesyłanie zadania usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="21c4d-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="21c4d-131">Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="21c4d-132">Wybierz hello **projektu U-SQL** typu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="21c4d-133">Program Visual Studio utworzy rozwiązanie z użyciem pliku **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="21c4d-134">Wklej hello poprzedni skrypt do hello **Script.usql** okna.</span><span class="sxs-lookup"><span data-stu-id="21c4d-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="21c4d-135">W lewym górnym narożniku hello hello **Script.usql** okna, określ konto usługi Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="21c4d-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![Przesyłanie projektu U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="21c4d-137">W lewym górnym narożniku hello hello **Script.usql** wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="21c4d-138">Sprawdź hello **konta usługi Analytics**, a następnie wybierz **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="21c4d-139">Wyniki przesyłania są dostępne w hello narzędzi Data Lake Tools dla programu Visual Studio wyników, po zakończeniu przesyłania hello.</span><span class="sxs-lookup"><span data-stu-id="21c4d-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![Przesyłanie projektu U-SQL programu Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="21c4d-141">toosee hello najnowszego zadania stanu i Odśwież hello ekran, kliknij przycisk **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="21c4d-142">Zadanie hello zakończy się powodzeniem, wyświetlane hello **wykres zadania**, **operacji na metadanych**, **historii stanu**, i **diagnostyki**:</span><span class="sxs-lookup"><span data-stu-id="21c4d-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Wykres wydajności zadania skryptu U-SQL programu Visual Studio w usłudze Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="21c4d-144">**Zadanie podsumowania** pokazuje hello podsumowanie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="21c4d-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="21c4d-145">**Szczegóły zadania** przedstawiono bardziej szczegółowe informacje o zadaniu hello, w tym hello skryptu, zasobów i wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="21c4d-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="21c4d-146">**Wykres zadania** wizualizuje hello postęp zadania hello.</span><span class="sxs-lookup"><span data-stu-id="21c4d-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="21c4d-147">**Operacji na metadanych** pokazuje wszystkie akcje hello w wykazie hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="21c4d-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="21c4d-148">**Dane** pokazuje wszystkie hello wejścia i wyjścia.</span><span class="sxs-lookup"><span data-stu-id="21c4d-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="21c4d-149">Karta **Diagnostyka** udostępnia zaawansowaną analizę wykonywania zadania i optymalizacji wydajności.</span><span class="sxs-lookup"><span data-stu-id="21c4d-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="21c4d-150">Stan zadania toocheck</span><span class="sxs-lookup"><span data-stu-id="21c4d-150">toocheck job state</span></span>

1. <span data-ttu-id="21c4d-151">W Eksploratorze serwera wybierz pozycje **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="21c4d-152">Rozwiń nazwę konta usługi Data Lake Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="21c4d-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="21c4d-153">Kliknij dwukrotnie pozycję **Zadania**.</span><span class="sxs-lookup"><span data-stu-id="21c4d-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="21c4d-154">Wybierz zadanie hello, które wcześniej zostały przesłane.</span><span class="sxs-lookup"><span data-stu-id="21c4d-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="21c4d-155">toosee hello dane wyjściowe zadania</span><span class="sxs-lookup"><span data-stu-id="21c4d-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="21c4d-156">W Eksploratorze serwera Przeglądaj toohello zadanie, które zostało przesłane.</span><span class="sxs-lookup"><span data-stu-id="21c4d-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="21c4d-157">Kliknij przycisk hello **danych** kartę.</span><span class="sxs-lookup"><span data-stu-id="21c4d-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="21c4d-158">W hello **dane wyjściowe zadania** kartę, zaznacz hello `"/data.csv"` pliku.</span><span class="sxs-lookup"><span data-stu-id="21c4d-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21c4d-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="21c4d-159">Next steps</span></span>

* [<span data-ttu-id="21c4d-160">Uruchamianie skryptów U-SQL na swojej stacji roboczej w celu testowania i debugowania</span><span class="sxs-lookup"><span data-stu-id="21c4d-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="21c4d-161">Debugowanie kodu C# w zadaniach U-SQL</span><span class="sxs-lookup"><span data-stu-id="21c4d-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="21c4d-162">Użyj hello Azure Data Lake Tools dla Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="21c4d-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
