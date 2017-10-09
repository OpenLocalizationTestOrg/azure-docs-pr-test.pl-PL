---
title: "Krok 2: Prześlij dane do eksperymentu uczenia maszynowego | Dokumentacja firmy Microsoft"
description: "Krok 2 hello opracowanie wskazówki rozwiązanie predykcyjne: przekazywanie przechowywanych danych publicznych do usługi Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="56725-103">Przewodnik, krok 2. Przekazywanie istniejących danych do eksperymentu usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="56725-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="56725-104">Jest to drugi etap wskazówki hello hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="56725-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="56725-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="56725-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="56725-106">**Przekazywanie istniejących danych**</span><span class="sxs-lookup"><span data-stu-id="56725-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="56725-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="56725-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="56725-108">Nauczanie i Ewaluacja modeli hello</span><span class="sxs-lookup"><span data-stu-id="56725-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="56725-109">Wdrażanie usługi sieci Web hello</span><span class="sxs-lookup"><span data-stu-id="56725-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="56725-110">Witaj dostępu do usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="56725-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="56725-111">toodevelop model predykcyjny dla oceny ryzyka kredytowego, potrzebujemy danych czy możemy użyć tootrain i przetestowanie hello modelu.</span><span class="sxs-lookup"><span data-stu-id="56725-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="56725-112">W ramach tego przewodnika użyjemy hello "UCI Statlog (niemieckim dane środki) zestawu danych" hello UC Irvine Machine Learning repozytorium.</span><span class="sxs-lookup"><span data-stu-id="56725-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="56725-113">Możesz go znaleźć tutaj:</span><span class="sxs-lookup"><span data-stu-id="56725-113">You can find it here:</span></span>  
<span data-ttu-id="56725-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://Archive.ICS.uci.edu/ml/DataSets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="56725-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="56725-115">Użyjemy hello plik o nazwie **german.data**.</span><span class="sxs-lookup"><span data-stu-id="56725-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="56725-116">Pobierz plik tooyour lokalnym dysku twardym.</span><span class="sxs-lookup"><span data-stu-id="56725-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="56725-117">Witaj **german.data** dataset zawiera wiersze 20 zmiennych dla 1000 ostatnich kandydatów do uznania.</span><span class="sxs-lookup"><span data-stu-id="56725-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="56725-118">Te zmienne 20 reprezentują zestaw funkcji hello dataset (hello *wektor funkcji*), zapewniające cechy identyfikacyjne dla każdego zgłaszającego kredytowej.</span><span class="sxs-lookup"><span data-stu-id="56725-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="56725-119">Dodatkowe kolumny w każdym wierszu reprezentuje kandydata hello ryzyka kredytowego obliczeniowej, z 700 kandydatami zidentyfikowane jako niskie ryzyko kredytowe i 300 jako wysokiego ryzyka.</span><span class="sxs-lookup"><span data-stu-id="56725-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="56725-120">Witaj UCI witryny sieci Web zawiera opis atrybutów hello hello wektor funkcji dla tych danych.</span><span class="sxs-lookup"><span data-stu-id="56725-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="56725-121">W tym informacji finansowych, historii kredytów status zatrudnienia i informacje osobiste.</span><span class="sxs-lookup"><span data-stu-id="56725-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="56725-122">Dla każdego zgłaszającego klasyfikacji binarnej został podany, wskazującą, czy są one niski lub wysoki ryzyka karty kredytowej.</span><span class="sxs-lookup"><span data-stu-id="56725-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="56725-123">Użyjemy tego tootrain danych modelu analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="56725-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="56725-124">Gdy skończymy, nasz model powinny być możliwe tooaccept wektorem funkcji dla nowej osoby i prognozowania, czy użytkownik jest ryzyko kredytowe niski i wysoki.</span><span class="sxs-lookup"><span data-stu-id="56725-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="56725-125">Oto interesujące dołączony.</span><span class="sxs-lookup"><span data-stu-id="56725-125">Here's an interesting twist.</span></span> <span data-ttu-id="56725-126">Witaj opis zestawu danych hello na powitania UCI witryny sieci Web uwagi kosztach jeśli mamy misclassify ryzyko kredytowe osoby.</span><span class="sxs-lookup"><span data-stu-id="56725-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="56725-127">Jeśli hello model przewiduje ryzyko kredytowe wysokiej osobie, która jest rzeczywiście niskie ryzyko kredytowe, hello model wprowadził błędną klasyfikację.</span><span class="sxs-lookup"><span data-stu-id="56725-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="56725-128">Ale odwrotnej błędną klasyfikację hello jest pięć razy bardziej kosztowne instytucji finansowej toohello: Jeśli hello model przewiduje niskie ryzyko kredytowe osoby, która jest rzeczywiście ryzyko kredytowe wysokiej.</span><span class="sxs-lookup"><span data-stu-id="56725-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="56725-129">Dlatego chcemy tootrain nasz model tak, aby koszt hello tego typu ostatnie błędu klasyfikacji pięć razy wyższa niż misclassifying hello inny sposób.</span><span class="sxs-lookup"><span data-stu-id="56725-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="56725-130">Jeden prosty sposób toodo to podczas uczenia modelu hello w naszym doświadczeniu jest duplikując (pięć razy) zapisów reprezentujących ktoś z ryzyko kredytowe wysoki.</span><span class="sxs-lookup"><span data-stu-id="56725-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="56725-131">Następnie jeśli hello model klasyfikuje ktoś jako niskie ryzyko kredytowe, gdy są faktycznie wysokiego ryzyka, hello modelu nie tego samego błędu klasyfikacji pięć razy raz dla każdego duplikatu.</span><span class="sxs-lookup"><span data-stu-id="56725-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="56725-132">To spowoduje zwiększenie kosztów hello tego błędu w wynikach szkolenia hello.</span><span class="sxs-lookup"><span data-stu-id="56725-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="56725-133">Konwertuj hello formacie zestawu danych</span><span class="sxs-lookup"><span data-stu-id="56725-133">Convert hello dataset format</span></span>
<span data-ttu-id="56725-134">Witaj oryginalnego zestawu danych w formacie oddzielone puste.</span><span class="sxs-lookup"><span data-stu-id="56725-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="56725-135">Usługa Machine Learning Studio działa lepiej z pliku wartości rozdzielanych przecinkami (CSV), więc będzie nie możemy przekonwertować zestawu danych hello zastępując spacje przecinkami.</span><span class="sxs-lookup"><span data-stu-id="56725-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="56725-136">Istnieje wiele sposobów tooconvert tych danych.</span><span class="sxs-lookup"><span data-stu-id="56725-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="56725-137">Jednym ze sposobów jest za pomocą następującego polecenia programu Windows PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="56725-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="56725-138">Innym sposobem jest za pomocą polecenia mniejszyć Unix hello:</span><span class="sxs-lookup"><span data-stu-id="56725-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="56725-139">W obu przypadkach utworzono wersję przecinkami hello danych w pliku o nazwie **german.csv** który możemy użyć w naszym doświadczeniu.</span><span class="sxs-lookup"><span data-stu-id="56725-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="56725-140">Przekaż hello dataset tooMachine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="56725-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="56725-141">Po hello danych został przekonwertowany tooCSV format, potrzebujemy tooupload go do usługi Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="56725-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="56725-142">Strona główna usługi Machine Learning Studio Otwórz hello ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="56725-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="56725-143">Kliknij hello menu ![Menu][1] w hello lewym górnym rogu okna hello, kliknij przycisk **usługi Azure Machine Learning**, wybierz pozycję **Studio**i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="56725-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="56725-144">Kliknij przycisk **+ nowy** u dołu okna hello hello.</span><span class="sxs-lookup"><span data-stu-id="56725-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="56725-145">Wybierz **zestawu danych**.</span><span class="sxs-lookup"><span data-stu-id="56725-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="56725-146">Wybierz **z pliku lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="56725-146">Select **FROM LOCAL FILE**.</span></span>

    ![Dodaj zestaw danych z pliku lokalnego][2]

6. <span data-ttu-id="56725-148">W hello **przekazać nowy zestaw danych** okna dialogowego, kliknij przycisk **Przeglądaj** i Znajdź hello **german.csv** utworzony plik.</span><span class="sxs-lookup"><span data-stu-id="56725-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="56725-149">Wprowadź nazwę dla zestawu danych hello.</span><span class="sxs-lookup"><span data-stu-id="56725-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="56725-150">W ramach tego przewodnika wywołać ją "Dane karty kredytowej niemiecki UCI".</span><span class="sxs-lookup"><span data-stu-id="56725-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="56725-151">Dla typu danych, wybierz **ogólnego pliku CSV bez nagłówka (. nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="56725-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="56725-152">Dodaj opis, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="56725-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="56725-153">Kliknij przycisk hello **OK** znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="56725-153">Click hello **OK** check mark.</span></span>  

    ![Przekaż hello zestawu danych][3]

<span data-ttu-id="56725-155">Do modułu zestawu danych, które pomagają w eksperymencie operacji przekazywania danych hello.</span><span class="sxs-lookup"><span data-stu-id="56725-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="56725-156">Można zarządzać zestawów danych, klikając hello przesłaniu tooStudio **zestawów danych** toohello kartę pozostałych hello Studio okna.</span><span class="sxs-lookup"><span data-stu-id="56725-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Zarządzanie zbiory danych][4]

<span data-ttu-id="56725-158">Aby uzyskać więcej informacji o importowaniu inne typy danych do eksperymentu, zobacz [importowanie danych szkoleniowych w usłudze Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="56725-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="56725-159">**Następnie: [Tworzenie nowego eksperymentu](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="56725-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
