---
title: "Tworzenie niestandardowe R moduły w Azure Machine Learning | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 964ddb551a475243891abce8a2b835e65569a4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="10c3d-103">Tworzenie niestandardowych modułów R w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="10c3d-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="10c3d-104">W tym temacie opisano sposób tworzenia i wdrażania niestandardowego modułu R w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="10c3d-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="10c3d-105">Wyjaśniono, co to są niestandardowych modułów R i które pliki są używane do definiowania ich.</span><span class="sxs-lookup"><span data-stu-id="10c3d-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="10c3d-106">Go ilustruje sposób tworzenia plików, które definiują modułu i jak można zarejestrować modułu do wdrożenia w obszarze roboczym uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="10c3d-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="10c3d-107">Elementy i atrybuty używane w definicji niestandardowego modułu następnie są opisane bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="10c3d-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="10c3d-108">Również omówiono sposób użycia funkcji pomocniczych, plików i wielu wyjść.</span><span class="sxs-lookup"><span data-stu-id="10c3d-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="10c3d-109">Co to jest niestandardowego modułu R?</span><span class="sxs-lookup"><span data-stu-id="10c3d-109">What is a custom R module?</span></span>
<span data-ttu-id="10c3d-110">A **niestandardowego modułu** jest modułem zdefiniowane przez użytkownika, które można przekazać do swojego obszaru roboczego i wykonywane w ramach eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="10c3d-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="10c3d-111">A **niestandardowego modułu R** jest niestandardowy moduł, który wykonuje funkcję R zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10c3d-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="10c3d-112">**R** to język programowania statystyczne obliczeniowych i grafiki, powszechnie używaną służące chi i dane dotyczące implementowania algorytmów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="10c3d-113">R jest obecnie jedynym obsługiwanym niestandardowe moduły, ale pomocy technicznej dla dodatkowych języków zostało zaplanowane w przyszłych wersjach językiem.</span><span class="sxs-lookup"><span data-stu-id="10c3d-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="10c3d-114">Niestandardowe moduły mają **najwyższej jakości stan** w usłudze Azure Machine Learning, w tym sensie, że mogą być używane tak samo jak inne modułu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="10c3d-115">Można je wykonać na inne moduły zawarte w opublikowanych eksperymenty lub wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="10c3d-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="10c3d-116">Masz kontrolę nad algorytm implementowane przez moduł, danych wejściowych i wyjściowych porty mają zostać użyte parametry modelowania i innych różne zachowania środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="10c3d-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="10c3d-117">Eksperymentu, która zawiera niestandardowe moduły mogą być publikowane również do witryny Cortana Intelligence Gallery łatwe udostępnianie.</span><span class="sxs-lookup"><span data-stu-id="10c3d-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="10c3d-118">Pliki w niestandardowego modułu R</span><span class="sxs-lookup"><span data-stu-id="10c3d-118">Files in a custom R module</span></span>
<span data-ttu-id="10c3d-119">Niestandardowego modułu R jest zdefiniowane przez plik zip, który zawiera co najmniej dwa pliki:</span><span class="sxs-lookup"><span data-stu-id="10c3d-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="10c3d-120">A **plik źródłowy** R funkcji udostępnianych przez moduł, który zawiera</span><span class="sxs-lookup"><span data-stu-id="10c3d-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="10c3d-121">**Pliku definicji XML** , który opisuje interfejs niestandardowego modułu</span><span class="sxs-lookup"><span data-stu-id="10c3d-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="10c3d-122">Dodatkowe pliki pomocnicze można również uwzględnić w pliku zip, który zawiera funkcje, które są dostępne z niestandardowego modułu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="10c3d-123">Ta opcja została szczegółowo opisana w **argumenty** część sekcji odwołania **elementów w pliku definicji XML** poniższy przykład szybkiego startu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="10c3d-124">Przykład Szybki Start: zdefiniuj, pakowanie i zarejestrować niestandardowego modułu R</span><span class="sxs-lookup"><span data-stu-id="10c3d-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="10c3d-125">W tym przykładzie przedstawiono sposób tworzenia pliki wymagane przez niestandardowego modułu R, umieścić je w pliku zip, a następnie Zarejestruj moduł w obszaru roboczego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="10c3d-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="10c3d-126">Przykład zip pakietu i przykładowe pliki można pobrać z [CustomAddRows.zip Pobierz plik](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="10c3d-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="10c3d-127">Plik źródłowy</span><span class="sxs-lookup"><span data-stu-id="10c3d-127">The source file</span></span>
<span data-ttu-id="10c3d-128">Rozważmy przykładową **wierszy dodać niestandardowe** moduł, który modyfikuje standardowej implementacji **Dodawanie wierszy** moduł używany do łączenia wierszy (uwagi) z dwóch zestawów danych (danych ramki).</span><span class="sxs-lookup"><span data-stu-id="10c3d-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="10c3d-129">Standardowe **Dodawanie wierszy** modułu dołącza wiersze drugi zestaw danych wejściowych w celu pierwszego użycia zestawu danych wejściowych `rbind` algorytmu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="10c3d-130">Dostosowane `CustomAddRows` funkcja podobnie akceptuje dwa zestawy danych, ale również zawierać parametr wymiany logiczną jako dodatkowe dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="10c3d-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="10c3d-131">Jeśli ustawiono parametr wymiany **FALSE**, zwraca ten sam zestaw danych jako standardowej implementacji.</span><span class="sxs-lookup"><span data-stu-id="10c3d-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="10c3d-132">Ale jeśli parametr wymiany jest **TRUE**, funkcji dołącza wierszy pierwszego zestawu danych wejściowych w celu drugiego zestawu danych zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="10c3d-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="10c3d-133">Plik CustomAddRows.R, który zawiera implementację R `CustomAddRows` funkcji udostępnianych przez **wierszy dodać niestandardowe** moduł ma następujący kod R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

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

### <a name="the-xml-definition-file"></a><span data-ttu-id="10c3d-134">Plik definicji XML</span><span class="sxs-lookup"><span data-stu-id="10c3d-134">The XML definition file</span></span>
<span data-ttu-id="10c3d-135">Do udostępnienia to `CustomAddRows` funkcji jako moduł usługi Azure Machine Learning pliku definicji XML musi zostać utworzony do określenia jak **wierszy dodać niestandardowe** modułu powinien wyglądu i zachowania.</span><span class="sxs-lookup"><span data-stu-id="10c3d-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="10c3d-136">Warto zauważyć, że wartość **identyfikator** atrybuty **dane wejściowe** i **Arg** elementów w pliku XML muszą być zgodne nazwy parametrów funkcji kodu języka R w CustomAddRows.R dokładnie plików: (*dataset1*, *dataset2*, i *wymiany* w przykładzie).</span><span class="sxs-lookup"><span data-stu-id="10c3d-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="10c3d-137">Podobnie, wartość **punktu wejścia** atrybutu **języka** elementu musi odpowiadać nazwie funkcji w skrypcie R dokładnie: (*CustomAddRows* w przykładzie) .</span><span class="sxs-lookup"><span data-stu-id="10c3d-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="10c3d-138">Z kolei **identyfikator** atrybutu dla **dane wyjściowe** elementu nie odpowiada zmiennych w skrypcie R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="10c3d-139">Jeśli wymagane jest więcej niż jedno wyjście, po prostu zwraca listę z funkcji R z wynikami umieszczone *w tej samej kolejności* jako **dane wyjściowe** elementy są zadeklarowane w pliku XML.</span><span class="sxs-lookup"><span data-stu-id="10c3d-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="10c3d-140">Pakiet, a następnie zarejestrować modułu</span><span class="sxs-lookup"><span data-stu-id="10c3d-140">Package and register the module</span></span>
<span data-ttu-id="10c3d-141">Zapisz te dwa pliki jako *CustomAddRows.R* i *CustomAddRows.xml* , a następnie do zip ze sobą dwa pliki *CustomAddRows.zip* pliku.</span><span class="sxs-lookup"><span data-stu-id="10c3d-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="10c3d-142">Aby zarejestrować je w obszarze roboczym Machine Learning, przejdź do obszaru roboczego w Machine Learning Studio, kliknij przycisk **+ nowy** znajdującego się na dole i wybierz polecenie **modułu -> z pakietu ZIP** przekazać nowy **Wierszy dodać niestandardowe** modułu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Przekaż Zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="10c3d-144">**Wierszy dodać niestandardowe** moduł jest gotowy do dostęp do eksperymentów uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="10c3d-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="10c3d-145">Elementy w pliku definicji XML</span><span class="sxs-lookup"><span data-stu-id="10c3d-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="10c3d-146">Moduł elementów</span><span class="sxs-lookup"><span data-stu-id="10c3d-146">Module elements</span></span>
<span data-ttu-id="10c3d-147">**Modułu** element służy do definiowania niestandardowego modułu w pliku XML.</span><span class="sxs-lookup"><span data-stu-id="10c3d-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="10c3d-148">Można zdefiniować wiele modułów w jednym pliku XML przy użyciu wielu **modułu** elementów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="10c3d-149">Każdy moduł w obszarze roboczym musi mieć unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="10c3d-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="10c3d-150">Zarejestruj niestandardowego modułu o takiej samej nazwie jak istniejący moduł niestandardowych i zastępuje istniejący moduł nowym.</span><span class="sxs-lookup"><span data-stu-id="10c3d-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="10c3d-151">Niestandardowe moduły można jednak zarejestrowane o takiej samej nazwie jak istniejący moduł usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="10c3d-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="10c3d-152">Jeśli tak, pojawią się one w **niestandardowy** kategorii palety modułów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="10c3d-153">W ramach **modułu** elementu, można określić dwa dodatkowe elementy opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="10c3d-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="10c3d-154">**właściciela** element, który jest osadzony w module</span><span class="sxs-lookup"><span data-stu-id="10c3d-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="10c3d-155">**opis** element zawierający tekst, który jest wyświetlany w szybką pomoc dla modułu i kiedy umieść kursor nad modułu w Interfejsie użytkownika Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="10c3d-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="10c3d-156">Zasady ograniczeń znaków w elementach modułu:</span><span class="sxs-lookup"><span data-stu-id="10c3d-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="10c3d-157">Wartość **nazwa** atrybutu w **modułu** element nie może przekraczać 64 znaków.</span><span class="sxs-lookup"><span data-stu-id="10c3d-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="10c3d-158">Zawartość **opis** element nie może przekraczać 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="10c3d-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="10c3d-159">Zawartość **właściciela** element nie może przekraczać 32 znaków.</span><span class="sxs-lookup"><span data-stu-id="10c3d-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="10c3d-160">Moduł wyniki mogą być deterministyczna lub nondeterministic.* * Domyślnie, wszystkie moduły są uważane za deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="10c3d-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="10c3d-161">Oznacza to mając niezmiennych zestaw parametrów wejściowych i danych, modułu powinien zwrócić tego samego eacRAND wyników lub czas functionh, który jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="10c3d-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="10c3d-162">To zachowanie, Azure Machine Learning Studio zwracające tylko moduły oznaczona jako deterministyczna, jeśli parametr lub danych wejściowych został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="10c3d-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="10c3d-163">Zwraca buforowane wyniki także znacznie szybsze wykonywanie eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="10c3d-164">Dostępne są funkcje, które są niedeterministyczne, takich jak RAND lub funkcji, która zwraca bieżącą datę lub godzinę.</span><span class="sxs-lookup"><span data-stu-id="10c3d-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="10c3d-165">Jeśli niedeterministyczna funkcja korzysta z modułu, można określić, czy moduł jest deterministyczna przez ustawienie opcjonalne **isDeterministic** atrybutu **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="10c3d-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="10c3d-166">Dzięki temu, że moduł zostanie uruchomiona ponownie, przy każdym uruchomieniu eksperyment, nawet jeśli nie zmieniono moduł danych wejściowych i parametrów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="10c3d-167">Język definicji</span><span class="sxs-lookup"><span data-stu-id="10c3d-167">Language Definition</span></span>
<span data-ttu-id="10c3d-168">**Języka** elementu w pliku definicji XML jest używany do określenia niestandardowego modułu języka.</span><span class="sxs-lookup"><span data-stu-id="10c3d-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="10c3d-169">R jest obecnie jedynym obsługiwanym językiem.</span><span class="sxs-lookup"><span data-stu-id="10c3d-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="10c3d-170">Wartość **sourceFile** atrybutu musi być nazwą pliku R, który zawiera funkcji do wywołania po uruchomieniu modułu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="10c3d-171">Ten plik musi być częścią pakietu zip.</span><span class="sxs-lookup"><span data-stu-id="10c3d-171">This file must be part of the zip package.</span></span> <span data-ttu-id="10c3d-172">Wartość **punktu wejścia** atrybut jest Nazwa wywoływanej funkcji i musi być zgodna z prawidłową funkcji zdefiniowanej przy w pliku źródłowym.</span><span class="sxs-lookup"><span data-stu-id="10c3d-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="10c3d-173">Porty</span><span class="sxs-lookup"><span data-stu-id="10c3d-173">Ports</span></span>
<span data-ttu-id="10c3d-174">Porty wejściowe i wyjściowe dla niestandardowego modułu są określone w elementach podrzędnych **porty** sekcja pliku definicji XML.</span><span class="sxs-lookup"><span data-stu-id="10c3d-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="10c3d-175">Kolejność tych elementów określa układ doświadczonym (UX) przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="10c3d-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="10c3d-176">Pierwszy element podrzędny **wejściowych** lub **dane wyjściowe** wymienionych w **porty** port wejściowy lewej w UX. Learning maszyny staje się element pliku XML</span><span class="sxs-lookup"><span data-stu-id="10c3d-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="10c3d-177">Każdy wejściowy i port wyjściowy może być opcjonalny **opis** elementu podrzędnego, który określa tekst wyświetlany, gdy Przesuń wskaźnik myszy za pośrednictwem portu w Interfejsie użytkownika Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="10c3d-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="10c3d-178">**Porty reguły**:</span><span class="sxs-lookup"><span data-stu-id="10c3d-178">**Ports Rules**:</span></span>

* <span data-ttu-id="10c3d-179">Maksymalna liczba **porty wejściowe i wyjściowe** to 8 dla każdego.</span><span class="sxs-lookup"><span data-stu-id="10c3d-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="10c3d-180">Elementów wejściowych</span><span class="sxs-lookup"><span data-stu-id="10c3d-180">Input elements</span></span>
<span data-ttu-id="10c3d-181">Porty wejściowe umożliwiają przekazywanie danych do obszaru roboczego i funkcja R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="10c3d-182">**Typy danych** obsługiwanych dla porty wejściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="10c3d-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="10c3d-183">**Element DataTable:** tego typu jest przekazany do funkcji R jako data.frame.</span><span class="sxs-lookup"><span data-stu-id="10c3d-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="10c3d-184">W rzeczywistości żadnych typów (na przykład plików CSV lub pliki ARFF), które są obsługiwane przez uczenia maszynowego i które są zgodne z **DataTable** są konwertowane na data.frame automatycznie.</span><span class="sxs-lookup"><span data-stu-id="10c3d-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="10c3d-185">**Identyfikator** atrybut skojarzony z poszczególnymi **DataTable** port wejściowy musi mieć unikatową wartość i wartość ta musi odpowiadać odpowiadającego nazwany parametr w funkcji R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="10c3d-186">Opcjonalne **DataTable** portów, które nie są przekazywane jako dane wejściowe w eksperymencie ma wartość **NULL** przekazany do funkcji R i opcjonalnie zip, porty są ignorowane, jeśli dane wejściowe nie jest połączony.</span><span class="sxs-lookup"><span data-stu-id="10c3d-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="10c3d-187">**IsOptional** atrybutu jest opcjonalny dla obu **DataTable** i **Zip** typów i jest *false* domyślnie.</span><span class="sxs-lookup"><span data-stu-id="10c3d-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="10c3d-188">**ZIP:** niestandardowe moduły można zaakceptować plik zip jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="10c3d-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="10c3d-189">Tych danych wejściowych jest rozpakowane do katalogu roboczego R funkcji</span><span class="sxs-lookup"><span data-stu-id="10c3d-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="10c3d-190">Dla niestandardowych modułów R identyfikator portu Zip nie musi odpowiadać żadnych parametrów funkcji R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="10c3d-191">Jest to spowodowane pliku zip jest automatycznie wyodrębniane do katalogu roboczego R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="10c3d-192">**Reguły wprowadzania:**</span><span class="sxs-lookup"><span data-stu-id="10c3d-192">**Input Rules:**</span></span>

* <span data-ttu-id="10c3d-193">Wartość **identyfikator** atrybutu **dane wejściowe** element musi być prawidłową nazwą zmiennej języka R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="10c3d-194">Wartość **identyfikator** atrybutu **dane wejściowe** element nie może być dłuższa niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="10c3d-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="10c3d-195">Wartość **nazwa** atrybutu **dane wejściowe** element nie może być dłuższa niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="10c3d-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="10c3d-196">Zawartość **opis** element nie może być dłuższa niż 128 znaków</span><span class="sxs-lookup"><span data-stu-id="10c3d-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="10c3d-197">Wartość **typu** atrybutu **dane wejściowe** element musi być *Zip* lub *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="10c3d-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="10c3d-198">Wartość **isOptional** atrybutu **dane wejściowe** element nie jest wymagana (i jest *false* domyślnie, gdy nie określono); ale jeśli jest określona, musi ona być *true* lub *false*.</span><span class="sxs-lookup"><span data-stu-id="10c3d-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="10c3d-199">Elementy danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="10c3d-199">Output elements</span></span>
<span data-ttu-id="10c3d-200">**Standardowe dane wyjściowe porty:** porty dane wyjściowe są mapowane na wartości zwracanych z funkcji R, które mogą być następnie używane przez kolejne modułów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="10c3d-201">*Element DataTable* jest typ portu tylko standardowe wyjście obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="10c3d-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="10c3d-202">(Obsługę *uczących* i *przekształca* nadchodzi.) A *DataTable* danych wyjściowych jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="10c3d-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="10c3d-203">Dla danych wyjściowych w niestandardowych modułów R, wartość **identyfikator** atrybutu nie musi odpowiadać dowolny skrypt języka R, ale musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="10c3d-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="10c3d-204">Dla wyjścia pojedynczy moduł, musi być wartość zwrócona przez funkcję R *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="10c3d-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="10c3d-205">W celu przekazania więcej niż jeden obiekt obsługiwany typ danych, porty odpowiednie dane wyjściowe muszą być określone w pliku definicji XML i muszą być zwracane w postaci listy obiektów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="10c3d-206">Obiekty danych wyjściowych są przypisywane do danych wyjściowych porty od lewej do prawej, odzwierciedlający kolejności, w których obiekty są umieszczane w liście zwracanych.</span><span class="sxs-lookup"><span data-stu-id="10c3d-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="10c3d-207">Na przykład, jeśli chcesz zmodyfikować **wierszy dodać niestandardowe** modułu do oryginalnego dwóch zestawów danych wyjściowych *dataset1* i *dataset2*, oprócz sprzężonych nowy zestaw danych *dataset*, (w kolejności od lewej do prawej, jako: *dataset*, *dataset1*, *dataset2*), następnie zdefiniuj porty wyjścia w CustomAddRows.xml pliku w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="10c3d-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

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


<span data-ttu-id="10c3d-208">I zwracają listę obiektów w postaci listy we właściwej kolejności w "CustomAddRows.R":</span><span class="sxs-lookup"><span data-stu-id="10c3d-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="10c3d-209">**Wizualizacja danych wyjściowych:** można także określić port wyjściowy typu *wizualizacji*, który zawiera dane wyjściowe z R grafiki urządzenia i konsola danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="10c3d-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="10c3d-210">Ten port nie jest częścią dane wyjściowe funkcji R i nie zakłóca kolejność inne typy portów danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="10c3d-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="10c3d-211">Aby dodać port wizualizacji na niestandardowe moduły, Dodaj **dane wyjściowe** element o wartości *wizualizacji* dla jego **typu** atrybutu:</span><span class="sxs-lookup"><span data-stu-id="10c3d-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="10c3d-212">**Dane wyjściowe reguły:**</span><span class="sxs-lookup"><span data-stu-id="10c3d-212">**Output Rules:**</span></span>

* <span data-ttu-id="10c3d-213">Wartość **identyfikator** atrybutu **dane wyjściowe** element musi być prawidłową nazwą zmiennej języka R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="10c3d-214">Wartość **identyfikator** atrybutu **dane wyjściowe** element nie może być dłuższa niż 32 znaki.</span><span class="sxs-lookup"><span data-stu-id="10c3d-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="10c3d-215">Wartość **nazwa** atrybutu **dane wyjściowe** element nie może być dłuższa niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="10c3d-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="10c3d-216">Wartość **typu** atrybutu **dane wyjściowe** element musi być *wizualizacji*.</span><span class="sxs-lookup"><span data-stu-id="10c3d-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="10c3d-217">Argumenty</span><span class="sxs-lookup"><span data-stu-id="10c3d-217">Arguments</span></span>
<span data-ttu-id="10c3d-218">Dodatkowe dane mogą zostać przekazane do funkcji R za pośrednictwem modułu parametrów, które są zdefiniowane w **argumenty** elementu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="10c3d-219">Te parametry są wyświetlane w okienku po prawej stronie właściwości interfejsu użytkownika nie jest Machine Learning, w przypadku wybrania modułu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="10c3d-220">Argumenty może być dowolną z obsługiwanych typów lub można utworzyć niestandardowe wyliczenie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="10c3d-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="10c3d-221">Podobnie jak **porty** elementów, **argumenty** elementy mogą mieć opcjonalny **opis** element, który określa tekst, który jest wyświetlany, gdy wskaźnik myszy nad Nazwa parametru.</span><span class="sxs-lookup"><span data-stu-id="10c3d-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="10c3d-222">Opcjonalne właściwości dla modułu, na przykład defaultValue minValue i maxValue może zostać dodana do wszystkich argumentów jako atrybuty **właściwości** elementu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="10c3d-223">Prawidłowe właściwości dla **właściwości** elementu są zależne od typu argumentu i opisano z typami argumentów obsługiwanych w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="10c3d-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="10c3d-224">Argumenty z **isOptional** ustawioną właściwość **"true"** nie wymagają od użytkownika wprowadzenia wartości.</span><span class="sxs-lookup"><span data-stu-id="10c3d-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="10c3d-225">Jeśli wartość nie zostanie przekazany do argumentu, argument nie jest przekazany do funkcji punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="10c3d-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="10c3d-226">Argumenty funkcji punktu wejścia, które są opcjonalne muszą być jawnie obsługiwany przez funkcję, np. domyślna wartość NULL w definicji funkcji punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="10c3d-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="10c3d-227">Opcjonalny argument będzie tylko wymuszać innych ograniczeń argumentu, tj. min lub max, jeśli wartość jest podana przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10c3d-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="10c3d-228">Zgodnie z wejściami i wyjściami jest krytyczny, że każdego z parametrów ma unikatowy identyfikator skojarzony z nimi.</span><span class="sxs-lookup"><span data-stu-id="10c3d-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="10c3d-229">W naszym przykładzie szybki start został skojarzony identyfikator i parametru *wymiany*.</span><span class="sxs-lookup"><span data-stu-id="10c3d-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="10c3d-230">ARG — element</span><span class="sxs-lookup"><span data-stu-id="10c3d-230">Arg element</span></span>
<span data-ttu-id="10c3d-231">Parametr modułu jest definiowana za pomocą **Arg** elementem podrzędnym **argumenty** sekcja pliku definicji XML.</span><span class="sxs-lookup"><span data-stu-id="10c3d-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="10c3d-232">W przypadku elementów podrzędnych w **porty** sekcji kolejność parametrów w **argumenty** sekcja definiuje układu w UX.</span><span class="sxs-lookup"><span data-stu-id="10c3d-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="10c3d-233">Parametry są wyświetlane od góry w dół w Interfejsie użytkownika w tej samej kolejności, w którym są zdefiniowane w pliku XML.</span><span class="sxs-lookup"><span data-stu-id="10c3d-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="10c3d-234">Typy obsługiwane przez usługi Machine Learning parametrów są wyświetlane tutaj.</span><span class="sxs-lookup"><span data-stu-id="10c3d-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="10c3d-235">**int** — parametr (32-bitowy) typu Liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="10c3d-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="10c3d-236">*Opcjonalne właściwości*: **min**, **max**, **domyślne** i **isOptional**</span><span class="sxs-lookup"><span data-stu-id="10c3d-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="10c3d-237">**Podwójna** — parametr typu double.</span><span class="sxs-lookup"><span data-stu-id="10c3d-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="10c3d-238">*Opcjonalne właściwości*: **min**, **max**, **domyślne** i **isOptional**</span><span class="sxs-lookup"><span data-stu-id="10c3d-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="10c3d-239">**wartość logiczna** — parametrem logicznym reprezentowanego przez pole wyboru w UX.</span><span class="sxs-lookup"><span data-stu-id="10c3d-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="10c3d-240">*Opcjonalne właściwości*: **domyślne** — wartość false, gdy nie jest ustawiona</span><span class="sxs-lookup"><span data-stu-id="10c3d-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="10c3d-241">**ciąg**: ciąg standardowy</span><span class="sxs-lookup"><span data-stu-id="10c3d-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="10c3d-242">*Opcjonalne właściwości*: **domyślne** i **isOptional**</span><span class="sxs-lookup"><span data-stu-id="10c3d-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="10c3d-243">**ColumnPicker**: parametr wybór kolumny.</span><span class="sxs-lookup"><span data-stu-id="10c3d-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="10c3d-244">Ten typ renderowania w środowiska użytkownika jako selektora kolumn.</span><span class="sxs-lookup"><span data-stu-id="10c3d-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="10c3d-245">**Właściwości** element jest tu używany do określenia identyfikatora portu, z której są wybierane kolumny, której typ port docelowy musi być *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="10c3d-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="10c3d-246">Wynik kolumnę zaznaczenia jest przekazany do funkcji R jako listę ciągów zawierającą nazwy zaznaczonej kolumny.</span><span class="sxs-lookup"><span data-stu-id="10c3d-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="10c3d-247">*Wymagane właściwości*: **portId** — identyfikator elementu danych wejściowych jest zgodny z typem *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="10c3d-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="10c3d-248">*Opcjonalne właściwości*:</span><span class="sxs-lookup"><span data-stu-id="10c3d-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="10c3d-249">**allowedTypes** — filtry kolumny typów, z której można wybrać.</span><span class="sxs-lookup"><span data-stu-id="10c3d-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="10c3d-250">Prawidłowe wartości to:</span><span class="sxs-lookup"><span data-stu-id="10c3d-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="10c3d-251">numeryczne</span><span class="sxs-lookup"><span data-stu-id="10c3d-251">Numeric</span></span>
    * <span data-ttu-id="10c3d-252">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="10c3d-252">Boolean</span></span>
    * <span data-ttu-id="10c3d-253">Podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="10c3d-253">Categorical</span></span>
    * <span data-ttu-id="10c3d-254">Ciąg</span><span class="sxs-lookup"><span data-stu-id="10c3d-254">String</span></span>
    * <span data-ttu-id="10c3d-255">Etykieta</span><span class="sxs-lookup"><span data-stu-id="10c3d-255">Label</span></span>
    * <span data-ttu-id="10c3d-256">Funkcja</span><span class="sxs-lookup"><span data-stu-id="10c3d-256">Feature</span></span>
    * <span data-ttu-id="10c3d-257">Wynik</span><span class="sxs-lookup"><span data-stu-id="10c3d-257">Score</span></span>
    * <span data-ttu-id="10c3d-258">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="10c3d-258">All</span></span>
  * <span data-ttu-id="10c3d-259">**domyślne** -prawidłowy domyślny wybór selektor kolumn obejmują:</span><span class="sxs-lookup"><span data-stu-id="10c3d-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="10c3d-260">Brak</span><span class="sxs-lookup"><span data-stu-id="10c3d-260">None</span></span>
    * <span data-ttu-id="10c3d-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="10c3d-261">NumericFeature</span></span>
    * <span data-ttu-id="10c3d-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="10c3d-262">NumericLabel</span></span>
    * <span data-ttu-id="10c3d-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="10c3d-263">NumericScore</span></span>
    * <span data-ttu-id="10c3d-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="10c3d-264">NumericAll</span></span>
    * <span data-ttu-id="10c3d-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="10c3d-265">BooleanFeature</span></span>
    * <span data-ttu-id="10c3d-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="10c3d-266">BooleanLabel</span></span>
    * <span data-ttu-id="10c3d-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="10c3d-267">BooleanScore</span></span>
    * <span data-ttu-id="10c3d-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="10c3d-268">BooleanAll</span></span>
    * <span data-ttu-id="10c3d-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="10c3d-269">CategoricalFeature</span></span>
    * <span data-ttu-id="10c3d-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="10c3d-270">CategoricalLabel</span></span>
    * <span data-ttu-id="10c3d-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="10c3d-271">CategoricalScore</span></span>
    * <span data-ttu-id="10c3d-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="10c3d-272">CategoricalAll</span></span>
    * <span data-ttu-id="10c3d-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="10c3d-273">StringFeature</span></span>
    * <span data-ttu-id="10c3d-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="10c3d-274">StringLabel</span></span>
    * <span data-ttu-id="10c3d-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="10c3d-275">StringScore</span></span>
    * <span data-ttu-id="10c3d-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="10c3d-276">StringAll</span></span>
    * <span data-ttu-id="10c3d-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="10c3d-277">AllLabel</span></span>
    * <span data-ttu-id="10c3d-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="10c3d-278">AllFeature</span></span>
    * <span data-ttu-id="10c3d-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="10c3d-279">AllScore</span></span>
    * <span data-ttu-id="10c3d-280">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="10c3d-280">All</span></span>

<span data-ttu-id="10c3d-281">**Lista rozwijana**: listę wyliczany określone przez użytkownika (rozwijaną).</span><span class="sxs-lookup"><span data-stu-id="10c3d-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="10c3d-282">Elementy listy rozwijanej są określane w **właściwości** przy użyciu elementu **elementu** elementu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="10c3d-283">**Identyfikator** dla każdego **elementu** musi być unikatowa i prawidłową zmienną R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="10c3d-284">Wartość **nazwa** z **elementu** służy jako tekst, który zostanie wyświetlony i wartość, która została przekazana do funkcji R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="10c3d-285">*Opcjonalne właściwości*:</span><span class="sxs-lookup"><span data-stu-id="10c3d-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="10c3d-286">**domyślne** — wartość domyślna właściwości musi być zgodna z wartość spośród **elementu** elementów.</span><span class="sxs-lookup"><span data-stu-id="10c3d-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="10c3d-287">Pliki pomocnicze</span><span class="sxs-lookup"><span data-stu-id="10c3d-287">Auxiliary Files</span></span>
<span data-ttu-id="10c3d-288">Każdego pliku, który znajduje się w pliku ZIP niestandardowego modułu będzie można używać w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="10c3d-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="10c3d-289">Wszelkich struktur katalogów obecne są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="10c3d-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="10c3d-290">Oznacza to, czy plik sourcing działa takie same lokalnie i w usłudze Azure Machine Learning na wykonanie.</span><span class="sxs-lookup"><span data-stu-id="10c3d-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="10c3d-291">Zwróć uwagę, że wszystkie pliki są wyodrębniane do katalogu 'src', powinien mieć wszystkie ścieżki ' src / "prefiks.</span><span class="sxs-lookup"><span data-stu-id="10c3d-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="10c3d-292">Załóżmy na przykład, że chcesz usunąć wszystkie wiersze z NAs z zestawu danych, a także usunąć wszystkie zduplikowane wiersze przed wyprowadzanie go do CustomAddRows i zostały już zapisane funkcję R, która robi to w pliku RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="10c3d-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="10c3d-293">Może pobierać plików pomocniczych RemoveDupNARows.R w funkcji CustomAddRows:</span><span class="sxs-lookup"><span data-stu-id="10c3d-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

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

<span data-ttu-id="10c3d-294">Następnie przekaż plik zip zawierający "CustomAddRows.R", "CustomAddRows.xml" i "RemoveDupNARows.R" jako niestandardowego modułu R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="10c3d-295">Środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="10c3d-295">Execution Environment</span></span>
<span data-ttu-id="10c3d-296">Środowisko wykonanie skryptu języka R używa tej samej wersji R jako **wykonanie skryptu języka R** modułu i używać tego samego domyślne pakiety.</span><span class="sxs-lookup"><span data-stu-id="10c3d-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="10c3d-297">Można również dodać dodatkowe pakiety języka R do niestandardowego modułu przez włączenie ich do pakietu zip niestandardowego modułu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="10c3d-298">Wystarczy załadować je w skrypcie R tak jak w środowisku R.</span><span class="sxs-lookup"><span data-stu-id="10c3d-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="10c3d-299">**Ograniczenia środowiska wykonawczego** obejmują:</span><span class="sxs-lookup"><span data-stu-id="10c3d-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="10c3d-300">System plików nie trwała: pliki napisane po uruchomieniu niestandardowego modułu nie są zachowywane w wielu uruchomień tego samego modułu.</span><span class="sxs-lookup"><span data-stu-id="10c3d-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="10c3d-301">Nie dostępu do sieci</span><span class="sxs-lookup"><span data-stu-id="10c3d-301">No network access</span></span>

