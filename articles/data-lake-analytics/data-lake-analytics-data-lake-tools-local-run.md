---
title: "Testowanie i debugowanie zadań U-SQL przy użyciu zestawu SDK usługi Azure Data Lake U-SQL i lokalne uruchamianie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure Data Lake Tools dla programu Visual Studio i zestaw SDK usługi Azure Data Lake U-SQL umożliwia testowanie i debugowanie zadań U-SQL w sieci lokalnej stacji roboczej."
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
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="71a51-103">Testowanie i debugowanie zadań U-SQL przy użyciu lokalnego uruchamiania i zestawu SDK usługi Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="71a51-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="71a51-104">Przy użyciu narzędzi Azure Data Lake Tools for Visual Studio i zestawu SDK U-SQL usługi Azure Data Lake można uruchamiać zadania U-SQL na stacji roboczej, podobnie jak w usłudze Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="71a51-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="71a51-105">Te dwie funkcje uruchamiania lokalnego pozwalają zaoszczędzić czas poświęcony na testowanie i debugowanie zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="71a51-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="71a51-106">Folder główny danych i ścieżka pliku</span><span class="sxs-lookup"><span data-stu-id="71a51-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="71a51-107">Zarówno przebiegu lokalnego, jak i zestawu SDK języka U-SQL wymagają folderu głównego danych.</span><span class="sxs-lookup"><span data-stu-id="71a51-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="71a51-108">Folder główny danych jest "Magazyn lokalny" dla konta lokalnego obliczeń.</span><span class="sxs-lookup"><span data-stu-id="71a51-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="71a51-109">Odpowiada to konto usługi Azure Data Lake Store z kontem usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="71a51-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="71a51-110">Przełączanie do folderu różnych głównych danych jest podobnie jak przełączanie do konta magazynu innego.</span><span class="sxs-lookup"><span data-stu-id="71a51-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="71a51-111">Jeśli chcesz uzyskać dostęp do danych często udostępnione z innego katalogu głównym danych folderów, należy użyć ścieżek bezwzględnych w skryptach.</span><span class="sxs-lookup"><span data-stu-id="71a51-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="71a51-112">Lub Utwórz łącza symbolicznego systemu plików (na przykład **mklink** na NTFS) w folderze głównym danych wskaż udostępnionych danych.</span><span class="sxs-lookup"><span data-stu-id="71a51-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="71a51-113">Folder główny danych służy do:</span><span class="sxs-lookup"><span data-stu-id="71a51-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="71a51-114">Przechowywania metadanych, w tym baz danych, tabel, przechowywanymi w tabeli funkcji (funkcji Tvf) i zestawów.</span><span class="sxs-lookup"><span data-stu-id="71a51-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="71a51-115">Wyszukiwanie wejściowymi i wyjściowymi ścieżek, które są zdefiniowane jako ścieżek względnych w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="71a51-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="71a51-116">Używanie ścieżek względnych ułatwia wdrażanie projektów języka U-SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="71a51-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="71a51-117">W skryptów U-SQL, można użyć zarówno ścieżki względnej, jak i lokalną ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="71a51-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="71a51-118">Ścieżka względna jest względem ścieżki katalogu głównym danych określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="71a51-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="71a51-119">Firma Microsoft zaleca użycie "/" jako separatora ścieżki do sprawia, że skrypty zgodne z po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="71a51-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="71a51-120">Oto kilka przykładów ścieżek względnych i ich równoważne ścieżki bezwzględnej.</span><span class="sxs-lookup"><span data-stu-id="71a51-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="71a51-121">W tych przykładach C:\LocalRunDataRoot jest folder główny danych.</span><span class="sxs-lookup"><span data-stu-id="71a51-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="71a51-122">Ścieżka względna</span><span class="sxs-lookup"><span data-stu-id="71a51-122">Relative path</span></span>|<span data-ttu-id="71a51-123">Ścieżki bezwzględne</span><span class="sxs-lookup"><span data-stu-id="71a51-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="71a51-124">/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="71a51-124">/abc/def/input.csv</span></span> |<span data-ttu-id="71a51-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="71a51-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="71a51-126">ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="71a51-126">abc/def/input.csv</span></span>  |<span data-ttu-id="71a51-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="71a51-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="71a51-128">D:/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="71a51-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="71a51-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="71a51-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="71a51-130">Użyj lokalnego uruchomienia z programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71a51-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="71a51-131">Narzędzia Data Lake Tools dla programu Visual Studio zapewnia obsługę lokalnej — Uruchom U-SQL w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71a51-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="71a51-132">Za pomocą tej funkcji, można:</span><span class="sxs-lookup"><span data-stu-id="71a51-132">By using this feature, you can:</span></span>

- <span data-ttu-id="71a51-133">Uruchom skrypt U-SQL lokalnie, wraz z zestawami języka C#.</span><span class="sxs-lookup"><span data-stu-id="71a51-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="71a51-134">Debugowanie zestawu języka C# lokalnie.</span><span class="sxs-lookup"><span data-stu-id="71a51-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="71a51-135">Tworzenie, wyświetlanie i usuwanie katalogów U-SQL (lokalnych baz danych, zestawy, schematy i tabele) z poziomu Eksploratora serwera.</span><span class="sxs-lookup"><span data-stu-id="71a51-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="71a51-136">Lokalny katalog można również znaleźć również z Eksploratora serwera.</span><span class="sxs-lookup"><span data-stu-id="71a51-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Narzędzia Data Lake Tools dla katalogu lokalnego lokalnego uruchomienia programu Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="71a51-138">Data Lake Tools Instalator tworzy folder C:\LocalRunRoot ma być używany jako domyślny folder główny danych.</span><span class="sxs-lookup"><span data-stu-id="71a51-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="71a51-139">Równoległość lokalnego uruchomienia domyślny to 1.</span><span class="sxs-lookup"><span data-stu-id="71a51-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="71a51-140">Aby skonfigurować przebiegu lokalnego w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71a51-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="71a51-141">Otwórz program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71a51-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="71a51-142">Otwórz **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="71a51-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="71a51-143">Rozwiń węzeł **Azure** > **usługi Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="71a51-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="71a51-144">Kliknij przycisk **usługi Data Lake** menu, a następnie kliknij przycisk **opcje i ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="71a51-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="71a51-145">W drzewie po lewej stronie rozwiń **usługi Azure Data Lake**, a następnie rozwiń węzeł **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="71a51-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Narzędzia Data Lake Tools dla programu Visual Studio Uruchom lokalny Konfigurowanie ustawień](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="71a51-147">Projektu programu Visual Studio U-SQL jest wymagana do wykonania lokalnego uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="71a51-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="71a51-148">Ta część różni się od uruchamiania skryptów U-SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="71a51-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="71a51-149">Aby uruchomić skrypt U-SQL lokalnie</span><span class="sxs-lookup"><span data-stu-id="71a51-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="71a51-150">W programie Visual Studio Otwórz projekt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="71a51-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="71a51-151">Kliknij prawym przyciskiem myszy skrypt U-SQL w Eksploratorze rozwiązań, a następnie kliknij przycisk **Prześlij skrypt**.</span><span class="sxs-lookup"><span data-stu-id="71a51-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="71a51-152">Wybierz **(Local)** jako konta usługi Analytics, aby uruchomić skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="71a51-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="71a51-153">Możesz również kliknąć **(Local)** konta w górnej części okna Skrypt, a następnie kliknij przycisk **przesyłania** (lub użyj klawiszy Ctrl + F5 skrót klawiaturowy).</span><span class="sxs-lookup"><span data-stu-id="71a51-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Narzędzia Data Lake Tools dla Visual Studio lokalnego uruchomienia przesyłania zadań](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="71a51-155">Debugowanie skryptów i zestawów języka C# lokalnie</span><span class="sxs-lookup"><span data-stu-id="71a51-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="71a51-156">Można debugować zestawy języka C# bez przesyłania i rejestrowania ich do Azure Data Lake Analytics usługi.</span><span class="sxs-lookup"><span data-stu-id="71a51-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="71a51-157">Można ustawić punkty przerwania w kodzie pliku oraz w projekcie języka C#, do którego się odwołujesz.</span><span class="sxs-lookup"><span data-stu-id="71a51-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="71a51-158">Aby debugować kod lokalny w kodzie pliku</span><span class="sxs-lookup"><span data-stu-id="71a51-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="71a51-159">Ustaw punkty przerwania w kodzie pliku.</span><span class="sxs-lookup"><span data-stu-id="71a51-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="71a51-160">Naciśnij klawisz F5, aby debugować skrypt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="71a51-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="71a51-161">Poniższa procedura dotyczy tylko programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="71a51-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="71a51-162">W starszych wersjach programu Visual Studio może być konieczne ręczne dodanie plików pdb.</span><span class="sxs-lookup"><span data-stu-id="71a51-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="71a51-163">Aby debugować kod lokalny w występującym w odwołaniu projekcie C#</span><span class="sxs-lookup"><span data-stu-id="71a51-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="71a51-164">Utwórz projekt zestawu języka C# i skompiluj go, aby wygenerować wyjściowy plik dll.</span><span class="sxs-lookup"><span data-stu-id="71a51-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="71a51-165">Zarejestruj plik dll za pomocą instrukcji U-SQL:</span><span class="sxs-lookup"><span data-stu-id="71a51-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="71a51-166">Ustaw punkty przerwania w kodzie C#.</span><span class="sxs-lookup"><span data-stu-id="71a51-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="71a51-167">Naciśnij klawisz F5, aby debugować skrypt z wywoływanym C# biblioteki dll lokalnie.</span><span class="sxs-lookup"><span data-stu-id="71a51-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="71a51-168">Użyj lokalnego uruchomienia z pakietu SDK Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="71a51-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="71a51-169">Poza uruchamianiem skryptów U-SQL lokalnie, używając programu Visual Studio, zestawu SDK usługi Azure Data Lake U-SQL służy do uruchamiania skryptów U-SQL lokalnie z wiersza polecenia i programowania interfejsów.</span><span class="sxs-lookup"><span data-stu-id="71a51-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="71a51-170">Za pomocą tych opcji można skalować test lokalnego skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="71a51-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="71a51-171">Dowiedz się więcej o [zestawu SDK usługi Azure Data Lake U-SQL](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="71a51-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="71a51-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71a51-172">Next steps</span></span>

* <span data-ttu-id="71a51-173">Aby wyświetlić bardziej złożonego zapytania, zobacz [analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="71a51-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="71a51-174">Aby wyświetlić szczegóły zadania, zobacz [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="71a51-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="71a51-175">Aby użyć widoku wykonania wierzchołka, zobacz [użyć widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="71a51-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
