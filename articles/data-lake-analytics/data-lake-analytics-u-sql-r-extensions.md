---
title: "skrypty U-SQL aaaExtend z języka R w usłudze Azure Data Lake Analytics | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kod toorun R skryptów U-SQL"
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
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="7f9fa-103">Samouczek: Rozpoczynanie pracy z rozszerzanie U-SQL z języka R</span><span class="sxs-lookup"><span data-stu-id="7f9fa-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="7f9fa-104">Witaj poniższy przykład przedstawia hello podstawowe kroki wdrażania R kodu:</span><span class="sxs-lookup"><span data-stu-id="7f9fa-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="7f9fa-105">Użyj hello `REFERENCE ASSEMBLY` rozszerzenia tooenable R instrukcji hello skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="7f9fa-106">Użyj` REDUCE` operacji toopartition hello wprowadzić dane dla klucza.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="7f9fa-107">rozszerzenia Hello R U-SQL obejmują wbudowane reduktor (`Extension.R.Reducer`) uruchomione na każdy wierzchołek przypisane toohello reduktor kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="7f9fa-108">Użycie dedykowanych o nazwie ramek danych o nazwie `inputFromUSQL` i `outputToUSQL `odpowiednio toopass danych między U-SQL i R. dane wejściowe i wyjściowe są rozwiązywane DataFrame identyfikator nazwy (oznacza to, użytkownicy nie można zmienić tych wstępnie zdefiniowanych nazw danych wejściowych i wyjściowych DataFrame identyfikatory).</span><span class="sxs-lookup"><span data-stu-id="7f9fa-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="7f9fa-109">Osadzanie kodu języka R w hello skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="7f9fa-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="7f9fa-110">Można kodu hello R wbudowanego skryptu U-SQL przy użyciu parametru polecenia hello hello `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="7f9fa-111">Na przykład można zadeklarować hello skrypt języka R jako zmienna typu ciąg i przekaż go jako parametru toohello reduktor.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="7f9fa-112">Zachowaj w osobnym pliku kodu hello R i odwołaj skryptu hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="7f9fa-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="7f9fa-113">Hello poniższy przykład przedstawia użycie bardziej złożonych.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="7f9fa-114">W takim przypadku hello R kod jest wdrażany jako zasób, który jest hello skryptu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="7f9fa-115">Zapisz ten kod R jako oddzielny plik.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="7f9fa-116">Za pomocą toodeploy skryptu U-SQL ten skrypt języka R hello instrukcji wdrażania zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="7f9fa-117">Jak R integruje się z języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="7f9fa-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="7f9fa-118">Typy danych</span><span class="sxs-lookup"><span data-stu-id="7f9fa-118">Datatypes</span></span>
* <span data-ttu-id="7f9fa-119">Ciąg, jak i numeryczne kolumny z U-SQL są konwertowane na — między R DataFrame i języka U-SQL [obsługiwane typy: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="7f9fa-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="7f9fa-120">Witaj `Factor` typu danych nie jest obsługiwane w języku U-SQL.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="7f9fa-121">`byte[]`musi być Zserializowany jako algorytmem base64 `string`.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="7f9fa-122">Ciągi U-SQL może być przekonwertowany toofactors w kodzie języka R, kiedy U-SQL utworzony dataframe wejściowych R lub przez ustawienie parametru reduktor hello `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="7f9fa-123">Schematy</span><span class="sxs-lookup"><span data-stu-id="7f9fa-123">Schemas</span></span>
* <span data-ttu-id="7f9fa-124">Zestaw danych skryptu U-SQL nie mogą mieć zduplikowanych nazw kolumn.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="7f9fa-125">Nazwy kolumn U-SQL zestawów danych muszą być ciągami.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="7f9fa-126">Nazwy kolumn muszą hello w tej samej w skryptów U-SQL i R.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="7f9fa-127">Kolumny tylko do odczytu nie może być częścią hello dataframe danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="7f9fa-128">Ponieważ kolumny tylko do odczytu są automatycznie wprowadzić Wstecz w tabeli U-SQL hello, jeśli jest częścią UDO schemat danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="7f9fa-129">Ograniczenia funkcjonalności</span><span class="sxs-lookup"><span data-stu-id="7f9fa-129">Functional limitations</span></span>
* <span data-ttu-id="7f9fa-130">Witaj aparat R nie można utworzyć wystąpienia dwa razy w hello tego samego procesu.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="7f9fa-131">U-SQL nie obsługuje obecnie udo łączenia do przewidywania za pomocą partycjonowanego modeli wygenerowanych przy użyciu udo reduktor.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="7f9fa-132">Użytkownicy mogą zadeklarować modeli hello partycjonowane jako zasób i używać ich w ich skrypt języka R (zobacz przykładowy kod `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="7f9fa-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="7f9fa-133">Wersje R</span><span class="sxs-lookup"><span data-stu-id="7f9fa-133">R Versions</span></span>
<span data-ttu-id="7f9fa-134">R 3.2.2 jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="7f9fa-135">Standardowe moduły R</span><span class="sxs-lookup"><span data-stu-id="7f9fa-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="7f9fa-136">Dane wejściowe i ograniczenia rozmiaru danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="7f9fa-136">Input and Output size limitations</span></span>
<span data-ttu-id="7f9fa-137">Każdy wierzchołek ma ograniczoną ilość pamięci przypisana tooit.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="7f9fa-138">Ponieważ hello DataFrames wejściowych i wyjściowych musi istnieć w pamięci w kodzie hello R, łączny rozmiar hello hello danych wejściowych i wyjściowych nie może przekraczać 500 MB.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="7f9fa-139">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="7f9fa-139">Sample Code</span></span>
<span data-ttu-id="7f9fa-140">Więcej przykładowy kod jest dostępny na koncie usługi Data Lake Store, po zainstalowaniu hello rozszerzeń analizy zaawansowane U-SQL.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="7f9fa-141">Ścieżka Hello więcej przykładowy kod jest: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="7f9fa-142">Wdrożenie modułów R niestandardowe w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="7f9fa-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="7f9fa-143">Najpierw należy utworzyć niestandardowego modułu R i zip go, a następnie przekaż hello zip R niestandardowego modułu pliku tooyour ADL magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="7f9fa-144">Przykład Witaj możemy przekazać głównym toohello magittr_1.5.zip hello domyślnego konta ADLS hello ADLA konta, którego użyto.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="7f9fa-145">Po przekazaniu hello modułu tooADL magazynu, Zadeklaruj ją jako Użyj toomake wdrażanie zasobów udostępniana w skryptu U-SQL i wywołanie `install.packages` tooinstall go.</span><span class="sxs-lookup"><span data-stu-id="7f9fa-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
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

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="7f9fa-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f9fa-146">Next Steps</span></span>
* [<span data-ttu-id="7f9fa-147">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="7f9fa-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="7f9fa-148">Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f9fa-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="7f9fa-149">Zadania usługi Azure Data Lake Analytics przy użyciu funkcji okna języka U-SQL</span><span class="sxs-lookup"><span data-stu-id="7f9fa-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
