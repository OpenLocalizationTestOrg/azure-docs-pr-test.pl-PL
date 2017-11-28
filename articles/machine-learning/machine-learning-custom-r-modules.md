---
title: "aaaAuthor niestandardowych modułów R w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Szybki start do tworzenia niestandardowych modułów R w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="0f269-103">Tworzenie niestandardowych modułów R w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0f269-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="0f269-104">W tym temacie opisano sposób tooauthor i wdrażanie niestandardowego modułu R w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0f269-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="0f269-105">Wyjaśniono, co to są niestandardowych modułów R i które pliki są używane toodefine je.</span><span class="sxs-lookup"><span data-stu-id="0f269-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="0f269-106">Go pokazano, jak tooconstruct hello pliki, które definiują modułu i jak tooregister hello modułu do wdrożenia w obszarze roboczym uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="0f269-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="0f269-107">Witaj elementy i atrybuty użyte w definicji hello niestandardowego modułu hello są następnie opisane bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="0f269-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="0f269-108">Jak również omówiono funkcje pomocnicze toouse, plików i wielu wyjść.</span><span class="sxs-lookup"><span data-stu-id="0f269-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="0f269-109">Co to jest niestandardowego modułu R?</span><span class="sxs-lookup"><span data-stu-id="0f269-109">What is a custom R module?</span></span>
<span data-ttu-id="0f269-110">A **niestandardowego modułu** jest moduł zdefiniowane przez użytkownika, które mogą być przekazywane tooyour obszaru roboczego i wykonywane w ramach eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="0f269-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="0f269-111">A **niestandardowego modułu R** jest niestandardowy moduł, który wykonuje funkcję R zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f269-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="0f269-112">**R** to język programowania statystyczne obliczeniowych i grafiki, powszechnie używaną służące chi i dane dotyczące implementowania algorytmów.</span><span class="sxs-lookup"><span data-stu-id="0f269-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="0f269-113">R jest obecnie hello języka tylko obsługiwane niestandardowe moduły, ale pomocy technicznej dla dodatkowych języków zostało zaplanowane w przyszłych wersjach.</span><span class="sxs-lookup"><span data-stu-id="0f269-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="0f269-114">Niestandardowe moduły mają **najwyższej jakości stan** w usłudze Azure Machine Learning w hello sensie, że mogą być używane tak samo jak inne modułu.</span><span class="sxs-lookup"><span data-stu-id="0f269-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="0f269-115">Można je wykonać na inne moduły zawarte w opublikowanych eksperymenty lub wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="0f269-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="0f269-116">Mają kontrolę nad algorytm hello zaimplementowana przez moduł hello, hello toobe porty wejściowe i wyjściowe używany, hello parametry modelowania i innych różnych zachowanie w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0f269-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="0f269-117">Eksperymentu, która zawiera niestandardowe moduły mogą być publikowane na powitania Cortana Intelligence Gallery łatwe udostępnianie.</span><span class="sxs-lookup"><span data-stu-id="0f269-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="0f269-118">Pliki w niestandardowego modułu R</span><span class="sxs-lookup"><span data-stu-id="0f269-118">Files in a custom R module</span></span>
<span data-ttu-id="0f269-119">Niestandardowego modułu R jest zdefiniowane przez plik zip, który zawiera co najmniej dwa pliki:</span><span class="sxs-lookup"><span data-stu-id="0f269-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="0f269-120">A **plik źródłowy** implementującej hello R funkcji udostępnianych przez moduł hello</span><span class="sxs-lookup"><span data-stu-id="0f269-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="0f269-121">**Pliku definicji XML** , który opisuje interfejs niestandardowego modułu hello</span><span class="sxs-lookup"><span data-stu-id="0f269-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="0f269-122">Dodatkowe pliki pomocnicze można również uwzględnić w pliku .zip hello, który zawiera funkcje, które są dostępne z hello niestandardowego modułu.</span><span class="sxs-lookup"><span data-stu-id="0f269-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="0f269-123">Ta opcja została szczegółowo opisana w hello **argumenty** część sekcji odwołania hello **elementów w pliku definicji XML hello** poniższy przykład szybkiego startu hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="0f269-124">Przykład Szybki Start: zdefiniuj, pakowanie i zarejestrować niestandardowego modułu R</span><span class="sxs-lookup"><span data-stu-id="0f269-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="0f269-125">W tym przykładzie pokazano, jak tooconstruct hello pliki wymagane przez niestandardowego modułu R, umieścić je w pliku zip, a następnie moduł hello rejestru w obszaru roboczego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="0f269-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="0f269-126">Witaj przykład zip pakietu i przykładowe pliki można pobrać z [CustomAddRows.zip Pobierz plik](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0f269-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="0f269-127">plik źródłowy Hello</span><span class="sxs-lookup"><span data-stu-id="0f269-127">hello source file</span></span>
<span data-ttu-id="0f269-128">Rozważ przykład hello **wierszy dodać niestandardowe** moduł, który modyfikuje hello standardowej implementacji hello **Dodawanie wierszy** moduł używany tooconcatenate wierszy (uwagi) z dwóch zestawów danych (danych ramki).</span><span class="sxs-lookup"><span data-stu-id="0f269-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="0f269-129">Standardowa Hello **Dodawanie wierszy** modułu dołącza wierszy hello końca hello drugi zestaw danych wejściowych toohello hello pierwszego wejściowego zestawu danych za pomocą hello `rbind` algorytmu.</span><span class="sxs-lookup"><span data-stu-id="0f269-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="0f269-130">Witaj, dostosowane `CustomAddRows` funkcja podobnie akceptuje dwa zestawy danych, ale również zawierać parametr wymiany logiczną jako dodatkowe dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0f269-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="0f269-131">Jeśli parametr wymiany hello ustawiono zbyt**FALSE**, jego zwraca hello tego samego zestawu danych, ponieważ hello standardowej implementacji.</span><span class="sxs-lookup"><span data-stu-id="0f269-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="0f269-132">Jeśli parametr wymiany hello jest jednak **TRUE**, funkcja hello dołącza wierszy pierwszego zestawu danych wejściowych toohello koniec hello drugi zestaw danych, zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="0f269-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="0f269-133">Witaj CustomAddRows.R pliku, który zawiera implementację hello hello R `CustomAddRows` funkcji udostępnianych przez hello **wierszy dodać niestandardowe** moduł ma hello następującego kodu języka R.</span><span class="sxs-lookup"><span data-stu-id="0f269-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a><span data-ttu-id="0f269-134">Plik definicji XML Hello</span><span class="sxs-lookup"><span data-stu-id="0f269-134">hello XML definition file</span></span>
<span data-ttu-id="0f269-135">tooexpose to `CustomAddRows` funkcji jako moduł usługi Azure Machine Learning pliku definicji XML muszą być tworzone toospecify jak hello **wierszy dodać niestandardowe** modułu powinien wyglądu i zachowania.</span><span class="sxs-lookup"><span data-stu-id="0f269-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="0f269-136">Jest toonote krytyczny, który hello wartość hello **identyfikator** atrybuty hello **dane wejściowe** i **Arg** elementów w pliku XML hello musi odpowiadać nazwy parametrów funkcji hello hello R kod w pliku CustomAddRows.R hello dokładnie: (*dataset1*, *dataset2*, i *wymiany* w przykładzie hello).</span><span class="sxs-lookup"><span data-stu-id="0f269-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="0f269-137">Podobnie, hello wartość hello **punktu wejścia** atrybutu hello **języka** elementu muszą być zgodne hello nazwę funkcji hello w skrypcie hello R: (*CustomAddRows* w przykładzie hello).</span><span class="sxs-lookup"><span data-stu-id="0f269-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="0f269-138">Z kolei hello **identyfikator** atrybutu hello **dane wyjściowe** elementu nie odpowiada tooany zmienne w skrypcie hello R.</span><span class="sxs-lookup"><span data-stu-id="0f269-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="0f269-139">Jeśli wymagane jest więcej niż jedno wyjście, po prostu zwraca listę z funkcji hello R z wynikami umieszczone *w hello tej samej kolejności* jako **dane wyjściowe** elementy są zadeklarowane w pliku XML hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="0f269-140">Moduł hello pakietu i rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="0f269-140">Package and register hello module</span></span>
<span data-ttu-id="0f269-141">Zapisz te dwa pliki jako *CustomAddRows.R* i *CustomAddRows.xml* , a następnie zip hello dwa pliki ze sobą w *CustomAddRows.zip* pliku.</span><span class="sxs-lookup"><span data-stu-id="0f269-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="0f269-142">tooregister je w obszarze roboczym uczenia maszynowego, obszar roboczy tooyour Przejdź w hello Machine Learning Studio, kliknij przycisk hello **+ nowy** znajdującego się na dole hello i wybierz polecenie **modułu -> z pakietu ZIP** tooupload nowe Hello **wierszy dodać niestandardowe** modułu.</span><span class="sxs-lookup"><span data-stu-id="0f269-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Przekaż Zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="0f269-144">Witaj **wierszy dodać niestandardowe** modułu jest teraz gotowy toobe dostęp do eksperymentów uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="0f269-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="0f269-145">Elementy w pliku definicji XML hello</span><span class="sxs-lookup"><span data-stu-id="0f269-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="0f269-146">Moduł elementów</span><span class="sxs-lookup"><span data-stu-id="0f269-146">Module elements</span></span>
<span data-ttu-id="0f269-147">Witaj **modułu** element jest używany toodefine niestandardowego modułu w pliku XML hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="0f269-148">Można zdefiniować wiele modułów w jednym pliku XML przy użyciu wielu **modułu** elementów.</span><span class="sxs-lookup"><span data-stu-id="0f269-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="0f269-149">Każdy moduł w obszarze roboczym musi mieć unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="0f269-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="0f269-150">Zarejestruj niestandardowego modułu z hello sama nazwę istniejącej niestandardowego modułu i jego zastępuje istniejący moduł hello hello nową.</span><span class="sxs-lookup"><span data-stu-id="0f269-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="0f269-151">Niestandardowe moduły można jednak zarejestrowany hello sama nazwa jak istniejący moduł usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0f269-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="0f269-152">Jeśli tak, pojawią się one w hello **niestandardowy** kategorii hello palety modułów.</span><span class="sxs-lookup"><span data-stu-id="0f269-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="0f269-153">W ramach hello **modułu** elementu, można określić dwa dodatkowe elementy opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="0f269-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="0f269-154">**właściciela** element, który jest osadzony w hello module</span><span class="sxs-lookup"><span data-stu-id="0f269-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="0f269-155">**opis** element zawierający tekst, który jest wyświetlany w szybką pomoc dla modułu hello i po umieszczeniu na powitania modułu w hello Machine Learning w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f269-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="0f269-156">Zasady ograniczeń znaków w elementach modułu hello:</span><span class="sxs-lookup"><span data-stu-id="0f269-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="0f269-157">Witaj wartość hello **nazwa** atrybutu w hello **modułu** element nie może przekraczać 64 znaków.</span><span class="sxs-lookup"><span data-stu-id="0f269-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="0f269-158">Witaj zawartości hello **opis** element nie może przekraczać 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="0f269-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="0f269-159">Witaj zawartości hello **właściciela** element nie może przekraczać 32 znaków.</span><span class="sxs-lookup"><span data-stu-id="0f269-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="0f269-160">Moduł wyniki mogą być deterministyczna lub nondeterministic.* * Domyślnie, wszystkie moduły są traktowane jako toobe deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="0f269-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="0f269-161">Oznacza to mając niezmiennych zestaw parametrów wejściowych i danych, modułu hello powinien zwrócić hello takie same wyniki eacRAND lub czas functionh, który jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="0f269-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="0f269-162">To zachowanie, Azure Machine Learning Studio zwracające tylko moduły oznaczona jako deterministyczna, jeśli parametr lub danych wejściowych hello została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="0f269-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="0f269-163">Zwracania wyników hello w pamięci podręcznej udostępnia znacznie szybsze wykonywanie eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="0f269-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="0f269-164">Brak funkcji, które są niedeterministyczne, takich jak RAND lub funkcji, która zwraca hello bieżącą datę lub godzinę.</span><span class="sxs-lookup"><span data-stu-id="0f269-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="0f269-165">Jeśli niedeterministyczna funkcja korzysta z modułu, można określić tego modułu hello jest deterministyczna przez ustawienie opcjonalne hello **isDeterministic** atrybutu zbyt**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="0f269-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="0f269-166">Dzięki temu, że ten moduł hello jest ponownie uruchamiany przy każdym uruchomieniu eksperymentu hello, nawet jeśli hello wejścia modułu i parametrów nie uległy zmianie.</span><span class="sxs-lookup"><span data-stu-id="0f269-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="0f269-167">Język definicji</span><span class="sxs-lookup"><span data-stu-id="0f269-167">Language Definition</span></span>
<span data-ttu-id="0f269-168">Witaj **języka** elementu w pliku definicji XML jest używane toospecify hello niestandardowego modułu języka.</span><span class="sxs-lookup"><span data-stu-id="0f269-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="0f269-169">Obecnie R jest hello tylko obsługiwanego języka.</span><span class="sxs-lookup"><span data-stu-id="0f269-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="0f269-170">Witaj wartość hello **sourceFile** atrybutu musi być nazwą hello hello R zawierający toocall funkcja powitania po uruchomieniu hello modułu.</span><span class="sxs-lookup"><span data-stu-id="0f269-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="0f269-171">Ten plik musi być częścią pakietu zip hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="0f269-172">Witaj wartość hello **punktu wejścia** atrybut jest hello nazwę wywoływanej funkcji hello i musi być zgodna z prawidłową funkcji zdefiniowanej przy w pliku źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="0f269-173">Porty</span><span class="sxs-lookup"><span data-stu-id="0f269-173">Ports</span></span>
<span data-ttu-id="0f269-174">Witaj porty wejściowe i wyjściowe dla niestandardowego modułu są określone w elementach podrzędnych hello **porty** sekcja pliku definicji XML hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="0f269-175">kolejność Hello tych elementów określa hello układu doświadczonym (UX) przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f269-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="0f269-176">pierwszym elementem podrzędnym Hello **wejściowych** lub **dane wyjściowe** hello na liście **porty** element pliku XML hello staje się hello lewej portu wejściowego w hello Machine Learning UX.</span><span class="sxs-lookup"><span data-stu-id="0f269-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="0f269-177">Każdy wejściowy i port wyjściowy może być opcjonalny **opis** element podrzędny, który określa hello tekst wyświetlany, gdy Przesuń wskaźnik myszy hello za pośrednictwem portu hello w hello Machine Learning w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0f269-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="0f269-178">**Porty reguły**:</span><span class="sxs-lookup"><span data-stu-id="0f269-178">**Ports Rules**:</span></span>

* <span data-ttu-id="0f269-179">Maksymalna liczba **porty wejściowe i wyjściowe** to 8 dla każdego.</span><span class="sxs-lookup"><span data-stu-id="0f269-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="0f269-180">Elementów wejściowych</span><span class="sxs-lookup"><span data-stu-id="0f269-180">Input elements</span></span>
<span data-ttu-id="0f269-181">Porty wejściowe pozwalają toopass danych tooyour R funkcji i obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="0f269-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="0f269-182">Witaj **typy danych** obsługiwanych dla porty wejściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="0f269-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="0f269-183">**Element DataTable:** tego typu jest przekazywana funkcja tooyour R jako data.frame.</span><span class="sxs-lookup"><span data-stu-id="0f269-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="0f269-184">W rzeczywistości żadnych typów (na przykład plików CSV lub pliki ARFF), które są obsługiwane przez uczenia maszynowego i które są zgodne z **DataTable** są automatycznie data.frame tooa przekonwertowany.</span><span class="sxs-lookup"><span data-stu-id="0f269-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="0f269-185">Witaj **identyfikator** atrybut skojarzony z poszczególnymi **DataTable** port wejściowy musi mieć unikatową wartość i wartość ta musi odpowiadać odpowiadającego nazwany parametr w funkcji R.</span><span class="sxs-lookup"><span data-stu-id="0f269-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="0f269-186">Opcjonalne **DataTable** portów, które nie są przekazywane jako dane wejściowe w eksperymencie ma wartość hello **NULL** funkcja przekazany toohello R i zip opcjonalne porty są ignorowane, jeśli hello danych wejściowych nie jest połączona.</span><span class="sxs-lookup"><span data-stu-id="0f269-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="0f269-187">Witaj **isOptional** atrybutu jest opcjonalny w przypadku obu hello **DataTable** i **Zip** typów i jest *false* domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0f269-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="0f269-188">**ZIP:** niestandardowe moduły można zaakceptować plik zip jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="0f269-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="0f269-189">Tych danych wejściowych jest rozpakowane do katalogu roboczego hello R funkcji</span><span class="sxs-lookup"><span data-stu-id="0f269-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="0f269-190">Dla niestandardowych modułów R identyfikator hello portu Zip ma toomatch parametrów funkcji hello R.</span><span class="sxs-lookup"><span data-stu-id="0f269-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="0f269-191">Jest to spowodowane plik zip hello jest automatycznie wyodrębnionego toohello R katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="0f269-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="0f269-192">**Reguły wprowadzania:**</span><span class="sxs-lookup"><span data-stu-id="0f269-192">**Input Rules:**</span></span>

* <span data-ttu-id="0f269-193">Witaj wartość hello **identyfikator** atrybutu hello **dane wejściowe** element musi być prawidłową nazwą zmiennej języka R.</span><span class="sxs-lookup"><span data-stu-id="0f269-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="0f269-194">Witaj wartość hello **identyfikator** atrybutu hello **dane wejściowe** element nie może być dłuższa niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="0f269-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="0f269-195">Witaj wartość hello **nazwa** atrybutu hello **dane wejściowe** element nie może być dłuższa niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="0f269-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="0f269-196">Witaj zawartości hello **opis** element nie może być dłuższa niż 128 znaków</span><span class="sxs-lookup"><span data-stu-id="0f269-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="0f269-197">Witaj wartość hello **typu** atrybutu hello **dane wejściowe** element musi być *Zip* lub *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="0f269-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="0f269-198">Witaj wartość hello **isOptional** atrybutu hello **dane wejściowe** element nie jest wymagana (i jest *false* domyślnie, gdy nie określono); ale jeśli jest określona, musi ona być *true* lub *false*.</span><span class="sxs-lookup"><span data-stu-id="0f269-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="0f269-199">Elementy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="0f269-199">Output elements</span></span>
<span data-ttu-id="0f269-200">**Standardowe dane wyjściowe porty:** porty dane wyjściowe są mapowane toohello wartości zwracanych z funkcji R, które mogą być następnie używane przez kolejne modułów.</span><span class="sxs-lookup"><span data-stu-id="0f269-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="0f269-201">*Element DataTable* jest typ portu tylko standardowe wyjście hello obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0f269-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="0f269-202">(Obsługę *uczących* i *przekształca* nadchodzi.) A *DataTable* danych wyjściowych jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="0f269-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="0f269-203">Dla danych wyjściowych w niestandardowych modułów R, hello wartość hello **identyfikator** atrybut nie ma w skrypcie hello R toocorrespond przy użyciu innych, ale musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="0f269-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="0f269-204">Dla wyjścia pojedynczy moduł, musi być hello wartość zwrócona przez funkcję hello R *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="0f269-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="0f269-205">W kolejność toooutput więcej niż jeden obiekt obsługiwany typ danych, hello odpowiednie dane wyjściowe porty muszą toobe określony w pliku definicji XML hello i hello obiekty wymagają toobe zwracane w postaci listy.</span><span class="sxs-lookup"><span data-stu-id="0f269-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="0f269-206">obiekty danych wyjściowych Hello są przypisywane porty toooutput z tooright po lewej stronie, odzwierciedlający hello kolejność, w którym obiekty hello są umieszczane w hello zwrócił listę.</span><span class="sxs-lookup"><span data-stu-id="0f269-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="0f269-207">Na przykład, jeśli chcesz toomodify hello **niestandardowe Dodawanie wierszy** toooutput modułu hello oryginalnego dwóch zestawów danych, *dataset1* i *dataset2*, ponadto przyłączone toohello nowego zestaw danych, *zestawu danych*, (w kolejności od lewej tooright jako: *dataset*, *dataset1*, *dataset2*), następnie zdefiniuj hello dane wyjściowe porty w pliku CustomAddRows.xml hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0f269-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="0f269-208">I zwróć hello listy obiektów na liście w kolejności poprawne hello w "CustomAddRows.R":</span><span class="sxs-lookup"><span data-stu-id="0f269-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="0f269-209">**Wizualizacja danych wyjściowych:** można także określić port wyjściowy typu *wizualizacji*, który zawiera dane wyjściowe hello hello R grafiki urządzenia i konsola danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0f269-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="0f269-210">Ten port nie jest częścią dane wyjściowe funkcji hello R i nie zakłóca hello kolejność hello inne typy portów output.</span><span class="sxs-lookup"><span data-stu-id="0f269-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="0f269-211">Dodaj wizualizacji portu toohello niestandardowe moduły tooadd **dane wyjściowe** element o wartości *wizualizacji* dla jego **typu** atrybutu:</span><span class="sxs-lookup"><span data-stu-id="0f269-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="0f269-212">**Dane wyjściowe reguły:**</span><span class="sxs-lookup"><span data-stu-id="0f269-212">**Output Rules:**</span></span>

* <span data-ttu-id="0f269-213">Witaj wartość hello **identyfikator** atrybutu hello **dane wyjściowe** element musi być prawidłową nazwą zmiennej języka R.</span><span class="sxs-lookup"><span data-stu-id="0f269-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="0f269-214">Witaj wartość hello **identyfikator** atrybutu hello **dane wyjściowe** element nie może być dłuższa niż 32 znaki.</span><span class="sxs-lookup"><span data-stu-id="0f269-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="0f269-215">Witaj wartość hello **nazwa** atrybutu hello **dane wyjściowe** element nie może być dłuższa niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="0f269-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="0f269-216">Witaj wartość hello **typu** atrybutu hello **dane wyjściowe** element musi być *wizualizacji*.</span><span class="sxs-lookup"><span data-stu-id="0f269-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="0f269-217">Argumenty</span><span class="sxs-lookup"><span data-stu-id="0f269-217">Arguments</span></span>
<span data-ttu-id="0f269-218">Dodatkowe dane mogą być przekazywane toohello R funkcji za pośrednictwem modułu parametrów, które są zdefiniowane w hello **argumenty** elementu.</span><span class="sxs-lookup"><span data-stu-id="0f269-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="0f269-219">Te parametry są wyświetlane w okienku po prawej stronie właściwości hello hello Machine Learning w interfejsie użytkownika w przypadku wybrania modułu hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="0f269-220">Argumenty mogą być dowolnego typu hello obsługiwane lub można utworzyć niestandardowe wyliczenie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0f269-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="0f269-221">Podobne toohello **porty** elementów **argumenty** elementy mogą mieć opcjonalny **opis** element, który określa hello tekst wyświetlany, gdy wskaźnik myszy hello za pośrednictwem hello Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="0f269-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="0f269-222">Opcjonalne właściwości dla modułu, na przykład defaultValue minValue i maxValue można dodać argument tooany jako atrybuty tooa **właściwości** elementu.</span><span class="sxs-lookup"><span data-stu-id="0f269-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="0f269-223">Prawidłowe właściwości hello **właściwości** elementu są zależne od typu argumentu hello i opisano z typami argumentów hello obsługiwane w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="0f269-224">Argumenty z hello **isOptional** właściwość zbyt**"true"** hello użytkownika tooenter wartość nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="0f269-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="0f269-225">Jeśli wartość nie zostanie podany toohello argument, następnie hello argument nie zostanie przekazany funkcję punktu wejścia toohello.</span><span class="sxs-lookup"><span data-stu-id="0f269-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="0f269-226">Argumenty funkcji punktu wejścia hello, które są toobe opcjonalne muszą jawnie obsługiwany przez funkcję hello przypisane np. domyślna wartość NULL w definicji funkcji punktu wejścia hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="0f269-227">Opcjonalny argument będzie tylko wymuszać hello innych ograniczeń argumentu, tj. min lub max, jeśli wartość jest podana przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="0f269-228">Zgodnie z wejściami i wyjściami jest krytyczny, że parametrów hello mieć skojarzone z nimi wartości unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="0f269-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="0f269-229">W naszym szybki start zostało przykład hello skojarzony identyfikator i parametru *wymiany*.</span><span class="sxs-lookup"><span data-stu-id="0f269-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="0f269-230">ARG — element</span><span class="sxs-lookup"><span data-stu-id="0f269-230">Arg element</span></span>
<span data-ttu-id="0f269-231">Parametr modułu jest definiowana za pomocą hello **Arg** elementem podrzędnym hello **argumenty** sekcja pliku definicji XML hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="0f269-232">Jak hello elementy podrzędne w hello **porty** sekcji, hello kolejność parametrów na powitania **argumenty** sekcja definiuje układ hello w hello UX.</span><span class="sxs-lookup"><span data-stu-id="0f269-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="0f269-233">Witaj parametry są wyświetlane od góry w dół w hello interfejsu użytkownika w hello sam porządek, w którym są zdefiniowane w pliku XML hello.</span><span class="sxs-lookup"><span data-stu-id="0f269-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="0f269-234">obsługiwane przez usługi Machine Learning parametrów typów Hello są wyświetlane tutaj.</span><span class="sxs-lookup"><span data-stu-id="0f269-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="0f269-235">**int** — parametr (32-bitowy) typu Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="0f269-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="0f269-236">*Opcjonalne właściwości*: **min**, **max**, **domyślne** i **isOptional**</span><span class="sxs-lookup"><span data-stu-id="0f269-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="0f269-237">**Podwójna** — parametr typu double.</span><span class="sxs-lookup"><span data-stu-id="0f269-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="0f269-238">*Opcjonalne właściwości*: **min**, **max**, **domyślne** i **isOptional**</span><span class="sxs-lookup"><span data-stu-id="0f269-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="0f269-239">**wartość logiczna** — parametrem logicznym reprezentowanego przez pole wyboru w UX.</span><span class="sxs-lookup"><span data-stu-id="0f269-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="0f269-240">*Opcjonalne właściwości*: **domyślne** — wartość false, gdy nie jest ustawiona</span><span class="sxs-lookup"><span data-stu-id="0f269-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="0f269-241">**ciąg**: ciąg standardowy</span><span class="sxs-lookup"><span data-stu-id="0f269-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="0f269-242">*Opcjonalne właściwości*: **domyślne** i **isOptional**</span><span class="sxs-lookup"><span data-stu-id="0f269-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="0f269-243">**ColumnPicker**: parametr wybór kolumny.</span><span class="sxs-lookup"><span data-stu-id="0f269-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="0f269-244">Ten typ renderowania w hello UX jako selektora kolumn.</span><span class="sxs-lookup"><span data-stu-id="0f269-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="0f269-245">Witaj **właściwości** element jest używany tutaj toospecify identyfikator hello hello portu, z której są wybierane kolumny, której typ port docelowy hello musi być *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="0f269-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="0f269-246">wynik Hello hello kolumnę zaznaczenia jest przekazywana funkcja toohello R jako lista ciągów zawierająca nazwy kolumn hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="0f269-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="0f269-247">*Wymagane właściwości*: **portId** -dopasowań hello identyfikator elementu danych wejściowych z typem *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="0f269-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="0f269-248">*Opcjonalne właściwości*:</span><span class="sxs-lookup"><span data-stu-id="0f269-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="0f269-249">**allowedTypes** — filtry hello kolumny typów, z której można wybrać.</span><span class="sxs-lookup"><span data-stu-id="0f269-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="0f269-250">Prawidłowe wartości to:</span><span class="sxs-lookup"><span data-stu-id="0f269-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="0f269-251">numeryczne</span><span class="sxs-lookup"><span data-stu-id="0f269-251">Numeric</span></span>
    * <span data-ttu-id="0f269-252">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="0f269-252">Boolean</span></span>
    * <span data-ttu-id="0f269-253">Podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="0f269-253">Categorical</span></span>
    * <span data-ttu-id="0f269-254">Ciąg</span><span class="sxs-lookup"><span data-stu-id="0f269-254">String</span></span>
    * <span data-ttu-id="0f269-255">Etykieta</span><span class="sxs-lookup"><span data-stu-id="0f269-255">Label</span></span>
    * <span data-ttu-id="0f269-256">Funkcja</span><span class="sxs-lookup"><span data-stu-id="0f269-256">Feature</span></span>
    * <span data-ttu-id="0f269-257">Wynik</span><span class="sxs-lookup"><span data-stu-id="0f269-257">Score</span></span>
    * <span data-ttu-id="0f269-258">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="0f269-258">All</span></span>
  * <span data-ttu-id="0f269-259">**domyślne** -prawidłowy domyślny wybór selektor kolumn hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="0f269-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="0f269-260">Brak</span><span class="sxs-lookup"><span data-stu-id="0f269-260">None</span></span>
    * <span data-ttu-id="0f269-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="0f269-261">NumericFeature</span></span>
    * <span data-ttu-id="0f269-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="0f269-262">NumericLabel</span></span>
    * <span data-ttu-id="0f269-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="0f269-263">NumericScore</span></span>
    * <span data-ttu-id="0f269-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="0f269-264">NumericAll</span></span>
    * <span data-ttu-id="0f269-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="0f269-265">BooleanFeature</span></span>
    * <span data-ttu-id="0f269-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="0f269-266">BooleanLabel</span></span>
    * <span data-ttu-id="0f269-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="0f269-267">BooleanScore</span></span>
    * <span data-ttu-id="0f269-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="0f269-268">BooleanAll</span></span>
    * <span data-ttu-id="0f269-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="0f269-269">CategoricalFeature</span></span>
    * <span data-ttu-id="0f269-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="0f269-270">CategoricalLabel</span></span>
    * <span data-ttu-id="0f269-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="0f269-271">CategoricalScore</span></span>
    * <span data-ttu-id="0f269-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="0f269-272">CategoricalAll</span></span>
    * <span data-ttu-id="0f269-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="0f269-273">StringFeature</span></span>
    * <span data-ttu-id="0f269-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="0f269-274">StringLabel</span></span>
    * <span data-ttu-id="0f269-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="0f269-275">StringScore</span></span>
    * <span data-ttu-id="0f269-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="0f269-276">StringAll</span></span>
    * <span data-ttu-id="0f269-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="0f269-277">AllLabel</span></span>
    * <span data-ttu-id="0f269-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="0f269-278">AllFeature</span></span>
    * <span data-ttu-id="0f269-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="0f269-279">AllScore</span></span>
    * <span data-ttu-id="0f269-280">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="0f269-280">All</span></span>

<span data-ttu-id="0f269-281">**Lista rozwijana**: listę wyliczany określone przez użytkownika (rozwijaną).</span><span class="sxs-lookup"><span data-stu-id="0f269-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="0f269-282">elementy listy rozwijanej Hello są określone w hello **właściwości** przy użyciu elementu **elementu** elementu.</span><span class="sxs-lookup"><span data-stu-id="0f269-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="0f269-283">Witaj **identyfikator** dla każdego **elementu** musi być unikatowa i prawidłową zmienną R.</span><span class="sxs-lookup"><span data-stu-id="0f269-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="0f269-284">Witaj wartość hello **nazwa** z **elementu** służy jako tekst hello widoczny i wartość hello przekazywana funkcja toohello R.</span><span class="sxs-lookup"><span data-stu-id="0f269-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="0f269-285">*Opcjonalne właściwości*:</span><span class="sxs-lookup"><span data-stu-id="0f269-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="0f269-286">**domyślne** — Witaj wartość dla właściwości domyślnej hello musi być zgodna z wartość jednego z hello **elementu** elementów.</span><span class="sxs-lookup"><span data-stu-id="0f269-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="0f269-287">Pliki pomocnicze</span><span class="sxs-lookup"><span data-stu-id="0f269-287">Auxiliary Files</span></span>
<span data-ttu-id="0f269-288">Każdego pliku, który znajduje się w pliku ZIP niestandardowego modułu jest toobe będzie dostępna do użycia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0f269-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="0f269-289">Wszelkich struktur katalogów obecne są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="0f269-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="0f269-290">Oznacza to, że działa źródeł pliku hello sam lokalnie i w usłudze Azure Machine Learning na wykonanie.</span><span class="sxs-lookup"><span data-stu-id="0f269-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f269-291">Zwróć uwagę, że wszystkie pliki zostały wyodrębnione too'src "katalogu, więc wszystkie ścieżki powinny mieć" src / "prefiks.</span><span class="sxs-lookup"><span data-stu-id="0f269-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="0f269-292">Na przykład chcesz tooremove wszystkie wiersze z NAs z hello zestawu danych, a także usunąć wszystkie zduplikowane wiersze przed wyprowadzanie go do CustomAddRows i zostały już zapisane funkcję R, która robi to w pliku RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="0f269-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="0f269-293">Może pobierać hello dodatkowego pliku RemoveDupNARows.R w hello CustomAddRows funkcji:</span><span class="sxs-lookup"><span data-stu-id="0f269-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="0f269-294">Następnie przekaż plik zip zawierający "CustomAddRows.R", "CustomAddRows.xml" i "RemoveDupNARows.R" jako niestandardowego modułu R.</span><span class="sxs-lookup"><span data-stu-id="0f269-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="0f269-295">Środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="0f269-295">Execution Environment</span></span>
<span data-ttu-id="0f269-296">środowiska wykonawczego Hello skryptu hello R używa hello tej samej wersji elementu R, co hello **wykonanie skryptu języka R** modułu i można Użyj hello same domyślne pakiety.</span><span class="sxs-lookup"><span data-stu-id="0f269-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="0f269-297">Można również dodać dodatkowe pakiety tooyour niestandardowego modułu R przez włączenie ich do pakietu zip hello niestandardowego modułu.</span><span class="sxs-lookup"><span data-stu-id="0f269-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="0f269-298">Wystarczy załadować je w skrypcie R tak jak w środowisku R.</span><span class="sxs-lookup"><span data-stu-id="0f269-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="0f269-299">**Ograniczenia środowiska wykonawczego hello** obejmują:</span><span class="sxs-lookup"><span data-stu-id="0f269-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="0f269-300">System plików nie trwała: pliki napisane po uruchomieniu hello niestandardowego modułu nie są zachowywane w wielu uruchomień hello tego samego modułu.</span><span class="sxs-lookup"><span data-stu-id="0f269-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="0f269-301">Nie dostępu do sieci</span><span class="sxs-lookup"><span data-stu-id="0f269-301">No network access</span></span>

