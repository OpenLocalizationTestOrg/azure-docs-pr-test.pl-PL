---
title: "Uruchamiania lokalnego skryptu U-SQL skali i testowania przy użyciu zestawu SDK usługi Azure Data Lake U-SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać zestawu SDK usługi Azure Data Lake U-SQL do zadań skali U-SQL lokalnego uruchamiania i testu z wiersza polecenia i interfejsów programowania na na lokalnej stacji roboczej."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="2e030-103">Uruchamiania lokalnego skryptu U-SQL skali i testowania przy użyciu zestawu SDK usługi Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="2e030-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="2e030-104">Podczas tworzenia skryptu U-SQL, jest często do uruchomienia i skrypt testu U-SQL lokalnie przed przesłać do chmury.</span><span class="sxs-lookup"><span data-stu-id="2e030-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="2e030-105">Azure Data Lake umożliwia pakietu Nuget o nazwie zestawu SDK usługi Azure Data Lake U-SQL, w tym scenariuszu, za pomocą którego można łatwo skalować uruchamiania lokalnego skryptu U-SQL i testowania.</span><span class="sxs-lookup"><span data-stu-id="2e030-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="2e030-106">Istnieje również możliwość zintegrowania ten test U-SQL przy użyciu systemu CI (ciągłej integracji) do automatyzowania kompilowania i testowania.</span><span class="sxs-lookup"><span data-stu-id="2e030-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="2e030-107">Jeśli potrzebne informacje jak ręcznie lokalnymi Uruchom i debugowania skryptu U-SQL z narzędzi z graficznym interfejsem użytkownika, możesz użyć usługi Azure Data Lake Tools dla programu Visual Studio, w tym.</span><span class="sxs-lookup"><span data-stu-id="2e030-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="2e030-108">Dowiedz się więcej o [tutaj](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="2e030-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="2e030-109">Instalacja usługi Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="2e030-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="2e030-110">Można pobrać zestaw SDK usługi Azure Data Lake U-SQL [tutaj](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) na Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2e030-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="2e030-111">I przed jego użyciem należy upewnić się, że zależności w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="2e030-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="2e030-112">Zależności</span><span class="sxs-lookup"><span data-stu-id="2e030-112">Dependencies</span></span>

<span data-ttu-id="2e030-113">Data Lake U-SQL zestaw SDK wymaga następujących zależności:</span><span class="sxs-lookup"><span data-stu-id="2e030-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="2e030-114">[Microsoft .NET Framework 4.6 lub nowszą](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="2e030-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="2e030-115">Microsoft Visual C++ 14 i zestaw Windows SDK 10.0.10240.0 lub nowszą (nazywany CppSDK w tym artykule).</span><span class="sxs-lookup"><span data-stu-id="2e030-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="2e030-116">Istnieją dwa sposoby uzyskania CppSDK:</span><span class="sxs-lookup"><span data-stu-id="2e030-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="2e030-117">Zainstaluj [programu Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="2e030-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="2e030-118">W folderze Program Files — na przykład C:\Program Files (x86) \Windows Kits\10\ będziesz mieć folderu \Windows Kits\10.</span><span class="sxs-lookup"><span data-stu-id="2e030-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="2e030-119">Zawiera ona również wersji zestawu Windows 10 SDK w \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="2e030-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="2e030-120">Jeśli nie widzisz tych folderów, zainstaluj ponownie program Visual Studio i należy wybrać podczas instalacji zestawu Windows 10 SDK.</span><span class="sxs-lookup"><span data-stu-id="2e030-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="2e030-121">Jeśli masz to zainstalowane z programem Visual Studio kompilatora lokalnego skryptu U-SQL znajdziesz ją automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2e030-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![Narzędzia Data Lake Tools dla programu Visual Studio lokalnego uruchomienia systemu Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="2e030-123">Zainstaluj [Data Lake Tools dla programu Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="2e030-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="2e030-124">Można znaleźć opakowaniach jednostkowych Visual C++ i zestaw Windows SDK plików w C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="2e030-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="2e030-125">W takim przypadku kompilatora lokalnego skryptu U-SQL nie można automatycznie odnaleźć zależności.</span><span class="sxs-lookup"><span data-stu-id="2e030-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="2e030-126">Należy określić ścieżkę CppSDK dla niego.</span><span class="sxs-lookup"><span data-stu-id="2e030-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="2e030-127">Możesz skopiować pliki do innej lokalizacji lub użyj go jako jest.</span><span class="sxs-lookup"><span data-stu-id="2e030-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="2e030-128">Zrozumienie podstawowych pojęć</span><span class="sxs-lookup"><span data-stu-id="2e030-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="2e030-129">Główny danych</span><span class="sxs-lookup"><span data-stu-id="2e030-129">Data root</span></span>

<span data-ttu-id="2e030-130">Folder główny danych jest "Magazyn lokalny" dla konta lokalnego obliczeń.</span><span class="sxs-lookup"><span data-stu-id="2e030-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="2e030-131">Odpowiada to konto usługi Azure Data Lake Store z kontem usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2e030-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="2e030-132">Przełączanie do folderu różnych głównych danych jest podobnie jak przełączanie do konta magazynu innego.</span><span class="sxs-lookup"><span data-stu-id="2e030-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="2e030-133">Jeśli chcesz uzyskać dostęp do danych często udostępnione z innego katalogu głównym danych folderów, należy użyć ścieżek bezwzględnych w skryptach.</span><span class="sxs-lookup"><span data-stu-id="2e030-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="2e030-134">Lub Utwórz łącza symbolicznego systemu plików (na przykład **mklink** na NTFS) w folderze głównym danych wskaż udostępnionych danych.</span><span class="sxs-lookup"><span data-stu-id="2e030-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="2e030-135">Folder główny danych służy do:</span><span class="sxs-lookup"><span data-stu-id="2e030-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="2e030-136">Przechowywania metadanych lokalnego, w tym baz danych, tabel, przechowywanymi w tabeli funkcji (funkcji Tvf) i zestawy.</span><span class="sxs-lookup"><span data-stu-id="2e030-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="2e030-137">Wyszukiwanie wejściowymi i wyjściowymi ścieżek, które są zdefiniowane jako ścieżek względnych w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2e030-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="2e030-138">Używanie ścieżek względnych ułatwia wdrażanie projektów języka U-SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2e030-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="2e030-139">Ścieżka pliku w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="2e030-139">File path in U-SQL</span></span>

<span data-ttu-id="2e030-140">W skryptów U-SQL, można użyć zarówno ścieżki względnej, jak i lokalną ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="2e030-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="2e030-141">Ścieżka względna jest względem ścieżki katalogu głównym danych określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="2e030-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="2e030-142">Firma Microsoft zaleca użycie "/" jako separatora ścieżki do sprawia, że skrypty zgodne z po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="2e030-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="2e030-143">Oto kilka przykładów ścieżek względnych i ich równoważne ścieżki bezwzględnej.</span><span class="sxs-lookup"><span data-stu-id="2e030-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="2e030-144">W tych przykładach C:\LocalRunDataRoot jest folder główny danych.</span><span class="sxs-lookup"><span data-stu-id="2e030-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="2e030-145">Ścieżka względna</span><span class="sxs-lookup"><span data-stu-id="2e030-145">Relative path</span></span>|<span data-ttu-id="2e030-146">Ścieżki bezwzględne</span><span class="sxs-lookup"><span data-stu-id="2e030-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="2e030-147">/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="2e030-147">/abc/def/input.csv</span></span> |<span data-ttu-id="2e030-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="2e030-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="2e030-149">ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="2e030-149">abc/def/input.csv</span></span>  |<span data-ttu-id="2e030-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="2e030-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="2e030-151">D:/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="2e030-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="2e030-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="2e030-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="2e030-153">Katalog roboczy</span><span class="sxs-lookup"><span data-stu-id="2e030-153">Working directory</span></span>

<span data-ttu-id="2e030-154">Podczas uruchamiania lokalnego skryptu U-SQL, przejdź do katalogu roboczego został utworzony podczas kompilacji w bieżącym katalogu uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="2e030-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="2e030-155">Oprócz dane wyjściowe kompilacji pliki obsługi potrzebne dla lokalnych wykonań będzie kopiowany do katalogu roboczego w tle.</span><span class="sxs-lookup"><span data-stu-id="2e030-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="2e030-156">Folder główny katalog roboczy jest nazywany "ScopeWorkDir" i pliki w katalogu roboczego są następujące:</span><span class="sxs-lookup"><span data-stu-id="2e030-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="2e030-157">Pliku lub katalogu</span><span class="sxs-lookup"><span data-stu-id="2e030-157">Directory/file</span></span>|<span data-ttu-id="2e030-158">Pliku lub katalogu</span><span class="sxs-lookup"><span data-stu-id="2e030-158">Directory/file</span></span>|<span data-ttu-id="2e030-159">Pliku lub katalogu</span><span class="sxs-lookup"><span data-stu-id="2e030-159">Directory/file</span></span>|<span data-ttu-id="2e030-160">Definicja</span><span class="sxs-lookup"><span data-stu-id="2e030-160">Definition</span></span>|<span data-ttu-id="2e030-161">Opis</span><span class="sxs-lookup"><span data-stu-id="2e030-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="2e030-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="2e030-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="2e030-163">Ciąg skrótu wersji środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="2e030-163">Hash string of runtime version</span></span>|<span data-ttu-id="2e030-164">Pliki środowiska uruchomieniowego niezbędne do wykonania lokalnej kopii w tle</span><span class="sxs-lookup"><span data-stu-id="2e030-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="2e030-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="2e030-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="2e030-166">Nazwa skryptu + wyznaczania wartości skrótu ciągu ścieżki skryptu</span><span class="sxs-lookup"><span data-stu-id="2e030-166">Script name + hash string of script path</span></span>|<span data-ttu-id="2e030-167">Dane wyjściowe kompilacji i wykonywanie kroku rejestrowania</span><span class="sxs-lookup"><span data-stu-id="2e030-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="2e030-168">\_skrypt\_.abr</span><span class="sxs-lookup"><span data-stu-id="2e030-168">\_script\_.abr</span></span>|<span data-ttu-id="2e030-169">Dane wyjściowe kompilatora</span><span class="sxs-lookup"><span data-stu-id="2e030-169">Compiler output</span></span>|<span data-ttu-id="2e030-170">Plik algebraiczną</span><span class="sxs-lookup"><span data-stu-id="2e030-170">Algebra file</span></span>|
| | |<span data-ttu-id="2e030-171">\_ScopeCodeGen\_. *</span><span class="sxs-lookup"><span data-stu-id="2e030-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="2e030-172">Dane wyjściowe kompilatora</span><span class="sxs-lookup"><span data-stu-id="2e030-172">Compiler output</span></span>|<span data-ttu-id="2e030-173">Wygenerowanego kodu zarządzanego</span><span class="sxs-lookup"><span data-stu-id="2e030-173">Generated managed code</span></span>|
| | |<span data-ttu-id="2e030-174">\_ScopeCodeGenEngine\_. *</span><span class="sxs-lookup"><span data-stu-id="2e030-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="2e030-175">Dane wyjściowe kompilatora</span><span class="sxs-lookup"><span data-stu-id="2e030-175">Compiler output</span></span>|<span data-ttu-id="2e030-176">Wygenerowany kod natywny</span><span class="sxs-lookup"><span data-stu-id="2e030-176">Generated native code</span></span>|
| | |<span data-ttu-id="2e030-177">przywoływanych zestawach</span><span class="sxs-lookup"><span data-stu-id="2e030-177">referenced assemblies</span></span>|<span data-ttu-id="2e030-178">Odwołanie do zestawu</span><span class="sxs-lookup"><span data-stu-id="2e030-178">Assembly reference</span></span>|<span data-ttu-id="2e030-179">Przywoływany zestaw plików</span><span class="sxs-lookup"><span data-stu-id="2e030-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="2e030-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="2e030-180">deployed_resources</span></span>|<span data-ttu-id="2e030-181">Wdrażanie zasobu</span><span class="sxs-lookup"><span data-stu-id="2e030-181">Resource deployment</span></span>|<span data-ttu-id="2e030-182">Pliki zasobów wdrożenia</span><span class="sxs-lookup"><span data-stu-id="2e030-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="2e030-183">xxxxxxxx.xxx[1..n]\_\*. *</span><span class="sxs-lookup"><span data-stu-id="2e030-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="2e030-184">Dziennik wykonywania.</span><span class="sxs-lookup"><span data-stu-id="2e030-184">Execution log</span></span>|<span data-ttu-id="2e030-185">Dziennik wykonywania czynności</span><span class="sxs-lookup"><span data-stu-id="2e030-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="2e030-186">Korzystanie z zestawu SDK z poziomu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="2e030-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="2e030-187">Interfejs wiersza polecenia z aplikacją pomocniczą</span><span class="sxs-lookup"><span data-stu-id="2e030-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="2e030-188">W obszarze SDK directory\build\runtime LocalRunHelper.exe to aplikacja pomocnika wiersza polecenia, która zapewnia interfejsy do większości często używane funkcje lokalnego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="2e030-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="2e030-189">Należy pamiętać, że zarówno polecenia i przełączniki argumentów jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="2e030-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="2e030-190">Aby wywołać go:</span><span class="sxs-lookup"><span data-stu-id="2e030-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="2e030-191">Uruchom LocalRunHelper.exe bez argumentów lub z **pomocy** przełącznik, aby wyświetlić informacje pomocy:</span><span class="sxs-lookup"><span data-stu-id="2e030-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="2e030-192">Informacje pomocy:</span><span class="sxs-lookup"><span data-stu-id="2e030-192">In the help information:</span></span>

-  <span data-ttu-id="2e030-193">**Polecenie** nadaje nazwę polecenia.</span><span class="sxs-lookup"><span data-stu-id="2e030-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="2e030-194">**Argument wymagany** listę argumentów, które należy podać.</span><span class="sxs-lookup"><span data-stu-id="2e030-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="2e030-195">**Opcjonalny Argument** listę argumentów, które są opcjonalne, wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="2e030-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="2e030-196">Logiczna Argumenty opcjonalne nie ma parametrów, a ich wyglądu oznacza ujemna przywrócić wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="2e030-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="2e030-197">Wartość zwracana i rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="2e030-197">Return value and logging</span></span>

<span data-ttu-id="2e030-198">Zwraca aplikacją pomocniczą **0** w przypadku powodzenia i **-1** niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="2e030-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="2e030-199">Domyślnie pomocnika wysyła komunikaty do bieżącej konsoli.</span><span class="sxs-lookup"><span data-stu-id="2e030-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="2e030-200">Jednak większość potrzebnych poleceń obsługuje **path_to_log_file - MessageOut** opcjonalny argument, który przekierowuje dane wyjściowe do pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="2e030-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="2e030-201">Konfigurowanie zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="2e030-201">Environment variable configuring</span></span>

<span data-ttu-id="2e030-202">Uruchom wymaga głównego określone dane jako konto magazynu lokalnego, jak i zależności dla określonej ścieżki CppSDK lokalnego U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2e030-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="2e030-203">Można jednocześnie ustawić argument w zmiennej środowiskowej wiersza polecenia lub ustaw dla nich.</span><span class="sxs-lookup"><span data-stu-id="2e030-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="2e030-204">Ustaw **SCOPE_CPP_SDK** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="2e030-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="2e030-205">Jeśli środowisko Microsoft Visual C++ i zestaw Windows SDK, instalując narzędzi Data Lake Tools dla programu Visual Studio, sprawdź, czy następujący folder:</span><span class="sxs-lookup"><span data-stu-id="2e030-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="2e030-206">Zdefiniuj nową zmienną środowiskową o nazwie **SCOPE_CPP_SDK** wskaż tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="2e030-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="2e030-207">Skopiuj folder do innej lokalizacji lub określ **SCOPE_CPP_SDK** jak.</span><span class="sxs-lookup"><span data-stu-id="2e030-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="2e030-208">Oprócz ustawienie zmiennej środowiskowej, można określić **- CppSDK** argumentu podczas korzystania z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2e030-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="2e030-209">Ten argument jest zastąpienie zmiennej środowiskowej CppSDK Twojego domyślne.</span><span class="sxs-lookup"><span data-stu-id="2e030-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="2e030-210">Ustaw **LOCALRUN_DATAROOT** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="2e030-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="2e030-211">Zdefiniuj nową zmienną środowiskową o nazwie **LOCALRUN_DATAROOT** wskazującego w katalogu głównym danych.</span><span class="sxs-lookup"><span data-stu-id="2e030-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="2e030-212">Oprócz ustawienie zmiennej środowiskowej, można określić **- DataRoot** argumentu ze ścieżką katalogu głównym danych podczas korzystania z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2e030-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="2e030-213">Ten argument zastępuje zmiennej środowiskowej katalogu głównym danych programu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="2e030-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="2e030-214">Należy dodać ten argument do każdego wiersza polecenia, którego używasz, dzięki czemu mogą zastępować zmiennej środowiskowej danych głównych domyślnego dla wszystkich operacji.</span><span class="sxs-lookup"><span data-stu-id="2e030-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="2e030-215">Przykłady użycia wiersza polecenia zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="2e030-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="2e030-216">Kompilowanie i uruchamianie</span><span class="sxs-lookup"><span data-stu-id="2e030-216">Compile and run</span></span>

<span data-ttu-id="2e030-217">**Uruchom** polecenie służy do Kompiluj skrypt, a następnie wykonaj skompilowanych wyników.</span><span class="sxs-lookup"><span data-stu-id="2e030-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="2e030-218">Argumenty wiersza polecenia są kombinacją od **skompilować** i **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="2e030-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="2e030-219">Poniżej przedstawiono opcjonalne argumenty **Uruchom**:</span><span class="sxs-lookup"><span data-stu-id="2e030-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="2e030-220">Argument</span><span class="sxs-lookup"><span data-stu-id="2e030-220">Argument</span></span>|<span data-ttu-id="2e030-221">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="2e030-221">Default value</span></span>|<span data-ttu-id="2e030-222">Opis</span><span class="sxs-lookup"><span data-stu-id="2e030-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="2e030-223">Plik CodeBehind-</span><span class="sxs-lookup"><span data-stu-id="2e030-223">-CodeBehind</span></span>|<span data-ttu-id="2e030-224">False</span><span class="sxs-lookup"><span data-stu-id="2e030-224">False</span></span>|<span data-ttu-id="2e030-225">Skrypt ma .cs kodzie</span><span class="sxs-lookup"><span data-stu-id="2e030-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="2e030-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="2e030-226">-CppSDK</span></span>| |<span data-ttu-id="2e030-227">CppSDK katalogu</span><span class="sxs-lookup"><span data-stu-id="2e030-227">CppSDK Directory</span></span>|
|<span data-ttu-id="2e030-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="2e030-228">-DataRoot</span></span>| <span data-ttu-id="2e030-229">Zmienna środowiskowa DataRoot</span><span class="sxs-lookup"><span data-stu-id="2e030-229">DataRoot environment variable</span></span>|<span data-ttu-id="2e030-230">DataRoot dla lokalnego uruchomienia domyślną do zmiennej środowiskowej "LOCALRUN_DATAROOT"</span><span class="sxs-lookup"><span data-stu-id="2e030-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="2e030-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="2e030-231">-MessageOut</span></span>| |<span data-ttu-id="2e030-232">Komunikaty w konsoli w pliku zrzutu</span><span class="sxs-lookup"><span data-stu-id="2e030-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="2e030-233">-Równoległe</span><span class="sxs-lookup"><span data-stu-id="2e030-233">-Parallel</span></span>|<span data-ttu-id="2e030-234">1</span><span class="sxs-lookup"><span data-stu-id="2e030-234">1</span></span>|<span data-ttu-id="2e030-235">Uruchom planu z określonym równoległości</span><span class="sxs-lookup"><span data-stu-id="2e030-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="2e030-236">— Odwołania</span><span class="sxs-lookup"><span data-stu-id="2e030-236">-References</span></span>| |<span data-ttu-id="2e030-237">Lista ścieżek do zestawów odwołań dodatkowe lub pliki danych w kodzie, oddzielone ";"</span><span class="sxs-lookup"><span data-stu-id="2e030-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="2e030-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="2e030-238">-UdoRedirect</span></span>|<span data-ttu-id="2e030-239">False</span><span class="sxs-lookup"><span data-stu-id="2e030-239">False</span></span>|<span data-ttu-id="2e030-240">Generowanie konfiguracji przekierowania zestawu Udo</span><span class="sxs-lookup"><span data-stu-id="2e030-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="2e030-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="2e030-241">-UseDatabase</span></span>|<span data-ttu-id="2e030-242">master</span><span class="sxs-lookup"><span data-stu-id="2e030-242">master</span></span>|<span data-ttu-id="2e030-243">Bazy danych do użycia na potrzeby kodu tymczasowej zestawu rejestracji</span><span class="sxs-lookup"><span data-stu-id="2e030-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="2e030-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="2e030-244">-Verbose</span></span>|<span data-ttu-id="2e030-245">False</span><span class="sxs-lookup"><span data-stu-id="2e030-245">False</span></span>|<span data-ttu-id="2e030-246">Pokaż szczegółowe dane wyjściowe z środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="2e030-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="2e030-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="2e030-247">-WorkDir</span></span>|<span data-ttu-id="2e030-248">Bieżący katalog</span><span class="sxs-lookup"><span data-stu-id="2e030-248">Current Directory</span></span>|<span data-ttu-id="2e030-249">Katalog dla kompilatora użycia i dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="2e030-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="2e030-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="2e030-250">-RunScopeCEP</span></span>|<span data-ttu-id="2e030-251">0</span><span class="sxs-lookup"><span data-stu-id="2e030-251">0</span></span>|<span data-ttu-id="2e030-252">Tryb ScopeCEP</span><span class="sxs-lookup"><span data-stu-id="2e030-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="2e030-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="2e030-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="2e030-254">Temp</span><span class="sxs-lookup"><span data-stu-id="2e030-254">temp</span></span>|<span data-ttu-id="2e030-255">Tymczasowy ścieżkę używaną do strumieniowego przesyłania danych</span><span class="sxs-lookup"><span data-stu-id="2e030-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="2e030-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="2e030-256">-OptFlags</span></span>| |<span data-ttu-id="2e030-257">Rozdzielana przecinkami lista flagi optymalizacji</span><span class="sxs-lookup"><span data-stu-id="2e030-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="2e030-258">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="2e030-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="2e030-259">Oprócz łączenie **skompilować** i **wykonania**, możesz skompilować i wykonywać skompilowane pliki wykonywalne niezależnie.</span><span class="sxs-lookup"><span data-stu-id="2e030-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="2e030-260">Kompiluj skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="2e030-260">Compile a U-SQL script</span></span>

<span data-ttu-id="2e030-261">**Skompilować** polecenia jest używana do kompilowania skryptu U-SQL do plików wykonywalnych.</span><span class="sxs-lookup"><span data-stu-id="2e030-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="2e030-262">Poniżej przedstawiono opcjonalne argumenty **skompilować**:</span><span class="sxs-lookup"><span data-stu-id="2e030-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="2e030-263">Argument</span><span class="sxs-lookup"><span data-stu-id="2e030-263">Argument</span></span>|<span data-ttu-id="2e030-264">Opis</span><span class="sxs-lookup"><span data-stu-id="2e030-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="2e030-265">-Plik CodeBehind [domyślna wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="2e030-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="2e030-266">Skrypt ma .cs kodzie</span><span class="sxs-lookup"><span data-stu-id="2e030-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="2e030-267">-CppSDK [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="2e030-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="2e030-268">CppSDK katalogu</span><span class="sxs-lookup"><span data-stu-id="2e030-268">CppSDK Directory</span></span>|
| <span data-ttu-id="2e030-269">-DataRoot [wartość domyślna "DataRoot zmiennej środowiskowej"]</span><span class="sxs-lookup"><span data-stu-id="2e030-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="2e030-270">DataRoot dla lokalnego uruchomienia domyślną do zmiennej środowiskowej "LOCALRUN_DATAROOT"</span><span class="sxs-lookup"><span data-stu-id="2e030-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="2e030-271">-MessageOut [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="2e030-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="2e030-272">Komunikaty w konsoli w pliku zrzutu</span><span class="sxs-lookup"><span data-stu-id="2e030-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="2e030-273">-Odwołuje się do [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="2e030-273">-References [default value '']</span></span>|<span data-ttu-id="2e030-274">Lista ścieżek do zestawów odwołań dodatkowe lub pliki danych w kodzie, oddzielone ";"</span><span class="sxs-lookup"><span data-stu-id="2e030-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="2e030-275">-Małym [domyślną wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="2e030-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="2e030-276">Skrócona kompilacji</span><span class="sxs-lookup"><span data-stu-id="2e030-276">Shallow compile</span></span>|
| <span data-ttu-id="2e030-277">-UdoRedirect [domyślna wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="2e030-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="2e030-278">Generowanie konfiguracji przekierowania zestawu Udo</span><span class="sxs-lookup"><span data-stu-id="2e030-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="2e030-279">-UseDatabase [wartość domyślna 'master']</span><span class="sxs-lookup"><span data-stu-id="2e030-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="2e030-280">Bazy danych do użycia na potrzeby kodu tymczasowej zestawu rejestracji</span><span class="sxs-lookup"><span data-stu-id="2e030-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="2e030-281">-WorkDir [wartość domyślna "Bieżący katalog"]</span><span class="sxs-lookup"><span data-stu-id="2e030-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="2e030-282">Katalog dla kompilatora użycia i dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="2e030-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="2e030-283">-RunScopeCEP [domyślna wartość "0"]</span><span class="sxs-lookup"><span data-stu-id="2e030-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="2e030-284">Tryb ScopeCEP</span><span class="sxs-lookup"><span data-stu-id="2e030-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="2e030-285">-ScopeCEPTempPath [wartość domyślna "temp"]</span><span class="sxs-lookup"><span data-stu-id="2e030-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="2e030-286">Tymczasowy ścieżkę używaną do strumieniowego przesyłania danych</span><span class="sxs-lookup"><span data-stu-id="2e030-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="2e030-287">-OptFlags [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="2e030-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="2e030-288">Rozdzielana przecinkami lista flagi optymalizacji</span><span class="sxs-lookup"><span data-stu-id="2e030-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="2e030-289">Oto kilka przykładów użycia.</span><span class="sxs-lookup"><span data-stu-id="2e030-289">Here are some usage examples.</span></span>

<span data-ttu-id="2e030-290">Kompiluj skrypt U-SQL:</span><span class="sxs-lookup"><span data-stu-id="2e030-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="2e030-291">Kompiluj skrypt U-SQL i ustaw folder główny danych.</span><span class="sxs-lookup"><span data-stu-id="2e030-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="2e030-292">Należy pamiętać, że spowoduje to zastąpienie ustaw dla zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="2e030-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="2e030-293">Kompiluj skrypt U-SQL i Ustaw katalog roboczy, odwołanie do zestawu i bazy danych:</span><span class="sxs-lookup"><span data-stu-id="2e030-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="2e030-294">Wykonanie skompilowanych wyników</span><span class="sxs-lookup"><span data-stu-id="2e030-294">Execute compiled results</span></span>

<span data-ttu-id="2e030-295">**Wykonania** polecenie służy do wykonywania skompilowanych wyników.</span><span class="sxs-lookup"><span data-stu-id="2e030-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="2e030-296">Poniżej przedstawiono opcjonalne argumenty **wykonania**:</span><span class="sxs-lookup"><span data-stu-id="2e030-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="2e030-297">Argument</span><span class="sxs-lookup"><span data-stu-id="2e030-297">Argument</span></span>|<span data-ttu-id="2e030-298">Opis</span><span class="sxs-lookup"><span data-stu-id="2e030-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="2e030-299">-DataRoot [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="2e030-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="2e030-300">Główny danych wykonywania metadanych.</span><span class="sxs-lookup"><span data-stu-id="2e030-300">Data root for metadata execution.</span></span> <span data-ttu-id="2e030-301">Domyślnie **LOCALRUN_DATAROOT** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="2e030-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="2e030-302">-MessageOut [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="2e030-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="2e030-303">Zrzut wiadomości na konsoli do pliku.</span><span class="sxs-lookup"><span data-stu-id="2e030-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="2e030-304">-Równoległe [domyślna wartość '1']</span><span class="sxs-lookup"><span data-stu-id="2e030-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="2e030-305">Wskaźnik wykonanie kroków wygenerowanego lokalnego uruchomienia równoległości określony poziom.</span><span class="sxs-lookup"><span data-stu-id="2e030-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="2e030-306">-Verbose [domyślna wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="2e030-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="2e030-307">Wskaźnik do wyświetlenia szczegółowych danych wyjściowych ze środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="2e030-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="2e030-308">Oto przykład użycia:</span><span class="sxs-lookup"><span data-stu-id="2e030-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="2e030-309">Interfejsy programowania za pomocą zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="2e030-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="2e030-310">Interfejsy programowania znajdują się w LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="2e030-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="2e030-311">Można używać ich do integracji funkcji zestawu SDK U-SQL oraz struktury testowej C#, aby skalować test lokalnego skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2e030-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="2e030-312">W tym artykule I używa standardowych C# jednostkowy projekt testowy do pokazują, jak używać tych interfejsów, aby przetestować skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2e030-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="2e030-313">Krok 1: Tworzenie projektu testu jednostki C# i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="2e030-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="2e030-314">Tworzenie projektu testu jednostki C# za pomocą pliku > Nowy > Projekt > Visual C# > Test > projektu testu jednostki.</span><span class="sxs-lookup"><span data-stu-id="2e030-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="2e030-315">Dodaj LocalRunHelper.exe jako odwołanie dla projektu.</span><span class="sxs-lookup"><span data-stu-id="2e030-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="2e030-316">LocalRunHelper.exe znajduje się pod adresem \build\runtime\LocalRunHelper.exe w pakiecie Nuget.</span><span class="sxs-lookup"><span data-stu-id="2e030-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Zestaw SDK usługi Azure Data Lake U-SQL Dodaj odwołanie](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="2e030-318">Zestaw SDK U-SQL **tylko** środowisko obsługi x64, upewnij się, by ustawić je jako x64 kompilacji platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="2e030-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="2e030-319">Które można ustawić za pomocą właściwości projektu > kompilacji > platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="2e030-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![Zestaw SDK usługi Azure Data Lake U-SQL skonfigurować x64 projektu](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="2e030-321">Upewnij się, by ustawić je jako x64 środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="2e030-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="2e030-322">W programie Visual Studio, możesz ustawić za pomocą testu > Testuj ustawienia > domyślny procesor > x64.</span><span class="sxs-lookup"><span data-stu-id="2e030-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Zestaw SDK usługi Azure Data Lake U-SQL skonfigurować x64 środowiska testowego](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="2e030-324">Upewnij się skopiować wszystkie pliki zależności w NugetPackage\build\runtime\ do katalogu, który zazwyczaj znajduje się w obszarze ProjectFolder\bin\x64\Debug roboczego projektu.</span><span class="sxs-lookup"><span data-stu-id="2e030-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="2e030-325">Krok 2: Tworzenie przypadku testowego skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="2e030-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="2e030-326">Poniżej znajduje się przykładowy kod dla testu skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2e030-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="2e030-327">Do testowania, musisz przygotować skrypty, pliki wejściowe i oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2e030-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget to close MessageOutput to get logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="2e030-328">Interfejsy programowania w języku LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="2e030-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="2e030-329">LocalRunHelper.exe udostępnia interfejsów programowania dla kompilacji lokalnego skryptu U-SQL, uruchom itp. Poniżej wymieniono interfejsy.</span><span class="sxs-lookup"><span data-stu-id="2e030-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="2e030-330">**Konstruktor**</span><span class="sxs-lookup"><span data-stu-id="2e030-330">**Constructor**</span></span>

<span data-ttu-id="2e030-331">publiczny LocalRunHelper ([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="2e030-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="2e030-332">Parametr</span><span class="sxs-lookup"><span data-stu-id="2e030-332">Parameter</span></span>|<span data-ttu-id="2e030-333">Typ</span><span class="sxs-lookup"><span data-stu-id="2e030-333">Type</span></span>|<span data-ttu-id="2e030-334">Opis</span><span class="sxs-lookup"><span data-stu-id="2e030-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="2e030-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="2e030-335">messageOutput</span></span>|<span data-ttu-id="2e030-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="2e030-336">System.IO.TextWriter</span></span>|<span data-ttu-id="2e030-337">dane wyjściowe wiadomości ustawić wartości null przy użyciu konsoli</span><span class="sxs-lookup"><span data-stu-id="2e030-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="2e030-338">**Właściwości**</span><span class="sxs-lookup"><span data-stu-id="2e030-338">**Properties**</span></span>

|<span data-ttu-id="2e030-339">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2e030-339">Property</span></span>|<span data-ttu-id="2e030-340">Typ</span><span class="sxs-lookup"><span data-stu-id="2e030-340">Type</span></span>|<span data-ttu-id="2e030-341">Opis</span><span class="sxs-lookup"><span data-stu-id="2e030-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="2e030-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="2e030-342">AlgebraPath</span></span>|<span data-ttu-id="2e030-343">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-343">string</span></span>|<span data-ttu-id="2e030-344">Ścieżka do pliku algebraiczną (plik algebraiczną jest jednym z rezultatów kompilacji)</span><span class="sxs-lookup"><span data-stu-id="2e030-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="2e030-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="2e030-345">CodeBehindReferences</span></span>|<span data-ttu-id="2e030-346">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-346">string</span></span>|<span data-ttu-id="2e030-347">Jeśli skrypt ma dodatkowe kodzie odwołań, określ ścieżki oddzielone znakiem ";"</span><span class="sxs-lookup"><span data-stu-id="2e030-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="2e030-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="2e030-348">CppSdkDir</span></span>|<span data-ttu-id="2e030-349">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-349">string</span></span>|<span data-ttu-id="2e030-350">CppSDK katalogu</span><span class="sxs-lookup"><span data-stu-id="2e030-350">CppSDK directory</span></span>|
|<span data-ttu-id="2e030-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="2e030-351">CurrentDir</span></span>|<span data-ttu-id="2e030-352">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-352">string</span></span>|<span data-ttu-id="2e030-353">Bieżący katalog</span><span class="sxs-lookup"><span data-stu-id="2e030-353">Current directory</span></span>|
|<span data-ttu-id="2e030-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="2e030-354">DataRoot</span></span>|<span data-ttu-id="2e030-355">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-355">string</span></span>|<span data-ttu-id="2e030-356">Ścieżka katalogu głównego danych</span><span class="sxs-lookup"><span data-stu-id="2e030-356">Data root path</span></span>|
|<span data-ttu-id="2e030-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="2e030-357">DebuggerMailPath</span></span>|<span data-ttu-id="2e030-358">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-358">string</span></span>|<span data-ttu-id="2e030-359">Ścieżka do mailslot debugera</span><span class="sxs-lookup"><span data-stu-id="2e030-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="2e030-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="2e030-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="2e030-361">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2e030-361">bool</span></span>|<span data-ttu-id="2e030-362">Jeśli chcemy, aby generować przekierowywania zastąpienie konfiguracji ładowania zestawu</span><span class="sxs-lookup"><span data-stu-id="2e030-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="2e030-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="2e030-363">HasCodeBehind</span></span>|<span data-ttu-id="2e030-364">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2e030-364">bool</span></span>|<span data-ttu-id="2e030-365">Jeśli skrypt ma kodzie</span><span class="sxs-lookup"><span data-stu-id="2e030-365">If the script has code behind</span></span>|
|<span data-ttu-id="2e030-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="2e030-366">InputDir</span></span>|<span data-ttu-id="2e030-367">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-367">string</span></span>|<span data-ttu-id="2e030-368">Katalog dla danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="2e030-368">Directory for input data</span></span>|
|<span data-ttu-id="2e030-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="2e030-369">MessagePath</span></span>|<span data-ttu-id="2e030-370">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-370">string</span></span>|<span data-ttu-id="2e030-371">Ścieżka pliku zrzutu wiadomości</span><span class="sxs-lookup"><span data-stu-id="2e030-371">Message dump file path</span></span>|
|<span data-ttu-id="2e030-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="2e030-372">OutputDir</span></span>|<span data-ttu-id="2e030-373">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-373">string</span></span>|<span data-ttu-id="2e030-374">Katalog danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="2e030-374">Directory for output data</span></span>|
|<span data-ttu-id="2e030-375">Równoległość</span><span class="sxs-lookup"><span data-stu-id="2e030-375">Parallelism</span></span>|<span data-ttu-id="2e030-376">int</span><span class="sxs-lookup"><span data-stu-id="2e030-376">int</span></span>|<span data-ttu-id="2e030-377">Równoległość do uruchomienia algebraiczną</span><span class="sxs-lookup"><span data-stu-id="2e030-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="2e030-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="2e030-378">ParentPid</span></span>|<span data-ttu-id="2e030-379">int</span><span class="sxs-lookup"><span data-stu-id="2e030-379">int</span></span>|<span data-ttu-id="2e030-380">Identyfikator procesu elementu nadrzędnego, na którym monitoruje usługę, aby zakończyć, równa 0 lub negatywną ignorowanie</span><span class="sxs-lookup"><span data-stu-id="2e030-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="2e030-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="2e030-381">ResultPath</span></span>|<span data-ttu-id="2e030-382">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-382">string</span></span>|<span data-ttu-id="2e030-383">Ścieżka pliku zrzutu wyników</span><span class="sxs-lookup"><span data-stu-id="2e030-383">Result dump file path</span></span>|
|<span data-ttu-id="2e030-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="2e030-384">RuntimeDir</span></span>|<span data-ttu-id="2e030-385">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-385">string</span></span>|<span data-ttu-id="2e030-386">Katalogu środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="2e030-386">Runtime directory</span></span>|
|<span data-ttu-id="2e030-387">scriptPath</span><span class="sxs-lookup"><span data-stu-id="2e030-387">ScriptPath</span></span>|<span data-ttu-id="2e030-388">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-388">string</span></span>|<span data-ttu-id="2e030-389">Gdzie można znaleźć skryptu</span><span class="sxs-lookup"><span data-stu-id="2e030-389">Where to find the script</span></span>|
|<span data-ttu-id="2e030-390">Skrócona</span><span class="sxs-lookup"><span data-stu-id="2e030-390">Shallow</span></span>|<span data-ttu-id="2e030-391">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2e030-391">bool</span></span>|<span data-ttu-id="2e030-392">Skrócona kompilacji lub nie</span><span class="sxs-lookup"><span data-stu-id="2e030-392">Shallow compile or not</span></span>|
|<span data-ttu-id="2e030-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="2e030-393">TempDir</span></span>|<span data-ttu-id="2e030-394">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-394">string</span></span>|<span data-ttu-id="2e030-395">Katalog tymczasowy</span><span class="sxs-lookup"><span data-stu-id="2e030-395">Temp directory</span></span>|
|<span data-ttu-id="2e030-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="2e030-396">UseDataBase</span></span>|<span data-ttu-id="2e030-397">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-397">string</span></span>|<span data-ttu-id="2e030-398">Określ bazę danych do użycia na potrzeby kodzie rejestracji tymczasowego zestawu głównego domyślnie</span><span class="sxs-lookup"><span data-stu-id="2e030-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="2e030-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="2e030-399">WorkDir</span></span>|<span data-ttu-id="2e030-400">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2e030-400">string</span></span>|<span data-ttu-id="2e030-401">Preferowany katalog roboczy</span><span class="sxs-lookup"><span data-stu-id="2e030-401">Preferred working directory</span></span>|


<span data-ttu-id="2e030-402">**— Metoda**</span><span class="sxs-lookup"><span data-stu-id="2e030-402">**Method**</span></span>

|<span data-ttu-id="2e030-403">Metoda</span><span class="sxs-lookup"><span data-stu-id="2e030-403">Method</span></span>|<span data-ttu-id="2e030-404">Opis</span><span class="sxs-lookup"><span data-stu-id="2e030-404">Description</span></span>|<span data-ttu-id="2e030-405">Zwraca</span><span class="sxs-lookup"><span data-stu-id="2e030-405">Return</span></span>|<span data-ttu-id="2e030-406">Parametr</span><span class="sxs-lookup"><span data-stu-id="2e030-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="2e030-407">publiczny bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="2e030-407">public bool DoCompile()</span></span>|<span data-ttu-id="2e030-408">Kompiluj skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="2e030-408">Compile the U-SQL script</span></span>|<span data-ttu-id="2e030-409">Wartość true w przypadku powodzenia</span><span class="sxs-lookup"><span data-stu-id="2e030-409">True on success</span></span>| |
|<span data-ttu-id="2e030-410">publiczny bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="2e030-410">public bool DoExec()</span></span>|<span data-ttu-id="2e030-411">Skompilowany wynik wykonywania</span><span class="sxs-lookup"><span data-stu-id="2e030-411">Execute the compiled result</span></span>|<span data-ttu-id="2e030-412">Wartość true w przypadku powodzenia</span><span class="sxs-lookup"><span data-stu-id="2e030-412">True on success</span></span>| |
|<span data-ttu-id="2e030-413">publiczny bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="2e030-413">public bool DoRun()</span></span>|<span data-ttu-id="2e030-414">Uruchom skrypt U-SQL (kompilacji + Execute)</span><span class="sxs-lookup"><span data-stu-id="2e030-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="2e030-415">Wartość true w przypadku powodzenia</span><span class="sxs-lookup"><span data-stu-id="2e030-415">True on success</span></span>| |
|<span data-ttu-id="2e030-416">publiczny bool IsValidRuntimeDir (ciąg ścieżki)</span><span class="sxs-lookup"><span data-stu-id="2e030-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="2e030-417">Sprawdź, czy podana ścieżka jest runtime prawidłową ścieżkę</span><span class="sxs-lookup"><span data-stu-id="2e030-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="2e030-418">Wartość true dla prawidłowe</span><span class="sxs-lookup"><span data-stu-id="2e030-418">True for valid</span></span>|<span data-ttu-id="2e030-419">Ścieżka katalogu środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="2e030-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="2e030-420">Często zadawane pytania dotyczące typowych problem</span><span class="sxs-lookup"><span data-stu-id="2e030-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="2e030-421">Błąd 1:</span><span class="sxs-lookup"><span data-stu-id="2e030-421">Error 1:</span></span>
<span data-ttu-id="2e030-422">E_CSC_SYSTEM_INTERNAL: Błąd wewnętrzny!</span><span class="sxs-lookup"><span data-stu-id="2e030-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="2e030-423">Nie można załadować pliku lub zestawu 'ScopeEngineManaged.dll' lub jednej z jego zależności.</span><span class="sxs-lookup"><span data-stu-id="2e030-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="2e030-424">Nie można odnaleźć określonego modułu.</span><span class="sxs-lookup"><span data-stu-id="2e030-424">The specified module could not be found.</span></span>

<span data-ttu-id="2e030-425">Sprawdź, czy następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2e030-425">Please check the following:</span></span>

- <span data-ttu-id="2e030-426">Upewnij się, że masz x64 środowiska.</span><span class="sxs-lookup"><span data-stu-id="2e030-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="2e030-427">Platforma docelowa kompilacji i środowiska testowego należy x64, zapoznaj się **krok 1: tworzenie C# jednostki Testowanie projektu i konfiguracji** powyżej.</span><span class="sxs-lookup"><span data-stu-id="2e030-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="2e030-428">Upewnij się, że wszystkie pliki zależności w NugetPackage\build\runtime\ zostały skopiowane do katalogu roboczego projektu.</span><span class="sxs-lookup"><span data-stu-id="2e030-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2e030-429">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e030-429">Next steps</span></span>

* <span data-ttu-id="2e030-430">Aby dowiedzieć się więcej o języku U-SQL, zobacz [Wprowadzenie do języka U-SQL w usłudze Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2e030-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="2e030-431">Rejestrowanie informacji diagnostycznych, zobacz [uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="2e030-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="2e030-432">Aby wyświetlić bardziej złożonego zapytania, zobacz [analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="2e030-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="2e030-433">Aby wyświetlić szczegóły zadania, zobacz [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="2e030-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="2e030-434">Aby użyć widoku wykonania wierzchołka, zobacz [użyć widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="2e030-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
