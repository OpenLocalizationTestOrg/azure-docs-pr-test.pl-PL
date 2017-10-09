---
title: "aaaCopy machine learning przykład eksperymenty - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak uczenia maszynowego przykład toouse experiments toocreate nowych eksperymentów z Cortana Intelligence Gallery i Microsoft Azure Machine Learning."
keywords: machine learning examples, sample experiment, machine learning sample
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 555f05cf9af2040d1703707f7583396d5da9f156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-example-experiments-toocreate-new-machine-learning-experiments"></a><span data-ttu-id="09173-104">Skopiuj przykładowy eksperymenty toocreate nowe uczenia maszynowego eksperymenty</span><span class="sxs-lookup"><span data-stu-id="09173-104">Copy example experiments toocreate new machine learning experiments</span></span>
<span data-ttu-id="09173-105">Dowiedz się, jak toostart przykładu eksperymentów z [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) zamiast tworzenia uczeniem maszynowym od podstaw.</span><span class="sxs-lookup"><span data-stu-id="09173-105">Learn how toostart with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="09173-106">Możesz użyć toobuild przykłady hello własne machine learning rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="09173-106">You can use hello examples toobuild your own machine learning solution.</span></span>

<span data-ttu-id="09173-107">Galeria Hello ma przykład eksperymenty hello zespołu Microsoft Azure Machine Learning, jak również przykłady współużytkowane przez hello społeczności uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="09173-107">hello gallery has example experiments by hello Microsoft Azure Machine Learning team as well as examples shared by hello Machine Learning community.</span></span> <span data-ttu-id="09173-108">Można również zadawać pytania i publikować komentarze dotyczące eksperymentów.</span><span class="sxs-lookup"><span data-stu-id="09173-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="09173-109">toosee jak toouse hello galerii, obejrzyj hello 3-minutowy film wideo [skopiować inne osoby pracy toodo danych nauki](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) z serii hello [nauki danych dla początkujących](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="09173-109">toosee how toouse hello gallery, watch hello 3-minute video [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from hello series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-toocopy-in-cortana-intelligence-gallery"></a><span data-ttu-id="09173-110">Znajdź toocopy eksperymentu w Cortana Intelligence Gallery</span><span class="sxs-lookup"><span data-stu-id="09173-110">Find an experiment toocopy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="09173-111">toosee jakie eksperymenty są dostępne, przejdź do pozycji toohello [galerii](https://gallery.cortanaintelligence.com/) i kliknij przycisk **eksperymenty** u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="09173-111">toosee what experiments are available, go toohello [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at hello top of hello page.</span></span>

### <a name="find-hello-newest-or-most-popular-experiments"></a><span data-ttu-id="09173-112">Znajdź najnowsze lub najpopularniejszych eksperymenty hello</span><span class="sxs-lookup"><span data-stu-id="09173-112">Find hello newest or most popular experiments</span></span>
<span data-ttu-id="09173-113">Na tej stronie można zobaczyć **ostatnio dodane** eksperymenty lub przewiń w dół toolook w **co to jest popularnych** lub hello najnowszych **popularnych Microsoft experiments**.</span><span class="sxs-lookup"><span data-stu-id="09173-113">On this page, you can see **Recently added** experiments, or scroll down toolook at **What's popular** or hello latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="09173-114">Wyszukiwanie eksperymentu spełniającego określone wymagania</span><span class="sxs-lookup"><span data-stu-id="09173-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="09173-115">experiments toobrowse wszystkie:</span><span class="sxs-lookup"><span data-stu-id="09173-115">toobrowse all experiments:</span></span>

1. <span data-ttu-id="09173-116">Kliknij przycisk **Przeglądaj wszystkie** u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="09173-116">Click **Browse all** at hello top of hello page.</span></span>
2. <span data-ttu-id="09173-117">Na powitania po lewej stronie w obszarze **Uściślij według** w hello **kategorii** zaznacz **eksperymentu** toosee hello wszystkie eksperymenty w hello galerii.</span><span class="sxs-lookup"><span data-stu-id="09173-117">On hello left-hand side, under **Refine by** in hello **Categories** section, select **Experiment** toosee all hello experiments in hello Gallery.</span></span>
3. <span data-ttu-id="09173-118">Eksperymenty spełniające wymagania możesz znaleźć na kilka różnych sposobów:</span><span class="sxs-lookup"><span data-stu-id="09173-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="09173-119">**Wybierz Filtry po lewej stronie powitania.**</span><span class="sxs-lookup"><span data-stu-id="09173-119">**Select filters on hello left.**</span></span> <span data-ttu-id="09173-120">Na przykład eksperymenty toobrowse korzystających z algorytmu wykrywania anomalii oparte na PCA: Z **eksperymentu** wybranego w obszarze **kategorii**, kliknij przycisk **Pokaż wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="09173-120">For example, toobrowse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="09173-121">Następnie w obszarze **Algorithms Used** (Używane algorytmy) wybierz opcję **PCA-Based Anomaly Detection** (Wykrywanie anomalii oparte na PCA).</span><span class="sxs-lookup"><span data-stu-id="09173-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="09173-122">
     ![Wybierz filtry](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="09173-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="09173-123">**Użyj pola wyszukiwania hello.**</span><span class="sxs-lookup"><span data-stu-id="09173-123">**Use hello search box.**</span></span> <span data-ttu-id="09173-124">Na przykład toofind eksperymenty zamieszczone przez firmę Microsoft związane z rozpoznawania toodigit, które używają algorytmu maszyny wektor dwie klasy pomocy technicznej, wprowadź "rozpoznawaniem cyfr" hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="09173-124">For example, toofind experiments contributed by Microsoft related toodigit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in hello search box.</span></span> <span data-ttu-id="09173-125">Następnie wybierz hello filtry **eksperymentu**, **tylko zawartość firmy Microsoft**, i **maszyny wektorowa obsługa Two-Class**:</span><span class="sxs-lookup"><span data-stu-id="09173-125">Then, select hello filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="09173-126">
     ![Użyj pola wyszukiwania hello](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="09173-126">
![Use hello search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="09173-127">Kliknij eksperyment toolearn więcej informacji na ten temat.</span><span class="sxs-lookup"><span data-stu-id="09173-127">Click an experiment toolearn more about it.</span></span>
5. <span data-ttu-id="09173-128">toorun i/lub zmodyfikować eksperyment hello, kliknij przycisk **Otwórz w Studio** na stronie powitania eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="09173-128">toorun and/or modify hello experiment, click **Open in Studio** on hello experiment's page.</span></span> <br></br>

    ![Przykładowy eksperyment](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="09173-130">Po otwarciu eksperymentu w usłudze Machine Learning Studio powitania po raz pierwszy, możesz Wypróbuj bezpłatnie lub kupić subskrypcję Azure.</span><span class="sxs-lookup"><span data-stu-id="09173-130">When you open an experiment in Machine Learning Studio for hello first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="09173-131">Dowiedz się więcej o hello Machine Learning Studio bezpłatnej wersji próbnej lub płatnej usługi</span><span class="sxs-lookup"><span data-stu-id="09173-131">Learn about hello Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="09173-132">Tworzenie nowego eksperymentu przy użyciu przykładu jako szablonu</span><span class="sxs-lookup"><span data-stu-id="09173-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="09173-133">Nowy eksperyment można również utworzyć w usłudze Machine Learning Studio, używając przykładu z galerii jako szablonu.</span><span class="sxs-lookup"><span data-stu-id="09173-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="09173-134">Zaloguj się przy użyciu programu toohello poświadczeń konta Microsoft [Studio](https://studio.azureml.net), a następnie kliknij przycisk **nowy** toocreate eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="09173-134">Sign in with your Microsoft account credentials toohello [Studio](https://studio.azureml.net), and then click **New** toocreate an experiment.</span></span>
2. <span data-ttu-id="09173-135">Przeglądanie zawartości przykład hello i kliknij jeden.</span><span class="sxs-lookup"><span data-stu-id="09173-135">Browse through hello example content and click one.</span></span>

<span data-ttu-id="09173-136">W obszarze roboczym Machine Learning Studio za pomocą hello przykład eksperymentu jako szablonu zostanie utworzony nowy eksperyment.</span><span class="sxs-lookup"><span data-stu-id="09173-136">A new experiment is created in your Machine Learning Studio workspace using hello example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09173-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09173-137">Next steps</span></span>
* [<span data-ttu-id="09173-138">Importowanie danych z różnych źródeł</span><span class="sxs-lookup"><span data-stu-id="09173-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="09173-139">Samouczek Szybki Start dla języka hello R w uczeniu maszynowym</span><span class="sxs-lookup"><span data-stu-id="09173-139">Quickstart tutorial for hello R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="09173-140">Wdrażanie usługi sieci Web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="09173-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
