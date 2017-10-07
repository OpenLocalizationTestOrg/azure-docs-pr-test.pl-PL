---
title: "aaaScale U-SQL lokalne uruchamianie i testowanie z zestawem SDK usługi Azure Data Lake U-SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse zestawu SDK usługi Azure Data Lake U-SQL tooscale U-SQL zadania lokalne uruchamianie i testowanie z wiersza polecenia i interfejsów programowania na na lokalnej stacji roboczej."
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
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="59871-103">Uruchamiania lokalnego skryptu U-SQL skali i testowania przy użyciu zestawu SDK usługi Azure Data Lake U-SQL</span><span class="sxs-lookup"><span data-stu-id="59871-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="59871-104">Podczas tworzenia skryptu U-SQL, jest typowe toorun i skrypt testu U-SQL lokalnie przed przesłać toocloud.</span><span class="sxs-lookup"><span data-stu-id="59871-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="59871-105">Azure Data Lake umożliwia pakietu Nuget o nazwie zestawu SDK usługi Azure Data Lake U-SQL, w tym scenariuszu, za pomocą którego można łatwo skalować uruchamiania lokalnego skryptu U-SQL i testowania.</span><span class="sxs-lookup"><span data-stu-id="59871-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="59871-106">Możliwe jest również możliwe toointegrate U-SQL testu z kompilacji hello tooautomate systemu CI (ciągłej integracji) i testowania.</span><span class="sxs-lookup"><span data-stu-id="59871-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="59871-107">Jeśli potrzebne informacje jak toomanually lokalnego Uruchom i debugowania skryptu U-SQL z narzędzi z graficznym interfejsem użytkownika, możesz użyć usługi Azure Data Lake Tools dla programu Visual Studio, w tym.</span><span class="sxs-lookup"><span data-stu-id="59871-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="59871-108">Dowiedz się więcej o [tutaj](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="59871-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="59871-109">Instalacja usługi Azure Data Lake U-SQL SDK</span><span class="sxs-lookup"><span data-stu-id="59871-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="59871-110">Możesz uzyskać hello zestawu SDK usługi Azure Data Lake U-SQL [tutaj](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) na Nuget.org. I przed jej użyciem należy upewnić się, że zależności w następujący sposób toomake.</span><span class="sxs-lookup"><span data-stu-id="59871-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="59871-111">Zależności</span><span class="sxs-lookup"><span data-stu-id="59871-111">Dependencies</span></span>

<span data-ttu-id="59871-112">Witaj Data Lake U-SQL SDK wymaga hello następujące zależności:</span><span class="sxs-lookup"><span data-stu-id="59871-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="59871-113">[Microsoft .NET Framework 4.6 lub nowszą](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="59871-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="59871-114">Microsoft Visual C++ 14 i zestaw Windows SDK 10.0.10240.0 lub nowszą (nazywany CppSDK w tym artykule).</span><span class="sxs-lookup"><span data-stu-id="59871-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="59871-115">Istnieją dwa sposoby tooget CppSDK:</span><span class="sxs-lookup"><span data-stu-id="59871-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="59871-116">Zainstaluj [programu Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="59871-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="59871-117">W folderze Program Files hello — na przykład C:\Program Files (x86) \Windows Kits\10\ będziesz mieć folderu \Windows Kits\10.</span><span class="sxs-lookup"><span data-stu-id="59871-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="59871-118">Można również hello wersji zestawu Windows 10 SDK w \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="59871-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="59871-119">Jeśli nie widzisz tych folderów, zainstaluj pakiet Visual Studio i można się tooselect hello zestawu Windows 10 SDK podczas instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="59871-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="59871-120">Jeśli masz to zainstalowane z programem Visual Studio kompilatora lokalne powitania U-SQL znajdziesz ją automatycznie.</span><span class="sxs-lookup"><span data-stu-id="59871-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Narzędzia Data Lake Tools dla programu Visual Studio lokalnego uruchomienia systemu Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="59871-122">Zainstaluj [Data Lake Tools dla programu Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="59871-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="59871-123">Znajdziesz się, że pliki Visual C++ i zestaw Windows SDK w C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK opakowane hello.</span><span class="sxs-lookup"><span data-stu-id="59871-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="59871-124">W takim przypadku kompilatora lokalne powitania U-SQL nie można automatycznie odnaleźć hello zależności.</span><span class="sxs-lookup"><span data-stu-id="59871-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="59871-125">Należy ścieżką CppSDK hello toospecify dla niego.</span><span class="sxs-lookup"><span data-stu-id="59871-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="59871-126">Możesz skopiować lokalizacji tooanother pliki hello lub użyj go jako jest.</span><span class="sxs-lookup"><span data-stu-id="59871-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="59871-127">Zrozumienie podstawowych pojęć</span><span class="sxs-lookup"><span data-stu-id="59871-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="59871-128">Główny danych</span><span class="sxs-lookup"><span data-stu-id="59871-128">Data root</span></span>

<span data-ttu-id="59871-129">folder główny danych Hello dotyczy konto obliczeniowe lokalne powitania "Magazyn lokalny".</span><span class="sxs-lookup"><span data-stu-id="59871-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="59871-130">To konto usługi Azure Data Lake Store równoważne toohello konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="59871-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="59871-131">Przełączanie tooa folder różnych głównych danych jest podobnie jak przełączanie tooa magazynu innego konta.</span><span class="sxs-lookup"><span data-stu-id="59871-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="59871-132">Jeśli chcesz tooaccess często udostępnionych danych z różnych głównych danych folderów, należy użyć ścieżek bezwzględnych w skryptach.</span><span class="sxs-lookup"><span data-stu-id="59871-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="59871-133">Lub Utwórz łącza symbolicznego systemu plików (na przykład **mklink** na NTFS) w obszarze hello danych głównych folder toopoint toohello udostępnionych danych.</span><span class="sxs-lookup"><span data-stu-id="59871-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="59871-134">folder główny danych Hello jest używany do:</span><span class="sxs-lookup"><span data-stu-id="59871-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="59871-135">Przechowywania metadanych lokalnego, w tym baz danych, tabel, przechowywanymi w tabeli funkcji (funkcji Tvf) i zestawy.</span><span class="sxs-lookup"><span data-stu-id="59871-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="59871-136">Wyszukiwanie hello danych wejściowych i wyjściowych ścieżek, które są zdefiniowane jako ścieżek względnych w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59871-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="59871-137">Używanie ścieżek względnych umożliwia łatwiejsze toodeploy Twojego tooAzure projektów języka U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59871-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="59871-138">Ścieżka pliku w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="59871-138">File path in U-SQL</span></span>

<span data-ttu-id="59871-139">W skryptów U-SQL, można użyć zarówno ścieżki względnej, jak i lokalną ścieżkę bezwzględną.</span><span class="sxs-lookup"><span data-stu-id="59871-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="59871-140">Ścieżka względna Hello jest ścieżka folderu względna toohello określony katalog główny danych.</span><span class="sxs-lookup"><span data-stu-id="59871-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="59871-141">Zaleca się, że można użyć "/" jako hello toomake separatora ścieżki skryptów zgodny z powitania po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="59871-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="59871-142">Oto kilka przykładów ścieżek względnych i ich równoważne ścieżki bezwzględnej.</span><span class="sxs-lookup"><span data-stu-id="59871-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="59871-143">W tym przykładzie C:\LocalRunDataRoot jest folder główny danych hello.</span><span class="sxs-lookup"><span data-stu-id="59871-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="59871-144">Ścieżka względna</span><span class="sxs-lookup"><span data-stu-id="59871-144">Relative path</span></span>|<span data-ttu-id="59871-145">Ścieżki bezwzględne</span><span class="sxs-lookup"><span data-stu-id="59871-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="59871-146">/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="59871-146">/abc/def/input.csv</span></span> |<span data-ttu-id="59871-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="59871-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="59871-148">ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="59871-148">abc/def/input.csv</span></span>  |<span data-ttu-id="59871-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="59871-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="59871-150">D:/ABC/DEF/Input.csv</span><span class="sxs-lookup"><span data-stu-id="59871-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="59871-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="59871-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="59871-152">Katalog roboczy</span><span class="sxs-lookup"><span data-stu-id="59871-152">Working directory</span></span>

<span data-ttu-id="59871-153">Podczas uruchamiania lokalnego skryptu U-SQL hello, przejdź do katalogu roboczego został utworzony podczas kompilacji w bieżącym katalogu uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="59871-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="59871-154">Ponadto danych wyjściowych kompilacji toohello, hello wymagane pliki środowiska uruchomieniowego dla lokalnych wykonań będzie katalog roboczy toothis skopiowane w tle.</span><span class="sxs-lookup"><span data-stu-id="59871-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="59871-155">katalog główny folder roboczy Hello jest nazywany "ScopeWorkDir" i hello pliki w katalogu roboczego hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="59871-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="59871-156">Pliku lub katalogu</span><span class="sxs-lookup"><span data-stu-id="59871-156">Directory/file</span></span>|<span data-ttu-id="59871-157">Pliku lub katalogu</span><span class="sxs-lookup"><span data-stu-id="59871-157">Directory/file</span></span>|<span data-ttu-id="59871-158">Pliku lub katalogu</span><span class="sxs-lookup"><span data-stu-id="59871-158">Directory/file</span></span>|<span data-ttu-id="59871-159">Definicja</span><span class="sxs-lookup"><span data-stu-id="59871-159">Definition</span></span>|<span data-ttu-id="59871-160">Opis</span><span class="sxs-lookup"><span data-stu-id="59871-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="59871-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="59871-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="59871-162">Ciąg skrótu wersji środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="59871-162">Hash string of runtime version</span></span>|<span data-ttu-id="59871-163">Pliki środowiska uruchomieniowego niezbędne do wykonania lokalnej kopii w tle</span><span class="sxs-lookup"><span data-stu-id="59871-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="59871-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="59871-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="59871-165">Nazwa skryptu + wyznaczania wartości skrótu ciągu ścieżki skryptu</span><span class="sxs-lookup"><span data-stu-id="59871-165">Script name + hash string of script path</span></span>|<span data-ttu-id="59871-166">Dane wyjściowe kompilacji i wykonywanie kroku rejestrowania</span><span class="sxs-lookup"><span data-stu-id="59871-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="59871-167">\_skrypt\_.abr</span><span class="sxs-lookup"><span data-stu-id="59871-167">\_script\_.abr</span></span>|<span data-ttu-id="59871-168">Dane wyjściowe kompilatora</span><span class="sxs-lookup"><span data-stu-id="59871-168">Compiler output</span></span>|<span data-ttu-id="59871-169">Plik algebraiczną</span><span class="sxs-lookup"><span data-stu-id="59871-169">Algebra file</span></span>|
| | |<span data-ttu-id="59871-170">\_ScopeCodeGen\_. *</span><span class="sxs-lookup"><span data-stu-id="59871-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="59871-171">Dane wyjściowe kompilatora</span><span class="sxs-lookup"><span data-stu-id="59871-171">Compiler output</span></span>|<span data-ttu-id="59871-172">Wygenerowanego kodu zarządzanego</span><span class="sxs-lookup"><span data-stu-id="59871-172">Generated managed code</span></span>|
| | |<span data-ttu-id="59871-173">\_ScopeCodeGenEngine\_. *</span><span class="sxs-lookup"><span data-stu-id="59871-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="59871-174">Dane wyjściowe kompilatora</span><span class="sxs-lookup"><span data-stu-id="59871-174">Compiler output</span></span>|<span data-ttu-id="59871-175">Wygenerowany kod natywny</span><span class="sxs-lookup"><span data-stu-id="59871-175">Generated native code</span></span>|
| | |<span data-ttu-id="59871-176">przywoływanych zestawach</span><span class="sxs-lookup"><span data-stu-id="59871-176">referenced assemblies</span></span>|<span data-ttu-id="59871-177">Odwołanie do zestawu</span><span class="sxs-lookup"><span data-stu-id="59871-177">Assembly reference</span></span>|<span data-ttu-id="59871-178">Przywoływany zestaw plików</span><span class="sxs-lookup"><span data-stu-id="59871-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="59871-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="59871-179">deployed_resources</span></span>|<span data-ttu-id="59871-180">Wdrażanie zasobu</span><span class="sxs-lookup"><span data-stu-id="59871-180">Resource deployment</span></span>|<span data-ttu-id="59871-181">Pliki zasobów wdrożenia</span><span class="sxs-lookup"><span data-stu-id="59871-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="59871-182">xxxxxxxx.xxx[1..n]\_\*. *</span><span class="sxs-lookup"><span data-stu-id="59871-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="59871-183">Dziennik wykonywania.</span><span class="sxs-lookup"><span data-stu-id="59871-183">Execution log</span></span>|<span data-ttu-id="59871-184">Dziennik wykonywania czynności</span><span class="sxs-lookup"><span data-stu-id="59871-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="59871-185">Użyj hello zestawu SDK z wiersza polecenia hello</span><span class="sxs-lookup"><span data-stu-id="59871-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="59871-186">Interfejs wiersza polecenia z aplikacją pomocniczą hello</span><span class="sxs-lookup"><span data-stu-id="59871-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="59871-187">W obszarze directory\build\runtime zestawu SDK LocalRunHelper.exe to aplikacja wiersza polecenia pomocnika hello, która zapewnia interfejsy toomost z najczęściej używanych hello lokalnego uruchomienia funkcji.</span><span class="sxs-lookup"><span data-stu-id="59871-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="59871-188">Należy pamiętać, że oba hello polecenia i przełączniki argumentów hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="59871-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="59871-189">tooinvoke go:</span><span class="sxs-lookup"><span data-stu-id="59871-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="59871-190">Uruchom LocalRunHelper.exe bez argumentów lub hello **pomocy** przełącznika tooshow hello informacje:</span><span class="sxs-lookup"><span data-stu-id="59871-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="59871-191">Informacje pomocy w hello:</span><span class="sxs-lookup"><span data-stu-id="59871-191">In hello help information:</span></span>

-  <span data-ttu-id="59871-192">**Polecenie** zapewnia hello nazwę polecenia.</span><span class="sxs-lookup"><span data-stu-id="59871-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="59871-193">**Argument wymagany** listę argumentów, które należy podać.</span><span class="sxs-lookup"><span data-stu-id="59871-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="59871-194">**Opcjonalny Argument** listę argumentów, które są opcjonalne, wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="59871-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="59871-195">Argumenty opcjonalne logicznych nie mają parametrów, a ich wyglądu oznaczają tootheir ujemna wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="59871-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="59871-196">Wartość zwracana i rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="59871-196">Return value and logging</span></span>

<span data-ttu-id="59871-197">Zwraca aplikacją pomocniczą Hello **0** w przypadku powodzenia i **-1** niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="59871-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="59871-198">Domyślnie pomocnika hello wysyła wszystkie komunikaty toohello bieżącej konsoli.</span><span class="sxs-lookup"><span data-stu-id="59871-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="59871-199">Jednak większość poleceń hello obsługuje hello **path_to_log_file - MessageOut** opcjonalny argument, który przekierowuje hello generuje plik dziennika tooa.</span><span class="sxs-lookup"><span data-stu-id="59871-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="59871-200">Konfigurowanie zmiennej środowiskowej</span><span class="sxs-lookup"><span data-stu-id="59871-200">Environment variable configuring</span></span>

<span data-ttu-id="59871-201">Uruchom wymaga głównego określone dane jako konto magazynu lokalnego, jak i zależności dla określonej ścieżki CppSDK lokalnego U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59871-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="59871-202">Możesz zarówno argument hello zestawu w zmiennej środowiskowej wiersza polecenia lub ustaw dla nich.</span><span class="sxs-lookup"><span data-stu-id="59871-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="59871-203">Zestaw hello **SCOPE_CPP_SDK** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="59871-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="59871-204">Jeśli środowisko Microsoft Visual C++ i zestawu SDK systemu Windows hello przez zainstalowanie narzędzi Data Lake Tools dla programu Visual Studio, sprawdź, czy hello następującego folderu:</span><span class="sxs-lookup"><span data-stu-id="59871-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="59871-205">Zdefiniuj nową zmienną środowiskową o nazwie **SCOPE_CPP_SDK** toopoint toothis katalogu.</span><span class="sxs-lookup"><span data-stu-id="59871-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="59871-206">Lub skopiuj toohello folderu hello z innej lokalizacji i określ **SCOPE_CPP_SDK** jak.</span><span class="sxs-lookup"><span data-stu-id="59871-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="59871-207">W zmiennej środowiskowej hello toosetting dodanie, można określić hello **- CppSDK** argumentu podczas korzystania z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="59871-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="59871-208">Ten argument jest zastąpienie zmiennej środowiskowej CppSDK Twojego domyślne.</span><span class="sxs-lookup"><span data-stu-id="59871-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="59871-209">Zestaw hello **LOCALRUN_DATAROOT** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="59871-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="59871-210">Zdefiniuj nową zmienną środowiskową o nazwie **LOCALRUN_DATAROOT** wskazującego toohello danych głównych.</span><span class="sxs-lookup"><span data-stu-id="59871-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="59871-211">W zmiennej środowiskowej hello toosetting dodanie, można określić hello **- DataRoot** argumentu ze ścieżką katalogu głównym danych hello podczas korzystania z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="59871-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="59871-212">Ten argument zastępuje zmiennej środowiskowej katalogu głównym danych programu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="59871-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="59871-213">Należy tooadd ten argument wiersza polecenia tooevery, których używasz, dzięki czemu mogą zastępować zmiennej środowiskowej hello domyślnego katalogu głównym danych dla wszystkich operacji.</span><span class="sxs-lookup"><span data-stu-id="59871-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="59871-214">Przykłady użycia wiersza polecenia zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="59871-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="59871-215">Kompilowanie i uruchamianie</span><span class="sxs-lookup"><span data-stu-id="59871-215">Compile and run</span></span>

<span data-ttu-id="59871-216">Witaj **Uruchom** używane jest polecenie toocompile hello skrypt, a następnie wykonaj skompilowanych wyników.</span><span class="sxs-lookup"><span data-stu-id="59871-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="59871-217">Argumenty wiersza polecenia są kombinacją od **skompilować** i **wykonania**.</span><span class="sxs-lookup"><span data-stu-id="59871-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="59871-218">Witaj następujące czynności są opcjonalne argumenty **Uruchom**:</span><span class="sxs-lookup"><span data-stu-id="59871-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="59871-219">Argument</span><span class="sxs-lookup"><span data-stu-id="59871-219">Argument</span></span>|<span data-ttu-id="59871-220">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="59871-220">Default value</span></span>|<span data-ttu-id="59871-221">Opis</span><span class="sxs-lookup"><span data-stu-id="59871-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="59871-222">Plik CodeBehind-</span><span class="sxs-lookup"><span data-stu-id="59871-222">-CodeBehind</span></span>|<span data-ttu-id="59871-223">False</span><span class="sxs-lookup"><span data-stu-id="59871-223">False</span></span>|<span data-ttu-id="59871-224">skrypt Hello ma .cs kodzie</span><span class="sxs-lookup"><span data-stu-id="59871-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="59871-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="59871-225">-CppSDK</span></span>| |<span data-ttu-id="59871-226">CppSDK katalogu</span><span class="sxs-lookup"><span data-stu-id="59871-226">CppSDK Directory</span></span>|
|<span data-ttu-id="59871-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="59871-227">-DataRoot</span></span>| <span data-ttu-id="59871-228">Zmienna środowiskowa DataRoot</span><span class="sxs-lookup"><span data-stu-id="59871-228">DataRoot environment variable</span></span>|<span data-ttu-id="59871-229">DataRoot dla przebiegu lokalnego zbyt domyślna zmiennej środowiskowej "LOCALRUN_DATAROOT"</span><span class="sxs-lookup"><span data-stu-id="59871-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="59871-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="59871-230">-MessageOut</span></span>| |<span data-ttu-id="59871-231">Komunikaty zrzutu w pliku tooa konsoli</span><span class="sxs-lookup"><span data-stu-id="59871-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="59871-232">-Równoległe</span><span class="sxs-lookup"><span data-stu-id="59871-232">-Parallel</span></span>|<span data-ttu-id="59871-233">1</span><span class="sxs-lookup"><span data-stu-id="59871-233">1</span></span>|<span data-ttu-id="59871-234">Uruchom hello wybrany plan z hello równoległości</span><span class="sxs-lookup"><span data-stu-id="59871-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="59871-235">— Odwołania</span><span class="sxs-lookup"><span data-stu-id="59871-235">-References</span></span>| |<span data-ttu-id="59871-236">Lista zestawów odwołań tooextra ścieżki lub pliki danych w kodzie, oddzielone ";"</span><span class="sxs-lookup"><span data-stu-id="59871-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="59871-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="59871-237">-UdoRedirect</span></span>|<span data-ttu-id="59871-238">False</span><span class="sxs-lookup"><span data-stu-id="59871-238">False</span></span>|<span data-ttu-id="59871-239">Generowanie konfiguracji przekierowania zestawu Udo</span><span class="sxs-lookup"><span data-stu-id="59871-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="59871-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="59871-240">-UseDatabase</span></span>|<span data-ttu-id="59871-241">master</span><span class="sxs-lookup"><span data-stu-id="59871-241">master</span></span>|<span data-ttu-id="59871-242">Toouse bazy danych dla kodu tymczasowej zestawu rejestracji</span><span class="sxs-lookup"><span data-stu-id="59871-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="59871-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="59871-243">-Verbose</span></span>|<span data-ttu-id="59871-244">False</span><span class="sxs-lookup"><span data-stu-id="59871-244">False</span></span>|<span data-ttu-id="59871-245">Pokaż szczegółowe dane wyjściowe z środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="59871-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="59871-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="59871-246">-WorkDir</span></span>|<span data-ttu-id="59871-247">Bieżący katalog</span><span class="sxs-lookup"><span data-stu-id="59871-247">Current Directory</span></span>|<span data-ttu-id="59871-248">Katalog dla kompilatora użycia i dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="59871-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="59871-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="59871-249">-RunScopeCEP</span></span>|<span data-ttu-id="59871-250">0</span><span class="sxs-lookup"><span data-stu-id="59871-250">0</span></span>|<span data-ttu-id="59871-251">Toouse tryb ScopeCEP</span><span class="sxs-lookup"><span data-stu-id="59871-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="59871-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="59871-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="59871-253">Temp</span><span class="sxs-lookup"><span data-stu-id="59871-253">temp</span></span>|<span data-ttu-id="59871-254">Toouse ścieżki tymczasowej do strumieniowego przesyłania danych</span><span class="sxs-lookup"><span data-stu-id="59871-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="59871-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="59871-255">-OptFlags</span></span>| |<span data-ttu-id="59871-256">Rozdzielana przecinkami lista flagi optymalizacji</span><span class="sxs-lookup"><span data-stu-id="59871-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="59871-257">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="59871-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="59871-258">Oprócz łączenie **skompilować** i **wykonania**, możesz skompilować i wykonywać hello skompilowane pliki wykonywalne niezależnie.</span><span class="sxs-lookup"><span data-stu-id="59871-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="59871-259">Kompiluj skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="59871-259">Compile a U-SQL script</span></span>

<span data-ttu-id="59871-260">Witaj **skompilować** polecenie jest tooexecutables skryptu używane toocompile U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59871-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="59871-261">Witaj następujące czynności są opcjonalne argumenty **skompilować**:</span><span class="sxs-lookup"><span data-stu-id="59871-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="59871-262">Argument</span><span class="sxs-lookup"><span data-stu-id="59871-262">Argument</span></span>|<span data-ttu-id="59871-263">Opis</span><span class="sxs-lookup"><span data-stu-id="59871-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="59871-264">-Plik CodeBehind [domyślna wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="59871-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="59871-265">skrypt Hello ma .cs kodzie</span><span class="sxs-lookup"><span data-stu-id="59871-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="59871-266">-CppSDK [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="59871-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="59871-267">CppSDK katalogu</span><span class="sxs-lookup"><span data-stu-id="59871-267">CppSDK Directory</span></span>|
| <span data-ttu-id="59871-268">-DataRoot [wartość domyślna "DataRoot zmiennej środowiskowej"]</span><span class="sxs-lookup"><span data-stu-id="59871-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="59871-269">DataRoot dla przebiegu lokalnego zbyt domyślna zmiennej środowiskowej "LOCALRUN_DATAROOT"</span><span class="sxs-lookup"><span data-stu-id="59871-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="59871-270">-MessageOut [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="59871-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="59871-271">Komunikaty zrzutu w pliku tooa konsoli</span><span class="sxs-lookup"><span data-stu-id="59871-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="59871-272">-Odwołuje się do [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="59871-272">-References [default value '']</span></span>|<span data-ttu-id="59871-273">Lista zestawów odwołań tooextra ścieżki lub pliki danych w kodzie, oddzielone ";"</span><span class="sxs-lookup"><span data-stu-id="59871-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="59871-274">-Małym [domyślną wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="59871-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="59871-275">Skrócona kompilacji</span><span class="sxs-lookup"><span data-stu-id="59871-275">Shallow compile</span></span>|
| <span data-ttu-id="59871-276">-UdoRedirect [domyślna wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="59871-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="59871-277">Generowanie konfiguracji przekierowania zestawu Udo</span><span class="sxs-lookup"><span data-stu-id="59871-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="59871-278">-UseDatabase [wartość domyślna 'master']</span><span class="sxs-lookup"><span data-stu-id="59871-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="59871-279">Toouse bazy danych dla kodu tymczasowej zestawu rejestracji</span><span class="sxs-lookup"><span data-stu-id="59871-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="59871-280">-WorkDir [wartość domyślna "Bieżący katalog"]</span><span class="sxs-lookup"><span data-stu-id="59871-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="59871-281">Katalog dla kompilatora użycia i dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="59871-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="59871-282">-RunScopeCEP [domyślna wartość "0"]</span><span class="sxs-lookup"><span data-stu-id="59871-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="59871-283">Toouse tryb ScopeCEP</span><span class="sxs-lookup"><span data-stu-id="59871-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="59871-284">-ScopeCEPTempPath [wartość domyślna "temp"]</span><span class="sxs-lookup"><span data-stu-id="59871-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="59871-285">Toouse ścieżki tymczasowej do strumieniowego przesyłania danych</span><span class="sxs-lookup"><span data-stu-id="59871-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="59871-286">-OptFlags [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="59871-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="59871-287">Rozdzielana przecinkami lista flagi optymalizacji</span><span class="sxs-lookup"><span data-stu-id="59871-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="59871-288">Oto kilka przykładów użycia.</span><span class="sxs-lookup"><span data-stu-id="59871-288">Here are some usage examples.</span></span>

<span data-ttu-id="59871-289">Kompiluj skrypt U-SQL:</span><span class="sxs-lookup"><span data-stu-id="59871-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="59871-290">Kompiluj skrypt U-SQL i ustaw folder główny danych hello.</span><span class="sxs-lookup"><span data-stu-id="59871-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="59871-291">Należy pamiętać, że spowoduje to zastąpienie hello ustaw dla zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="59871-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="59871-292">Kompiluj skrypt U-SQL i Ustaw katalog roboczy, odwołanie do zestawu i bazy danych:</span><span class="sxs-lookup"><span data-stu-id="59871-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="59871-293">Wykonanie skompilowanych wyników</span><span class="sxs-lookup"><span data-stu-id="59871-293">Execute compiled results</span></span>

<span data-ttu-id="59871-294">Witaj **wykonania** polecenia jest używane tooexecute skompilowany wyników.</span><span class="sxs-lookup"><span data-stu-id="59871-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="59871-295">Witaj następujące czynności są opcjonalne argumenty **wykonania**:</span><span class="sxs-lookup"><span data-stu-id="59871-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="59871-296">Argument</span><span class="sxs-lookup"><span data-stu-id="59871-296">Argument</span></span>|<span data-ttu-id="59871-297">Opis</span><span class="sxs-lookup"><span data-stu-id="59871-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="59871-298">-DataRoot [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="59871-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="59871-299">Główny danych wykonywania metadanych.</span><span class="sxs-lookup"><span data-stu-id="59871-299">Data root for metadata execution.</span></span> <span data-ttu-id="59871-300">Domyślnie toohello **LOCALRUN_DATAROOT** zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="59871-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="59871-301">-MessageOut [wartość domyślna "]</span><span class="sxs-lookup"><span data-stu-id="59871-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="59871-302">Zrzut wiadomości powitania konsoli tooa pliku.</span><span class="sxs-lookup"><span data-stu-id="59871-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="59871-303">-Równoległe [domyślna wartość '1']</span><span class="sxs-lookup"><span data-stu-id="59871-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="59871-304">Wskaźnik toorun hello wygenerowany lokalnego wykonywania kroków za pomocą hello określony poziom równoległości.</span><span class="sxs-lookup"><span data-stu-id="59871-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="59871-305">-Verbose [domyślna wartość 'False']</span><span class="sxs-lookup"><span data-stu-id="59871-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="59871-306">Wskaźnik tooshow szczegółowe dane wyjściowe z środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="59871-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="59871-307">Oto przykład użycia:</span><span class="sxs-lookup"><span data-stu-id="59871-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="59871-308">Witaj SDK za pomocą interfejsów programowania</span><span class="sxs-lookup"><span data-stu-id="59871-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="59871-309">interfejsy programowania Hello znajdują się w hello LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="59871-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="59871-310">Można używać ich funkcji hello toointegrate hello SDK U-SQL i hello C# test framework tooscale test lokalnego skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59871-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="59871-311">W tym artykule będzie używać hello standard języka C# jednostki testu projektu tooshow jak toouse te interfejsy tootest skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59871-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="59871-312">Krok 1: Tworzenie projektu testu jednostki C# i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="59871-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="59871-313">Tworzenie projektu testu jednostki C# za pomocą pliku > Nowy > Projekt > Visual C# > Test > projektu testu jednostki.</span><span class="sxs-lookup"><span data-stu-id="59871-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="59871-314">Dodaj LocalRunHelper.exe jako punkt odniesienia dla hello projektu.</span><span class="sxs-lookup"><span data-stu-id="59871-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="59871-315">Witaj LocalRunHelper.exe znajduje się pod adresem \build\runtime\LocalRunHelper.exe w pakiecie Nuget.</span><span class="sxs-lookup"><span data-stu-id="59871-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Zestaw SDK usługi Azure Data Lake U-SQL Dodaj odwołanie](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="59871-317">Zestaw SDK U-SQL **tylko** środowisko obsługi x64, upewnij się, że tooset kompilacji platformy docelowej jako x64.</span><span class="sxs-lookup"><span data-stu-id="59871-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="59871-318">Które można ustawić za pomocą właściwości projektu > kompilacji > platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="59871-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Zestaw SDK usługi Azure Data Lake U-SQL skonfigurować x64 projektu](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="59871-320">Upewnij się, że tooset środowiska testowego jako x64.</span><span class="sxs-lookup"><span data-stu-id="59871-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="59871-321">W programie Visual Studio, możesz ustawić za pomocą testu > Testuj ustawienia > domyślny procesor > x64.</span><span class="sxs-lookup"><span data-stu-id="59871-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Zestaw SDK usługi Azure Data Lake U-SQL skonfigurować x64 środowiska testowego](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="59871-323">Upewnij się, że toocopy wszystkie pliki zależności w katalogu roboczego tooproject NugetPackage\build\runtime\, który zazwyczaj znajduje się w obszarze ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="59871-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="59871-324">Krok 2: Tworzenie przypadku testowego skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="59871-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="59871-325">Poniżej znajduje się hello przykładowy kod dla testu skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="59871-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="59871-326">Do testowania, należy tooprepare skrypty, pliki wejściowe i oczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="59871-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

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
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
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

                //Don't forget tooclose MessageOutput tooget logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="59871-327">Interfejsy programowania w języku LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="59871-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="59871-328">LocalRunHelper.exe zapewnia hello interfejsów dla kompilacji lokalnego skryptu U-SQL, uruchom programowania, interfejsy hello itp., są następujące.</span><span class="sxs-lookup"><span data-stu-id="59871-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="59871-329">**Konstruktor**</span><span class="sxs-lookup"><span data-stu-id="59871-329">**Constructor**</span></span>

<span data-ttu-id="59871-330">publiczny LocalRunHelper ([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="59871-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="59871-331">Parametr</span><span class="sxs-lookup"><span data-stu-id="59871-331">Parameter</span></span>|<span data-ttu-id="59871-332">Typ</span><span class="sxs-lookup"><span data-stu-id="59871-332">Type</span></span>|<span data-ttu-id="59871-333">Opis</span><span class="sxs-lookup"><span data-stu-id="59871-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="59871-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="59871-334">messageOutput</span></span>|<span data-ttu-id="59871-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="59871-335">System.IO.TextWriter</span></span>|<span data-ttu-id="59871-336">komunikaty Ustaw toouse toonull konsoli</span><span class="sxs-lookup"><span data-stu-id="59871-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="59871-337">**Właściwości**</span><span class="sxs-lookup"><span data-stu-id="59871-337">**Properties**</span></span>

|<span data-ttu-id="59871-338">Właściwość</span><span class="sxs-lookup"><span data-stu-id="59871-338">Property</span></span>|<span data-ttu-id="59871-339">Typ</span><span class="sxs-lookup"><span data-stu-id="59871-339">Type</span></span>|<span data-ttu-id="59871-340">Opis</span><span class="sxs-lookup"><span data-stu-id="59871-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="59871-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="59871-341">AlgebraPath</span></span>|<span data-ttu-id="59871-342">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-342">string</span></span>|<span data-ttu-id="59871-343">Witaj ścieżki tooalgebra pliku (pliku algebraiczną jest jeden z wyników kompilacji hello)</span><span class="sxs-lookup"><span data-stu-id="59871-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="59871-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="59871-344">CodeBehindReferences</span></span>|<span data-ttu-id="59871-345">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-345">string</span></span>|<span data-ttu-id="59871-346">Jeśli skrypt hello ma dodatkowe kodzie odwołań, określ ścieżki hello oddzielone znakiem ";"</span><span class="sxs-lookup"><span data-stu-id="59871-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="59871-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="59871-347">CppSdkDir</span></span>|<span data-ttu-id="59871-348">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-348">string</span></span>|<span data-ttu-id="59871-349">CppSDK katalogu</span><span class="sxs-lookup"><span data-stu-id="59871-349">CppSDK directory</span></span>|
|<span data-ttu-id="59871-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="59871-350">CurrentDir</span></span>|<span data-ttu-id="59871-351">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-351">string</span></span>|<span data-ttu-id="59871-352">Bieżący katalog</span><span class="sxs-lookup"><span data-stu-id="59871-352">Current directory</span></span>|
|<span data-ttu-id="59871-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="59871-353">DataRoot</span></span>|<span data-ttu-id="59871-354">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-354">string</span></span>|<span data-ttu-id="59871-355">Ścieżka katalogu głównego danych</span><span class="sxs-lookup"><span data-stu-id="59871-355">Data root path</span></span>|
|<span data-ttu-id="59871-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="59871-356">DebuggerMailPath</span></span>|<span data-ttu-id="59871-357">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-357">string</span></span>|<span data-ttu-id="59871-358">Witaj ścieżki toodebugger mailslot</span><span class="sxs-lookup"><span data-stu-id="59871-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="59871-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="59871-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="59871-360">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="59871-360">bool</span></span>|<span data-ttu-id="59871-361">Jeśli chcemy ładowania zestawu toogenerate przekierowania zastępują konfiguracji</span><span class="sxs-lookup"><span data-stu-id="59871-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="59871-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="59871-362">HasCodeBehind</span></span>|<span data-ttu-id="59871-363">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="59871-363">bool</span></span>|<span data-ttu-id="59871-364">Jeśli skrypt hello ma kodzie</span><span class="sxs-lookup"><span data-stu-id="59871-364">If hello script has code behind</span></span>|
|<span data-ttu-id="59871-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="59871-365">InputDir</span></span>|<span data-ttu-id="59871-366">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-366">string</span></span>|<span data-ttu-id="59871-367">Katalog dla danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="59871-367">Directory for input data</span></span>|
|<span data-ttu-id="59871-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="59871-368">MessagePath</span></span>|<span data-ttu-id="59871-369">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-369">string</span></span>|<span data-ttu-id="59871-370">Ścieżka pliku zrzutu wiadomości</span><span class="sxs-lookup"><span data-stu-id="59871-370">Message dump file path</span></span>|
|<span data-ttu-id="59871-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="59871-371">OutputDir</span></span>|<span data-ttu-id="59871-372">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-372">string</span></span>|<span data-ttu-id="59871-373">Katalog danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="59871-373">Directory for output data</span></span>|
|<span data-ttu-id="59871-374">Równoległość</span><span class="sxs-lookup"><span data-stu-id="59871-374">Parallelism</span></span>|<span data-ttu-id="59871-375">int</span><span class="sxs-lookup"><span data-stu-id="59871-375">int</span></span>|<span data-ttu-id="59871-376">Równoległość toorun hello algebraiczną</span><span class="sxs-lookup"><span data-stu-id="59871-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="59871-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="59871-377">ParentPid</span></span>|<span data-ttu-id="59871-378">int</span><span class="sxs-lookup"><span data-stu-id="59871-378">int</span></span>|<span data-ttu-id="59871-379">Identyfikator PID procesu hello elementu nadrzędnego, na które hello monitoruje tooexit, too0 zestaw lub tooignore ujemna</span><span class="sxs-lookup"><span data-stu-id="59871-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="59871-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="59871-380">ResultPath</span></span>|<span data-ttu-id="59871-381">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-381">string</span></span>|<span data-ttu-id="59871-382">Ścieżka pliku zrzutu wyników</span><span class="sxs-lookup"><span data-stu-id="59871-382">Result dump file path</span></span>|
|<span data-ttu-id="59871-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="59871-383">RuntimeDir</span></span>|<span data-ttu-id="59871-384">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-384">string</span></span>|<span data-ttu-id="59871-385">Katalogu środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="59871-385">Runtime directory</span></span>|
|<span data-ttu-id="59871-386">scriptPath</span><span class="sxs-lookup"><span data-stu-id="59871-386">ScriptPath</span></span>|<span data-ttu-id="59871-387">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-387">string</span></span>|<span data-ttu-id="59871-388">Gdzie toofind hello skryptu</span><span class="sxs-lookup"><span data-stu-id="59871-388">Where toofind hello script</span></span>|
|<span data-ttu-id="59871-389">Skrócona</span><span class="sxs-lookup"><span data-stu-id="59871-389">Shallow</span></span>|<span data-ttu-id="59871-390">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="59871-390">bool</span></span>|<span data-ttu-id="59871-391">Skrócona kompilacji lub nie</span><span class="sxs-lookup"><span data-stu-id="59871-391">Shallow compile or not</span></span>|
|<span data-ttu-id="59871-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="59871-392">TempDir</span></span>|<span data-ttu-id="59871-393">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-393">string</span></span>|<span data-ttu-id="59871-394">Katalog tymczasowy</span><span class="sxs-lookup"><span data-stu-id="59871-394">Temp directory</span></span>|
|<span data-ttu-id="59871-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="59871-395">UseDataBase</span></span>|<span data-ttu-id="59871-396">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-396">string</span></span>|<span data-ttu-id="59871-397">Określ hello toouse bazy danych dla kodzie rejestracji tymczasowego zestawu głównego domyślnie</span><span class="sxs-lookup"><span data-stu-id="59871-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="59871-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="59871-398">WorkDir</span></span>|<span data-ttu-id="59871-399">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59871-399">string</span></span>|<span data-ttu-id="59871-400">Preferowany katalog roboczy</span><span class="sxs-lookup"><span data-stu-id="59871-400">Preferred working directory</span></span>|


<span data-ttu-id="59871-401">**— Metoda**</span><span class="sxs-lookup"><span data-stu-id="59871-401">**Method**</span></span>

|<span data-ttu-id="59871-402">Metoda</span><span class="sxs-lookup"><span data-stu-id="59871-402">Method</span></span>|<span data-ttu-id="59871-403">Opis</span><span class="sxs-lookup"><span data-stu-id="59871-403">Description</span></span>|<span data-ttu-id="59871-404">Zwraca</span><span class="sxs-lookup"><span data-stu-id="59871-404">Return</span></span>|<span data-ttu-id="59871-405">Parametr</span><span class="sxs-lookup"><span data-stu-id="59871-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="59871-406">publiczny bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="59871-406">public bool DoCompile()</span></span>|<span data-ttu-id="59871-407">Kompilacja skryptu hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="59871-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="59871-408">Wartość true w przypadku powodzenia</span><span class="sxs-lookup"><span data-stu-id="59871-408">True on success</span></span>| |
|<span data-ttu-id="59871-409">publiczny bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="59871-409">public bool DoExec()</span></span>|<span data-ttu-id="59871-410">Wykonanie hello skompilowany wyników</span><span class="sxs-lookup"><span data-stu-id="59871-410">Execute hello compiled result</span></span>|<span data-ttu-id="59871-411">Wartość true w przypadku powodzenia</span><span class="sxs-lookup"><span data-stu-id="59871-411">True on success</span></span>| |
|<span data-ttu-id="59871-412">publiczny bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="59871-412">public bool DoRun()</span></span>|<span data-ttu-id="59871-413">Uruchom skrypt U-SQL hello (kompilacji + Execute)</span><span class="sxs-lookup"><span data-stu-id="59871-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="59871-414">Wartość true w przypadku powodzenia</span><span class="sxs-lookup"><span data-stu-id="59871-414">True on success</span></span>| |
|<span data-ttu-id="59871-415">publiczny bool IsValidRuntimeDir (ciąg ścieżki)</span><span class="sxs-lookup"><span data-stu-id="59871-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="59871-416">Sprawdź, czy hello podanej ścieżki runtime prawidłową ścieżkę</span><span class="sxs-lookup"><span data-stu-id="59871-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="59871-417">Wartość true dla prawidłowe</span><span class="sxs-lookup"><span data-stu-id="59871-417">True for valid</span></span>|<span data-ttu-id="59871-418">Witaj ścieżkę katalogu środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="59871-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="59871-419">Często zadawane pytania dotyczące typowych problem</span><span class="sxs-lookup"><span data-stu-id="59871-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="59871-420">Błąd 1:</span><span class="sxs-lookup"><span data-stu-id="59871-420">Error 1:</span></span>
<span data-ttu-id="59871-421">E_CSC_SYSTEM_INTERNAL: Błąd wewnętrzny!</span><span class="sxs-lookup"><span data-stu-id="59871-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="59871-422">Nie można załadować pliku lub zestawu 'ScopeEngineManaged.dll' lub jednej z jego zależności.</span><span class="sxs-lookup"><span data-stu-id="59871-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="59871-423">Nie można odnaleźć określonego modułu Hello.</span><span class="sxs-lookup"><span data-stu-id="59871-423">hello specified module could not be found.</span></span>

<span data-ttu-id="59871-424">Sprawdź, czy następujące hello:</span><span class="sxs-lookup"><span data-stu-id="59871-424">Please check hello following:</span></span>

- <span data-ttu-id="59871-425">Upewnij się, że masz x64 środowiska.</span><span class="sxs-lookup"><span data-stu-id="59871-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="59871-426">Platforma docelowa kompilacji Hello i środowiska testowego hello powinien x64, zapoznaj się zbyt**krok 1: tworzenie C# jednostki Testowanie projektu i konfiguracji** powyżej.</span><span class="sxs-lookup"><span data-stu-id="59871-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="59871-427">Upewnij się, że zostały skopiowane wszystkie pliki zależności w katalogu roboczego tooproject NugetPackage\build\runtime\.</span><span class="sxs-lookup"><span data-stu-id="59871-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="59871-428">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59871-428">Next steps</span></span>

* <span data-ttu-id="59871-429">toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="59871-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="59871-430">informacje diagnostyczne toolog, zobacz [uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="59871-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="59871-431">toosee bardziej złożonego zapytania, zobacz [analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="59871-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="59871-432">Zobacz szczegóły zadania tooview, [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="59871-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="59871-433">widoku wykonania wierzchołka hello toouse, zobacz [hello użyj widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="59871-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
