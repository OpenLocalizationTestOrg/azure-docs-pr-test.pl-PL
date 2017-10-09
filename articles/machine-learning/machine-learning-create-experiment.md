---
title: "aaaA prostego eksperymentu w usłudze Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Ten samouczek uczenia maszynowego przeprowadzi Cię przez łatwy eksperyment dotyczący przetwarzania danych. Firma Microsoft będzie prognozowania hello ceny samochodu przy użyciu algorytmu regresji."
keywords: experiment,linear regression,machine learning algorithms,machine learning tutorial,predictive modeling techniques,data science experiment
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="11a15-105">Samouczek dotyczący uczenia maszynowego: tworzenie pierwszego eksperymentu związanego z przetwarzaniem danych w usłudze Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="11a15-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="11a15-106">Ten samouczek jest przeznaczony dla osób, którym nie zdarzyło się korzystać z usługi **Azure Machine Learning Studio**.</span><span class="sxs-lookup"><span data-stu-id="11a15-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="11a15-107">W tym samouczku zostanie omówiony sposób toouse Studio na powitania po raz pierwszy toocreate eksperymentu uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="11a15-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="11a15-108">Witaj eksperymentu przetestuje analitycznych modelu, który prognozuje cenę samochodów na podstawie różnych zmiennych, takich jak marka i specyfikacja techniczna hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="11a15-109">W tym samouczku przedstawiono hello podstawy modułów jak toodrag i upuść na eksperymentu, je połączyć ze sobą, uruchom eksperyment hello i przyjrzyj się hello wyników.</span><span class="sxs-lookup"><span data-stu-id="11a15-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="11a15-110">Nie chcemy się, że toodiscuss hello ogólny temat uczenia maszynowego lub jak tooselect i użyj hello 100 + wbudowanych algorytmów i danych manipulowania modułów zawarte w Studio.</span><span class="sxs-lookup"><span data-stu-id="11a15-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="11a15-111">Jeśli nowy learning toomachine hello seria filmów [nauki danych dla początkujących](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) może być toostart dobrym miejscem.</span><span class="sxs-lookup"><span data-stu-id="11a15-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="11a15-112">Ta seria wideo jest doskonały wprowadzenie learning toomachine, przy użyciu języka codzienne oraz pojęcia.</span><span class="sxs-lookup"><span data-stu-id="11a15-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="11a15-113">Jeśli znasz uczenia maszynowego, ale szukasz bardziej ogólne informacje o usłudze Machine Learning Studio i algorytmów, które zawiera uczenia maszynowego hello, Przedstawiamy materiały, dobrym:</span><span class="sxs-lookup"><span data-stu-id="11a15-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="11a15-114">Co to jest Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="11a15-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="11a15-115">— ogólne omówienie usługi Studio.</span><span class="sxs-lookup"><span data-stu-id="11a15-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="11a15-116">[Machine learning podstawy wraz z przykładami algorytmu](machine-learning-basics-infographic-with-algorithm-examples.md) -tego infographic jest przydatne w przypadku toolearn więcej o różnych typach hello algorytmów uczenia maszynowego uwzględnionych w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="11a15-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="11a15-117">[Przewodnik Learning maszyny](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) — w tym przewodniku dotyczą podobne informacje jako infographic hello powyżej, ale w format interakcyjny.</span><span class="sxs-lookup"><span data-stu-id="11a15-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="11a15-118">[Machine learning algorytmu ściągawka](machine-learning-algorithm-cheat-sheet.md) i [jak algorytmów toochoose Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) — tym plakat do pobrania i towarzyszące artykułu omówiono w nim algorytmów Studio hello szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="11a15-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="11a15-119">[Usługi Machine Learning Studio: Algorytm i pomóc modułu](https://msdn.microsoft.com/library/azure/dn905974.aspx) — jest to hello pełną dokumentację dla wszystkich modułów Studio, w tym algorytmów uczenia maszynowego,</span><span class="sxs-lookup"><span data-stu-id="11a15-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="11a15-120">W czym pomaga usługa Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="11a15-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="11a15-121">Usługa Machine Learning Studio umożliwia łatwe tooset się przy użyciu modułów przeciągania i upuszczania wcześniej zaplanowane techniki modelowania predykcyjnego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="11a15-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="11a15-122">Przy użyciu wizualnego interfejsu można przeciągać ***zestawy danych*** oraz ***moduły*** analiz i upuszczać je na interakcyjny obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="11a15-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="11a15-123">Podłącz je razem tooform ***eksperymentu*** uruchomionymi w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="11a15-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="11a15-124">Możesz ***utworzyć model***, ***uczenia modelu hello***, i ***oceny i testowania hello modelu***.</span><span class="sxs-lookup"><span data-stu-id="11a15-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="11a15-125">Można wykonać iterację projektu modelu edycji eksperymentu hello i uruchomić je, dopóki zapewnia hello wyników, którego szukasz.</span><span class="sxs-lookup"><span data-stu-id="11a15-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="11a15-126">Gotowy model można opublikować jako ***usługę sieci Web***. Pozwoli to innym osobom uzyskiwać prognozy na podstawie nowych danych.</span><span class="sxs-lookup"><span data-stu-id="11a15-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="11a15-127">Otwieranie usługi Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="11a15-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="11a15-128">tooget wprowadzenie Studio Przejdź zbyt[https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="11a15-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="11a15-129">Jeśli logujesz się w usłudze Machine Learning Studio nie po raz pierwszy, kliknij pozycję **Sign in** (Zaloguj się).</span><span class="sxs-lookup"><span data-stu-id="11a15-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="11a15-130">W przeciwnym razie kliknij pozycję **Sign up here** (Zarejestruj się) i wybierz opcję darmową lub płatną.</span><span class="sxs-lookup"><span data-stu-id="11a15-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="11a15-131">![Zaloguj się tooMachine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="11a15-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="11a15-132">
***Zaloguj się tooMachine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="11a15-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="11a15-133">Pięć kroków toocreate eksperymentu</span><span class="sxs-lookup"><span data-stu-id="11a15-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="11a15-134">W tym samouczek dotyczący uczenia maszynowego możesz wykonać pięć podstawowych kroków toobuild eksperymentu w usłudze Machine Learning Studio toocreate, pociągu i score model:</span><span class="sxs-lookup"><span data-stu-id="11a15-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="11a15-135">**Tworzenie modelu**</span><span class="sxs-lookup"><span data-stu-id="11a15-135">**Create a model**</span></span>
    - <span data-ttu-id="11a15-136">[Krok 1. Pobieranie danych]</span><span class="sxs-lookup"><span data-stu-id="11a15-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="11a15-137">[Krok 2: Przygotowanie hello danych]</span><span class="sxs-lookup"><span data-stu-id="11a15-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="11a15-138">[Krok 3. Definiowanie funkcji]</span><span class="sxs-lookup"><span data-stu-id="11a15-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="11a15-139">**Train hello model**</span><span class="sxs-lookup"><span data-stu-id="11a15-139">**Train hello model**</span></span>
    - <span data-ttu-id="11a15-140">[Krok 4. Wybieranie i stosowanie algorytmu uczenia]</span><span class="sxs-lookup"><span data-stu-id="11a15-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="11a15-141">**Oceny i testowania hello modelu**</span><span class="sxs-lookup"><span data-stu-id="11a15-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="11a15-142">[Krok 5. Przewidywanie nowych cen samochodów]</span><span class="sxs-lookup"><span data-stu-id="11a15-142">[Step 5: Predict new automobile prices]</span></span>

[Krok 1. Pobieranie danych]: #step-1-get-data
[Krok 2: Przygotowanie hello danych]: #step-2-prepare-the-data
[Krok 3. Definiowanie funkcji]: #step-3-define-features
[Krok 4. Wybieranie i stosowanie algorytmu uczenia]: #step-4-choose-and-apply-a-learning-algorithm
[Krok 5. Przewidywanie nowych cen samochodów]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="11a15-148">Kopia robocza hello można znaleźć następujących eksperymentu w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="11a15-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="11a15-149">Przejdź za**[pierwsze połączenie analiz danych eksperymentu - Prognozowanie cen samochodów](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  i kliknij przycisk **Otwórz w Studio** toodownload kopię hello eksperymentu w Twojej uczenia maszynowego Obszar roboczy Studio.</span><span class="sxs-lookup"><span data-stu-id="11a15-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="11a15-150">Krok 1. Pobieranie danych</span><span class="sxs-lookup"><span data-stu-id="11a15-150">Step 1: Get data</span></span>

<span data-ttu-id="11a15-151">najpierw Hello należy uczenia maszynowego tooperform są dane.</span><span class="sxs-lookup"><span data-stu-id="11a15-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="11a15-152">Usługa Machine Learning Studio udostępnia wiele przykładowych zestawów danych do wyboru. Dane można również importować z wielu źródeł.</span><span class="sxs-lookup"><span data-stu-id="11a15-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="11a15-153">W tym przykładzie użyjemy hello przykładowego zestawu danych, **samochodów price data (Raw)**, który znajduje się w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="11a15-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="11a15-154">Zestaw ten zawiera dane różnych modeli samochodów, na przykład informacje dotyczące marki, ceny czy specyfikacji technicznej.</span><span class="sxs-lookup"><span data-stu-id="11a15-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="11a15-155">Oto, jak tooget hello zestawu danych do eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="11a15-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="11a15-156">Utwórz nowy eksperyment, klikając **+ nowy** u dołu okna Machine Learning Studio hello hello, wybierz **EKSPERYMENTU**, a następnie wybierz **puste eksperymentu**.</span><span class="sxs-lookup"><span data-stu-id="11a15-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="11a15-157">Witaj eksperymentu znajduje się domyślną nazwę wyświetlaną u góry hello hello kanwy.</span><span class="sxs-lookup"><span data-stu-id="11a15-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="11a15-158">Wybierz ten tekst i zmień jego nazwę toosomething opisowy, na przykład **Prognozowanie cen samochodów**.</span><span class="sxs-lookup"><span data-stu-id="11a15-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="11a15-159">Nazwa Hello nie wymaga toobe unikatowy.</span><span class="sxs-lookup"><span data-stu-id="11a15-159">hello name doesn't need toobe unique.</span></span>

    ![Zmień nazwę eksperymentu hello][rename-experiment]

2. <span data-ttu-id="11a15-161">po lewej toohello kanwy eksperymentu hello znajduje się paleta zawierająca zestawy danych i moduły.</span><span class="sxs-lookup"><span data-stu-id="11a15-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="11a15-162">Typ **samochodów** w polu wyszukiwania hello na powitania górnej części tej palety toofind hello zestaw danych z etykietą **samochodów price data (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="11a15-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="11a15-163">Przeciągnij kanwy eksperymentu toohello tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="11a15-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="11a15-164">![Znajdź hello samochodów zestawu danych i przeciągnij go na kanwie eksperymentu hello][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="11a15-165">***Znajdź hello samochodów zestawu danych i przeciągnij go na kanwie eksperymentu hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="11a15-166">toosee co dane wygląda na to, kliknij port wyjściowy hello u dołu hello hello samochodów zestawu danych, a następnie wybierz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="11a15-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="11a15-167">![Kliknij port wyjściowy hello i wybierz pozycję "Wizualizacja"][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="11a15-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="11a15-168">
***Kliknij port wyjściowy hello i wybierz pozycję "Wizualizacja"***</span><span class="sxs-lookup"><span data-stu-id="11a15-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="11a15-169">Zestawy danych i moduły mają wejściowe i porty wyjścia reprezentowany przez małe okręgi — porty wejściowe u góry hello wyjściowe porty u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="11a15-170">toocreate przepływu danych eksperymentu, uzyskasz połączenie portem wyjściowym port wejściowy tooan jeden moduł innego.</span><span class="sxs-lookup"><span data-stu-id="11a15-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="11a15-171">W dowolnym momencie możesz kliknąć portem wyjściowym hello toosee dataset lub moduł danych hello wygląda w tym momencie hello przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="11a15-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="11a15-172">W tym przykładowego zestawu danych każdego wystąpienia modeli samochodów występuje jako wiersz i hello zmiennych skojarzonych z każdym samochodów są wyświetlane jako kolumny.</span><span class="sxs-lookup"><span data-stu-id="11a15-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="11a15-173">Mając hello zmienne dla określonego samochód, chcemy tootry toopredict hello cen w skrajna prawa kolumna (kolumna 26 zatytułowana "price").</span><span class="sxs-lookup"><span data-stu-id="11a15-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="11a15-174">![Wyświetl dane samochodów hello okno wizualizacji danych hello][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="11a15-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="11a15-175">
***Wyświetl dane samochodów hello okno wizualizacji danych hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="11a15-176">Hello Zamknij okno wizualizacji, klikając hello "**x**" w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="11a15-177">Krok 2: Przygotowanie hello danych</span><span class="sxs-lookup"><span data-stu-id="11a15-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="11a15-178">Zestawy danych zwykle wymagają przetworzenia wstępnego przed rozpoczęciem analizy.</span><span class="sxs-lookup"><span data-stu-id="11a15-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="11a15-179">Na przykład można zauważyć hello brakujących wartości w kolumnach hello różnych wierszy.</span><span class="sxs-lookup"><span data-stu-id="11a15-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="11a15-180">Te brakujące wartości muszą toobe wyczyszczone, aby umożliwić hello modelu można analizować dane hello poprawnie.</span><span class="sxs-lookup"><span data-stu-id="11a15-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="11a15-181">W naszym przykładzie usuniemy wszystkie wiersze z brakującymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="11a15-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="11a15-182">Ponadto hello **kolumny znormalizowane straty** kolumna ma dużą część brakujące wartości, dlatego firma Microsoft będzie wykluczyć tę kolumnę z modelu hello całkowicie.</span><span class="sxs-lookup"><span data-stu-id="11a15-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="11a15-183">Czyszczenia hello brakujących wartości w danych wejściowych jest wymaganiem wstępnym większość modułów hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="11a15-184">Najpierw dodamy moduł, który usuwa hello **kolumny znormalizowane straty** kolumny całkowicie, a następnie możemy dodać inny moduł, która usuwa wszystkie wiersze z brakującymi danymi.</span><span class="sxs-lookup"><span data-stu-id="11a15-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="11a15-185">Typ **wybierz kolumny** w polu wyszukiwania hello u góry hello hello modułu palety toofind hello [Select Columns in Dataset] [ select-columns] modułu, przeciągnij je toohello kanwy eksperymentu .</span><span class="sxs-lookup"><span data-stu-id="11a15-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="11a15-186">Ten moduł pozwala nam tooselect kolumny danych, firma Microsoft ma tooinclude lub do wykluczenia w hello modelu.</span><span class="sxs-lookup"><span data-stu-id="11a15-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="11a15-187">Połącz port wyjściowy hello hello **samochodów price data (Raw)** toohello zestawu danych wejściowych portu hello [Select Columns in Dataset] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="11a15-188">![Dodaj roboczego eksperymentu toohello modułu "Wybieranie kolumn w zestawie danych" hello i podłącz go][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="11a15-189">***Dodaj roboczego eksperymentu toohello modułu "Wybieranie kolumn w zestawie danych" hello i podłącz go***</span><span class="sxs-lookup"><span data-stu-id="11a15-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="11a15-190">Kliknij przycisk hello [Select Columns in Dataset] [ select-columns] modułu i kliknij przycisk **Uruchom selektor kolumn** w hello **właściwości** okienka.</span><span class="sxs-lookup"><span data-stu-id="11a15-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="11a15-191">Powitania po lewej stronie, kliknij przycisk **przy użyciu reguł**</span><span class="sxs-lookup"><span data-stu-id="11a15-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="11a15-192">W obszarze **Begin With** (Rozpocznij od) kliknij pozycję **All columns** (Wszystkie kolumny).</span><span class="sxs-lookup"><span data-stu-id="11a15-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="11a15-193">Dzięki temu [Select Columns in Dataset] [ select-columns] toopass za pośrednictwem wszystkich kolumn hello (z wyjątkiem tych kolumn jesteśmy o tooexclude).</span><span class="sxs-lookup"><span data-stu-id="11a15-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="11a15-194">Wybierz z listy hello rozwijane, **wykluczyć** i **nazwy kolumn**, a następnie kliknij wewnątrz pola tekstowego hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="11a15-195">Zostanie wyświetlona lista kolumn.</span><span class="sxs-lookup"><span data-stu-id="11a15-195">A list of columns is displayed.</span></span> <span data-ttu-id="11a15-196">Wybierz **kolumny znormalizowane straty**, i jest dodany toohello pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="11a15-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="11a15-197">Kliknij przycisk hello znacznika wyboru (OK) przycisk tooclose hello selektora kolumn (w prawym dolnym hello).</span><span class="sxs-lookup"><span data-stu-id="11a15-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="11a15-198">![Uruchom selektor kolumn hello i wykluczyć kolumnę hello "kolumny znormalizowane straty"][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="11a15-199">***Uruchom selektor kolumn hello i wykluczyć kolumnę hello "kolumny znormalizowane straty"***</span><span class="sxs-lookup"><span data-stu-id="11a15-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="11a15-200">Teraz hello okienka właściwości modułu **Select Columns in Dataset** wskazuje, że zostaną przetworzone wszystkie kolumny z hello zestawu danych, z wyjątkiem **kolumny znormalizowane straty**.</span><span class="sxs-lookup"><span data-stu-id="11a15-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="11a15-201">![w okienku właściwości Hello pokazuje tej kolumny hello "kolumny znormalizowane straty" jest wyłączona][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="11a15-202">***w okienku właściwości Hello pokazuje tej kolumny hello "kolumny znormalizowane straty" jest wyłączona***</span><span class="sxs-lookup"><span data-stu-id="11a15-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="11a15-203">Można dodać moduł tooa komentarza, klikając dwukrotnie pozycję modułu hello i wprowadzanie tekstu.</span><span class="sxs-lookup"><span data-stu-id="11a15-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="11a15-204">Może to ułatwić jednym rzutem oka ocenić zadań jakie hello modułu w eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="11a15-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="11a15-205">W takim przypadku kliknij dwukrotnie hello [Select Columns in Dataset] [ select-columns] moduł i wpisz tekst hello komentarz "Wyklucz znormalizowane straty".</span><span class="sxs-lookup"><span data-stu-id="11a15-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="11a15-206">![Kliknij dwukrotnie moduł tooadd komentarz][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="11a15-207">***Kliknij dwukrotnie moduł tooadd komentarz***</span><span class="sxs-lookup"><span data-stu-id="11a15-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="11a15-208">Przeciągnij hello [Clean Missing Data] [ clean-missing-data] toohello modułu obszaru roboczego eksperymentu i połącz go toohello [Select Columns in Dataset] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="11a15-209">W hello **właściwości** okienku wybierz **Usuń cały wiersz** w obszarze **tryb czyszczenia**.</span><span class="sxs-lookup"><span data-stu-id="11a15-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="11a15-210">Dzięki temu [Clean Missing Data] [ clean-missing-data] tooclean hello dane przez usunięcie wierszy, które nie mają żadnych wartości.</span><span class="sxs-lookup"><span data-stu-id="11a15-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="11a15-211">Kliknij dwukrotnie hello moduł i wpisz hello komentarz "Usunięcie wierszy z brakującymi wartościami".</span><span class="sxs-lookup"><span data-stu-id="11a15-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="11a15-212">![Ustaw tryb czyszczenia hello zbyt "Usuń cały wiersz" dla modułu "Clean Missing Data" hello][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="11a15-213">***Ustaw tryb czyszczenia hello zbyt "Usuń cały wiersz" dla modułu "Clean Missing Data" hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="11a15-214">Uruchom eksperyment hello klikając **Uruchom** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="11a15-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="11a15-215">Po zakończeniu eksperymentu hello uruchomione wszystkie moduły hello ma tooindicate zielony znacznik wyboru, które zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="11a15-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="11a15-216">Zwróć uwagę, również hello **zakończeniu działania** stan w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="11a15-217">![Po jej uruchomieniu, hello eksperyment powinien wyglądać mniej więcej tak][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="11a15-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="11a15-218">
***Po jej uruchomieniu, hello eksperyment powinien wyglądać mniej więcej tak***</span><span class="sxs-lookup"><span data-stu-id="11a15-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="11a15-219">Dlaczego przeprowadzana eksperymentu hello teraz?</span><span class="sxs-lookup"><span data-stu-id="11a15-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="11a15-220">Przez uruchomione hello eksperymentu, hello definicje kolumn dla danych przekazywania z hello zestawu danych, za pomocą hello [Select Columns in Dataset] [ select-columns] modułu, za pośrednictwem hello [Clean Missing Data] [ clean-missing-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="11a15-221">Oznacza to, że wszystkie moduły połączymy zbyt[Clean Missing Data] [ clean-missing-data] będą także mieć te same informacje.</span><span class="sxs-lookup"><span data-stu-id="11a15-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="11a15-222">Firma Microsoft to zostało zrobione w eksperymencie hello się toothis punktu będzie czystą hello danych.</span><span class="sxs-lookup"><span data-stu-id="11a15-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="11a15-223">Zestaw tooview hello czyszczenia danych, kliknij przycisk hello pozostałych portem wyjściowym hello [Clean Missing Data] [ clean-missing-data] moduł i zaznacz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="11a15-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="11a15-224">Zwróć uwagę, że hello **kolumny znormalizowane straty** kolumna nie jest już uwzględniana i nie znajdują się brakujące wartości.</span><span class="sxs-lookup"><span data-stu-id="11a15-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="11a15-225">Teraz, dane hello jest czysty, jest gotowy toospecify funkcji firma Microsoft, które ma toouse w model predykcyjny hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="11a15-226">Krok 3. Definiowanie cech</span><span class="sxs-lookup"><span data-stu-id="11a15-226">Step 3: Define features</span></span>

<span data-ttu-id="11a15-227">W uczeniu maszynowym *cechy* to poszczególne mierzalne właściwości określonych informacji.</span><span class="sxs-lookup"><span data-stu-id="11a15-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="11a15-228">W naszym zestawie danych poszczególne wiersze odpowiadają różnym samochodom, a kolumny — cechom tych samochodów.</span><span class="sxs-lookup"><span data-stu-id="11a15-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="11a15-229">Znajdowanie dobrej zestaw funkcji do tworzenia modelu predykcyjnego, wymaga eksperymentowania oraz wiedzą na temat problemu hello ma toosolve.</span><span class="sxs-lookup"><span data-stu-id="11a15-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="11a15-230">Niektóre funkcje są lepsze do prognozowania danych docelowych powitania od innych.</span><span class="sxs-lookup"><span data-stu-id="11a15-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="11a15-231">Ponadto niektóre cechy są ściśle powiązane z innymi, dlatego można je usunąć.</span><span class="sxs-lookup"><span data-stu-id="11a15-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="11a15-232">Na przykład miasto mpg i paliwa są ściśle powiązane, firma Microsoft może zachować jedną i usunąć hello innych bez znaczącego wpływu na powitania prognozowania.</span><span class="sxs-lookup"><span data-stu-id="11a15-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="11a15-233">Utworzymy model, który korzysta z podzbioru cech hello w naszym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="11a15-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="11a15-234">Można później i wybrać różne funkcje, ponownie uruchom eksperyment hello i zobacz, jeśli możesz uzyskać lepsze wyniki.</span><span class="sxs-lookup"><span data-stu-id="11a15-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="11a15-235">Ale toostart, spróbujmy hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="11a15-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="11a15-236">Przeciągnij kolejny [Select Columns in Dataset] [ select-columns] kanwy eksperymentu toohello modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="11a15-237">Połącz hello pozostałych portem wyjściowym hello [Clean Missing Data] [ clean-missing-data] danych wejściowych toohello modułu hello [Select Columns in Dataset] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="11a15-238">![Połącz moduł "Clean Missing Data" toohello dla hello "Wybieranie kolumn w zestawie danych"][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="11a15-239">***Połącz moduł "Clean Missing Data" toohello dla hello "Wybieranie kolumn w zestawie danych"***</span><span class="sxs-lookup"><span data-stu-id="11a15-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="11a15-240">Kliknij dwukrotnie hello moduł i wpisz "Wybieranie cech w celu prognozowania."</span><span class="sxs-lookup"><span data-stu-id="11a15-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="11a15-241">Kliknij przycisk **Uruchom selektor kolumn** w hello **właściwości** okienka.</span><span class="sxs-lookup"><span data-stu-id="11a15-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="11a15-242">Kliknij pozycję **With rules** (Za pomocą reguł).</span><span class="sxs-lookup"><span data-stu-id="11a15-242">Click **With rules**.</span></span>

4. <span data-ttu-id="11a15-243">W obszarze **Begin With** (Rozpocznij od) kliknij pozycję **No columns** (Brak kolumn).</span><span class="sxs-lookup"><span data-stu-id="11a15-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="11a15-244">W wierszu filtru hello, wybierz **Include** i **nazwy kolumn** i wybierz w polu tekstowym hello naszą listę nazw kolumn.</span><span class="sxs-lookup"><span data-stu-id="11a15-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="11a15-245">Kieruje hello modułu toonot przekazywania żadnych kolumn (funkcje), z wyjątkiem tych, które określono hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="11a15-246">Kliknij przycisk znacznika wyboru (OK) hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="11a15-247">![Wybierz prognozowania hello hello tooinclude kolumn (funkcje)][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="11a15-248">***Wybierz prognozowania hello hello tooinclude kolumn (funkcje)***</span><span class="sxs-lookup"><span data-stu-id="11a15-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="11a15-249">Daje to filtrowanego zestawu danych zawierającego tylko funkcje hello chcemy toohello toopass uczenia algorytmu, który zostanie użyta w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="11a15-250">Możesz później wrócić do tego kroku i wybrać inny zbiór cech.</span><span class="sxs-lookup"><span data-stu-id="11a15-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="11a15-251">Krok 4. Wybieranie i stosowanie algorytmu uczenia</span><span class="sxs-lookup"><span data-stu-id="11a15-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="11a15-252">Teraz, dane hello jest gotowy, konstruowania modelu predykcyjnego obejmuje uczenie i testowanie.</span><span class="sxs-lookup"><span data-stu-id="11a15-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="11a15-253">Użyjemy naszego modelu hello tootrain danych, a następnie przetestujemy toosee modelu hello jak blisko jest ceny toopredict stanie.</span><span class="sxs-lookup"><span data-stu-id="11a15-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="11a15-254">Algorytmy *klasyfikacji* i *regresji* to dwa typy nadzorowanego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="11a15-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="11a15-255">Klasyfikacja przewiduje odpowiedź na podstawie zdefiniowanego zestawu kategorii, takich jak kolory (czerwony, niebieski lub zielony).</span><span class="sxs-lookup"><span data-stu-id="11a15-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="11a15-256">Regresja jest używane toopredict liczbą.</span><span class="sxs-lookup"><span data-stu-id="11a15-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="11a15-257">Ponieważ chcemy ceny toopredict, która jest liczbą, użyjemy algorytm regresji.</span><span class="sxs-lookup"><span data-stu-id="11a15-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="11a15-258">W tym przykładzie użyjemy prostego modelu *regresji liniowej*.</span><span class="sxs-lookup"><span data-stu-id="11a15-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="11a15-259">Toolearn więcej o różnych typach algorytmów uczenia maszynowego i gdy toouse ich może wyświetlić wideo pierwszy hello w hello nauki danych serii początkujących [hello pięciu pytania dotyczące danych nauki odpowiedzi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="11a15-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="11a15-260">Może też przyjrzeć hello infographic [Machine learning podstawy wraz z przykładami algorytmu](machine-learning-basics-infographic-with-algorithm-examples.md), lub sprawdź hello [Machine learning arkusz ze wskazówkami dotyczącymi algorytmu](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="11a15-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="11a15-261">Firma Microsoft uczenia modelu hello przez nadanie mu zestaw danych, który zawiera cen hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="11a15-262">Hello model skanuje hello danych i wyszukać korelacji między samochodów funkcji i jej cenę.</span><span class="sxs-lookup"><span data-stu-id="11a15-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="11a15-263">Następnie przetestujemy modelu hello — firma Microsoft będzie nadaj zestaw funkcji dla samochodów, który jest zapoznać się z i zobacz, jak blisko hello modelu pochodzi cen znane hello toopredicting.</span><span class="sxs-lookup"><span data-stu-id="11a15-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="11a15-264">Użyjemy danych zarówno uczenie modelu hello i testowanie go przez podział danych hello na oddzielnych celów szkoleniowych i testów zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="11a15-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="11a15-265">Wybierz i przeciągnij hello [podziału danych] [ split] toohello modułu obszaru roboczego eksperymentu i połącz go toohello ostatnio [Select Columns in Dataset] [ select-columns] Moduł.</span><span class="sxs-lookup"><span data-stu-id="11a15-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="11a15-266">Kliknij przycisk hello [podziału danych] [ split] tooselect modułu go.</span><span class="sxs-lookup"><span data-stu-id="11a15-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="11a15-267">Znajdź hello **ułamek wierszy w hello najpierw wyjściowy zestaw danych** (w hello **właściwości** toohello okienko prawo do kanwy hello) i ustaw dla niej too0.75.</span><span class="sxs-lookup"><span data-stu-id="11a15-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="11a15-268">Dzięki temu firma Microsoft będzie przy użyciu 75 procent hello danych tootrain hello modelu, a pozostałe 25% do testowania (później możesz eksperymentować z różnych wartości procentowych).</span><span class="sxs-lookup"><span data-stu-id="11a15-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="11a15-269">![Zestaw hello podzielić część too0.75 modułu "Podziel dane" hello][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="11a15-270">***Zestaw hello podzielić część too0.75 modułu "Podziel dane" hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="11a15-271">Zmieniając hello **Random seed** parametru, można uzyskać różne próbki losowe do celów szkoleniowych i testów.</span><span class="sxs-lookup"><span data-stu-id="11a15-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="11a15-272">Ten parametr określa hello wstępne wypełnianie hello pseudolosowego generatora liczb.</span><span class="sxs-lookup"><span data-stu-id="11a15-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="11a15-273">Uruchom eksperyment hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-273">Run hello experiment.</span></span> <span data-ttu-id="11a15-274">Uruchomienie eksperymentu hello hello [Select Columns in Dataset] [ select-columns] i [podziału danych] [ split] modułów przekazać toohello definicje kolumn Moduły możemy będą dodawane później.</span><span class="sxs-lookup"><span data-stu-id="11a15-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="11a15-275">Algorytm uczenia hello tooselect rozwiń hello **Machine Learning** kategorii w lewej toohello palety modułu hello z hello obszaru roboczego, a następnie rozwiń **zainicjować modelu**.</span><span class="sxs-lookup"><span data-stu-id="11a15-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="11a15-276">Zostaną wyświetlone różne kategorie modułów, które mogą być algorytmów uczenia maszynowego tooinitialize używane.</span><span class="sxs-lookup"><span data-stu-id="11a15-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="11a15-277">W tym eksperymencie wybierz hello [regresji liniowej] [ linear-regression] moduł hello **regresji** , kategoria i przeciągnij go toohello kanwy eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="11a15-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="11a15-278">(Można również znaleźć modułu hello, wpisując "linear regression" w polu wyszukiwania palety hello.)</span><span class="sxs-lookup"><span data-stu-id="11a15-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="11a15-279">Znajdź i przeciągnij hello [Train Model] [ train-model] kanwy eksperymentu toohello modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="11a15-280">Połącz dane wyjściowe hello hello [regresji liniowej] [ linear-regression] toohello modułu pozostałych danych wejściowych hello [Train Model] [ train-model] modułu i połącz hello uczenie danych dane wyjściowe (po lewej portu) hello [podziału danych] [ split] modułu toohello dane wejściowe z hello [Train Model] [ train-model] Moduł.</span><span class="sxs-lookup"><span data-stu-id="11a15-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="11a15-281">![Połącz hello "Train Model" moduł tooboth hello "Linear Regression" i "Podział dane" modułów][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="11a15-282">***Połącz hello "Train Model" moduł tooboth hello "Linear Regression" i "Podział dane" modułów***</span><span class="sxs-lookup"><span data-stu-id="11a15-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="11a15-283">Kliknij przycisk hello [Train Model] [ train-model] modułu, kliknij przycisk **Uruchom selektor kolumn** w hello **właściwości** okienka, a następnie wybierz opcję hello **cen** kolumny.</span><span class="sxs-lookup"><span data-stu-id="11a15-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="11a15-284">Jest to nasz model toopredict będzie wartość hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="11a15-285">Wybierz hello **cen** kolumny selektora kolumn hello przez przeniesienie ich z hello **dostępne kolumny** listy toohello **wybrane kolumny** listy.</span><span class="sxs-lookup"><span data-stu-id="11a15-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="11a15-286">![Wybierz kolumnę cen powitania dla modułu "Train Model" hello][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="11a15-287">***Wybierz kolumnę cen powitania dla modułu "Train Model" hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="11a15-288">Uruchom eksperyment hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-288">Run hello experiment.</span></span>

<span data-ttu-id="11a15-289">Mamy teraz nauczony model regresji, który może być używane tooscore nowych danych samochodów toomake cen prognoz.</span><span class="sxs-lookup"><span data-stu-id="11a15-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="11a15-290">![Po uruchomieniu, eksperymentu hello powinna wyglądać mniej więcej tak][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="11a15-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="11a15-291">
***Po uruchomieniu, eksperymentu hello powinna wyglądać mniej więcej tak***</span><span class="sxs-lookup"><span data-stu-id="11a15-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="11a15-292">Krok 5. Przewidywanie nowych cen samochodów</span><span class="sxs-lookup"><span data-stu-id="11a15-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="11a15-293">Teraz, gdy udało się nauczyć model hello przy użyciu 75% danych, firma Microsoft może być używany tooscore hello pozostałe 25 procent toosee danych hello, jak dobrze funkcjonowania modelu.</span><span class="sxs-lookup"><span data-stu-id="11a15-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="11a15-294">Znajdź i przeciągnij hello [Score Model] [ score-model] kanwy eksperymentu toohello modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="11a15-295">Połącz dane wyjściowe hello hello [Train Model] [ train-model] toohello modułu pozostałych port wejściowy z [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="11a15-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="11a15-296">Połącz hello danymi wyjściowymi testów (prawy port) z hello [podziału danych] [ split] port wejściowy prawo toohello modułu [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="11a15-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="11a15-297">![Połącz hello "Score Model" moduł tooboth hello "Train Model" i "Podział dane" modułów][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="11a15-298">***Połącz hello "Score Model" moduł tooboth hello "Train Model" i "Podział dane" modułów***</span><span class="sxs-lookup"><span data-stu-id="11a15-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="11a15-299">Uruchom eksperyment hello i wyświetlić dane wyjściowe hello hello [Score Model] [ score-model] modułu (kliknij port wyjściowy hello [Score Model] [ score-model] i wybierz pozycję **Wizualizacji**).</span><span class="sxs-lookup"><span data-stu-id="11a15-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="11a15-300">przedstawia dane wyjściowe Hello hello przewidywane wartości cen i znane wartości z danych testowych hello hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="11a15-301">![Dane wyjściowe z modułu "Score Model" hello][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="11a15-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="11a15-302">***Dane wyjściowe z modułu "Score Model" hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="11a15-303">Ponadto firma Microsoft testuje hello jakość hello wyników.</span><span class="sxs-lookup"><span data-stu-id="11a15-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="11a15-304">Wybierz i przeciągnij hello [Evaluate Model] [ evaluate-model] toohello modułu obszaru roboczego eksperymentu i połącz dane wyjściowe hello hello [Score Model] [ score-model] Moduł toohello pozostałych danych wejściowych [Evaluate Model][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="11a15-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="11a15-305">Istnieją dwa porty wejściowe na powitania [Evaluate Model] [ evaluate-model] moduł może być używane toocompare dwa modele obok siebie.</span><span class="sxs-lookup"><span data-stu-id="11a15-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="11a15-306">Później można dodać innego eksperymentu toohello algorytmu i używać [Evaluate Model] [ evaluate-model] toosee, co zapewnia lepsze wyniki.</span><span class="sxs-lookup"><span data-stu-id="11a15-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="11a15-307">Uruchom eksperyment hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-307">Run hello experiment.</span></span>

<span data-ttu-id="11a15-308">dane wyjściowe hello tooview hello [Evaluate Model] [ evaluate-model] modułu, kliknij port wyjściowy hello, a następnie wybierz **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="11a15-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="11a15-309">![Wyniki oceny do eksperymentu hello][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="11a15-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="11a15-310">
***Wyniki oceny do eksperymentu hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="11a15-311">Witaj następujące statystyki są wyświetlane dla naszego modelu:</span><span class="sxs-lookup"><span data-stu-id="11a15-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="11a15-312">**Oznacza błąd absolutny** (MAE): hello średnia bezwzględnych błędów ( *błąd* hello różnic między hello przewidzieć wartość i wartością rzeczywistą hello).</span><span class="sxs-lookup"><span data-stu-id="11a15-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="11a15-313">**Błąd kwadratów oznacza główny** (RMSE): pierwiastek kwadratowy hello hello średniej kwadratów błędów prognoz dla zestawu danych testowych hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="11a15-314">**Względny błąd absolutny**: hello średniej błędów absolutnych względną toohello bezwzględnej wartości różnicy między wartościami rzeczywistymi a średnią wszystkich wartości rzeczywistych hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="11a15-315">**Błąd względny Średniokwadratowy**: hello średniej kwadratów błędów względną toohello kwadrat różnica między wartościami rzeczywistymi hello i hello średnią wszystkich wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="11a15-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="11a15-316">**Współczynnik determinacji**: nazywane również hello **wartość R-kwadrat**, jest miarą statystyczną stopień dopasowania hello danych modelu.</span><span class="sxs-lookup"><span data-stu-id="11a15-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="11a15-317">Dla każdego błędu hello statystyk mniejsze wartości oznaczają lepszą.</span><span class="sxs-lookup"><span data-stu-id="11a15-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="11a15-318">Mniejsze wartości błędów wskazują, że prognoz hello ściślejsze dopasowanie hello rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="11a15-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="11a15-319">Aby uzyskać **współczynnika determinacji**, hello bliżej jego wartość wynosi tooone (1.0) hello lepsze hello prognoz.</span><span class="sxs-lookup"><span data-stu-id="11a15-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="11a15-320">Eksperyment końcowy</span><span class="sxs-lookup"><span data-stu-id="11a15-320">Final experiment</span></span>

<span data-ttu-id="11a15-321">Witaj końcowy eksperyment powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="11a15-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="11a15-322">![końcowy eksperyment Hello][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="11a15-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="11a15-323">
***końcowy eksperyment Hello***</span><span class="sxs-lookup"><span data-stu-id="11a15-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="11a15-324">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11a15-324">Next steps</span></span>

<span data-ttu-id="11a15-325">Po ukończeniu hello pierwszy samouczek dotyczący uczenia maszynowego i mieć skonfigurowanego eksperymentu można kontynuować tooimprove hello modelu i wdrożyć go jako usługę sieci web predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="11a15-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="11a15-326">**Iterowanie modelu hello tooimprove tootry** — na przykład można zmienić funkcji hello używane do prognozowania.</span><span class="sxs-lookup"><span data-stu-id="11a15-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="11a15-327">Można też zmodyfikować właściwości hello hello [regresji liniowej] [ linear-regression] algorytm lub spróbuj całkowicie innego algorytmu.</span><span class="sxs-lookup"><span data-stu-id="11a15-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="11a15-328">Można dodać wiele maszyny eksperymentu tooyour algorytmów uczenia w tym samym czasie i porównać dwa z nich przy użyciu hello [Evaluate Model] [ evaluate-model] modułu.</span><span class="sxs-lookup"><span data-stu-id="11a15-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="11a15-329">Przykład toocompare wielu modeli w jednym eksperymentu, zobacz temat [porównania Regresorów](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="11a15-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="11a15-330">toocopy dowolną iterację eksperymentu, użyj hello **SAVE AS** przycisk u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="11a15-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="11a15-331">Wszystkie iteracje eksperymentu hello można wyświetlić, klikając **WYŚWIETL HISTORIĘ URUCHAMIANIA** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="11a15-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="11a15-332">Aby uzyskać bardziej szczegółowe informacje, zobacz [Manage experiment iterations in Azure Machine Learning Studio][runhistory] (Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="11a15-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="11a15-333">**Wdróż model hello jako usługę sieci web predykcyjnej** — po zakończeniu z danym modelem, możesz go wdrożyć jako toobe usługi sieci web używaną cen samochodów toopredict przy użyciu nowych danych.</span><span class="sxs-lookup"><span data-stu-id="11a15-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="11a15-334">Aby uzyskać dodatkowe informacje, zobacz [Deploy an Azure Machine Learning web service][publish] (Wdrażanie usługi sieci Web Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="11a15-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="11a15-335">Potrzebujesz więcej toolearn?</span><span class="sxs-lookup"><span data-stu-id="11a15-335">Want toolearn more?</span></span> <span data-ttu-id="11a15-336">Aby uzyskać bardziej rozbudowanym i szczegółowym przewodnikiem hello proces tworzenia, szkolenia, ocenianie i wdrażanie modelu, zobacz [tworzenie rozwiązania predykcyjnego za pomocą usługi Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="11a15-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
