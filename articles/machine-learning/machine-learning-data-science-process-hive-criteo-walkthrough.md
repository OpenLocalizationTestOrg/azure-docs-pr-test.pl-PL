---
title: "Proces nauki danych zespołu w akcji — przy użyciu klastra usługi Azure HDInsight Hadoop w zestawie danych 1 TB | Dokumentacja firmy Microsoft"
description: "Scenariusz end-to-end wykorzystujących klastra usługi Hadoop w usłudze HDInsight do tworzenia i wdrażania modelu przy użyciu dużych publicznie dostępnych dataset (1 TB) przy użyciu procesu nauki danych Team"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 8e6143bca819c9a0484221f8b4feb319aaaa73f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="3c2d2-103">Proces nauki danych zespołu w akcji — przy użyciu klastra usługi Azure HDInsight Hadoop na 1 TB zestawu danych</span><span class="sxs-lookup"><span data-stu-id="3c2d2-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="3c2d2-104">W tym przewodniku zostaje przedstawiony przy użyciu procesu nauki danych zespołu w scenariuszu end-to-end z [klastra usługi Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) do przechowywania, Eksploruj funkcji odtwarzania i przykładowych danych z jedną z dostępnych publicznie w dół [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="3c2d2-105">Używamy uczenie maszynowe Azure do tworzenia modelu klasyfikacji binarnej na tych danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-105">We use Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="3c2d2-106">Możemy również pokazują, jak do publikowania jednego z tych modeli jako usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-106">We also show how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="3c2d2-107">Istnieje również możliwość Notes IPython służy do wykonywania zadań przedstawionych w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="3c2d2-108">Aby skorzystać z tej metody użytkownicy powinni skontaktować [wskazówki Criteo za pomocą połączenia ODBC programu Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tematu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="3c2d2-109"><a name="dataset"></a>Opis elementu Criteo Dataset</span><span class="sxs-lookup"><span data-stu-id="3c2d2-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="3c2d2-110">Criteo, danych to około 370 GB plików TSV gzip skompresowane (~1.3TB nieskompresowane), zestawu danych prognozowania kliknij składającej się z więcej niż 4.3 miliardy rekordów.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="3c2d2-111">Jest ona pobierana z 24 dni kliknij danych udostępnionych przez [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="3c2d2-112">Dla wygody analityków danych Firma Microsoft ma rozpakowane danych dostępnych do nas eksperymentować.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span></span>

<span data-ttu-id="3c2d2-113">Każdy rekord w tym elemencie dataset zawiera kolumny 40:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="3c2d2-114">Pierwsza kolumna jest kolumną etykietę wskazującą, czy użytkownik kliknie **Dodaj** (wartość 1) lub w ogóle nie kliknij jedną (wartość 0)</span><span class="sxs-lookup"><span data-stu-id="3c2d2-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="3c2d2-115">następnie 13 kolumny są numeryczną, i</span><span class="sxs-lookup"><span data-stu-id="3c2d2-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="3c2d2-116">ostatni 26 są podzielone na kategorie kolumn</span><span class="sxs-lookup"><span data-stu-id="3c2d2-116">last 26 are categorical columns</span></span>

<span data-ttu-id="3c2d2-117">Kolumny są anonimowe i szereg wyliczany nazwy: "Col1" (dla kolumny etykiety) do "Col40" (dla ostatniej kolumny podzielone na kategorie).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="3c2d2-118">Poniżej przedstawiono fragment 20 pierwszych kolumn dwóch uwag (wiersze) z tego zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="3c2d2-119">W tym zestawie danych istnieją brakujące wartości w kolumnach liczbowych i podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="3c2d2-120">Przedstawione prostą metodę obsługi brakujące wartości.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-120">We describe a simple method for handling the missing values.</span></span> <span data-ttu-id="3c2d2-121">Dodatkowe szczegóły danych są zbadane, gdy będziemy przechowywać w tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-121">Additional details of the data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="3c2d2-122">**Definicja:** *szybkość przeglądowego (kont.):* procent kliknięć w danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="3c2d2-123">W tym zestawie danych Criteo Ewidencyjne to około 3.3% lub 0.033.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="3c2d2-124"><a name="mltasks"></a>Przykłady prognozowania zadań</span><span class="sxs-lookup"><span data-stu-id="3c2d2-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="3c2d2-125">Dwa przykładowe prognozowania problemy zostały rozwiązane w tym przewodniku:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="3c2d2-126">**Klasyfikacji binarnej**: wskazuje, czy użytkownik kliknął add:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="3c2d2-127">Klasa 0: Nie kliknij</span><span class="sxs-lookup"><span data-stu-id="3c2d2-127">Class 0: No Click</span></span>
   * <span data-ttu-id="3c2d2-128">Klasa 1: kliknij przycisk</span><span class="sxs-lookup"><span data-stu-id="3c2d2-128">Class 1: Click</span></span>
2. <span data-ttu-id="3c2d2-129">**Regresja**: prognozuje prawdopodobieństwo kliknij ad z funkcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <span data-ttu-id="3c2d2-130"><a name="setup"></a>Ustaw się HDInsight klastra usługi Hadoop do analizy danych</span><span class="sxs-lookup"><span data-stu-id="3c2d2-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="3c2d2-131">**Uwaga:** jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="3c2d2-132">Konfigurowanie środowiska Azure nauki danych do tworzenia rozwiązań analizy predykcyjnej z klastrami usługi HDInsight w trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="3c2d2-133">[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md): to konto magazynu jest używany do przechowywania danych w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="3c2d2-134">Dane używane w klastrach HDInsight są przechowywane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="3c2d2-135">[Dostosowywanie Hadoop w usłudze Azure Hdinsight do analizy danych](machine-learning-data-science-customize-hadoop-cluster.md): ten krok umożliwia utworzenie klastra usługi Azure HDInsight Hadoop z 64-bitowych Anaconda Python 2.7 zainstalowane we wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="3c2d2-136">Istnieją dwie ważne czynności (opisanej w tym temacie) do wykonania w przypadku dostosowywania klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="3c2d2-137">Należy połączyć utworzony w kroku 1 z klastrem usługi HDInsight, po utworzeniu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="3c2d2-138">To konto magazynu jest używane do uzyskiwania dostępu do danych, które mogą być przetwarzane w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="3c2d2-139">Należy włączyć dostęp zdalny do węzła głównego klastra po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="3c2d2-140">Pamiętaj poświadczenia dostępu zdalnego określone w tym miejscu (inny niż określone dla klastra podczas jego tworzenia): potrzebne do wykonania poniższych procedur.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="3c2d2-141">[Utwórz obszar roboczy usługi Azure ML](machine-learning-create-workspace.md): to Azure Machine Learning obszaru roboczego jest używany do tworzenia modeli uczenia maszyny po Eksploracja danych początkowych i w dół próbkowania w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <span data-ttu-id="3c2d2-142"><a name="getdata"></a>Pobierz i wykorzystują dane ze źródła publiczny</span><span class="sxs-lookup"><span data-stu-id="3c2d2-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="3c2d2-143">[Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) zestawu danych jest możliwy klikając łącze, akceptowania warunków użytkowania i podanie nazwy.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="3c2d2-144">Migawki to wygląda jak jest następujący:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-144">A snapshot of what this looks like is shown here:</span></span>

![Zaakceptuj postanowienia Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="3c2d2-146">Kliknij przycisk **Kontynuuj, aby pobrać** Aby dowiedzieć się więcej o zestawie danych i ich dostępność.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="3c2d2-147">Dane znajdują się w folderze publicznym [magazynu obiektów blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) lokalizacji: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-147">The data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="3c2d2-148">"wasb" odwołuje się do lokalizacji magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="3c2d2-149">Dane w tym magazynie obiektów blob publicznego składa się z trzech podfoldery rozpakowane danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="3c2d2-150">Podfolder *raw/licznik/* zawiera pierwszy 21 dni dane — od dnia\_00 do dnia\_20</span><span class="sxs-lookup"><span data-stu-id="3c2d2-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="3c2d2-151">Podfolder *raw/train/* składa się z jednego dnia danych, dzień\_21</span><span class="sxs-lookup"><span data-stu-id="3c2d2-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="3c2d2-152">Podfolder *pierwotnych i testowanie/* składa się z dwóch dni danych, dzień\_22 i dzień\_23</span><span class="sxs-lookup"><span data-stu-id="3c2d2-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="3c2d2-153">Dla osób, które chcesz rozpocząć od danych pierwotnych gzip, są one również dostępne w folderze głównym *raw /* jako day_NN.gz, gdzie NN przechodzi od 00 do 23.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="3c2d2-154">Informacje o innym podejściu do uzyskania dostępu, zapoznaj się i model te dane, które nie wymaga żadnych lokalne pliki do pobrania jest szczegółowo w dalszej części tego przewodnika po utworzymy tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="3c2d2-155"><a name="login"></a>Zaloguj się do headnode klastra</span><span class="sxs-lookup"><span data-stu-id="3c2d2-155"><a name="login"></a>Log in to the cluster headnode</span></span>
<span data-ttu-id="3c2d2-156">Aby zalogować się do headnode klastra, należy użyć [portalu Azure](https://ms.portal.azure.com) można znaleźć klastra.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="3c2d2-157">Kliknij ikonę Słoń HDInsight po lewej stronie, a następnie kliknij dwukrotnie nazwę klastra.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="3c2d2-158">Przejdź do **konfiguracji** , kliknij dwukrotnie ikonę POŁĄCZ na dole strony, a następnie wprowadź swoje poświadczenia dostępu zdalnego, po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="3c2d2-159">Zostanie wyświetlone headnode klastra.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="3c2d2-160">Poniżej przedstawiono typowe pierwszego logowania do headnode klastra wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![Zaloguj się do klastra](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="3c2d2-162">Po lewej stronie widzimy "Hadoop wiersza polecenia", czyli naszych najważniejszą metodą roboczą dla Eksploracja danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="3c2d2-163">Przedstawiono również dwa przydatne adresy URL - "Hadoop Yarn stanu" i "Hadoop nazwa węzła".</span><span class="sxs-lookup"><span data-stu-id="3c2d2-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="3c2d2-164">Adres URL stanu yarn przedstawia postęp zadania oraz adres URL węzła nazwa zwraca szczegółowe informacje dotyczące konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="3c2d2-165">Teraz możemy są skonfigurowane i gotowe do rozpoczęcia pierwszej części tego przewodnika: Eksploracja danych przy użyciu Hive i przygotowanie danych do usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="3c2d2-166"><a name="hive-db-tables"></a>Utwórz gałąź bazy danych i tabel</span><span class="sxs-lookup"><span data-stu-id="3c2d2-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="3c2d2-167">Aby utworzyć tabele programu Hive dla naszych Criteo zestawu danych, otwórz ***wiersza polecenia platformy Hadoop*** na pulpicie węzła głównego i wprowadź katalog Hive przez wprowadzenie polecenia</span><span class="sxs-lookup"><span data-stu-id="3c2d2-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="3c2d2-168">Uruchom wszystkie polecenia gałęzi w tym przewodniku z gałęzi bin / directory wiersza.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="3c2d2-169">Odpowiada on za wszelkie problemy ścieżki automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="3c2d2-170">Używane pojęcia "Hive katalogu wiersza", "bin gałęzi / directory wiersza" i "wiersza polecenia usługi Hadoop" zamiennie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="3c2d2-171">Aby wykonać wszelkie zapytania Hive, jeden zawsze Użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="3c2d2-172">Po wyświetleniu REPL gałąź z "hive >"Zaloguj się, po prostu wyciąć i wkleić ją wykonać kwerendę.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="3c2d2-173">Poniższy kod tworzy bazę danych "criteo", a następnie generuje 4 tabel:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="3c2d2-174">*tabeli do wygenerowania liczby* oparty na dzień dni\_00 do dnia\_20,</span><span class="sxs-lookup"><span data-stu-id="3c2d2-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="3c2d2-175">*tabeli jako zestawu danych train* oparty na dzień\_21, i</span><span class="sxs-lookup"><span data-stu-id="3c2d2-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="3c2d2-176">dwa *tabel do użycia jako zestawy danych test* oparty na dzień\_22 i dzień\_23 odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="3c2d2-177">Naszego zestawu danych testowych możemy podzielić na dwie różne tabele, ponieważ jeden z dni jest dniem wolnym od pracy i chcemy ustalić, można wykryć modelu różnice między dni wolnych i nie święta od szybkości przeglądowego.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span></span>

<span data-ttu-id="3c2d2-178">Skrypt [& #95 przykładowe; hive &#95; Utwórz &#95; criteo &#95; &#95; bazy danych i &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) są wyświetlane tutaj dla wygody:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="3c2d2-179">Firma Microsoft należy zauważyć, że te tabele zewnętrzne jak możemy wystarczy wskazać do lokalizacji magazynu obiektów Blob Azure (wasb).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="3c2d2-180">**Istnieją dwa sposoby wykonania zapytania ANY Hive teraz wspomina.**</span><span class="sxs-lookup"><span data-stu-id="3c2d2-180">**There are two ways to execute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="3c2d2-181">**Przy użyciu wiersza polecenia REPL Hive**: pierwsza to wydać polecenie "hive" i skopiuj i Wklej zapytanie z wiersza polecenia REPL Hive.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="3c2d2-182">Aby to zrobić, należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-182">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="3c2d2-183">Teraz w wierszu polecenia REPL, wycinanie i wklejanie zapytanie go uruchomi.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-183">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="3c2d2-184">**Zapisywanie zapytań do pliku i wykonywania polecenia**: drugi to można zapisać zapytania do pliku .hql ([& #95 przykładowe; hive &#95; Utwórz &#95; criteo &#95; &#95; bazy danych i &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) i następnie należy wydać następujące polecenie do wykonania zapytania:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="3c2d2-185">Potwierdź utworzenie bazy danych i tabeli</span><span class="sxs-lookup"><span data-stu-id="3c2d2-185">Confirm database and table creation</span></span>
<span data-ttu-id="3c2d2-186">Następnie potwierdzamy utworzenie bazy danych przy użyciu następującego polecenia z gałęzi bin / directory wiersza:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="3c2d2-187">Dzięki temu:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="3c2d2-188">Jest to potwierdzenie utworzenia nowej bazy danych "criteo".</span><span class="sxs-lookup"><span data-stu-id="3c2d2-188">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="3c2d2-189">Aby wyświetlić tabele utworzyliśmy, możemy po prostu należy wydać polecenie tutaj z gałęzi bin / directory wiersza:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="3c2d2-190">Następnie widzimy następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-190">We then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="3c2d2-191"><a name="exploration"></a>Eksploracja danych w gałęzi</span><span class="sxs-lookup"><span data-stu-id="3c2d2-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="3c2d2-192">Firma Microsoft są teraz gotowe do wykonania niektórych Eksploracja danych podstawowych, w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-192">Now we are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="3c2d2-193">Możemy rozpocząć liczbą przykładów w pociągu i testowanie tabel danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-193">We begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="3c2d2-194">Liczba train przykłady</span><span class="sxs-lookup"><span data-stu-id="3c2d2-194">Number of train examples</span></span>
<span data-ttu-id="3c2d2-195">Zawartość [& #95 przykładowe; hive &#95; liczba &#95; train &#95; tabeli &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) są wyświetlane tutaj:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="3c2d2-196">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="3c2d2-197">Alternatywnie jedną może również wydać następujące polecenie z bin gałęzi / directory wiersza:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="3c2d2-198">Wiele przykładów testu w dwóch zestawach testu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-198">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="3c2d2-199">Mamy teraz określić liczbę przykłady w dwóch zestawach testu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-199">We now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="3c2d2-200">Zawartość [& #95 przykładowe hive &#95; liczba &#95; criteo &#95; test &#95; dzień &#95; 22 &#95; tabeli &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) są tutaj:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="3c2d2-201">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="3c2d2-202">W zwykły sposób, firma Microsoft może także wywołać skrypt z gałęzi bin / directory monit przez wydanie polecenia:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="3c2d2-203">Na koniec omówione liczba przykłady testu w zestawu danych testowych na podstawie dnia\_23.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="3c2d2-204">Polecenia w tym celu jest podobny do przedstawionego właśnie (dotyczą [& #95 przykładowe; hive &#95; liczba &#95; criteo &#95; test &#95; dzień &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="3c2d2-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="3c2d2-205">Dzięki temu:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="3c2d2-206">Dystrybucji etykiety w zestawie danych pociągu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-206">Label distribution in the train dataset</span></span>
<span data-ttu-id="3c2d2-207">Rozkład etykiety w zestawie danych pociągu jest.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-207">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="3c2d2-208">Aby to sprawdzić, zawartość zostanie przedstawiony [& #95 przykładowe; hive &#95; criteo &#95; & #95 etykiety; #95 & dystrybucji; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="3c2d2-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="3c2d2-209">Daje to dystrybucji etykiety:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-209">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="3c2d2-210">Należy pamiętać, że odsetek dodatnią etykiety około 3.3% (zgodne z oryginalnego zestawu danych).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="3c2d2-211">Dystrybucje Histogram niektóre liczbowe zmiennych w zestawie danych pociągu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-211">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="3c2d2-212">Możemy użyć natywnego gałęzi "histogram\_liczbowa" funkcji, aby dowiedzieć się, jak wygląda rozkład zmiennych liczbowych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="3c2d2-213">Poniżej przedstawiono zawartość [& #95 przykładowe; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="3c2d2-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="3c2d2-214">Daje to następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-214">This yields the following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="3c2d2-215">PENETRACJA widok - rozłożenie kombinacja w gałęzi służy do generowania danych wyjściowych przypominającego SQL zamiast standardowego listy.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="3c2d2-216">Należy pamiętać, że w tej tabeli, pierwsza kolumna odpowiada Centrum bin, a drugi częstotliwości bin.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="3c2d2-217">Przybliżony percentylu niektóre liczbowe zmiennych w zestawie danych pociągu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-217">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="3c2d2-218">Płynących ze zmiennymi liczbowych jest również obliczenia przybliżonej percentylu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-218">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="3c2d2-219">Gałąź do natywnego "percentyl\_przybliżone" robi to firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="3c2d2-220">Zawartość [& #95 przykładowe; hive &#95; criteo &#95; przybliżonej &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) są:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="3c2d2-221">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="3c2d2-222">Oznacz firma Microsoft, że dystrybucja percentylu jest blisko związane dystrybucji histogram żadnych liczbowa zmiennej zwykle.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="3c2d2-223">Znajdź liczbę unikatowych wartości dla niektórych podzielone na kategorie kolumn w zestawie danych pociągu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-223">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="3c2d2-224">Kontynuowanie Eksploracja danych, teraz okaże się, dla niektórych kolumn podzielone na kategorie, liczbę unikatowych wartości, które podejmują.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="3c2d2-225">Aby to zrobić, zawartość zostanie przedstawiony [& #95 przykładowe; hive &#95; criteo &#95; unikatowy &#95; wartości &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="3c2d2-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="3c2d2-226">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="3c2d2-227">Firma Microsoft Pamiętaj, że Col15 ma unikatowe wartości 19M!</span><span class="sxs-lookup"><span data-stu-id="3c2d2-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="3c2d2-228">Przy użyciu prostego technik, takich jak "hot jeden kodowanie" do kodowania tych wymiarów wysokiej zmienne podzielone na kategorie jest praktyce.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="3c2d2-229">W szczególności firma Microsoft wyjaśnić i Wykaż metoda zaawansowanych, niezawodnych, zwana [uczenia z liczby](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) dla wydajne rozwiązania problemu ten problem.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="3c2d2-230">Ta podsekcja możemy zakończyć analizując liczbę unikatowych wartości dla niektórych innych kategorii kolumn oraz.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="3c2d2-231">Zawartość [& #95 przykładowe; hive &#95; criteo &#95; unikatowy &#95; & #95 wartości wielu &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) są:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="3c2d2-232">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="3c2d2-233">Ponownie widzimy, z wyjątkiem Col20, wszystkie pozostałe kolumny ma wiele unikatowych wartości.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-233">Again we see that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="3c2d2-234">Wystąpienie wspólnej liczby par podzielone na kategorie zmiennych w zestawie danych pociągu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-234">Co-occurrence counts of pairs of categorical variables in the train dataset</span></span>

<span data-ttu-id="3c2d2-235">Liczby wystąpień wspólnej par podzielone na kategorie zmiennych jest również przydatne.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-235">The co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="3c2d2-236">To można określić, używając kodu w [& #95 przykładowe; hive &#95; criteo &#95; sparowanego &#95; podzielone na kategorie &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="3c2d2-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="3c2d2-237">Firma Microsoft odwrotna kolejność zliczeń według ich wystąpienia i przyjrzyj się górnej 15 w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="3c2d2-238">Dzięki temu nam:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="3c2d2-239"><a name="downsample"></a>Dół przykładowych zestawów danych dla usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3c2d2-239"><a name="downsample"></a> Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="3c2d2-240">Posiadanie przedstawione zestawy danych i sprawdzono, firma Microsoft może jak tego typu eksploracji dla zmiennych (takie jak kombinacje), możemy teraz dół przykładowych zestawów danych, aby firma Microsoft można tworzyć modele w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="3c2d2-241">Odwołania, który jest problem możemy skupić się na: podany zestaw atrybutów przykład (funkcja wartości z Col2 - Col40), możemy przewidzieć Jeśli Col1 jest 0 (nie kliknij) lub 1 (kliknij).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="3c2d2-242">W dół przykładowe naszych pociągu i przetestować zestawów danych oryginalny rozmiar % 1, używamy funkcji macierzystej RAND() gałęzi.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="3c2d2-243">Skrypt dalej [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) robi to train zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="3c2d2-244">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="3c2d2-245">Skrypt [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; test &#95; dzień &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) zrobi to za dane testowe dzień\_22:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="3c2d2-246">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="3c2d2-247">Na koniec skryptu [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; test &#95; dzień &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) zrobi to za dane testowe dzień\_23:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="3c2d2-248">Daje to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="3c2d2-249">O tym możemy przystąpić do naszej dół train próbki i testów zestawów danych do tworzenia modeli w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="3c2d2-250">Brak ważnych finalnych przed możemy przejść do usługi Azure Machine Learning, czyli dotyczy tabeli liczby.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span></span> <span data-ttu-id="3c2d2-251">W następnej sekcji podrzędne omówiono to szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-251">In the next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="3c2d2-252"><a name="count"></a>Krótkie omówienie w tabeli liczby</span><span class="sxs-lookup"><span data-stu-id="3c2d2-252"><a name="count"></a> A brief discussion on the count table</span></span>
<span data-ttu-id="3c2d2-253">Kilka kategorii zmienne widzieliśmy, mają bardzo duże wymiary.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="3c2d2-254">W naszym przewodniku możemy przedstawić zaawansowane techniki, zwanej [uczenia z liczby](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) do kodowania tych zmiennych w wydajny i niezawodny sposób.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="3c2d2-255">Więcej informacji na temat tej metody jest łączem.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-255">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="3c2d2-256">W tym przewodniku możemy skupić się na za pomocą liczby tabel do produkcji compact reprezentacje wymiarów wysokiej funkcji podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="3c2d2-257">To nie jest jedynym sposobem, aby zakodować podzielone na kategorie funkcji; Aby uzyskać więcej informacji na temat innych metod, można wyewidencjonować zainteresowanych użytkowników [co hot-encoding](http://en.wikipedia.org/wiki/One-hot) i [Tworzenie skrótu funkcji](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="3c2d2-258">Do tworzenia liczba tabel danych Liczba, używamy danych do folderu raw/liczby.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-258">To build count tables on the count data, we use the data in the folder raw/count.</span></span> <span data-ttu-id="3c2d2-259">W sekcji modelowania zostanie przedstawiony użytkowników sposobu tworzenia tych tabel liczba kategorii funkcji od początku, lub też używać tabeli liczbę wstępnie skompilowanych dla ich eksploracji.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="3c2d2-260">W jaki sposób podczas zwane "wbudowanych liczba tabel", firma Microsoft oznacza przy użyciu tabel liczba, które firma Microsoft udostępnia.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span></span> <span data-ttu-id="3c2d2-261">Szczegółowe informacje na temat dostęp do tych tabel znajdują się w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-261">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <span data-ttu-id="3c2d2-262"><a name="aml"></a>Tworzenie modelu przy użyciu usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3c2d2-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="3c2d2-263">Nasz model budowania procesu w usłudze Azure Machine Learning obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="3c2d2-264">Pobierz dane z tabele programu Hive w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3c2d2-264">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="3c2d2-265">Tworzenie eksperymentu: czyszczenie danych i featurize z liczby tabel</span><span class="sxs-lookup"><span data-stu-id="3c2d2-265">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="3c2d2-266">Tworzenie, szkolenia i klasyfikacja modelu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-266">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="3c2d2-267">Ocena modelu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-267">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="3c2d2-268">Opublikuj model jako usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="3c2d2-268">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="3c2d2-269">Teraz możemy rozpocząć tworzenie modeli w usłudze Azure Machine Learning studio.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-269">Now we are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="3c2d2-270">Nasze dół próbki danych zostanie zapisany jako tabele programu Hive w klastrze.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-270">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="3c2d2-271">Używamy usługi Azure Machine Learning **i zaimportuj dane** modułu do tych danych do odczytu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-271">We use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="3c2d2-272">Poświadczenia, aby uzyskać dostęp do konta magazynu tego klastra znajdują się w poniżej.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-272">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="3c2d2-273"><a name="step1"></a>Krok 1: Pobierz dane z tabel gałęzi do usługi Azure Machine Learning, za pomocą modułu importowanie danych i wybrać go do eksperymentu uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="3c2d2-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="3c2d2-274">Najpierw wybrać **+ nowy** -> **EKSPERYMENTU** -> **pusty eksperyment**.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="3c2d2-275">Następnie z **wyszukiwania** pole u góry po lewej, wyszukaj "Import Data".</span><span class="sxs-lookup"><span data-stu-id="3c2d2-275">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="3c2d2-276">Przeciągnij i upuść **i zaimportuj dane** modułu do eksperymentu kanwy (środkowej części ekranu), aby użyć modułu programu dla dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="3c2d2-277">Co to jest **i zaimportuj dane** wygląda jak podczas pobierania danych z tabeli Hive:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-277">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![Importuj dane pobiera dane](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="3c2d2-279">Dla **i zaimportuj dane** modułu, wartości parametrów, które znajdują się na rysunku przedstawiono tylko sortowanie wymaga podania wartości.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="3c2d2-280">Poniżej przedstawiono pewne ogólne wskazówki na temat sposobu wypełniania zestawu parametrów dla **i zaimportuj dane** modułu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="3c2d2-281">Wybierz "Zapytania Hive" **źródła danych**</span><span class="sxs-lookup"><span data-stu-id="3c2d2-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="3c2d2-282">W **zapytanie Hive bazy danych** polu Wybierz proste * FROM < Twojej\_bazy danych\_name.your\_tabeli\_nazwy >-jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-282">In the **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="3c2d2-283">**Identyfikator URI serwera Hcatalog**: Jeśli klaster jest "abc", to po prostu: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="3c2d2-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="3c2d2-284">**Nazwa konta użytkownika Hadoop**: nazwa użytkownika, wybierany w momencie uruchomienia urządzeń klastra.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="3c2d2-285">(Nie nazwa użytkownika dostępu zdalnego!)</span><span class="sxs-lookup"><span data-stu-id="3c2d2-285">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="3c2d2-286">**Hasło konta użytkownika Hadoop**: hasło dla nazwy użytkownika, wybierany w momencie uruchomienia urządzeń klastra.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="3c2d2-287">(Nie hasła dostępu zdalnego!)</span><span class="sxs-lookup"><span data-stu-id="3c2d2-287">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="3c2d2-288">**Lokalizacja danych wyjściowych**: wybierz polecenie "Azure"</span><span class="sxs-lookup"><span data-stu-id="3c2d2-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="3c2d2-289">**Nazwa konta magazynu Azure**: konta magazynu skojarzone z klastra</span><span class="sxs-lookup"><span data-stu-id="3c2d2-289">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="3c2d2-290">**Klucz konta magazynu Azure**: klucz konta magazynu skojarzone z klastrem.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="3c2d2-291">**Nazwa kontenera Azure**: Jeśli nazwa klastra jest "abc", a następnie zazwyczaj jest to po prostu "abc",.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="3c2d2-292">Raz **i zaimportuj dane** zakończeniu pobieranie danych (możesz zobaczyć zielony znacznik w Module), Zapisz te dane jako zestawu danych (o nazwie wybranych przez użytkownika).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="3c2d2-293">Co to wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-293">What this looks like:</span></span>

![Importuj dane zapisywanie danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="3c2d2-295">Kliknij prawym przyciskiem myszy portem wyjściowym **i zaimportuj dane** modułu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-295">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="3c2d2-296">Takie działanie spowoduje wyświetlenie **Zapisz jako zestawu danych** opcji i **wizualizacja** opcji.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="3c2d2-297">**Wizualizacja** opcji, po kliknięciu wyświetla 100 wierszy danych, wraz z prawym panelu, który jest przydatne w przypadku niektórych podsumowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="3c2d2-298">Aby zapisać dane, po prostu zaznacz **Zapisz jako zestawu danych** i postępuj zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-298">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="3c2d2-299">Aby wybrać zapisany zestaw danych do użycia w eksperymencie machine learning, Znajdź w zestawach danych przy użyciu **wyszukiwania** pole pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="3c2d2-300">Po prostu wpisz limit nazwa nadana częściowo się do niego dostęp, a następnie przeciągnij zestaw danych na panelu głównego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="3c2d2-301">Upuszczenie go na panelu głównego zaznacza go do użycia w machine learning modelowania.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![Zestaw danych Drage na panel główny](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="3c2d2-303">W tym pociąg i zestawy danych testu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-303">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="3c2d2-304">Ponadto należy użyć nazwy bazy danych i nazw tabel, których można użyć w tym celu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-304">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="3c2d2-305">Wartości używanych na rysunku są przeznaczone wyłącznie dla ilustracji purposes.* *</span><span class="sxs-lookup"><span data-stu-id="3c2d2-305">The values used in the figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="3c2d2-306"><a name="step2"></a>Krok 2: Tworzenie prostego eksperymentu w uczenie maszynowe Azure do prognozowania kliknięć / nie kliknięcia</span><span class="sxs-lookup"><span data-stu-id="3c2d2-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="3c2d2-307">Nasze eksperymentu uczenia Maszynowego Azure wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning eksperymentu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="3c2d2-309">Teraz omówione najważniejsze składniki tego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-309">We now examine the key components of this experiment.</span></span> <span data-ttu-id="3c2d2-310">Dla przypomnienia musimy przeciągnij naszych zapisane pociągu i przetestowanie zestawów danych do naszej kanwy eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="3c2d2-311">Brak danych</span><span class="sxs-lookup"><span data-stu-id="3c2d2-311">Clean Missing Data</span></span>
<span data-ttu-id="3c2d2-312">**Clean Missing Data** modułu jest sugeruje nazwa: go czyści brakujące dane w sposób, który może być określone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="3c2d2-313">Trwa wyszukiwanie w tym module, widzimy to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-313">Looking into this module, we see this:</span></span>

![Wyczyść brakujące dane](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="3c2d2-315">W tym miejscu Wybraliśmy Zamień wszystkie brakujące wartości 0.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-315">Here, we chose to replace all missing values with a 0.</span></span> <span data-ttu-id="3c2d2-316">Istnieją inne opcje zostaną również, które są wyświetlane analizując list rozwijanych w module.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="3c2d2-317">Inżynieria na danych</span><span class="sxs-lookup"><span data-stu-id="3c2d2-317">Feature engineering on the data</span></span>
<span data-ttu-id="3c2d2-318">Może istnieć miliony unikatowe wartości w przypadku niektórych funkcji podzielone na kategorie dużych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="3c2d2-319">Przy użyciu metod prosty przykład hot jeden kodowanie reprezentujący takich funkcji podzielone na kategorie wymiarów wysokiej jest całkowicie będzie niemożliwe.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="3c2d2-320">W tym przewodniku zostaje przedstawiony sposób korzystania z funkcji count przy użyciu wbudowanych modułów uczenia maszynowego Azure, aby wygenerować compact reprezentacje tych wymiarów wysokiej zmiennych podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="3c2d2-321">Wynik końcowy jest mniejszy rozmiar modelu, szkolenia szybsze i metryki wydajności, które są dość porównywalna przy użyciu innych technik.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="3c2d2-322">Kompilowanie zliczania transformacji</span><span class="sxs-lookup"><span data-stu-id="3c2d2-322">Building counting transforms</span></span>
<span data-ttu-id="3c2d2-323">Do tworzenia funkcji count, używamy **kompilacji zliczania przekształcenie** moduł, który jest dostępny w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="3c2d2-324">Moduł wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-324">The module looks like this:</span></span>

<span data-ttu-id="3c2d2-325">![Utworzenie modułu zliczania przekształcenie](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![kompilacji zliczania przekształcenie modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="3c2d2-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3c2d2-326">W **liczba kolumn** , możemy wprowadź te kolumny, które firma Microsoft chcą wykonywać liczby na.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span></span> <span data-ttu-id="3c2d2-327">Zazwyczaj są to (jak wspomniano) wymiarów wysokiej kolumny podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="3c2d2-328">Na początku, wspomniano, że element dataset Criteo zawiera kolumny podzielone na kategorie 26: z Col15 do Col40.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="3c2d2-329">W tym miejscu możemy liczba na wszystkich z nich i zapewnić ich indeksów (od 15 do 40 oddzielonych przecinkami, jak pokazano).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="3c2d2-330">Aby użyć modułu programu w trybie MapReduce (odpowiedni dla dużych zestawów danych), potrzebujemy dostęp do klastra usługi HDInsight Hadoop (używane do eksplorowania funkcji mogą być ponownie używane w tym celu również) i jego poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="3c2d2-331">Poprzednie ilustracjach jakie wypełniane wartości wygląda jak (Zastąp wartości ilustracyjną z tymi, które są istotne dla własnego przypadek użycia).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![Parametry modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="3c2d2-333">Na powyższej ilustracji zostanie przedstawiony sposób wprowadź lokalizację blob danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-333">In the figure above, we show how to enter the input blob location.</span></span> <span data-ttu-id="3c2d2-334">Ta lokalizacja zawiera dane, zarezerwowane dla tworzenia liczbę tabel w.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-334">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="3c2d2-335">Po zakończeniu tego modułu transformacji dla można zapisać później przez kliknięcie prawym przyciskiem myszy modułu i wybierając **Zapisz jako transformacji** opcji:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

![Opcję "Zapisz jako transformacji"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="3c2d2-337">W naszej architektury eksperymentu przedstawionych powyżej zestaw danych "ytransform2" odpowiada dokładnie transformacji liczba zapisanych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="3c2d2-338">W pozostałej części tego eksperymentu, przyjęto założenie, że czytnik używane **kompilacji zliczania przekształcenie** moduł na niektóre dane do generowania liczby i można następnie użyć tych liczby do generowania liczby funkcji na pociągu i testowania zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="3c2d2-339">Wybieranie, jakie liczbę funkcji do uwzględnienia jako część pociągu i testowania zestawów danych</span><span class="sxs-lookup"><span data-stu-id="3c2d2-339">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="3c2d2-340">Po mamy liczbą przekształcenie gotowe, użytkownik może wybrać, jakie funkcje do uwzględnienia w ich train a testów, zestawów danych przy użyciu **zmodyfikować liczby parametrów tabeli** modułu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="3c2d2-341">Ten moduł zostanie przedstawiony tylko tutaj kompletności, ale w celu uproszczenia nie faktycznie jest używana w naszym doświadczeniu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modyfikowanie tabeli liczba parametrów](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="3c2d2-343">W takim przypadku jak widać, wybraliśmy do używania właśnie prawdopodobieństwo dziennika i Ignoruj wycofywania kolumny.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span></span> <span data-ttu-id="3c2d2-344">Możemy również ustawić parametry, takie jak próg bin odzyskiwanie, ile artykule wcześniejsze przykłady można dodać wygładzanie oraz określić, czy używać żadnych szumu Laplacian lub nie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="3c2d2-345">Wszystkie te funkcje są zaawansowane i zauważyć, że wartości domyślne to dobry punkt wyjścia dla użytkowników, którzy dopiero zaczynasz korzystać z tego typu funkcji generowania.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="3c2d2-346">Przekształcenia danych przed wygenerowaniem funkcji count</span><span class="sxs-lookup"><span data-stu-id="3c2d2-346">Data transformation before generating the count features</span></span>
<span data-ttu-id="3c2d2-347">Teraz możemy skupić się na ważne punktu o Przekształcanie naszych train i testowanie danych przed wygenerowaniem faktycznie funkcji count.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="3c2d2-348">Należy pamiętać, że istnieją dwa **wykonanie skryptu języka R** moduły używane przed możemy przekształcenia count do naszych danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span></span>

![Wykonanie skryptu języka R modułów](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="3c2d2-350">W tym miejscu jest pierwszym skrypt języka R:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-350">Here is the first R script:</span></span>

![Pierwszy skrypt języka R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="3c2d2-352">Ten skrypt języka R możemy zmienić naszych kolumn do nazwy "Col1" do "Col40".</span><span class="sxs-lookup"><span data-stu-id="3c2d2-352">In this R script, we rename our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="3c2d2-353">Jest to spowodowane przekształcenia liczba oczekuje nazwy w tym formacie.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-353">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="3c2d2-354">W drugim skrypt języka R, możemy saldo dystrybucji między klasami dodatnie i ujemne (klasy 1 i 0 odpowiednio) poprzez próbkowanie ujemna klasy.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span></span> <span data-ttu-id="3c2d2-355">Skrypt języka R w tym miejscu pokazano, jak to zrobić:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-355">The R script here shows how to do this:</span></span>

![Drugi skrypt języka R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="3c2d2-357">W tym prostego skryptu języka R, używamy "pos\_minus\_współczynnik" można ustawić wielkość balansu między dodatnie i ujemne klasy.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="3c2d2-358">Jest to ważne ponieważ poprawy nierównowaga klasy zwykle ma zwiększenia wydajności dla klasyfikacji problemów w przypadku dystrybucji klasy niesymetryczna (odwołanie w tym przypadku mając klasy dodatnią 3.3% i 96.7% ujemna klasy).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="3c2d2-359">Stosowania przekształcenia liczba na naszych danych</span><span class="sxs-lookup"><span data-stu-id="3c2d2-359">Applying the count transformation on our data</span></span>
<span data-ttu-id="3c2d2-360">Ponadto możemy użyć **Zastosuj przekształcenie** modułu do stosowania przekształceń liczba na naszych train i testowania zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="3c2d2-361">Ten moduł pobiera przekształcenia liczby zapisanej jako jedno wejście i pociągu lub testowym zestawy danych jako dane wejściowe i zwraca danych za pomocą funkcji count.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="3c2d2-362">Przedstawiono tutaj:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-362">It is shown here:</span></span>

![Zastosuj przekształcenie modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="3c2d2-364">Fragment, jakie funkcje count wyglądać</span><span class="sxs-lookup"><span data-stu-id="3c2d2-364">An excerpt of what the count features look like</span></span>
<span data-ttu-id="3c2d2-365">Jest to istotne, aby zobaczyć, jak wyglądają liczba funkcji w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-365">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="3c2d2-366">W tym miejscu zostanie przedstawiony fragment to:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-366">Here we show an excerpt of this:</span></span>

![Liczba funkcji](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="3c2d2-368">W tym fragmencie zostanie przedstawiony, czy dla kolumn, które firma Microsoft zliczane na, możemy uzyskać liczby i dziennika prawdopodobieństwo oprócz wszelkie istotne backoffs.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="3c2d2-369">Firma Microsoft są teraz gotowe do tworzenia modelu uczenia maszynowego Azure przy użyciu tych przekształcone zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="3c2d2-370">W następnej sekcji zostanie przedstawiony sposób można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-370">In the next section, we show how this can be done.</span></span>

### <span data-ttu-id="3c2d2-371"><a name="step3"></a>Krok 3: Tworzenie uczenia i klasyfikacja modelu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-371"><a name="step3"></a> Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="3c2d2-372">Wybór uczeń</span><span class="sxs-lookup"><span data-stu-id="3c2d2-372">Choice of learner</span></span>
<span data-ttu-id="3c2d2-373">Najpierw należy wybrać uczeń.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-373">First, we need to choose a learner.</span></span> <span data-ttu-id="3c2d2-374">Firma Microsoft będzie używany drzewa decyzyjnego dwie klasy boosted jako naszych uczeń.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-374">We are going to use a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="3c2d2-375">Poniżej przedstawiono wartości domyślne dla tego uczeń:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-375">Here are the default options for this learner:</span></span>

![Parametry Two-Class Boosted drzewa decyzyjnego](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="3c2d2-377">Naszym doświadczeniu zamierzamy wybierz wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-377">For our experiment, we are going to choose the default values.</span></span> <span data-ttu-id="3c2d2-378">Firma Microsoft należy pamiętać, że wartości domyślne są zazwyczaj przydatne i sposób uzyskać szybkie planów bazowych na wydajność.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="3c2d2-379">Na wydajność można poprawić przez profilach parametrów, jeśli użytkownik chce po utworzeniu linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="3c2d2-380">Uczenie modelu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-380">Train the model</span></span>
<span data-ttu-id="3c2d2-381">Szkolenia, możemy po prostu Wywołaj **Train Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="3c2d2-382">Dwóch danych wejściowych do niego są uczeń Two-Class Boosted drzewa decyzyjnego i naszym zestawie danych pociągu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="3c2d2-383">To jest następujący:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-383">This is shown here:</span></span>

![Train Model modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="3c2d2-385">Ocena modelu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-385">Score the model</span></span>
<span data-ttu-id="3c2d2-386">Po mamy uczonego modelu możemy gotowy do wyniku na zestawu danych testowych i ocenę jego wydajności.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="3c2d2-387">Firma Microsoft to zrobić przy użyciu **Score Model** modułu pokazano na poniższej ilustracji, wraz z **Evaluate Model** modułu:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![Moduł Score Model (Generowanie wyników przez model)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="3c2d2-389"><a name="step4"></a>Krok 4: Ocena modelu</span><span class="sxs-lookup"><span data-stu-id="3c2d2-389"><a name="step4"></a> Step 4: Evaluate the model</span></span>
<span data-ttu-id="3c2d2-390">Wreszcie chcemy analizowanie wydajności modelu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-390">Finally, we would like to analyze model performance.</span></span> <span data-ttu-id="3c2d2-391">W przypadku problemów klasyfikacji (binarnego) dwie klasy dobrej miary jest zazwyczaj, AUC.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="3c2d2-392">To wizualizować, firma Microsoft podpinanie **Score Model** moduł **Evaluate Model** modułu dla tego.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="3c2d2-393">Kliknięcie przycisku **Visualize** na **Evaluate Model** modułu daje grafiki podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![Ocena modelu BDT modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="3c2d2-395">W danych binarnych (lub dwie klasy) klasyfikacji problemów, dobrym miara dokładności prognozy jest obszar w krzywej (AUC).</span><span class="sxs-lookup"><span data-stu-id="3c2d2-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="3c2d2-396">W poniżej zostanie przedstawiony naszych wyników przy użyciu tego modelu w naszym zestawu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="3c2d2-397">Aby uzyskać dostęp do tej, kliknij prawym przyciskiem myszy portem wyjściowym **Evaluate Model** modułu, a następnie **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![Wizualizuj modułu Evaluate Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="3c2d2-399"><a name="step5"></a>Krok 5: Opublikuj model jako usługę sieci Web</span><span class="sxs-lookup"><span data-stu-id="3c2d2-399"><a name="step5"></a> Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="3c2d2-400">Umożliwia publikowanie modelu uczenia maszynowego Azure jako usługi sieci web z co najmniej problemów jest przydatna funkcja dokonywania szeroko dostępne.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="3c2d2-401">Po zakończeniu tej operacji, każda osoba, która wykonywania wywołań do usługi sieci web z danych wejściowych muszą prognoz dotyczących, czy usługa sieci web używa modelu do zwrócenia tych prognoz.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="3c2d2-402">Aby to zrobić, możemy najpierw zapisać uczonego modelu obiektu Trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-402">To do this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="3c2d2-403">Jest to realizowane przez kliknięcie prawym przyciskiem myszy **Train Model** modułu i przy użyciu **Zapisz jako Uczonego modelu** opcji.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="3c2d2-404">Następnie należy utworzyć dane wejściowe i wyjściowe portów dla naszej usługi sieci web:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-404">Next, we need to create input and output ports for our web service:</span></span>

* <span data-ttu-id="3c2d2-405">port wejściowy pobiera dane w tym samym formularzu jako dane potrzebujemy prognoz dotyczących</span><span class="sxs-lookup"><span data-stu-id="3c2d2-405">an input port takes data in the same form as the data that we need predictions for</span></span>
* <span data-ttu-id="3c2d2-406">port wyjściowy zwraca etykiety oceniane i prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-406">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="3c2d2-407">Wybierz kilka wierszy danych dla portu wejściowego</span><span class="sxs-lookup"><span data-stu-id="3c2d2-407">Select a few rows of data for the input port</span></span>
<span data-ttu-id="3c2d2-408">Jest łatwe w użyciu **Zastosuj przekształcenie SQL** moduł wybrać tylko 10 wierszy jako danych wejściowych portów.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="3c2d2-409">Wybierz tylko te wiersze danych dla naszych portu wejściowego przy użyciu zapytania SQL, pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-409">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![Port wejściowy danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="3c2d2-411">Usługa sieci Web</span><span class="sxs-lookup"><span data-stu-id="3c2d2-411">Web service</span></span>
<span data-ttu-id="3c2d2-412">Możemy teraz gotowy do uruchomienia małych eksperymentu, która może być używana do publikowania naszej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-412">Now we are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="3c2d2-413">Generuj dane wejściowe dla usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="3c2d2-413">Generate input data for webservice</span></span>
<span data-ttu-id="3c2d2-414">Krokiem zeroth ponieważ tabeli count jest duży, możemy zająć kilka wierszy danych testowych i generowanie danych wyjściowych z jej z funkcji count.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="3c2d2-415">Może to służyć jako formatu danych wejściowych naszej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-415">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="3c2d2-416">To jest następujący:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-416">This is shown here:</span></span>

![Utwórz BDT danych wejściowych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="3c2d2-418">Format danych wejściowych używamy teraz dane wyjściowe **Featurizer liczba** modułu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="3c2d2-419">Po zakończeniu uruchamiania to eksperymentu, Zapisz dane wyjściowe z **Featurizer liczba** modułu jako zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="3c2d2-420">Ten zestaw danych jest używany dla danych wejściowych w usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-420">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="3c2d2-421">Ocenianie eksperymentu publikowania usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="3c2d2-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="3c2d2-422">Najpierw zostanie przedstawiony to wygląda następująco.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-422">First, we show what this looks like.</span></span> <span data-ttu-id="3c2d2-423">Struktura niezbędne jest **Score Model** moduł, który akceptuje naszych obiekt uczonego modelu i kilka wierszy danych wejściowych, generowany w poprzednich krokach za pomocą **Featurizer liczba** modułu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="3c2d2-424">Używamy "Wybieranie kolumn w zestawie danych" do projektu etykiety Scored i wynik prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![Wybieranie kolumn w zestawie danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="3c2d2-426">Powiadomienie jak **Select Columns in Dataset** modułu może służyć do "filtrowanie" danych z zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="3c2d2-427">Zostanie przedstawiony tutaj zawartość:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-427">We show the contents here:</span></span>

![Filtrowanie z Select Columns in Dataset modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="3c2d2-429">Aby uzyskać niebieski danych wejściowych i wyjściowych portów, po prostu kliknij **przygotowanie webservice** w prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="3c2d2-430">Uruchomienie tego eksperymentu również pozwoli nam opublikować usługi sieci web: kliknij **OPUBLIKOWAĆ usługi sieci WEB** ikonę u dołu tutaj prawym, wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![Publikowanie usługi sieci Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="3c2d2-432">Po opublikowaniu usługi sieci Web, możemy przekierowanie do strony, która wygląda w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-432">Once the webservice is published, we get redirected to a page that looks thus:</span></span>

![Pulpit nawigacyjny usługi sieci Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="3c2d2-434">Firma Microsoft, zobacz dwa linki dla usług sieci Web po lewej stronie:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-434">We see two links for webservices on the left side:</span></span>

* <span data-ttu-id="3c2d2-435">**Żądanie/odpowiedź** usługi (lub rekordy zasobów) jest przeznaczony dla jednego prognoz i będziemy korzystać w tym workshop.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="3c2d2-436">**BATCH EXECUTION** usługi (BES) służy do przewidywania partii i wymaga danych wejściowych w celu tworzenia prognoz, które znajdują się w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="3c2d2-437">Kliknięcie łącza **żądanie/odpowiedź** przyjmuje nam stronę, która udostępnia wstępnie puszkach kodu w języku C#, python i R. Ten kod może wygodnie służyć do wykonywania wywołań do usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="3c2d2-438">Należy pamiętać, że klucz interfejsu API na tej stronie musi być używane do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-438">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="3c2d2-439">Jest wygodną kopiować ten kod języka python w komórce nowego notesu IPython.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="3c2d2-440">W tym miejscu zostanie przedstawiony segment kodu python przy użyciu poprawnego klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-440">Here we show a segment of python code with the correct API key.</span></span>

![Kod języka Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="3c2d2-442">Należy pamiętać, możemy zastąpić domyślny klucz interfejsu API z kluczem interfejsu API naszych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-442">Note that we replaced the default API key with our webservices's API key.</span></span> <span data-ttu-id="3c2d2-443">Kliknięcie przycisku **Uruchom** w tej komórce w IPython notesu daje następującą odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="3c2d2-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![IPython odpowiedzi](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="3c2d2-445">Widzimy, że dwa przykłady testu żądanych o buforów (w ramach JSON skrypt w języku python), uzyskujemy wstecz odpowiedzi w formie "Scored Labels Scored Probabilities".</span><span class="sxs-lookup"><span data-stu-id="3c2d2-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="3c2d2-446">Należy pamiętać, że w takim przypadku Wybraliśmy wartości domyślne (0 dla wszystkich kolumn liczbowych i ciąg "value" dla wszystkich kolumn podzielone na kategorie) umożliwia wstępnie zdefiniowanym kodu.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="3c2d2-447">Zakończenie nasze wskazówki end-to-end przedstawiający sposób obsługi na dużą skalę zestawu danych za pomocą usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="3c2d2-448">Firma Microsoft wprowadzenie terabajtów danych, utworzyć modelu prognozy i wdrożyć go jako usługę sieci web w chmurze.</span><span class="sxs-lookup"><span data-stu-id="3c2d2-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span></span>

