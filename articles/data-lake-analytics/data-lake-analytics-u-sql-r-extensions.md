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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Samouczek: Rozpoczynanie pracy z rozszerzanie U-SQL z języka R

Witaj poniższy przykład przedstawia hello podstawowe kroki wdrażania R kodu:
* Użyj hello `REFERENCE ASSEMBLY` rozszerzenia tooenable R instrukcji hello skryptu U-SQL.
* Użyj` REDUCE` operacji toopartition hello wprowadzić dane dla klucza.
* rozszerzenia Hello R U-SQL obejmują wbudowane reduktor (`Extension.R.Reducer`) uruchomione na każdy wierzchołek przypisane toohello reduktor kodu języka R. 
* Użycie dedykowanych o nazwie ramek danych o nazwie `inputFromUSQL` i `outputToUSQL `odpowiednio toopass danych między U-SQL i R. dane wejściowe i wyjściowe są rozwiązywane DataFrame identyfikator nazwy (oznacza to, użytkownicy nie można zmienić tych wstępnie zdefiniowanych nazw danych wejściowych i wyjściowych DataFrame identyfikatory).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>Osadzanie kodu języka R w hello skryptu U-SQL

Można kodu hello R wbudowanego skryptu U-SQL przy użyciu parametru polecenia hello hello `Extension.R.Reducer`. Na przykład można zadeklarować hello skrypt języka R jako zmienna typu ciąg i przekaż go jako parametru toohello reduktor.


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Zachowaj w osobnym pliku kodu hello R i odwołaj skryptu hello U-SQL

Hello poniższy przykład przedstawia użycie bardziej złożonych. W takim przypadku hello R kod jest wdrażany jako zasób, który jest hello skryptu U-SQL.

Zapisz ten kod R jako oddzielny plik.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Za pomocą toodeploy skryptu U-SQL ten skrypt języka R hello instrukcji wdrażania zasobów.

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

## <a name="how-r-integrates-with-u-sql"></a>Jak R integruje się z języka U-SQL

### <a name="datatypes"></a>Typy danych
* Ciąg, jak i numeryczne kolumny z U-SQL są konwertowane na — między R DataFrame i języka U-SQL [obsługiwane typy: `double`, `string`, `bool`, `integer`, `byte`].
* Witaj `Factor` typu danych nie jest obsługiwane w języku U-SQL.
* `byte[]`musi być Zserializowany jako algorytmem base64 `string`.
* Ciągi U-SQL może być przekonwertowany toofactors w kodzie języka R, kiedy U-SQL utworzony dataframe wejściowych R lub przez ustawienie parametru reduktor hello `stringsAsFactors: true`.

### <a name="schemas"></a>Schematy
* Zestaw danych skryptu U-SQL nie mogą mieć zduplikowanych nazw kolumn.
* Nazwy kolumn U-SQL zestawów danych muszą być ciągami.
* Nazwy kolumn muszą hello w tej samej w skryptów U-SQL i R.
* Kolumny tylko do odczytu nie może być częścią hello dataframe danych wyjściowych. Ponieważ kolumny tylko do odczytu są automatycznie wprowadzić Wstecz w tabeli U-SQL hello, jeśli jest częścią UDO schemat danych wyjściowych.

### <a name="functional-limitations"></a>Ograniczenia funkcjonalności
* Witaj aparat R nie można utworzyć wystąpienia dwa razy w hello tego samego procesu. 
* U-SQL nie obsługuje obecnie udo łączenia do przewidywania za pomocą partycjonowanego modeli wygenerowanych przy użyciu udo reduktor. Użytkownicy mogą zadeklarować modeli hello partycjonowane jako zasób i używać ich w ich skrypt języka R (zobacz przykładowy kod `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>Wersje R
R 3.2.2 jest obsługiwana.

### <a name="standard-r-modules"></a>Standardowe moduły R

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

### <a name="input-and-output-size-limitations"></a>Dane wejściowe i ograniczenia rozmiaru danych wyjściowych
Każdy wierzchołek ma ograniczoną ilość pamięci przypisana tooit. Ponieważ hello DataFrames wejściowych i wyjściowych musi istnieć w pamięci w kodzie hello R, łączny rozmiar hello hello danych wejściowych i wyjściowych nie może przekraczać 500 MB.

### <a name="sample-code"></a>Przykładowy kod
Więcej przykładowy kod jest dostępny na koncie usługi Data Lake Store, po zainstalowaniu hello rozszerzeń analizy zaawansowane U-SQL. Ścieżka Hello więcej przykładowy kod jest: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Wdrożenie modułów R niestandardowe w języku U-SQL

Najpierw należy utworzyć niestandardowego modułu R i zip go, a następnie przekaż hello zip R niestandardowego modułu pliku tooyour ADL magazynu. Przykład Witaj możemy przekazać głównym toohello magittr_1.5.zip hello domyślnego konta ADLS hello ADLA konta, którego użyto. Po przekazaniu hello modułu tooADL magazynu, Zadeklaruj ją jako Użyj toomake wdrażanie zasobów udostępniana w skryptu U-SQL i wywołanie `install.packages` tooinstall go.

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

## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Zadania usługi Azure Data Lake Analytics przy użyciu funkcji okna języka U-SQL](data-lake-analytics-use-window-functions.md)
