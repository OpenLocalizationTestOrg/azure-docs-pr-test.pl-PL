---
title: zadania aaaDebug U-SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodebug U-SQL nie powiodło się wierzchołków przy użyciu programu Visual Studio."
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
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="5ebb7-103">Debugowanie zdefiniowane przez użytkownika kodu C#, dla zadań U-SQL nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="5ebb7-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="5ebb7-104">U-SQL zapewnia modelu rozszerzalności przy użyciu języka C#, co może zapisywać Twoje kodu tooadd funkcje, takie jak niestandardowe ekstraktory lub reduktor.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="5ebb7-105">toolearn więcej, zobacz [Podręcznik programowania U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="5ebb7-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="5ebb7-106">W praktyce dowolny kod może być konieczne debugowania i systemy danych big data mogą dostarczać tylko ograniczone środowiska uruchomieniowego debugowania informacje, takie jak pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="5ebb7-107">Azure Data Lake Tools dla programu Visual Studio udostępnia funkcję **nie można debugować wierzchołków**, co umożliwia sklonować zadanie zakończone niepowodzeniem z komputera lokalnego tooyour chmury hello do debugowania.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="5ebb7-108">klonowanie lokalne powitania przechwytuje środowiska chmury całego hello, w tym wszystkie dane wejściowe i kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="5ebb7-109">Witaj poniżej film wideo przedstawia nie powiodło się wierzchołków debugowania w Azure Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="5ebb7-110">Program Visual Studio wymaga powitania po dwóch aktualizacji, jeśli nie są już zainstalowane: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) i [Universal C środowiska uruchomieniowego systemu Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="5ebb7-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="5ebb7-111">Pobieranie nie powiodło się wierzchołków toolocal maszyny</span><span class="sxs-lookup"><span data-stu-id="5ebb7-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="5ebb7-112">Po otwarciu zadanie zakończone niepowodzeniem w Azure Data Lake Tools dla programu Visual Studio jest wyświetlany żółty pasek alertów o szczegółowe komunikaty o błędach na karcie błąd hello.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="5ebb7-113">Kliknij przycisk **Pobierz** toodownload hello wszystkich wymaganych zasobów i strumienie wejściowe.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="5ebb7-114">Jeśli pobieranie hello nie ukończone, kliknij przycisk **ponów**.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="5ebb7-115">Kliknij przycisk **Otwórz** po ukończeniu pobierania hello toogenerate środowisku debugowania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="5ebb7-116">Nowe wystąpienie programu Visual Studio z rozwiązaniem do debugowania jest automatycznie utworzony i otwarty.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL debugowania programu visual studio pobierania wierzchołków](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="5ebb7-118">Zadania mogą obejmować źródła plików z kodem lub zarejestrowanych zestawy, a te dwa typy mają różne scenariusze debugowania.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="5ebb7-119">Zadanie zakończone niepowodzeniem z kodem debugowania</span><span class="sxs-lookup"><span data-stu-id="5ebb7-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="5ebb7-120">Debugowanie zakończonego niepowodzeniem zadania przy użyciu zestawów</span><span class="sxs-lookup"><span data-stu-id="5ebb7-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="5ebb7-121">Debugowanie nie powiodło się z kodem — zadanie</span><span class="sxs-lookup"><span data-stu-id="5ebb7-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="5ebb7-122">Jeśli zadanie U-SQL zakończy się niepowodzeniem, a hello zadania obejmują kod użytkownika (zwykle o nazwie `Script.usql.cs` projektu U-SQL), aby kod źródłowy jest importowany do hello debugowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="5ebb7-123">Z tego miejsca można użyć hello Visual Studio debugowania narzędzi (czujki, zmienne, itp.) tootroubleshoot hello problem.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="5ebb7-124">Przed debugowania, należy się toocheck **wspólnego języka środowiska uruchomieniowego wyjątki** w oknie Ustawienia wyjątków hello (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="5ebb7-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Ustawienia programu visual studio debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="5ebb7-126">Naciśnij klawisz **F5** toorun hello CodeBehind kodu.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="5ebb7-127">Zostanie on uruchomiony, dopóki nie zostanie zatrzymana przez wyjątek.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="5ebb7-128">Otwórz hello `ADLTool_Codebehind.usql.cs` pliku i ustaw punkty przerwania, naciśnij klawisz **F5** toodebug hello kodu krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Wyjątek debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="5ebb7-130">Zadanie nie powiodło się z zestawami debugowania</span><span class="sxs-lookup"><span data-stu-id="5ebb7-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="5ebb7-131">Użycie zestawów zarejestrowanych za pomocą skryptu U-SQL, hello systemu nie można pobrać kodu źródłowego hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="5ebb7-132">W takim przypadku ręcznie dodać zestawy hello źródła kodu pliki toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="5ebb7-133">Konfigurowanie rozwiązania hello</span><span class="sxs-lookup"><span data-stu-id="5ebb7-133">Configure hello solution</span></span>

1. <span data-ttu-id="5ebb7-134">Kliknij prawym przyciskiem myszy **rozwiązania "VertexDebug" > Dodaj > istniejący projekt...**  toofind Witaj zestawy kodu źródłowego i Dodaj toohello projektu hello debugowanie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Dodawanie usługi Azure Data Lake Analytics U-SQL debugowania projektu](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="5ebb7-136">Kliknij prawym przyciskiem myszy **LocalVertexHost > właściwości** w hello rozwiązania i skopiuj hello **katalog roboczy** ścieżki.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="5ebb7-137">Kliknij prawym przyciskiem myszy **projektu kodu źródłowego zestawu > właściwości**, wybierz pozycję hello **kompilacji** po lewej stronie, a następnie wklej skopiowany hello ścieżkę jako **wyjściowy > Ścieżka wyjściowa**.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Ścieżka pliku pdb zestawu Azure Data Lake Analytics U-SQL debugowania](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="5ebb7-139">Naciśnij klawisz **Ctrl + Alt + E**, sprawdź **wspólnego języka środowiska uruchomieniowego wyjątki** w oknie Ustawienia wyjątków.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="5ebb7-140">Uruchom debugowania</span><span class="sxs-lookup"><span data-stu-id="5ebb7-140">Start debug</span></span>

1. <span data-ttu-id="5ebb7-141">Kliknij prawym przyciskiem myszy **projektu kodu źródłowego zestawu > odbudować** toooutput .pdb, pliki toohello `LocalVertexHost` katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="5ebb7-142">Naciśnij klawisz **F5** i hello projekt zostanie uruchomiony, dopóki nie zostanie zatrzymana przez wyjątek.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="5ebb7-143">Może pojawić się następujące ostrzeżenie można zignorować hello.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="5ebb7-144">Może potrwać tooa minuty tooget toohello debugowania ekranu.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Ostrzeżenie programu visual studio debugowania w usłudze Azure Data Lake Analytics U-SQL](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="5ebb7-146">Otwórz kod źródłowy i ustaw punkty przerwania, naciśnij klawisz **F5** toodebug hello kodu krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="5ebb7-147">Umożliwia także hello Visual Studio debugowania narzędzi (czujki, zmienne, itp.) tootroubleshoot hello problem.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="5ebb7-148">Odbuduj projekt kodu źródłowego zestawu hello każdorazowo po zmodyfikowaniu hello kodu toogenerate zaktualizowane .pdb, pliki.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="5ebb7-149">Po debugowaniu, jeśli hello projektu zostało ukończone pomyślnie hello okno danych wyjściowych zawiera następujące wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="5ebb7-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Azure Data Lake Analytics U-SQL debugowania powiodło się](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="5ebb7-151">Prześlij ponownie hello zadania</span><span class="sxs-lookup"><span data-stu-id="5ebb7-151">Resubmit hello job</span></span>

<span data-ttu-id="5ebb7-152">Po zakończeniu debugowania Prześlij ponownie hello zadania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="5ebb7-153">W przypadku zadań z rozwiązaniami związane z kodem, skopiuj kod C# do pliku źródłowego związane z kodem hello (zazwyczaj `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="5ebb7-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="5ebb7-154">Prac z zestawami Rejestrowanie zestawów .dll hello zaktualizowane w bazie danych ADLA:</span><span class="sxs-lookup"><span data-stu-id="5ebb7-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="5ebb7-155">W Eksploratorze serwera lub Eksploratorze chmury, rozwiń węzeł hello **konta ADLA > baz danych** węzła.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="5ebb7-156">Kliknij prawym przyciskiem myszy **zestawy** i Zarejestruj ponownie nowe zestawy dll z bazą danych ADLA hello: ![debugowania Azure Data Lake Analytics U-SQL Rejestrowanie zestawów](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="5ebb7-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="5ebb7-157">Prześlij swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="5ebb7-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ebb7-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ebb7-158">Next steps</span></span>

- [<span data-ttu-id="5ebb7-159">Podręcznik programowania U-SQL</span><span class="sxs-lookup"><span data-stu-id="5ebb7-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="5ebb7-160">Opracowywanie operatorów zdefiniowanych przez użytkownika U-SQL do zadania usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5ebb7-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="5ebb7-161">Samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ebb7-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
