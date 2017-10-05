---
title: "Zarządzanie iteracjami eksperymentów w usłudze Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 0e32a02358d1901bb80f356b0289b02b8e98afdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="e87a1-103">Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e87a1-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="e87a1-104">Tworzenie modelu analizy predykcyjnej jest procesem iteracyjnym - podczas modyfikowania różnych funkcji i parametry eksperymentu, wyniki stają się zbieżne aż do uzyskania czy masz wyuczonego, skutecznego modelu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="e87a1-105">Klucz do tego procesu służy do śledzenia różne iteracje eksperymentu parametrów i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e87a1-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e87a1-106">Możesz przejrzeć poprzedniej uruchomień eksperymentów w dowolnym momencie w celu testu, ponownie i ostatecznie albo upewnij się lub uściślić poprzedniej założeń.</span><span class="sxs-lookup"><span data-stu-id="e87a1-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="e87a1-107">Po uruchomieniu eksperymentu Machine Learning Studio zawiera historię uruchomienia, w tym zestaw danych, modułu, port połączenia i parametry.</span><span class="sxs-lookup"><span data-stu-id="e87a1-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="e87a1-108">Ta historia przechwytuje także wyniki, informacje środowiska uruchomieniowego start i czasy zatrzymania, komunikaty dziennika i stan wykonania.</span><span class="sxs-lookup"><span data-stu-id="e87a1-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="e87a1-109">Można przyjrzeć się wstecz żadnego z tych działa w dowolnym momencie można przejrzeć chronologii eksperymentu, a wyniki pośrednie.</span><span class="sxs-lookup"><span data-stu-id="e87a1-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="e87a1-110">Nawet służy poprzedniego uruchomienia eksperymencie można uruchomić w nowej fazy zapytania i odnajdowanie ścieżki do tworzenia prostego, złożonych lub nawet rozwiązania modelowania zespół.</span><span class="sxs-lookup"><span data-stu-id="e87a1-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="e87a1-111">Po wyświetleniu poprzedniego uruchomienia eksperymentu tej wersji eksperymentu jest zablokowany i nie można edytować.</span><span class="sxs-lookup"><span data-stu-id="e87a1-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span></span> <span data-ttu-id="e87a1-112">Można jednak zapisać kopię, klikając **SAVE AS** i podając nazwę nowej kopii.</span><span class="sxs-lookup"><span data-stu-id="e87a1-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span></span> <span data-ttu-id="e87a1-113">Usługa Machine Learning Studio otwiera nową kopię, które mogą edytować i uruchamiać.</span><span class="sxs-lookup"><span data-stu-id="e87a1-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span></span> <span data-ttu-id="e87a1-114">Jest dostępna w tym kopia eksperymentu **EKSPERYMENTY** listy oraz wszystkich innych eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="e87a1-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-the-prior-run"></a><span data-ttu-id="e87a1-115">Wyświetlanie poprzedniego uruchomienia</span><span class="sxs-lookup"><span data-stu-id="e87a1-115">Viewing the Prior Run</span></span>
<span data-ttu-id="e87a1-116">Jeśli masz otwarty eksperymentu uruchamianego co najmniej raz, uruchom poprzedniego doświadczenia można wyświetlić, klikając **uprzedniego uruchomienia** w okienku właściwości.</span><span class="sxs-lookup"><span data-stu-id="e87a1-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span></span>

<span data-ttu-id="e87a1-117">Załóżmy na przykład, tworzenie eksperymentu, a jednocześnie wersje 11:23 11:42 i 11:55.</span><span class="sxs-lookup"><span data-stu-id="e87a1-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="e87a1-118">Otwórz po ostatnim uruchomieniu eksperymentu (11:55) i kliknięcie **wcześniejszego uruchomienia**, wersja było uruchomione 11:42 jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="e87a1-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span></span>

## <a name="viewing-the-run-history"></a><span data-ttu-id="e87a1-119">Wyświetlanie historii wykonywania</span><span class="sxs-lookup"><span data-stu-id="e87a1-119">Viewing the Run History</span></span>
<span data-ttu-id="e87a1-120">Można wyświetlić wszystkich poprzednich uruchomień eksperyment, klikając **Wyświetl historię uruchamiania** w eksperymencie otwarte.</span><span class="sxs-lookup"><span data-stu-id="e87a1-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="e87a1-121">Na przykład załóżmy tworzenie eksperymentów z [regresji liniowej] [ linear-regression] modułu i chcesz obserwować wpływ zmiana wartości **tempo uczenia** na użytkownika wyniki eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="e87a1-122">Możesz uruchomić eksperyment wiele razy z różnych wartości tego parametru, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e87a1-122">You run the experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="e87a1-123">Wartość współczynnika Learning</span><span class="sxs-lookup"><span data-stu-id="e87a1-123">Learning Rate value</span></span> | <span data-ttu-id="e87a1-124">Czas rozpoczęcia wykonywania</span><span class="sxs-lookup"><span data-stu-id="e87a1-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="e87a1-125">0.1</span><span class="sxs-lookup"><span data-stu-id="e87a1-125">0.1</span></span> |<span data-ttu-id="e87a1-126">2014-9-11 4:18:58 pm</span><span class="sxs-lookup"><span data-stu-id="e87a1-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="e87a1-127">0.2</span><span class="sxs-lookup"><span data-stu-id="e87a1-127">0.2</span></span> |<span data-ttu-id="e87a1-128">2014-9-11:24:33 PM.</span><span class="sxs-lookup"><span data-stu-id="e87a1-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="e87a1-129">0.4</span><span class="sxs-lookup"><span data-stu-id="e87a1-129">0.4</span></span> |<span data-ttu-id="e87a1-130">2014-9-11 4:28:36 pm</span><span class="sxs-lookup"><span data-stu-id="e87a1-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="e87a1-131">0.5</span><span class="sxs-lookup"><span data-stu-id="e87a1-131">0.5</span></span> |<span data-ttu-id="e87a1-132">2014-9-11 4:33:31 pm</span><span class="sxs-lookup"><span data-stu-id="e87a1-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="e87a1-133">Jeśli klikniesz przycisk **WYŚWIETL HISTORIĘ URUCHAMIANIA**, wyświetlić listę wszystkich tych działa:</span><span class="sxs-lookup"><span data-stu-id="e87a1-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![Przykład Historia uruchomień][runhistory]

<span data-ttu-id="e87a1-135">Kliknij dowolny z tych działa, aby wyświetlić migawki doświadczenia w czasie jej uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e87a1-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span></span> <span data-ttu-id="e87a1-136">Konfiguracja, wartości parametrów, komentarze i wyniki są zachowywane daje pełny rekord z programem eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="e87a1-137">Do dokumentu programu iteracje eksperymentu, możesz zmodyfikować tytuł zawsze zostanie uruchomiony, możesz zaktualizować **Podsumowanie** doświadczenia we właściwościach okienku, a można dodać lub zaktualizować komentarze dotyczące poszczególnych modułów do rejestrowania programu zmiany.</span><span class="sxs-lookup"><span data-stu-id="e87a1-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span></span> <span data-ttu-id="e87a1-138">Tytuł, podsumowanie i moduł komentarze są zapisywane przy każdym uruchomieniu eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-138">The title, summary, and module comments are saved with each run of the experiment.</span></span>
> 
> 

<span data-ttu-id="e87a1-139">Lista eksperymenty w **EKSPERYMENTY** karty w usłudze Machine Learning Studio zawsze zawiera najnowszą wersję eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span></span> <span data-ttu-id="e87a1-140">Po otwarciu poprzedniego uruchomienia eksperyment (przy użyciu **uprzedniego uruchomienia** lub **WYŚWIETL HISTORIĘ URUCHAMIANIA**), można powrócić do wersji roboczej, klikając **WYŚWIETL HISTORIĘ URUCHAMIANIA** i wybierając polecenie iteracji, które ma **stanu** z **edytowalna**.</span><span class="sxs-lookup"><span data-stu-id="e87a1-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="e87a1-141">Iteracja na poprzedniego działania</span><span class="sxs-lookup"><span data-stu-id="e87a1-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="e87a1-142">Po kliknięciu **uprzedniego uruchomienia** lub **WYŚWIETL HISTORIĘ URUCHAMIANIA** i otwórz poprzedniego uruchomienia, Zakończono eksperymentu można wyświetlić w trybie tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="e87a1-143">Jeśli chcesz rozpocząć iterację eksperymentu począwszy od skonfigurowanych dla poprzedniego uruchomienia sposób, aby to zrobić, otwierając Uruchom i klikając pozycję **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="e87a1-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span></span> <span data-ttu-id="e87a1-144">To tworzy nowy eksperyment z nowy tytuł pustą, uruchom historii, i wszystkich składników i wartości parametrów poprzedniego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e87a1-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span></span> <span data-ttu-id="e87a1-145">Ten nowy eksperyment ma na liście **EXPERIMENTS** można zmodyfikować karty w usłudze Machine Learning Studio strony głównej, a i uruchom go, inicjowanie nowy Uruchom historii dla tej iteracji eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="e87a1-146">Załóżmy na przykład uruchomienie historii wyświetlone w poprzedniej sekcji eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-146">For example, suppose you have the experiment run history shown in the previous section.</span></span> <span data-ttu-id="e87a1-147">Chcesz obserwować, co się stanie w przypadku ustawienia **tempo uczenia** parametru 0,4 i spróbuj różnych wartości **liczba epok szkolenia** parametru.</span><span class="sxs-lookup"><span data-stu-id="e87a1-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="e87a1-148">Kliknij przycisk **WYŚWIETL HISTORIĘ URUCHAMIANIA** , a następnie otwórz iterację eksperymentu, uruchomionego godzinie 4:28:36 (w którym wartość parametru do 0,4).</span><span class="sxs-lookup"><span data-stu-id="e87a1-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span></span>
2. <span data-ttu-id="e87a1-149">Kliknij przycisk **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="e87a1-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="e87a1-150">Wprowadź nowy tytuł, a następnie kliknij przycisk **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="e87a1-150">Enter a new title and click the **OK** checkmark.</span></span> <span data-ttu-id="e87a1-151">Utworzono nową kopię eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e87a1-151">A new copy of the experiment is created.</span></span>
4. <span data-ttu-id="e87a1-152">Modyfikowanie **liczba epok szkolenia** parametru.</span><span class="sxs-lookup"><span data-stu-id="e87a1-152">Modify the **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="e87a1-153">Kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="e87a1-153">Click **RUN**.</span></span>

<span data-ttu-id="e87a1-154">Teraz możesz zmodyfikować i uruchomić tej wersji eksperymentu, tworzenie nowych Historia uruchomień, aby zapisać swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="e87a1-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
