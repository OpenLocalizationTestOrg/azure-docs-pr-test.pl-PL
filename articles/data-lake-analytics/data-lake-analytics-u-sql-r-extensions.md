---
title: "Rozszerzanie skryptów U-SQL z języka R w usłudze Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak uruchomić kod języka R w skryptów U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="c0e4e-103">Samouczek: Rozpoczynanie pracy z rozszerzanie U-SQL z języka R</span><span class="sxs-lookup"><span data-stu-id="c0e4e-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="c0e4e-104">Poniższy przykład przedstawia podstawowe kroki wdrażania R kodu:</span><span class="sxs-lookup"><span data-stu-id="c0e4e-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="c0e4e-105">Użyj `REFERENCE ASSEMBLY` instrukcji, aby włączyć rozszerzenia R skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="c0e4e-106">Użyj` REDUCE` operacji do partycjonowania danych wejściowych dla klucza.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="c0e4e-107">Rozszerzenia R U-SQL zawierają wbudowane reduktor (`Extension.R.Reducer`) uruchomione na każdy wierzchołek przypisane do reduktor kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="c0e4e-108">Użycie dedykowanych o nazwie ramek danych o nazwie `inputFromUSQL` i `outputToUSQL `odpowiednio do przekazywania danych między U-SQL i R. dane wejściowe i wyjściowe DataFrame rozwiązane nazwy identyfikatorów (oznacza to, użytkownicy nie można zmienić tych wstępnie zdefiniowanych nazw danych wejściowych i wyjściowych DataFrame identyfikatory).</span><span class="sxs-lookup"><span data-stu-id="c0e4e-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="c0e4e-109">Osadzanie kodu języka R w skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="c0e4e-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="c0e4e-110">Można R kodu skryptu U-SQL przy użyciu parametru polecenia wbudowanym `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="c0e4e-111">Na przykład można zadeklarować skrypt języka R jako zmienna typu ciąg i przekaż go jako parametru reduktor.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="c0e4e-112">Zachowaj w osobnym pliku kodu języka R i odwołaj się skrypt U-SQL</span><span class="sxs-lookup"><span data-stu-id="c0e4e-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="c0e4e-113">Poniższy przykład przedstawia użycie bardziej złożonych.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="c0e4e-114">W takim przypadku kodu języka R jest wdrażany jako zasób, który jest skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="c0e4e-115">Zapisz ten kod R jako oddzielny plik.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="c0e4e-116">Aby wdrożyć ten skrypt języka R z instrukcji wdrażania zasobów za pomocą skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="c0e4e-117">Jak R integruje się z języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="c0e4e-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="c0e4e-118">Typy danych</span><span class="sxs-lookup"><span data-stu-id="c0e4e-118">Datatypes</span></span>
* <span data-ttu-id="c0e4e-119">Ciąg, jak i numeryczne kolumny z U-SQL są konwertowane na — między R DataFrame i języka U-SQL [obsługiwane typy: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="c0e4e-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="c0e4e-120">`Factor` Typ danych nie jest obsługiwane w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="c0e4e-121">`byte[]`musi być Zserializowany jako algorytmem base64 `string`.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="c0e4e-122">Ciągi języka U-SQL może zostać przekonwertowany na czynniki w kodzie języka R, kiedy U-SQL utworzony dataframe wejściowych R lub przez ustawienie dla parametru reduktor `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="c0e4e-123">Schematy</span><span class="sxs-lookup"><span data-stu-id="c0e4e-123">Schemas</span></span>
* <span data-ttu-id="c0e4e-124">Zestaw danych skryptu U-SQL nie mogą mieć zduplikowanych nazw kolumn.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="c0e4e-125">Nazwy kolumn U-SQL zestawów danych muszą być ciągami.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="c0e4e-126">Nazwy kolumn muszą być takie same w języku U-SQL i skrypty R.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="c0e4e-127">Kolumny tylko do odczytu nie może być częścią dataframe danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="c0e4e-128">Ponieważ kolumny tylko do odczytu są automatycznie wprowadzić Wstecz w tabeli U-SQL, jeśli jest częścią UDO schemat danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="c0e4e-129">Ograniczenia funkcjonalności</span><span class="sxs-lookup"><span data-stu-id="c0e4e-129">Functional limitations</span></span>
* <span data-ttu-id="c0e4e-130">Nie można utworzyć wystąpienia aparatu R, dwukrotnie w tym samym procesie.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="c0e4e-131">U-SQL nie obsługuje obecnie udo łączenia do przewidywania za pomocą partycjonowanego modeli wygenerowanych przy użyciu udo reduktor.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="c0e4e-132">Użytkownicy mogą zadeklarować modeli partycjonowane jako zasób i używać ich w ich skrypt języka R (zobacz przykładowy kod `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="c0e4e-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="c0e4e-133">Wersje R</span><span class="sxs-lookup"><span data-stu-id="c0e4e-133">R Versions</span></span>
<span data-ttu-id="c0e4e-134">R 3.2.2 jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="c0e4e-135">Standardowe moduły R</span><span class="sxs-lookup"><span data-stu-id="c0e4e-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="c0e4e-136">Dane wejściowe i ograniczenia rozmiaru danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c0e4e-136">Input and Output size limitations</span></span>
<span data-ttu-id="c0e4e-137">Każdy wierzchołek ma ograniczoną ilość pamięci przypisanej do niego.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="c0e4e-138">Ponieważ DataFrames wejściowych i wyjściowych musi istnieć w pamięci w kodzie języka R, wówczas łączny rozmiar danych wejściowych i wyjściowych nie może przekraczać 500 MB.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="c0e4e-139">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="c0e4e-139">Sample Code</span></span>
<span data-ttu-id="c0e4e-140">Więcej przykładowy kod jest dostępny na koncie usługi Data Lake Store, po zainstalowaniu rozszerzenia Analytics zaawansowane U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="c0e4e-141">Ścieżka więcej przykładowy kod jest: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="c0e4e-142">Wdrożenie modułów R niestandardowe w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="c0e4e-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="c0e4e-143">Najpierw należy utworzyć niestandardowego modułu R i zip go, a następnie przekaż plik zip niestandardowego modułu R do magazynu ADL.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="c0e4e-144">W tym przykładzie możemy przekazać magittr_1.5.zip do katalogu głównego koncie ADLS domyślnego konta ADLA, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="c0e4e-145">Po przekazaniu modułu do magazynu ADL, Zadeklaruj ją jako umożliwia wdrażanie zasobów udostępnić skryptu U-SQL i wywołanie `install.packages` go zainstalować.</span><span class="sxs-lookup"><span data-stu-id="c0e4e-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="c0e4e-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c0e4e-146">Next Steps</span></span>
* [<span data-ttu-id="c0e4e-147">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c0e4e-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="c0e4e-148">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0e4e-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="c0e4e-149">Zadania usługi Azure Data Lake Analytics przy użyciu funkcji okna języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="c0e4e-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
