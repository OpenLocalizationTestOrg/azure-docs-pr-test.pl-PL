---
title: "aaaTest i debugowanie zadań U-SQL przy użyciu lokalnego uruchamiania i hello zestawu SDK usługi Azure Data Lake U-SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania toouse Azure Data Lake Tools dla Visual Studio i hello tootest zestawu SDK usługi Azure Data Lake U-SQL i debugowania skryptu U-SQL w sieci lokalnej stacji roboczej."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="f14e1-103">Testowanie i debugowanie zadań U-SQL przy użyciu lokalnego uruchamiania i hello zestawu SDK usługi Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="f14e1-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="f14e1-104">Można użyć usługi Azure Data Lake Tools dla Visual Studio i zadań U-SQL toorun zestawu SDK usługi Azure Data Lake U-SQL hello na stacji roboczej, tak samo jak w usłudze Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="f14e1-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="f14e1-105">Te dwie funkcje uruchamiania lokalnego pozwalają zaoszczędzić czas poświęcony na testowanie i debugowanie zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f14e1-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="f14e1-106">Folder główny danych hello i ścieżka pliku hello</span><span class="sxs-lookup"><span data-stu-id="f14e1-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="f14e1-107">Zarówno przebiegu lokalnego, jak i hello SDK U-SQL wymagają folderu głównego danych.</span><span class="sxs-lookup"><span data-stu-id="f14e1-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="f14e1-108">folder główny danych Hello dotyczy konto obliczeniowe lokalne powitania "Magazyn lokalny".</span><span class="sxs-lookup"><span data-stu-id="f14e1-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="f14e1-109">To konto usługi Azure Data Lake Store równoważne toohello konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f14e1-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="f14e1-110">Przełączanie tooa folder różnych głównych danych jest podobnie jak przełączanie tooa magazynu innego konta.</span><span class="sxs-lookup"><span data-stu-id="f14e1-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="f14e1-111">Jeśli chcesz tooaccess często udostępnionych danych z różnych głównych danych folderów, należy użyć ścieżek bezwzględnych w skryptach.</span><span class="sxs-lookup"><span data-stu-id="f14e1-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="f14e1-112">Lub Utwórz łącza symbolicznego systemu plików (na przykład **mklink** na NTFS) w obszarze hello danych głównych folder toopoint toohello udostępnionych danych.</span><span class="sxs-lookup"><span data-stu-id="f14e1-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="f14e1-113">folder główny danych Hello jest używany do:</span><span class="sxs-lookup"><span data-stu-id="f14e1-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="f14e1-114">Przechowywania metadanych, w tym baz danych, tabel, przechowywanymi w tabeli funkcji (funkcji Tvf) i zestawów.</span><span class="sxs-lookup"><span data-stu-id="f14e1-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="f14e1-115">Wyszukiwanie hello danych wejściowych i wyjściowych ścieżek, które są zdefiniowane jako ścieżek względnych w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f14e1-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="f14e1-116">Używanie ścieżek względnych umożliwia łatwiejsze toodeploy Twojego tooAzure projektów języka U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f14e1-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="f14e1-117">W skryptów U-SQL, można użyć zarówno ścieżki względnej, jak i lokalną ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="f14e1-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="f14e1-118">Ścieżka względna Hello jest ścieżka folderu względna toohello określony katalog główny danych.</span><span class="sxs-lookup"><span data-stu-id="f14e1-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="f14e1-119">Zaleca się, że można użyć "/" jako hello toomake separatora ścieżki skryptów zgodny z powitania po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="f14e1-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="f14e1-120">Oto kilka przykładów ścieżek względnych i ich równoważne ścieżki bezwzględnej.</span><span class="sxs-lookup"><span data-stu-id="f14e1-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="f14e1-121">W tym przykładzie C:\LocalRunDataRoot jest folder główny danych hello.</span><span class="sxs-lookup"><span data-stu-id="f14e1-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="f14e1-122">Ścieżka względna</span><span class="sxs-lookup"><span data-stu-id="f14e1-122">Relative path</span></span>|<span data-ttu-id="f14e1-123">Ścieżki bezwzględne</span><span class="sxs-lookup"><span data-stu-id="f14e1-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="f14e1-124">/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="f14e1-124">/abc/def/input.csv</span></span> |<span data-ttu-id="f14e1-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f14e1-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="f14e1-126">ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="f14e1-126">abc/def/input.csv</span></span>  |<span data-ttu-id="f14e1-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f14e1-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="f14e1-128">D:/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="f14e1-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="f14e1-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="f14e1-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="f14e1-130">Użyj lokalnego uruchomienia z programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f14e1-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="f14e1-131">Narzędzia Data Lake Tools dla programu Visual Studio zapewnia obsługę lokalnej — Uruchom U-SQL w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f14e1-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="f14e1-132">Za pomocą tej funkcji, można:</span><span class="sxs-lookup"><span data-stu-id="f14e1-132">By using this feature, you can:</span></span>

- <span data-ttu-id="f14e1-133">Uruchom skrypt U-SQL lokalnie, wraz z zestawami języka C#.</span><span class="sxs-lookup"><span data-stu-id="f14e1-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="f14e1-134">Debugowanie zestawu języka C# lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f14e1-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="f14e1-135">Tworzenie, wyświetlanie i usuwanie katalogów U-SQL (lokalnych baz danych, zestawy, schematy i tabele) z poziomu Eksploratora serwera.</span><span class="sxs-lookup"><span data-stu-id="f14e1-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="f14e1-136">Znajduje się też katalogu lokalnego hello także z poziomu Eksploratora serwera.</span><span class="sxs-lookup"><span data-stu-id="f14e1-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Narzędzia Data Lake Tools dla katalogu lokalnego lokalnego uruchomienia programu Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="f14e1-138">Witaj narzędzi Data Lake Tools Instalator tworzy toobe folderu C:\LocalRunRoot, używane jako hello domyślny folder główny danych.</span><span class="sxs-lookup"><span data-stu-id="f14e1-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="f14e1-139">Równoległość lokalnego uruchomienia domyślne Hello jest 1.</span><span class="sxs-lookup"><span data-stu-id="f14e1-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="f14e1-140">tooconfigure lokalnego uruchamiania programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f14e1-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="f14e1-141">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f14e1-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="f14e1-142">Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="f14e1-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="f14e1-143">Rozwiń węzeł **Azure** > **usługi Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f14e1-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="f14e1-144">Kliknij przycisk hello **usługi Data Lake** menu, a następnie kliknij przycisk **opcje i ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="f14e1-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="f14e1-145">W drzewie po lewej stronie powitania rozwiń **usługi Azure Data Lake**, a następnie rozwiń węzeł **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="f14e1-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Narzędzia Data Lake Tools dla programu Visual Studio Uruchom lokalny Konfigurowanie ustawień](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="f14e1-147">Projektu programu Visual Studio U-SQL jest wymagana do wykonania lokalnego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="f14e1-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="f14e1-148">Ta część różni się od uruchamiania skryptów U-SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f14e1-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="f14e1-149">skrypt toorun U-SQL lokalnie</span><span class="sxs-lookup"><span data-stu-id="f14e1-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="f14e1-150">W programie Visual Studio Otwórz projekt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f14e1-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="f14e1-151">Kliknij prawym przyciskiem myszy skrypt U-SQL w Eksploratorze rozwiązań, a następnie kliknij przycisk **Prześlij skrypt**.</span><span class="sxs-lookup"><span data-stu-id="f14e1-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="f14e1-152">Wybierz **(Local)** jako hello Analytics konta toorun skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f14e1-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="f14e1-153">Możesz również kliknąć hello **(Local)** konta na powitania u góry okna Skrypt, a następnie kliknij przycisk **przesyłania** (lub użyj Witaj Ctrl + F5 skrótu klawiaturowego).</span><span class="sxs-lookup"><span data-stu-id="f14e1-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio lokalnego uruchomienia przesyłania zadań](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="f14e1-155">Debugowanie skryptów i zestawów języka C# lokalnie</span><span class="sxs-lookup"><span data-stu-id="f14e1-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="f14e1-156">Można debugować zestawy języka C# bez przesyłania i rejestrowania ich tooAzure Data Lake Analytics usługi.</span><span class="sxs-lookup"><span data-stu-id="f14e1-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="f14e1-157">Można ustawić punktów przerwania w kodzie pliku zarówno hello i w odwołaniu projekcie C#.</span><span class="sxs-lookup"><span data-stu-id="f14e1-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="f14e1-158">toodebug kod lokalny w kodzie pliku</span><span class="sxs-lookup"><span data-stu-id="f14e1-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="f14e1-159">Ustaw punkty przerwania w kodzie hello pliku.</span><span class="sxs-lookup"><span data-stu-id="f14e1-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="f14e1-160">Naciśnij klawisz F5 toodebug hello skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f14e1-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="f14e1-161">Witaj następujące procedury działa tylko w programie Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="f14e1-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="f14e1-162">W starszych Visual Studio może być konieczne toomanually Dodaj hello pliki pdb.</span><span class="sxs-lookup"><span data-stu-id="f14e1-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="f14e1-163">toodebug kod lokalny w odwołaniu projekcie C#</span><span class="sxs-lookup"><span data-stu-id="f14e1-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="f14e1-164">Utwórz projekt zestawu języka C# i skompiluj go toogenerate hello wyjściowy plik dll.</span><span class="sxs-lookup"><span data-stu-id="f14e1-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="f14e1-165">Zarejestruj hello biblioteki dll przy użyciu instrukcji U-SQL:</span><span class="sxs-lookup"><span data-stu-id="f14e1-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="f14e1-166">Ustaw punkty przerwania w hello kod w języku C#.</span><span class="sxs-lookup"><span data-stu-id="f14e1-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="f14e1-167">Naciśnij klawisz F5 toodebug hello skryptu z wywoływanym dll hello C# lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f14e1-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="f14e1-168">Użyj lokalnego uruchamiania z hello SDK Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="f14e1-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="f14e1-169">Ponadto skrypty toorunning U-SQL lokalnie, używając programu Visual Studio, za pomocą skryptów U-SQL toorun hello w zestawie SDK usługi Azure Data Lake U-SQL lokalnie interfejsów programowania i z wierszem polecenia.</span><span class="sxs-lookup"><span data-stu-id="f14e1-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="f14e1-170">Za pomocą tych opcji można skalować test lokalnego skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f14e1-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="f14e1-171">Dowiedz się więcej o [zestawu SDK usługi Azure Data Lake U-SQL](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f14e1-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f14e1-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f14e1-172">Next steps</span></span>

* <span data-ttu-id="f14e1-173">toosee bardziej złożonego zapytania, zobacz [analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="f14e1-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="f14e1-174">Zobacz szczegóły zadania tooview, [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="f14e1-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="f14e1-175">widoku wykonania wierzchołka hello toouse, zobacz [hello użyj widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="f14e1-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
