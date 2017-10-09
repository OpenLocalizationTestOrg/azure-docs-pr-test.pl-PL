---
title: "aaaHDInsight Hadoop nauki wskazówki dotyczące danych na platformie Azure przy użyciu Hive | Dokumentacja firmy Microsoft"
description: "Przykłady hello zespołu w procesie nauki danych, których przeprowadzenie hello w systemie gałęzi analizy predykcyjnej toodo Azure HDInsight Hadoop."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="5eb3b-103">Hive HDInsight Hadoop nauki wskazówki dotyczące danych przy użyciu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5eb3b-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="5eb3b-104">Te wskazówki za pomocą Hive HDInsight Hadoop klastra toodo analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="5eb3b-105">One wykonaj kroki hello opisane w hello proces nauki danych zespołu.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="5eb3b-106">Omówienie hello zespołu w procesie nauki danych, zobacz [proces nauki danych](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5eb3b-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="5eb3b-107">Aby tooAzure wprowadzenie HDInsight, zobacz [tooAzure wprowadzenie HDInsight, hello stosu technologii Hadoop i klastrów platformy Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5eb3b-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="5eb3b-108">Wskazówki dotyczące nauki dodatkowych danych, wykonujących hello proces nauki danych Team są pogrupowane według hello **platformy** obsługującego:</span><span class="sxs-lookup"><span data-stu-id="5eb3b-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="5eb3b-109">Przewidywanie porady taksówki przy użyciu Hive z HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5eb3b-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="5eb3b-110">Witaj [klastrów HDInsight Hadoop użyj](machine-learning-data-science-process-hive-walkthrough.md) wskazówki korzysta z nowego Jorku taksówkach toopredict danych:</span><span class="sxs-lookup"><span data-stu-id="5eb3b-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="5eb3b-111">Określa, czy ma być stosowany porady</span><span class="sxs-lookup"><span data-stu-id="5eb3b-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="5eb3b-112">dystrybucji Hello Porada kwot</span><span class="sxs-lookup"><span data-stu-id="5eb3b-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="5eb3b-113">Scenariusz Hello jest implementowane przy użyciu programu Hive z [klastra usługi Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5eb3b-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="5eb3b-114">Dowiesz się, jak toostore, Eksploruj, funkcję odtwarzania dane z dostępnych publicznie podróży taksówki NYC i taryfy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="5eb3b-115">Również użyć usługi Azure Machine Learning toobuild i wdrażanie modeli hello.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="5eb3b-116">Przewidywanie kliknięć anonsu przy użyciu Hive z HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5eb3b-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="5eb3b-117">Witaj [Użyj Azure Hadoop w usłudze Hdinsight w zestawie danych 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) wskazówki używa publicznie dostępnych [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) kliknij toopredict zestawu danych, czy etykietki otrzymuje i hello zakresu kwoty oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="5eb3b-118">Scenariusz Hello jest implementowane przy użyciu programu Hive z [klastra usługi Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Eksploruj, funkcję odtwarzania i w dół przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="5eb3b-119">Używa usługi Azure Machine Learning toobuild, pociągu i score model klasyfikacji binarnej przewidywania, czy użytkownik kliknie anonsu.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="5eb3b-120">wskazówki Hello stwierdza, przedstawiający sposób toopublish te modele jako usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5eb3b-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5eb3b-121">Next steps</span></span>

<span data-ttu-id="5eb3b-122">Omówienie hello najważniejsze składniki wchodzące w skład hello zespołu w procesie nauki danych, zobacz [Omówienie procesu nauki danych zespołu](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5eb3b-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="5eb3b-123">Omówienie cyklu życia procesu nauki danych zespołu hello służy toostructure projektów analizy danych, zobacz [cyklu życia procesu nauki danych zespołu](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="5eb3b-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="5eb3b-124">cykl życia Hello opisano kroki hello, z toofinish start, która projektów wykonaj zazwyczaj, gdy są one wykonywane.</span><span class="sxs-lookup"><span data-stu-id="5eb3b-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

