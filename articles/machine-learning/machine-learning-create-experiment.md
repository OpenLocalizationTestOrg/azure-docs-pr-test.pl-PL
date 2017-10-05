---
title: "Prosty eksperyment w usłudze Machine Learning Studio | Microsoft Docs"
description: "Ten samouczek uczenia maszynowego przeprowadzi Cię przez łatwy eksperyment dotyczący przetwarzania danych. Będziemy prognozować cenę samochodu, używając algorytmu regresji."
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
ms.openlocfilehash: 0539e9d04c61d35de56a29d350c07654c095c576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="9d329-105">Samouczek dotyczący uczenia maszynowego: tworzenie pierwszego eksperymentu związanego z przetwarzaniem danych w usłudze Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="9d329-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="9d329-106">Ten samouczek jest przeznaczony dla osób, którym nie zdarzyło się korzystać z usługi **Azure Machine Learning Studio**.</span><span class="sxs-lookup"><span data-stu-id="9d329-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="9d329-107">Ten samouczek zawiera opis kroków tworzenia eksperymentu uczenia maszynowego po raz pierwszy przy użyciu usługi Studio.</span><span class="sxs-lookup"><span data-stu-id="9d329-107">In this tutorial, we'll walk through how to use Studio for the first time to create a machine learning experiment.</span></span> <span data-ttu-id="9d329-108">Eksperyment ten polega na przetestowaniu modelu analitycznego, który prognozuje cenę samochodów na podstawie różnych zmiennych, takich jak marka i specyfikacja techniczna.</span><span class="sxs-lookup"><span data-stu-id="9d329-108">The experiment will test an analytical model that predicts the price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="9d329-109">Podstawowe informacje przedstawione w tym samouczku obejmują przeciąganie modułów i upuszczanie ich w obszarze eksperymentu, łączenie modułów ze sobą, uruchamianie eksperymentu oraz przeglądanie wyników.</span><span class="sxs-lookup"><span data-stu-id="9d329-109">This tutorial shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="9d329-110">Samouczek nie zawiera ogólnego omówienia uczenia maszynowego ani instrukcji dotyczących wybierania oraz używania ponad 100 wbudowanych algorytmów i modułów manipulowania danymi dostępnych w usłudze Studio.</span><span class="sxs-lookup"><span data-stu-id="9d329-110">We're not going to discuss the general topic of machine learning or how to select and use the 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="9d329-111">Jeśli nie zdarzyło Ci się korzystać z uczenia maszynowego, najlepiej rozpocząć od serii filmów wideo [Przetwarzanie danych dla początkujących](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="9d329-111">If you're new to machine learning, the video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place to start.</span></span> <span data-ttu-id="9d329-112">Seria ta stanowi znakomite wprowadzenie do uczenia maszynowego, przedstawione przy użyciu potocznego języka i codziennych pojęć.</span><span class="sxs-lookup"><span data-stu-id="9d329-112">This video series is a great introduction to machine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="9d329-113">Jeśli znasz uczenie maszynowe, ale szukasz bardziej ogólnych informacji o usłudze Machine Learning Studio i udostępnianych przez nią algorytmach, oto kilka przydatnych zasobów:</span><span class="sxs-lookup"><span data-stu-id="9d329-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and the machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="9d329-114">Co to jest Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="9d329-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="9d329-115">— ogólne omówienie usługi Studio.</span><span class="sxs-lookup"><span data-stu-id="9d329-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="9d329-116">[Podstawy uczenia maszynowego z przykładowymi algorytmami](machine-learning-basics-infographic-with-algorithm-examples.md) — ta grafika informacyjna ułatwia uzyskanie dodatkowych informacji o różnych typach algorytmów uczenia maszynowego dostępnych w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9d329-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want to learn more about the different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="9d329-117">[Przewodnik po usłudze Machine Learning](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) — ten przewodnik zawiera podobne informacje co powyższa grafika informacyjna, ale przedstawione w interakcyjnym formacie.</span><span class="sxs-lookup"><span data-stu-id="9d329-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as the infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="9d329-118">[Ściągawka dotycząca algorytmów uczenia maszynowego](machine-learning-algorithm-cheat-sheet.md) i [Jak wybierać algorytmy w usłudze Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) — te dostępne do pobrania materiały, obejmujące plakat i artykuł, zawierają szczegółowe omówienie algorytmów usługi Studio.</span><span class="sxs-lookup"><span data-stu-id="9d329-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss the Studio algorithms in depth.</span></span>
- <span data-ttu-id="9d329-119">[Usługa Machine Learning Studio: pomoc dotycząca algorytmów i modułów](https://msdn.microsoft.com/library/azure/dn905974.aspx) — pełna dokumentacja wszystkich modułów usługi Studio, w tym algorytmów uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="9d329-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is the complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="9d329-120">W czym pomaga usługa Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="9d329-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="9d329-121">Usługa Machine Learning Studio ułatwia skonfigurowanie eksperymentu za pomocą modułów typu „przeciągnij i upuść” zaprogramowanych wstępnie metodami modelowania predykcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9d329-121">Machine Learning Studio makes it easy to set up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="9d329-122">Przy użyciu wizualnego interfejsu można przeciągać ***zestawy danych*** oraz ***moduły*** analiz i upuszczać je na interakcyjny obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="9d329-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="9d329-123">Łącząc te elementy, można utworzyć ***eksperyment***, a następnie uruchomić go przy użyciu usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9d329-123">You connect them together to form an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="9d329-124">Sekwencja działań obejmuje ***tworzenie modelu***, ***uczenie modelu***, ***generowanie wyników i testowanie modelu***.</span><span class="sxs-lookup"><span data-stu-id="9d329-124">You ***create a model***, ***train the model***, and ***score and test the model***.</span></span>

<span data-ttu-id="9d329-125">Można wykonywać iteracje projektu modelu, wielokrotnie edytując i uruchamiając eksperyment, do momentu uzyskania oczekiwanych wyników.</span><span class="sxs-lookup"><span data-stu-id="9d329-125">You can iterate on your model design, editing the experiment and running it until it gives you the results you're looking for.</span></span> <span data-ttu-id="9d329-126">Gotowy model można opublikować jako ***usługę sieci Web***. Pozwoli to innym osobom uzyskiwać prognozy na podstawie nowych danych.</span><span class="sxs-lookup"><span data-stu-id="9d329-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="9d329-127">Otwieranie usługi Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="9d329-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="9d329-128">Aby rozpocząć korzystanie z usługi Studio, otwórz stronę [https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="9d329-128">To get started with Studio, go to [https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="9d329-129">Jeśli logujesz się w usłudze Machine Learning Studio nie po raz pierwszy, kliknij pozycję **Sign in** (Zaloguj się).</span><span class="sxs-lookup"><span data-stu-id="9d329-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="9d329-130">W przeciwnym razie kliknij pozycję **Sign up here** (Zarejestruj się) i wybierz opcję darmową lub płatną.</span><span class="sxs-lookup"><span data-stu-id="9d329-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="9d329-131">![Logowanie do usługi Machine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="9d329-131">![Sign in to Machine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="9d329-132">
***Logowanie do usługi Machine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="9d329-132">
***Sign in to Machine Learning Studio***</span></span>

## <a name="five-steps-to-create-an-experiment"></a><span data-ttu-id="9d329-133">Tworzenie eksperymentu w pięciu krokach</span><span class="sxs-lookup"><span data-stu-id="9d329-133">Five steps to create an experiment</span></span>

<span data-ttu-id="9d329-134">W tym samouczku dotyczącym uczenia maszynowego wykonamy pięć podstawowych kroków, aby uruchomić eksperyment w usłudze Machine Learning Studio obejmujący tworzenie i uczenie modelu oraz generowanie wyników:</span><span class="sxs-lookup"><span data-stu-id="9d329-134">In this machine learning tutorial, you'll follow five basic steps to build an experiment in Machine Learning Studio to create, train, and score your model:</span></span>

- <span data-ttu-id="9d329-135">**Tworzenie modelu**</span><span class="sxs-lookup"><span data-stu-id="9d329-135">**Create a model**</span></span>
    - <span data-ttu-id="9d329-136">[Krok 1. Pobieranie danych]</span><span class="sxs-lookup"><span data-stu-id="9d329-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="9d329-137">[Krok 2. Przygotowanie danych]</span><span class="sxs-lookup"><span data-stu-id="9d329-137">[Step 2: Prepare the data]</span></span>
    - <span data-ttu-id="9d329-138">[Krok 3. Definiowanie funkcji]</span><span class="sxs-lookup"><span data-stu-id="9d329-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="9d329-139">**Uczenie modelu**</span><span class="sxs-lookup"><span data-stu-id="9d329-139">**Train the model**</span></span>
    - <span data-ttu-id="9d329-140">[Krok 4. Wybieranie i stosowanie algorytmu uczenia]</span><span class="sxs-lookup"><span data-stu-id="9d329-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="9d329-141">**Generowanie wyników i testowanie modelu**</span><span class="sxs-lookup"><span data-stu-id="9d329-141">**Score and test the model**</span></span>
    - <span data-ttu-id="9d329-142">[Krok 5. Przewidywanie nowych cen samochodów]</span><span class="sxs-lookup"><span data-stu-id="9d329-142">[Step 5: Predict new automobile prices]</span></span>

<span data-ttu-id="9d329-143">[Krok 1. Pobieranie danych]: #step-1-get-data</span><span class="sxs-lookup"><span data-stu-id="9d329-143">[Step 1: Get data]: #step-1-get-data</span></span>
<span data-ttu-id="9d329-144">[Krok 2. Przygotowanie danych]: #step-2-prepare-the-data</span><span class="sxs-lookup"><span data-stu-id="9d329-144">[Step 2: Prepare the data]: #step-2-prepare-the-data</span></span>
<span data-ttu-id="9d329-145">[Krok 3. Definiowanie funkcji]: #step-3-define-features</span><span class="sxs-lookup"><span data-stu-id="9d329-145">[Step 3: Define features]: #step-3-define-features</span></span>
<span data-ttu-id="9d329-146">[Krok 4. Wybieranie i stosowanie algorytmu uczenia]: #step-4-choose-and-apply-a-learning-algorithm</span><span class="sxs-lookup"><span data-stu-id="9d329-146">[Step 4: Choose and apply a learning algorithm]: #step-4-choose-and-apply-a-learning-algorithm</span></span>
<span data-ttu-id="9d329-147">[Krok 5. Przewidywanie nowych cen samochodów]: #step-5-predict-new-automobile-prices</span><span class="sxs-lookup"><span data-stu-id="9d329-147">[Step 5: Predict new automobile prices]: #step-5-predict-new-automobile-prices</span></span>

> [!TIP] 
> <span data-ttu-id="9d329-148">Funkcjonalną kopię poniższego eksperymentu można znaleźć w witrynie [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9d329-148">You can find a working copy of the following experiment in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9d329-149">Otwórz stronę **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** (Pierwszy eksperyment z przetwarzaniem danych — prognozowanie cen samochodów) i kliknij przycisk **Open in Studio** (Otwórz w usłudze Studio), aby pobrać kopię eksperymentu do obszaru roboczego usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9d329-149">Go to **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="9d329-150">Krok 1. Pobieranie danych</span><span class="sxs-lookup"><span data-stu-id="9d329-150">Step 1: Get data</span></span>

<span data-ttu-id="9d329-151">Do przeprowadzenia uczenia maszynowego potrzebne są dane.</span><span class="sxs-lookup"><span data-stu-id="9d329-151">The first thing you need to perform machine learning is data.</span></span>
<span data-ttu-id="9d329-152">Usługa Machine Learning Studio udostępnia wiele przykładowych zestawów danych do wyboru. Dane można również importować z wielu źródeł.</span><span class="sxs-lookup"><span data-stu-id="9d329-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="9d329-153">W tym scenariuszu będziemy używać przykładowego zestawu danych **Automobile price data (Raw)** (Nieprzetworzone dane z cenami samochodów), dołączonego do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="9d329-153">For this example, we'll use the sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="9d329-154">Zestaw ten zawiera dane różnych modeli samochodów, na przykład informacje dotyczące marki, ceny czy specyfikacji technicznej.</span><span class="sxs-lookup"><span data-stu-id="9d329-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="9d329-155">Poniżej przedstawiono procedurę dołączania zestawu danych do eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9d329-155">Here's how to get the dataset into your experiment.</span></span>

1. <span data-ttu-id="9d329-156">Utwórz nowy eksperyment, klikając pozycję **+NEW** (+NOWY) u dołu okna Machine Learning Studio i wybierz kolejno pozycje **EXPERIMENT** (EKSPERYMENT), **Blank Experiment** (Pusty eksperyment).</span><span class="sxs-lookup"><span data-stu-id="9d329-156">Create a new experiment by clicking **+NEW** at the bottom of the Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="9d329-157">Eksperymentowi zostanie nadana domyślna nazwa, wyświetlana w górnej części obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="9d329-157">The experiment is given a default name that you can see at the top of the canvas.</span></span> <span data-ttu-id="9d329-158">Zaznacz ten tekst i wpisz opisową nazwę, na przykład **Prognozowanie cen samochodów**.</span><span class="sxs-lookup"><span data-stu-id="9d329-158">Select this text and rename it to something meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="9d329-159">Nazwa nie musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="9d329-159">The name doesn't need to be unique.</span></span>

    ![Zmienianie nazwy eksperymentu][rename-experiment]

2. <span data-ttu-id="9d329-161">Z lewej strony obszaru roboczego eksperymentu znajduje się paleta zawierająca zestawy danych i moduły.</span><span class="sxs-lookup"><span data-stu-id="9d329-161">To the left of the experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="9d329-162">Wpisz **automobile** (samochód) w polu wyszukiwania w górnej części tej palety, aby znaleźć zestaw danych z etykietą **Automobile price data (Raw)** (Nieprzetworzone dane z cenami samochodów).</span><span class="sxs-lookup"><span data-stu-id="9d329-162">Type **automobile** in the Search box at the top of this palette to find the dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="9d329-163">Przeciągnij ten zestaw danych do obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9d329-163">Drag this dataset to the experiment canvas.</span></span>

    <span data-ttu-id="9d329-164">![Znajdowanie zestawu danych dotyczących samochodów i przeciąganie go do obszaru roboczego eksperymentu][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-164">![Find the automobile dataset and drag it onto the experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="9d329-165">***Znajdź samochodów zestawu danych i przeciągnij go do obszaru roboczego eksperymentu***</span><span class="sxs-lookup"><span data-stu-id="9d329-165">***Find the automobile dataset and drag it onto the experiment canvas***</span></span>

<span data-ttu-id="9d329-166">Aby wyświetlić graficzną reprezentację danych, kliknij port wyjściowy w dolnej części zestawu danych dotyczących samochodów, a następnie wybierz pozycję **Visualize** (Wizualizacja).</span><span class="sxs-lookup"><span data-stu-id="9d329-166">To see what this data looks like, click the output port at the bottom of the automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="9d329-167">![Klikanie portu wyjściowego i wybieranie polecenia „Visualize” (Wizualizacja)][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="9d329-167">![Click the output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="9d329-168">
***Klikanie portu wyjściowego i wybieranie polecenia „Visualize” (Wizualizacja)***</span><span class="sxs-lookup"><span data-stu-id="9d329-168">
***Click the output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="9d329-169">Zestawy danych i moduły mają porty wejściowe i wyjściowe oznaczone małymi kołami — porty wejściowe znajdują się u góry, a wyjściowe u dołu.</span><span class="sxs-lookup"><span data-stu-id="9d329-169">Datasets and modules have input and output ports represented by small circles - input ports at the top, output ports at the bottom.</span></span>
<span data-ttu-id="9d329-170">Aby utworzyć przepływ danych w eksperymencie, połącz port wyjściowy danego modułu z portem wejściowym innego modułu.</span><span class="sxs-lookup"><span data-stu-id="9d329-170">To create a flow of data through your experiment, you'll connect an output port of one module to an input port of another.</span></span>
<span data-ttu-id="9d329-171">W dowolnym momencie można kliknąć port wyjściowy zestawu danych lub modułu, aby wyświetlić dane w określonym punkcie przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="9d329-171">At any time, you can click the output port of a dataset or module to see what the data looks like at that point in the data flow.</span></span>

<span data-ttu-id="9d329-172">W tym przykładowym zestawie danych poszczególne wystąpienia modeli samochodów są wyświetlane w postaci wierszy, a zmienne skojarzone z samochodami są wyświetlane jako kolumny.</span><span class="sxs-lookup"><span data-stu-id="9d329-172">In this sample dataset, each instance of an automobile appears as a row, and the variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="9d329-173">Na podstawie zmiennych dotyczących konkretnego samochodu spróbujemy przewidzieć cenę w skrajnej prawej kolumnie (kolumna 26 o nazwie „price” [cena]).</span><span class="sxs-lookup"><span data-stu-id="9d329-173">Given the variables for a specific automobile, we're going to try to predict the price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="9d329-174">![Wyświetlanie danych samochodów w oknie wizualizacji danych][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="9d329-174">![View the automobile data in the data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="9d329-175">
***Wyświetlanie danych samochodów w oknie wizualizacji danych***</span><span class="sxs-lookup"><span data-stu-id="9d329-175">
***View the automobile data in the data visualization window***</span></span>

<span data-ttu-id="9d329-176">Aby zamknąć okno wizualizacji, kliknij znak „**x**” w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="9d329-176">Close the visualization window by clicking the "**x**" in the upper-right corner.</span></span>

## <a name="step-2-prepare-the-data"></a><span data-ttu-id="9d329-177">Krok 2. Przygotowanie danych</span><span class="sxs-lookup"><span data-stu-id="9d329-177">Step 2: Prepare the data</span></span>

<span data-ttu-id="9d329-178">Zestawy danych zwykle wymagają przetworzenia wstępnego przed rozpoczęciem analizy.</span><span class="sxs-lookup"><span data-stu-id="9d329-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="9d329-179">Na przykład może okazać się, że w przypadku niektórych wierszy w kolumnach brakuje wartości.</span><span class="sxs-lookup"><span data-stu-id="9d329-179">For example, you might have noticed the missing values present in the columns of various rows.</span></span> <span data-ttu-id="9d329-180">Te brakujące wartości muszą zostać wyczyszczone, aby umożliwić modelowi wykonanie poprawnej analizy danych.</span><span class="sxs-lookup"><span data-stu-id="9d329-180">These missing values need to be cleaned so the model can analyze the data correctly.</span></span> <span data-ttu-id="9d329-181">W naszym przykładzie usuniemy wszystkie wiersze z brakującymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="9d329-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="9d329-182">Ponadto w kolumnie **normalized-losses** (znormalizowane straty) występuje wiele przypadków brakujących wartości, dlatego całkowicie wykluczymy tę kolumnę z modelu.</span><span class="sxs-lookup"><span data-stu-id="9d329-182">Also, the **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from the model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="9d329-183">Większość modułów wymaga wyczyszczenia brakujących wartości w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9d329-183">Cleaning the missing values from input data is a prerequisite for using most of the modules.</span></span>

<span data-ttu-id="9d329-184">Najpierw dodamy moduł, który całkowicie usunie kolumnę **normalized-losses** (znormalizowane straty), a następnie inny moduł, który usunie wszystkie wiersze z brakującymi danymi.</span><span class="sxs-lookup"><span data-stu-id="9d329-184">First we add a module that removes the **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="9d329-185">Wpisz ciąg **select columns** (wybieranie kolumn) w polu wyszukiwania w górnej części palety modułów, aby znaleźć moduł [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych), a następnie przeciągnij go do obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9d329-185">Type **select columns** in the Search box at the top of the module palette to find the [Select Columns in Dataset][select-columns] module, then drag it to the experiment canvas.</span></span> <span data-ttu-id="9d329-186">Ten moduł pozwala wybierać kolumny danych, które mają zostać dołączone do modelu lub wykluczone z niego.</span><span class="sxs-lookup"><span data-stu-id="9d329-186">This module allows us to select which columns of data we want to include or exclude in the model.</span></span>

2. <span data-ttu-id="9d329-187">Połącz port wyjściowy zestawu danych **Automobile price data (Raw)** (Nieprzetworzone dane z cenami samochodów) z portem wejściowym modułu [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="9d329-187">Connect the output port of the **Automobile price data (Raw)** dataset to the input port of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="9d329-188">![Dodawanie modułu „Select Columns in Dataset” (Wybieranie kolumn w zestawie danych) do obszaru roboczego eksperymentu i tworzenie połączenia][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-188">![Add the "Select Columns in Dataset" module to the experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="9d329-189">***Dodaj moduł "Wybieranie kolumn w zestawie danych" do obszaru roboczego eksperymentu i połącz go***</span><span class="sxs-lookup"><span data-stu-id="9d329-189">***Add the "Select Columns in Dataset" module to the experiment canvas and connect it***</span></span>

3. <span data-ttu-id="9d329-190">Kliknij moduł [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych) i kliknij pozycję **Launch column selector** (Uruchom selektora kolumn) w okienku **Properties** (Właściwości).</span><span class="sxs-lookup"><span data-stu-id="9d329-190">Click the [Select Columns in Dataset][select-columns] module and click **Launch column selector** in the **Properties** pane.</span></span>

    - <span data-ttu-id="9d329-191">Po lewej stronie kliknij pozycję **With rules** (Za pomocą reguł).</span><span class="sxs-lookup"><span data-stu-id="9d329-191">On the left, click **With rules**</span></span>
    - <span data-ttu-id="9d329-192">W obszarze **Begin With** (Rozpocznij od) kliknij pozycję **All columns** (Wszystkie kolumny).</span><span class="sxs-lookup"><span data-stu-id="9d329-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="9d329-193">Spowoduje to przetworzenie wszystkich kolumn (z wyjątkiem tych wykluczonych) przez moduł [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="9d329-193">This directs [Select Columns in Dataset][select-columns] to pass through all the columns (except those columns we're about to exclude).</span></span>
    - <span data-ttu-id="9d329-194">Z list rozwijanych wybierz pozycje **Exclude** (Wyklucz) i **column names** (nazwy kolumn), a następnie kliknij wewnątrz pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9d329-194">From the drop-downs, select **Exclude** and **column names**, and then click inside the text box.</span></span> <span data-ttu-id="9d329-195">Zostanie wyświetlona lista kolumn.</span><span class="sxs-lookup"><span data-stu-id="9d329-195">A list of columns is displayed.</span></span> <span data-ttu-id="9d329-196">Wybierz pozycję **normalized-losses** (znormalizowane straty), aby dodać ją do pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9d329-196">Select **normalized-losses**, and it's added to the text box.</span></span>
    - <span data-ttu-id="9d329-197">Kliknij przycisk znacznika wyboru (OK), aby zamknąć selektora kolumn (w prawym dolnym rogu).</span><span class="sxs-lookup"><span data-stu-id="9d329-197">Click the check mark (OK) button to close the column selector (on the lower-right).</span></span>

    <span data-ttu-id="9d329-198">![Uruchamianie selektora kolumn i wykluczanie kolumny „normalized-losses” (znormalizowane straty)][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-198">![Launch the column selector and exclude the "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="9d329-199">***Uruchom selektor kolumn i wykluczyć kolumnę "kolumny znormalizowane straty"***</span><span class="sxs-lookup"><span data-stu-id="9d329-199">***Launch the column selector and exclude the "normalized-losses" column***</span></span>

    <span data-ttu-id="9d329-200">Zawartość okienka właściwości modułu **Select Columns in Dataset** (Wybieranie kolumn w zestawie danych) określa, że zostaną przetworzone wszystkie kolumny zestawu danych z wyjątkiem kolumny **normalized-losses** (znormalizowane straty).</span><span class="sxs-lookup"><span data-stu-id="9d329-200">Now the properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from the dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="9d329-201">![Zawartość okienka właściwości wskazuje na wykluczenie kolumny „normalized-losses” (znormalizowane straty)][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-201">![The properties pane shows that the "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="9d329-202">***W okienku właściwości pokazuje, że kolumna "kolumny znormalizowane straty" jest wyłączona***</span><span class="sxs-lookup"><span data-stu-id="9d329-202">***The properties pane shows that the "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="9d329-203">Aby dodać komentarz do modułu, kliknij dwukrotnie moduł i wpisz tekst.</span><span class="sxs-lookup"><span data-stu-id="9d329-203">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="9d329-204">Pozwoli to od razu sprawdzić rolę modułu w eksperymencie.</span><span class="sxs-lookup"><span data-stu-id="9d329-204">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="9d329-205">W tym przypadku kliknij dwukrotnie moduł [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych) i dodaj komentarz „Wykluczenie kolumny znormalizowanych strat”.</span><span class="sxs-lookup"><span data-stu-id="9d329-205">In this case double-click the [Select Columns in Dataset][select-columns] module and type the comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="9d329-206">![Dwukrotne kliknięcie modułu umożliwia dodanie komentarza][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-206">![Double-click a module to add a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="9d329-207">***Kliknij dwukrotnie moduł, który chcesz dodać komentarz***</span><span class="sxs-lookup"><span data-stu-id="9d329-207">***Double-click a module to add a comment***</span></span>

3. <span data-ttu-id="9d329-208">Przeciągnij moduł [Clean Missing Data][clean-missing-data] (Czyszczenie brakujących danych) do obszaru roboczego eksperymentu i połącz go z modułem [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="9d329-208">Drag the [Clean Missing Data][clean-missing-data] module to the experiment canvas and connect it to the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="9d329-209">W okienku **Properties** (Właściwości) w obszarze **Cleaning mode** (Tryb czyszczenia) wybierz pozycję **Remove entire row** (Usuń cały wiersz).</span><span class="sxs-lookup"><span data-stu-id="9d329-209">In the **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="9d329-210">Spowoduje to wyczyszczenie danych przez moduł [Clean Missing Data][clean-missing-data] (Czyszczenie brakujących danych) — zostaną usunięte wiersze, w których brakuje wartości.</span><span class="sxs-lookup"><span data-stu-id="9d329-210">This directs [Clean Missing Data][clean-missing-data] to clean the data by removing rows that have any missing values.</span></span> <span data-ttu-id="9d329-211">Kliknij dwukrotnie moduł i wpisz komentarz „Usunięcie wierszy z brakującymi wartościami”.</span><span class="sxs-lookup"><span data-stu-id="9d329-211">Double-click the module and type the comment "Remove missing value rows."</span></span>

    <span data-ttu-id="9d329-212">![Ustawianie trybu czyszczenia na wartość „Remove entire row” (Usuń cały wiersz) w module „Clean Missing Data” (Czyszczenie brakujących danych)][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-212">![Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="9d329-213">***Ustaw tryb czyszczenia "Usuń cały wiersz" dla modułu "Clean Missing Data"***</span><span class="sxs-lookup"><span data-stu-id="9d329-213">***Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="9d329-214">Uruchom eksperyment, klikając pozycję **URUCHOM** u dołu strony.</span><span class="sxs-lookup"><span data-stu-id="9d329-214">Run the experiment by clicking **RUN** at the bottom of the page.</span></span>

    <span data-ttu-id="9d329-215">Po zakończeniu eksperymentu na wszystkich modułach są widoczne zielone znaczniki wyboru. Oznacza to, że działanie modułów zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9d329-215">When the experiment has finished running, all the modules have a green check mark to indicate that they finished successfully.</span></span> <span data-ttu-id="9d329-216">Zwróć również uwagę na informację o **zakończeniu działania** wyświetlaną w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="9d329-216">Notice also the **Finished running** status in the upper-right corner.</span></span>

<span data-ttu-id="9d329-217">![Gdy działanie eksperymentu zakończy się, powinien on wyglądać mniej więcej tak][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="9d329-217">![After running it, the experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="9d329-218">
***Gdy działanie eksperymentu zakończy się, powinien on wyglądać mniej więcej tak***</span><span class="sxs-lookup"><span data-stu-id="9d329-218">
***After running it, the experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="9d329-219">Dlaczego teraz uruchomiliśmy eksperyment?</span><span class="sxs-lookup"><span data-stu-id="9d329-219">Why did we run the experiment now?</span></span> <span data-ttu-id="9d329-220">Uruchomienie eksperymentu spowodowało przekazanie definicji kolumn danych z zestawu danych do modułów [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych) i [Clean Missing Data][clean-missing-data] (Czyszczenie brakujących danych).</span><span class="sxs-lookup"><span data-stu-id="9d329-220">By running the experiment, the column definitions for our data pass from the dataset, through the [Select Columns in Dataset][select-columns] module, and through the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="9d329-221">Oznacza to, że informacje te będą dostępne dla wszystkich modułów połączonych z modułem [Clean Missing Data][clean-missing-data] (Czyszczenie brakujących danych).</span><span class="sxs-lookup"><span data-stu-id="9d329-221">This means that any modules we connect to [Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="9d329-222">Na tym etapie nasz eksperyment obejmuje tylko czyszczenie danych.</span><span class="sxs-lookup"><span data-stu-id="9d329-222">All we have done in the experiment up to this point is clean the data.</span></span> <span data-ttu-id="9d329-223">Jeśli chcesz wyświetlić oczyszczony zestaw danych, kliknij lewy port wyjściowy modułu [Clean Missing Data][clean-missing-data] (Czyszczenie brakujących danych) i wybierz pozycję **Visualize** (Wizualizacja).</span><span class="sxs-lookup"><span data-stu-id="9d329-223">If you want to view the cleaned dataset, click the left output port of the [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="9d329-224">Zwróć uwagę na to, że kolumna **normalized-losses** (znormalizowane straty) nie jest już uwzględniana i nie ma brakujących wartości.</span><span class="sxs-lookup"><span data-stu-id="9d329-224">Notice that the **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="9d329-225">Po oczyszczeniu danych można określić, jakie cechy zostaną użyte w modelu predykcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9d329-225">Now that the data is clean, we're ready to specify what features we're going to use in the predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="9d329-226">Krok 3. Definiowanie cech</span><span class="sxs-lookup"><span data-stu-id="9d329-226">Step 3: Define features</span></span>

<span data-ttu-id="9d329-227">W uczeniu maszynowym *cechy* to poszczególne mierzalne właściwości określonych informacji.</span><span class="sxs-lookup"><span data-stu-id="9d329-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="9d329-228">W naszym zestawie danych poszczególne wiersze odpowiadają różnym samochodom, a kolumny — cechom tych samochodów.</span><span class="sxs-lookup"><span data-stu-id="9d329-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="9d329-229">Znalezienie odpowiedniego zestawu cech, który ma służyć do utworzenia modelu predykcyjnego, wymaga eksperymentowania oraz dysponowania wiedzą na temat bieżącego problemu.</span><span class="sxs-lookup"><span data-stu-id="9d329-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about the problem you want to solve.</span></span> <span data-ttu-id="9d329-230">Pewne cechy lepiej nadają się do prognozowania danych docelowych.</span><span class="sxs-lookup"><span data-stu-id="9d329-230">Some features are better for predicting the target than others.</span></span> <span data-ttu-id="9d329-231">Ponadto niektóre cechy są ściśle powiązane z innymi, dlatego można je usunąć.</span><span class="sxs-lookup"><span data-stu-id="9d329-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="9d329-232">Na przykład dane dotyczące zużycia paliwa w mieście i w trasie mają bliski związek ze sobą, co sprawia, że usunięcie jednej z tych cech nie będzie miało zasadniczego wpływu na prognozę.</span><span class="sxs-lookup"><span data-stu-id="9d329-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove the other without significantly affecting the prediction.</span></span>

<span data-ttu-id="9d329-233">Utworzymy model, który korzysta z podzbioru cech zawartych w naszym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="9d329-233">Let's build a model that uses a subset of the features in our dataset.</span></span> <span data-ttu-id="9d329-234">W poszukiwaniu lepszych wyników można uruchamiać eksperymenty oparte na różnych podzbiorach cech.</span><span class="sxs-lookup"><span data-stu-id="9d329-234">You can come back later and select different features, run the experiment again, and see if you get better results.</span></span> <span data-ttu-id="9d329-235">Jednak aby rozpocząć, wypróbujmy następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="9d329-235">But to start, let's try the following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="9d329-236">Przeciągnij kolejny moduł [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych) do obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9d329-236">Drag another [Select Columns in Dataset][select-columns] module to the experiment canvas.</span></span> <span data-ttu-id="9d329-237">Połącz lewy port wyjściowy modułu [Clean Missing Data][clean-missing-data] (Czyszczenie brakujących danych) z wejściem modułu [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="9d329-237">Connect the left output port of the [Clean Missing Data][clean-missing-data] module to the input of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="9d329-238">![Łączenie modułu „Select Columns in Dataset” (Wybieranie kolumn w zestawie danych) z modułem „Clean Missing Data” (Czyszczenie brakujących danych)][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-238">![Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="9d329-239">***Moduł "Wybieranie kolumn w zestawie danych" nawiązać połączenia z modułem "Clean Missing Data"***</span><span class="sxs-lookup"><span data-stu-id="9d329-239">***Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="9d329-240">Kliknij dwukrotnie moduł i wpisz „Wybieranie cech w celu prognozowania”.</span><span class="sxs-lookup"><span data-stu-id="9d329-240">Double-click the module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="9d329-241">Kliknij pozycję **Launch column selector** (Uruchom selektora kolumn) w okienku **Properties** (Właściwości).</span><span class="sxs-lookup"><span data-stu-id="9d329-241">Click **Launch column selector** in the **Properties** pane.</span></span>

3. <span data-ttu-id="9d329-242">Kliknij pozycję **With rules** (Za pomocą reguł).</span><span class="sxs-lookup"><span data-stu-id="9d329-242">Click **With rules**.</span></span>

4. <span data-ttu-id="9d329-243">W obszarze **Begin With** (Rozpocznij od) kliknij pozycję **No columns** (Brak kolumn).</span><span class="sxs-lookup"><span data-stu-id="9d329-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="9d329-244">W wierszu filtru wybierz pozycje **Include** (Dołącz) i **column names** (nazwy kolumn), a następnie wybierz nazwy kolumn w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="9d329-244">In the filter row, select **Include** and **column names** and select our list of column names in the text box.</span></span> <span data-ttu-id="9d329-245">Spowoduje to nieprzekazywanie przez moduł żadnych kolumn (cech) z wyjątkiem tych, które zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="9d329-245">This directs the module to not pass through any columns (features) except the ones that we specify.</span></span>

5. <span data-ttu-id="9d329-246">Kliknij przycisk znacznika wyboru (OK).</span><span class="sxs-lookup"><span data-stu-id="9d329-246">Click the check mark (OK) button.</span></span>

    <span data-ttu-id="9d329-247">![Wybieranie kolumn (cech), które mają zostać uwzględnione w prognozie][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-247">![Select the columns (features) to include in the prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="9d329-248">***Wybierz kolumny (funkcje) do uwzględnienia w Prognozowanie***</span><span class="sxs-lookup"><span data-stu-id="9d329-248">***Select the columns (features) to include in the prediction***</span></span>

<span data-ttu-id="9d329-249">Powstanie filtrowany zestaw danych zawierający tylko cechy, które chcemy przekazać do algorytmu uczenia. Algorytm ten zostanie użyty w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="9d329-249">This produces a filtered dataset containing only the features we want to pass to the learning algorithm we'll use in the next step.</span></span> <span data-ttu-id="9d329-250">Możesz później wrócić do tego kroku i wybrać inny zbiór cech.</span><span class="sxs-lookup"><span data-stu-id="9d329-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="9d329-251">Krok 4. Wybieranie i stosowanie algorytmu uczenia</span><span class="sxs-lookup"><span data-stu-id="9d329-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="9d329-252">Po przygotowaniu danych można przystąpić do konstruowania modelu predykcyjnego, co obejmuje uczenie i testowanie.</span><span class="sxs-lookup"><span data-stu-id="9d329-252">Now that the data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="9d329-253">Użyjemy danych do nauczenia modelu, a następnie przetestujemy go, aby sprawdzić dokładność przewidywanych cen.</span><span class="sxs-lookup"><span data-stu-id="9d329-253">We'll use our data to train the model, and then we'll test the model to see how closely it's able to predict prices.</span></span>
<!-- For now, don't worry about *why* we need to train and then test a model.-->

<span data-ttu-id="9d329-254">Algorytmy *klasyfikacji* i *regresji* to dwa typy nadzorowanego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="9d329-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="9d329-255">Klasyfikacja przewiduje odpowiedź na podstawie zdefiniowanego zestawu kategorii, takich jak kolory (czerwony, niebieski lub zielony).</span><span class="sxs-lookup"><span data-stu-id="9d329-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="9d329-256">Regresja służy do prognozowania liczby.</span><span class="sxs-lookup"><span data-stu-id="9d329-256">Regression is used to predict a number.</span></span>

<span data-ttu-id="9d329-257">Ponieważ chcemy przewidzieć cenę, która jest liczbą, użyjemy algorytmu regresji.</span><span class="sxs-lookup"><span data-stu-id="9d329-257">Because we want to predict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="9d329-258">W tym przykładzie użyjemy prostego modelu *regresji liniowej*.</span><span class="sxs-lookup"><span data-stu-id="9d329-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="9d329-259">Jeśli chcesz dowiedzieć się więcej o różnych typach algorytmów uczenia maszynowego i ich zastosowaniach, obejrzyj pierwszy film wideo z serii Przetwarzanie danych dla początkujących: [5 pytań, na które analiza danych daje odpowiedzi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="9d329-259">If you want to learn more about different types of machine learning algorithms and when to use them, you might view the first video in the Data Science for Beginners series, [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="9d329-260">Możesz też przyjrzeć się grafice informacyjnej [Podstawy uczenia maszynowego z przykładowymi algorytmami](machine-learning-basics-infographic-with-algorithm-examples.md) lub zapoznać się z artykułem [Ściągawka dotycząca algorytmów uczenia maszynowego](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="9d329-260">You might also look at the infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out the [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="9d329-261">Uczenie modelu polega na przekazaniu mu zestawu danych zawierających cenę.</span><span class="sxs-lookup"><span data-stu-id="9d329-261">We train the model by giving it a set of data that includes the price.</span></span> <span data-ttu-id="9d329-262">Model skanuje dane i szuka korelacji między cechami samochodu a jego ceną.</span><span class="sxs-lookup"><span data-stu-id="9d329-262">The model scans the data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="9d329-263">Następnym krokiem jest przetestowanie modelu — otrzyma on zestaw cech określonych modeli samochodów w celu przewidzenia ich z góry znanych cen. Prognozy zostaną porównane z rzeczywistymi cenami samochodów.</span><span class="sxs-lookup"><span data-stu-id="9d329-263">Then we'll test the model - we'll give it a set of features for automobiles we're familiar with and see how close the model comes to predicting the known price.</span></span>

<span data-ttu-id="9d329-264">Dane dzielimy na dwa oddzielne zestawy, aby użyć ich do celów szkoleniowych i do testów.</span><span class="sxs-lookup"><span data-stu-id="9d329-264">We'll use our data for both training the model and testing it by splitting the data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="9d329-265">Wybierz moduł [Split Data][split] (Podział danych) i przeciągnij go do obszaru roboczego eksperymentu, a następnie połącz go z ostatnim modułem [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="9d329-265">Select and drag the [Split Data][split] module to the experiment canvas and connect it to the last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="9d329-266">Wybierz moduł [Split Data][split] (Podział danych), klikając go.</span><span class="sxs-lookup"><span data-stu-id="9d329-266">Click the [Split Data][split] module to select it.</span></span> <span data-ttu-id="9d329-267">Znajdź opcję **Fraction of rows in the first output dataset** (Odsetek wierszy w pierwszym zestawie danych wyjściowych) (w okienku **Właściwości** po prawej stronie obszaru roboczego) i ustaw dla niej wartość 0,75.</span><span class="sxs-lookup"><span data-stu-id="9d329-267">Find the **Fraction of rows in the first output dataset** (in the **Properties** pane to the right of the canvas) and set it to 0.75.</span></span> <span data-ttu-id="9d329-268">Dzięki temu 75% danych zostanie użytych do nauczenia modelu, a pozostałe 25% do testów (można eksperymentować, zmieniając wartość tej opcji).</span><span class="sxs-lookup"><span data-stu-id="9d329-268">This way, we'll use 75 percent of the data to train the model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="9d329-269">![Ustawianie parametru podziału modułu „Split Data” (Podział danych) na wartość 0,75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-269">![Set the split fraction of the "Split Data" module to 0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="9d329-270">***Ustaw na wartość 0,75 ułamek podzielonego modułu "Podziału danych"***</span><span class="sxs-lookup"><span data-stu-id="9d329-270">***Set the split fraction of the "Split Data" module to 0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="9d329-271">Zmieniając wartość parametru **Random seed** (Inicjator losowy) można uzyskać różne próbki losowe do celów szkoleniowych i testów.</span><span class="sxs-lookup"><span data-stu-id="9d329-271">By changing the **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="9d329-272">Ten parametr umożliwia sterowanie inicjacją pseudolosowego generatora liczb.</span><span class="sxs-lookup"><span data-stu-id="9d329-272">This parameter controls the seeding of the pseudo-random number generator.</span></span>

2. <span data-ttu-id="9d329-273">Uruchom eksperyment.</span><span class="sxs-lookup"><span data-stu-id="9d329-273">Run the experiment.</span></span> <span data-ttu-id="9d329-274">Po uruchomieniu eksperymentu moduły [Select Columns in Dataset][select-columns] (Wybieranie kolumn w zestawie danych) i [Split Data][split] (Podział danych) przekażą definicje kolumn do modułów, które będą dodawane później.</span><span class="sxs-lookup"><span data-stu-id="9d329-274">When the experiment is run, the [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions to the modules we'll be adding next.</span></span>  

3. <span data-ttu-id="9d329-275">Aby wybrać algorytm uczenia, rozwiń kategorię **Machine Learning** (Uczenie maszynowe) na palecie modułów wyświetlanej z lewej strony obszaru roboczego, a następnie rozwiń węzeł **Initialize Model** (Inicjacja modelu).</span><span class="sxs-lookup"><span data-stu-id="9d329-275">To select the learning algorithm, expand the **Machine Learning** category in the module palette to the left of the canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="9d329-276">Zostaną wyświetlone różne kategorie modułów, których można użyć do zainicjowania algorytmów uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="9d329-276">This displays several categories of modules that can be used to initialize machine learning algorithms.</span></span> <span data-ttu-id="9d329-277">W tym eksperymencie wybierz moduł [Linear Regression][linear-regression] (Regresja liniowa) z kategorii **Regression** (Regresja) i przeciągnij go do obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9d329-277">For this experiment, select the [Linear Regression][linear-regression] module under the **Regression** category, and drag it to the experiment canvas.</span></span>
<span data-ttu-id="9d329-278">(Możesz również znaleźć go, wpisując „linear regression” [regresja liniowa] w polu wyszukiwania palety).</span><span class="sxs-lookup"><span data-stu-id="9d329-278">(You can also find the module by typing "linear regression" in the palette Search box.)</span></span>

4. <span data-ttu-id="9d329-279">Znajdź moduł [Train Model][train-model] (Uczenie modelu) i przeciągnij go do obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9d329-279">Find and drag the [Train Model][train-model] module to the experiment canvas.</span></span> <span data-ttu-id="9d329-280">Połącz wyjście modułu [Linear Regression][linear-regression] (Regresja liniowa) z lewym wejściem modułu [Train Model][train-model] (Uczenie modelu) i połącz wyjście danych szkoleniowych (lewy port) modułu [Split Data][split] (Podział danych) z prawym wejściem modułu [Train Model][train-model] (Uczenie modelu).</span><span class="sxs-lookup"><span data-stu-id="9d329-280">Connect the output of the [Linear Regression][linear-regression] module to the left input of the [Train Model][train-model] module, and connect the training data output (left port) of the [Split Data][split] module to the right input of the [Train Model][train-model] module.</span></span>

    <span data-ttu-id="9d329-281">![Łączenie modułu „Train model” (Uczenie modelu) z modułami „Linear Regression” (Regresja liniowa) i „Split Data” (Podział danych)][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-281">![Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="9d329-282">***Nawiązać modułu "Train Model" moduły "Linear Regression" i "Podział dane"***</span><span class="sxs-lookup"><span data-stu-id="9d329-282">***Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="9d329-283">Kliknij moduł [Train Model][train-model] (Uczenie modelu), kliknij pozycję **Launch column selector** (Uruchom selektora kolumn) w okienku **Properties** (Właściwości), a następnie wybierz kolumnę **price** (cena).</span><span class="sxs-lookup"><span data-stu-id="9d329-283">Click the [Train Model][train-model] module, click **Launch column selector** in the **Properties** pane, and then select the **price** column.</span></span> <span data-ttu-id="9d329-284">Jest to wartość, która będzie prognozowana przez nasz model.</span><span class="sxs-lookup"><span data-stu-id="9d329-284">This is the value that our model is going to predict.</span></span>

    <span data-ttu-id="9d329-285">Kolumnę **price** (cena) możesz wybrać, przenosząc ją z listy **Available columns** (Dostępne kolumny) do listy **Selected columns** (Wybrane kolumny) w selektorze kolumn.</span><span class="sxs-lookup"><span data-stu-id="9d329-285">You select the **price** column in the column selector by moving it from the **Available columns** list to the **Selected columns** list.</span></span>

    <span data-ttu-id="9d329-286">![Wybieranie kolumny cen w module „Train model” (Uczenie modelu)][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-286">![Select the price column for the "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="9d329-287">***Wybierz kolumnę cen dla modułu "Train Model"***</span><span class="sxs-lookup"><span data-stu-id="9d329-287">***Select the price column for the "Train Model" module***</span></span>

6. <span data-ttu-id="9d329-288">Uruchom eksperyment.</span><span class="sxs-lookup"><span data-stu-id="9d329-288">Run the experiment.</span></span>

<span data-ttu-id="9d329-289">W efekcie powstał nauczony model regresji, który może służyć do generowania wyników na podstawie nowych danych samochodów w celu prognozowania cen.</span><span class="sxs-lookup"><span data-stu-id="9d329-289">We now have a trained regression model that can be used to score new automobile data to make price predictions.</span></span>

<span data-ttu-id="9d329-290">![Gdy działanie eksperymentu zakończy się, powinien on wyglądać mniej więcej tak][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="9d329-290">![After running, the experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="9d329-291">
***Gdy działanie eksperymentu zakończy się, powinien on wyglądać mniej więcej tak***</span><span class="sxs-lookup"><span data-stu-id="9d329-291">
***After running, the experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="9d329-292">Krok 5. Przewidywanie nowych cen samochodów</span><span class="sxs-lookup"><span data-stu-id="9d329-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="9d329-293">Gdy udało się nauczyć model przy użyciu 75% danych, można wygenerować wyniki dla pozostałych 25% danych, aby sprawdzić poprawność funkcjonowania modelu.</span><span class="sxs-lookup"><span data-stu-id="9d329-293">Now that we've trained the model using 75 percent of our data, we can use it to score the other 25 percent of the data to see how well our model functions.</span></span>

1. <span data-ttu-id="9d329-294">Znajdź moduł [Score Model][score-model] (Generowanie wyników przez model) i przeciągnij go do obszaru roboczego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9d329-294">Find and drag the [Score Model][score-model] module to the experiment canvas.</span></span> <span data-ttu-id="9d329-295">Połącz wyjście modułu [Train Model][train-model] (Uczenie modelu) z lewym portem wejściowym modułu [Score Model][score-model] (Generowanie wyników przez model).</span><span class="sxs-lookup"><span data-stu-id="9d329-295">Connect the output of the [Train Model][train-model] module to the left input port of [Score Model][score-model].</span></span> <span data-ttu-id="9d329-296">Połącz wyjście danych testowych (prawy port) modułu [Split Data][split] (Podział danych) z prawym portem wejściowym modułu [Score Model][score-model] (Generowanie wyników przez model).</span><span class="sxs-lookup"><span data-stu-id="9d329-296">Connect the test data output (right port) of the [Split Data][split] module to the right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="9d329-297">![Łączenie modułu „Score model” (Generowanie wyników przez model) z modułami „Train Model” (Uczenie modelu) i „Split Data” (Podział danych)][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-297">![Connect the "Score Model" module to both the "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="9d329-298">***Nawiązać modułu "Score Model" moduły "Train Model" i "Podział dane"***</span><span class="sxs-lookup"><span data-stu-id="9d329-298">***Connect the "Score Model" module to both the "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="9d329-299">Uruchom eksperyment, aby wyświetlić dane wyjściowe z modułu [Score Model][score-model] (Generowanie wyników przez model). W tym celu kliknij port wyjściowy modułu [Score Model][score-model] i wybierz pozycję **Visualize** (Wizualizacja).</span><span class="sxs-lookup"><span data-stu-id="9d329-299">Run the experiment and view the output from the [Score Model][score-model] module (click the output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="9d329-300">Dane wyjściowe zawierają przewidywane wartości cen oraz znane wartości pochodzące z danych testowych.</span><span class="sxs-lookup"><span data-stu-id="9d329-300">The output shows the predicted values for price and the known values from the test data.</span></span>  

    <span data-ttu-id="9d329-301">![Dane wyjściowe modułu „Score model” (Generowanie wyników przez model)][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="9d329-301">![Output of the "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="9d329-302">***Dane wyjściowe z modułu "Score Model"***</span><span class="sxs-lookup"><span data-stu-id="9d329-302">***Output of the "Score Model" module***</span></span>

3. <span data-ttu-id="9d329-303">Na koniec przetestujemy jakość wyników.</span><span class="sxs-lookup"><span data-stu-id="9d329-303">Finally, we test the quality of the results.</span></span> <span data-ttu-id="9d329-304">Wybierz moduł [Evaluate Model][evaluate-model] (Ocena modelu) i przeciągnij go do obszaru roboczego eksperymentu, a następnie połącz wyjście modułu [Score Model][score-model] (Generowanie wyników przez model) z lewym wejściem modułu [Evaluate Model][evaluate-model] (Ocena modelu).</span><span class="sxs-lookup"><span data-stu-id="9d329-304">Select and drag the [Evaluate Model][evaluate-model] module to the experiment canvas, and connect the output of the [Score Model][score-model] module to the left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="9d329-305">Moduł [Evaluate Model][evaluate-model] (Ocena modelu) ma dwa porty wejściowe, ponieważ może służyć do porównywania dwóch modeli.</span><span class="sxs-lookup"><span data-stu-id="9d329-305">There are two input ports on the [Evaluate Model][evaluate-model] module because it can be used to compare two models side by side.</span></span> <span data-ttu-id="9d329-306">Można później dodać do eksperymentu inny algorytm, a następnie sprawdzić, czy daje on lepsze wyniki za pomocą modułu [Evaluate Model][evaluate-model] (Ocena modelu).</span><span class="sxs-lookup"><span data-stu-id="9d329-306">Later, you can add another algorithm to the experiment and use [Evaluate Model][evaluate-model] to see which one gives better results.</span></span>

4. <span data-ttu-id="9d329-307">Uruchom eksperyment.</span><span class="sxs-lookup"><span data-stu-id="9d329-307">Run the experiment.</span></span>

<span data-ttu-id="9d329-308">Aby wyświetlić dane wyjściowe z modułu [Evaluate Model][evaluate-model] (Ocena modelu), kliknij port wyjściowy i wybierz pozycję **Visualize** (Wizualizacja).</span><span class="sxs-lookup"><span data-stu-id="9d329-308">To view the output from the [Evaluate Model][evaluate-model] module, click the output port, and then select **Visualize**.</span></span>

<span data-ttu-id="9d329-309">![Wyniki oceny eksperymentu][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="9d329-309">![Evaluation results for the experiment][evaluation-results]
</span></span><br/><span data-ttu-id="9d329-310">
***Wyniki oceny eksperymentu***</span><span class="sxs-lookup"><span data-stu-id="9d329-310">
***Evaluation results for the experiment***</span></span>

<span data-ttu-id="9d329-311">Wyświetlane są następujące statystyki dla modelu:</span><span class="sxs-lookup"><span data-stu-id="9d329-311">The following statistics are shown for our model:</span></span>

- <span data-ttu-id="9d329-312">**Średni bezwzględny błąd** (MAE, Mean Absolute Error): wartość średnia bezwzględnych błędów (*błąd* odpowiada różnicy między wartością prognozowaną a wartością rzeczywistą).</span><span class="sxs-lookup"><span data-stu-id="9d329-312">**Mean Absolute Error** (MAE): The average of absolute errors (an *error* is the difference between the predicted value and the actual value).</span></span>
- <span data-ttu-id="9d329-313">**Pierwiastek błędu średniokwadratowego** (RMSE, Root Mean Squared Error): pierwiastek kwadratowy ze średniej kwadratów błędów prognoz dla zestawu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="9d329-313">**Root Mean Squared Error** (RMSE): The square root of the average of squared errors of predictions made on the test dataset.</span></span>
- <span data-ttu-id="9d329-314">**Względny błąd absolutny**: iloraz średniej błędów absolutnych i bezwzględnej wartości różnicy między wartościami rzeczywistymi a średnią wszystkich wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="9d329-314">**Relative Absolute Error**: The average of absolute errors relative to the absolute difference between actual values and the average of all actual values.</span></span>
- <span data-ttu-id="9d329-315">**Błąd względny średniokwadratowy**: iloraz średniej kwadratów błędów i kwadratu różnicy między wartościami rzeczywistymi a średnią wszystkich wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="9d329-315">**Relative Squared Error**: The average of squared errors relative to the squared difference between the actual values and the average of all actual values.</span></span>
- <span data-ttu-id="9d329-316">**Współczynnik determinacji**: znany także jako **wartość R-kwadrat** jest miarą statystyczną jakości dopasowania modelu do danych.</span><span class="sxs-lookup"><span data-stu-id="9d329-316">**Coefficient of Determination**: Also known as the **R squared value**, this is a statistical metric indicating how well a model fits the data.</span></span>

<span data-ttu-id="9d329-317">W przypadku wszystkich powyższych statystyk mniejsze wartości oznaczają lepszą jakość modelu.</span><span class="sxs-lookup"><span data-stu-id="9d329-317">For each of the error statistics, smaller is better.</span></span> <span data-ttu-id="9d329-318">Mniejsze wartości błędów wskazują na ściślejsze dopasowanie prognoz do rzeczywistych wartości.</span><span class="sxs-lookup"><span data-stu-id="9d329-318">A smaller value indicates that the predictions more closely match the actual values.</span></span> <span data-ttu-id="9d329-319">W przypadku **współczynnika determinacji** prognozy są tym lepsze, im jego wartość jest bliższa jedności (1,0).</span><span class="sxs-lookup"><span data-stu-id="9d329-319">For **Coefficient of Determination**, the closer its value is to one (1.0), the better the predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="9d329-320">Eksperyment końcowy</span><span class="sxs-lookup"><span data-stu-id="9d329-320">Final experiment</span></span>

<span data-ttu-id="9d329-321">Końcowy eksperyment powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="9d329-321">The final experiment should look something like this:</span></span>

<span data-ttu-id="9d329-322">![Eksperyment końcowy][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="9d329-322">![The final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="9d329-323">
***Eksperyment końcowy***</span><span class="sxs-lookup"><span data-stu-id="9d329-323">
***The final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d329-324">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d329-324">Next steps</span></span>

<span data-ttu-id="9d329-325">Po ukończeniu pierwszego samouczka dotyczącego uczenia maszynowego i skonfigurowaniu eksperymentu można kontynuować ulepszanie modelu, a następnie wdrożyć go jako predykcyjną usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9d329-325">Now that you've completed the first machine learning tutorial and have your experiment set up, you can continue to improve the model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="9d329-326">**Powtarzanie eksperymentu w celu ulepszenia modelu** — można na przykład zmienić cechy używane na potrzeby prognozowania.</span><span class="sxs-lookup"><span data-stu-id="9d329-326">**Iterate to try to improve the model** - For example, you can change the features you use in your prediction.</span></span> <span data-ttu-id="9d329-327">Można też zmodyfikować właściwości algorytmu [regresji liniowej][linear-regression] lub użyć całkowicie innego algorytmu.</span><span class="sxs-lookup"><span data-stu-id="9d329-327">Or you can modify the properties of the [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="9d329-328">Można również dodać do eksperymentu wiele algorytmów uczenia maszynowego i porównać dwa z nich przy użyciu modułu [Evaluate Model][evaluate-model] (Ocena modelu).</span><span class="sxs-lookup"><span data-stu-id="9d329-328">You can even add multiple machine learning algorithms to your experiment at one time and compare two of them by using the [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="9d329-329">Przykładowe porównanie różnych modeli można znaleźć w eksperymencie [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) (Porównywanie regresorów) w witrynie [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9d329-329">For an example of how to compare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="9d329-330">Aby skopiować dowolną iterację eksperymentu, użyj przycisku **SAVE AS** (ZAPISZ JAKO) wyświetlanego u dołu strony.</span><span class="sxs-lookup"><span data-stu-id="9d329-330">To copy any iteration of your experiment, use the **SAVE AS** button at the bottom of the page.</span></span> <span data-ttu-id="9d329-331">Aby wyświetlić wszystkie iteracje eksperymentu, kliknij pozycję **VIEW RUN HISTORY** (WYŚWIETL HISTORIĘ PRZEBIEGÓW) u dołu strony.</span><span class="sxs-lookup"><span data-stu-id="9d329-331">You can see all the iterations of your experiment by clicking **VIEW RUN HISTORY** at the bottom of the page.</span></span> <span data-ttu-id="9d329-332">Aby uzyskać bardziej szczegółowe informacje, zobacz [Manage experiment iterations in Azure Machine Learning Studio][runhistory] (Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="9d329-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="9d329-333">**Wdrożenie modelu jako predykcyjnej usługi sieci Web** — jeśli model spełnia Twoje oczekiwania, możesz go wdrożyć jako usługę sieci Web i używać jej do prognozowania cen samochodów na podstawie nowych danych.</span><span class="sxs-lookup"><span data-stu-id="9d329-333">**Deploy the model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service to be used to predict automobile prices by using new data.</span></span> <span data-ttu-id="9d329-334">Aby uzyskać dodatkowe informacje, zobacz [Deploy an Azure Machine Learning web service][publish] (Wdrażanie usługi sieci Web Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="9d329-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="9d329-335">Chcesz dowiedzieć się więcej?</span><span class="sxs-lookup"><span data-stu-id="9d329-335">Want to learn more?</span></span> <span data-ttu-id="9d329-336">Aby zapoznać się z bardziej rozbudowanym i szczegółowym przewodnikiem po procesie tworzenia, uczenia i wdrażania modelu po wygenerowaniu wyników, zobacz [Develop a predictive solution by using Azure Machine Learning][walkthrough] (Opracowywanie rozwiązania predykcyjnego przy użyciu usługi Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="9d329-336">For a more extensive and detailed walkthrough of the process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

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

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
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
