---
title: "Debugowanie zadań U-SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można debugować wierzchołek nie powiodło się U-SQL przy użyciu programu Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 2a77c72d3062272305208934d6406d040266c753
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="0055c-103">Debugowanie zdefiniowane przez użytkownika kodu C#, dla zadań U-SQL nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0055c-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="0055c-104">U-SQL zapewnia modelu rozszerzalności przy użyciu języka C#, więc można pisać swój kod, aby dodać funkcje, takie jak niestandardowe ekstraktory lub reduktor.</span><span class="sxs-lookup"><span data-stu-id="0055c-104">U-SQL provides an extensibility model using C#, so you can write your code to add functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="0055c-105">Aby dowiedzieć się więcej, zobacz [Podręcznik programowania U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="0055c-105">To learn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="0055c-106">W praktyce dowolny kod może być konieczne debugowania i systemy danych big data mogą dostarczać tylko ograniczone środowiska uruchomieniowego debugowania informacje, takie jak pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="0055c-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="0055c-107">Azure Data Lake Tools dla programu Visual Studio udostępnia funkcję **nie można debugować wierzchołków**, co umożliwia sklonować zadanie zakończone niepowodzeniem z chmury na komputerze lokalnym do debugowania.</span><span class="sxs-lookup"><span data-stu-id="0055c-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from the cloud to your local machine for debugging.</span></span> <span data-ttu-id="0055c-108">Lokalne klonu przechwytuje środowiska chmury całego, w tym wszystkie dane wejściowe i kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0055c-108">The local clone captures the entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="0055c-109">Poniżej film wideo przedstawia nie powiodło się wierzchołków debugowania w Azure Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0055c-109">The following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="0055c-110">Program Visual Studio wymaga następujących dwóch aktualizacji, jeśli nie są już zainstalowane: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) i [Universal C środowiska uruchomieniowego systemu Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="0055c-110">Visual Studio requires the following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-to-local-machine"></a><span data-ttu-id="0055c-111">Pobieranie nie powiodło się wierzchołków do komputera lokalnego</span><span class="sxs-lookup"><span data-stu-id="0055c-111">Download failed vertex to local machine</span></span>

<span data-ttu-id="0055c-112">Po otwarciu zadanie zakończone niepowodzeniem w Azure Data Lake Tools dla programu Visual Studio jest wyświetlany żółty pasek alertów o szczegółowe komunikaty o błędach na karcie błąd.</span><span class="sxs-lookup"><span data-stu-id="0055c-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in the error tab.</span></span>

1. <span data-ttu-id="0055c-113">Kliknij przycisk **Pobierz** do pobrania wszystkich wymaganych zasobów i strumienie wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0055c-113">Click **Download** to download all the required resources and input streams.</span></span> <span data-ttu-id="0055c-114">Pobieranie nie zostało ukończone, kliknij przycisk **ponów**.</span><span class="sxs-lookup"><span data-stu-id="0055c-114">If the download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="0055c-115">Kliknij przycisk **Otwórz** po zakończeniu pobierania do generowania środowisku debugowania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0055c-115">Click **Open** after the download completes to generate a local debugging environment.</span></span> <span data-ttu-id="0055c-116">Nowe wystąpienie programu Visual Studio z rozwiązaniem do debugowania jest automatycznie utworzony i otwarty.</span><span class="sxs-lookup"><span data-stu-id="0055c-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL debugowania programu visual studio pobierania wierzchołków](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="0055c-118">Zadania mogą obejmować źródła plików z kodem lub zarejestrowanych zestawy, a te dwa typy mają różne scenariusze debugowania.</span><span class="sxs-lookup"><span data-stu-id="0055c-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="0055c-119">Zadanie zakończone niepowodzeniem z kodem debugowania</span><span class="sxs-lookup"><span data-stu-id="0055c-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="0055c-120">Debugowanie zakończonego niepowodzeniem zadania przy użyciu zestawów</span><span class="sxs-lookup"><span data-stu-id="0055c-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="0055c-121">Debugowanie nie powiodło się z kodem — zadanie</span><span class="sxs-lookup"><span data-stu-id="0055c-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="0055c-122">Jeśli zadanie U-SQL zakończy się niepowodzeniem, a zadanie zawiera kod użytkownika (zwykle o nazwie `Script.usql.cs` projektu U-SQL), aby kod źródłowy jest importowany do debugowania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0055c-122">If a U-SQL job fails, and the job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into the debugging solution.</span></span>  <span data-ttu-id="0055c-123">Z tego miejsca można użyć programu Visual Studio debugowanie narzędzia (czujki, zmienne, itp.) do rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="0055c-123">From there you can use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="0055c-124">Przed debugowania, należy sprawdzić **wspólnego języka środowiska uruchomieniowego wyjątki** w oknie Ustawienia wyjątków (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="0055c-124">Before debugging, be sure to check **Common Language Runtime Exceptions** in the Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Ustawienia programu visual studio debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="0055c-126">Naciśnij klawisz **F5** do uruchomienia kodu związane z kodem.</span><span class="sxs-lookup"><span data-stu-id="0055c-126">Press **F5** to run the code-behind code.</span></span> <span data-ttu-id="0055c-127">Zostanie on uruchomiony, dopóki nie zostanie zatrzymana przez wyjątek.</span><span class="sxs-lookup"><span data-stu-id="0055c-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="0055c-128">Otwórz `ADLTool_Codebehind.usql.cs` pliku i ustaw punkty przerwania, naciśnij klawisz **F5** do debugowania kodu krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="0055c-128">Open the `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** to debug the code step by step.</span></span>

    ![Wyjątek debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="0055c-130">Zadanie nie powiodło się z zestawami debugowania</span><span class="sxs-lookup"><span data-stu-id="0055c-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="0055c-131">Jeśli używasz zestawy zarejestrowanych za pomocą skryptu U-SQL, system nie można pobrać kodu źródłowego automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0055c-131">If you use registered assemblies in your U-SQL script, the system can't get the source code automatically.</span></span> <span data-ttu-id="0055c-132">W takim przypadku ręcznie dodać pliki kodu źródłowego te zestawy do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0055c-132">In this case, manually add the assemblies' source code files to the solution.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="0055c-133">Konfigurowanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="0055c-133">Configure the solution</span></span>

1. <span data-ttu-id="0055c-134">Kliknij prawym przyciskiem myszy **rozwiązania "VertexDebug" > Dodaj > istniejący projekt...**  Aby znaleźć te zestawy kodu źródłowego i dodać projektu do rozwiązania debugowania.</span><span class="sxs-lookup"><span data-stu-id="0055c-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** to find the assemblies' source code and add the project to the debugging solution.</span></span>

    ![Dodawanie usługi Azure Data Lake Analytics U-SQL debugowania projektu](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="0055c-136">Kliknij prawym przyciskiem myszy **LocalVertexHost > właściwości** w rozwiązaniu i skopiuj **katalog roboczy** ścieżki.</span><span class="sxs-lookup"><span data-stu-id="0055c-136">Right-click **LocalVertexHost > Properties** in the solution and copy the **Working Directory** path.</span></span>

3. <span data-ttu-id="0055c-137">Kliknij prawym przyciskiem myszy **projektu kodu źródłowego zestawu > właściwości**, wybierz pozycję **kompilacji** po lewej stronie, a następnie wklej skopiowany ścieżkę jako **wyjściowy > Ścieżka wyjściowa**.</span><span class="sxs-lookup"><span data-stu-id="0055c-137">Right-Click **assembly source code project > Properties**, select the **Build** tab at left, and paste the copied path as **Output > Output path**.</span></span>

    ![Ścieżka pliku pdb zestawu Azure Data Lake Analytics U-SQL debugowania](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="0055c-139">Naciśnij klawisz **Ctrl + Alt + E**, sprawdź **wspólnego języka środowiska uruchomieniowego wyjątki** w oknie Ustawienia wyjątków.</span><span class="sxs-lookup"><span data-stu-id="0055c-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="0055c-140">Uruchom debugowania</span><span class="sxs-lookup"><span data-stu-id="0055c-140">Start debug</span></span>

1. <span data-ttu-id="0055c-141">Kliknij prawym przyciskiem myszy **projektu kodu źródłowego zestawu > odbudować** pliki .pdb dane wyjściowe do `LocalVertexHost` katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="0055c-141">Right-click **assembly source code project > Rebuild** to output .pdb files to the `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="0055c-142">Naciśnij klawisz **F5** i projekt zostanie uruchomiony, dopóki nie zostanie zatrzymana przez wyjątek.</span><span class="sxs-lookup"><span data-stu-id="0055c-142">Press **F5** and the project will run until it is stopped by an exception.</span></span> <span data-ttu-id="0055c-143">Może zostać wyświetlony komunikat następujące ostrzeżenie, które można bezpiecznie zignorować.</span><span class="sxs-lookup"><span data-stu-id="0055c-143">You may see the following warning message, which you can safely ignore.</span></span> <span data-ttu-id="0055c-144">Może potrwać do minuty aby przejść do ekranu debugowania.</span><span class="sxs-lookup"><span data-stu-id="0055c-144">It can take up to a minute to get to the debug screen.</span></span>

    ![Ostrzeżenie programu visual studio debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="0055c-146">Otwórz kod źródłowy i ustaw punkty przerwania, naciśnij klawisz **F5** do debugowania kodu krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="0055c-146">Open your source code and set breakpoints, then press **F5** to debug the code step by step.</span></span>

<span data-ttu-id="0055c-147">Umożliwia także Visual Studio debugowanie narzędzia (czujki, zmienne, itp.) do rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="0055c-147">You can also use the Visual Studio debugging tools (watch, variables, etc.) to troubleshoot the problem.</span></span>

> [!NOTE]
> <span data-ttu-id="0055c-148">Odbuduj projekt kodu źródłowego zestawu każdorazowo po modyfikacji kod służący do generowania plików PDB zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="0055c-148">Rebuild the assembly source code project each time after you modify the code to generate updated .pdb files.</span></span>

<span data-ttu-id="0055c-149">Po debugowaniu, jeśli projekt zakończy się pomyślnie w oknie danych wyjściowych zawiera następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="0055c-149">After debugging, if the project completes successfully the output window shows the following message:</span></span>

```
The Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL debugowania powiodło się](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-the-job"></a><span data-ttu-id="0055c-151">Prześlij ponownie zadania</span><span class="sxs-lookup"><span data-stu-id="0055c-151">Resubmit the job</span></span>

<span data-ttu-id="0055c-152">Po zakończeniu debugowania Prześlij zadanie zakończone niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="0055c-152">Once you have completed debugging, resubmit the failed job.</span></span>

1. <span data-ttu-id="0055c-153">W przypadku zadań z rozwiązaniami związane z kodem, skopiuj kod C# do pliku źródła kodu powiązanego (zazwyczaj `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="0055c-153">For jobs with code-behind solutions, copy your C# code into the code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="0055c-154">W przypadku zadań z zestawami zarejestrować zestawy .dll zaktualizowane w bazie danych ADLA:</span><span class="sxs-lookup"><span data-stu-id="0055c-154">For jobs with assemblies, register the updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="0055c-155">W Eksploratorze serwera lub Eksploratorze chmury, rozwiń węzeł **konta ADLA > baz danych** węzła.</span><span class="sxs-lookup"><span data-stu-id="0055c-155">From Server Explorer or Cloud Explorer, expand the **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="0055c-156">Kliknij prawym przyciskiem myszy **zestawy** i Zarejestruj ponownie nowe zestawy dll z bazą danych ADLA: ![debugowania Azure Data Lake Analytics U-SQL Rejestrowanie zestawów](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="0055c-156">Right-click **Assemblies** and register your new .dll assemblies with the ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="0055c-157">Prześlij swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="0055c-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0055c-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0055c-158">Next steps</span></span>

- [<span data-ttu-id="0055c-159">Podręcznik programowania U-SQL</span><span class="sxs-lookup"><span data-stu-id="0055c-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="0055c-160">Opracowywanie operatorów zdefiniowanych przez użytkownika U-SQL do zadania usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0055c-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="0055c-161">Samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0055c-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
