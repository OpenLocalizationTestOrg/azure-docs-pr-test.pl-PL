---
title: "Hello proces nauki danych zespołu w akcji — na zestaw 1 TB danych przy użyciu klastra usługi Azure HDInsight Hadoop | Dokumentacja firmy Microsoft"
description: "Scenariusz end-to-end wykorzystujących usługi HDInsight Hadoop przy użyciu hello proces nauki danych zespołu toobuild klastra, a następnie wdrożyć model przy użyciu dużych publicznie dostępnych dataset (1 TB)"
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
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="e145b-103">Hello proces nauki danych zespołu w akcji — na zestaw 1 TB danych przy użyciu klastra usługi Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="e145b-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="e145b-104">W tym przewodniku zostaje przedstawiony przy użyciu hello proces nauki danych zespołu w scenariuszu end-to-end z [klastra usługi Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Eksploruj, funkcję odtwarzania i w dół przykładowych danych z jednego z hello publicznie dostępne [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="e145b-105">Używamy toobuild usługi Azure Machine Learning model klasyfikacji binarnej na tych danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="e145b-106">Zostanie przedstawiony, jak toopublish te modele jako usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e145b-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="e145b-107">Możliwe jest również możliwe toouse IPython notesu tooaccomplish hello zadania przedstawione w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="e145b-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="e145b-108">Użytkownicy, którzy będą jak tootry takie podejście powinni skontaktować hello [wskazówki Criteo za pomocą połączenia ODBC programu Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tematu.</span><span class="sxs-lookup"><span data-stu-id="e145b-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="e145b-109"><a name="dataset"></a>Opis elementu Criteo Dataset</span><span class="sxs-lookup"><span data-stu-id="e145b-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="e145b-110">Hello Criteo dane są około 370 GB plików TSV gzip skompresowane (~1.3TB nieskompresowane), zestawu danych prognozowania kliknij składającej się z ponad miliard 4.3 rekordów.</span><span class="sxs-lookup"><span data-stu-id="e145b-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="e145b-111">Jest ona pobierana z 24 dni kliknij danych udostępnionych przez [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="e145b-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="e145b-112">Dla wygody hello analityków danych Firma Microsoft ma rozpakowane dostępne tooexperiment toous danych z.</span><span class="sxs-lookup"><span data-stu-id="e145b-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="e145b-113">Każdy rekord w tym elemencie dataset zawiera kolumny 40:</span><span class="sxs-lookup"><span data-stu-id="e145b-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="e145b-114">Pierwsza kolumna Hello jest etykieta kolumny, która wskazuje, czy użytkownik kliknie **Dodaj** (wartość 1) lub w ogóle nie kliknij jedną (wartość 0)</span><span class="sxs-lookup"><span data-stu-id="e145b-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="e145b-115">następnie 13 kolumny są numeryczną, i</span><span class="sxs-lookup"><span data-stu-id="e145b-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="e145b-116">ostatni 26 są podzielone na kategorie kolumn</span><span class="sxs-lookup"><span data-stu-id="e145b-116">last 26 are categorical columns</span></span>

<span data-ttu-id="e145b-117">kolumny Hello są anonimowe i szereg wyliczany nazwy: "Col1" (dla kolumny etykiety hello) zbyt "Col40" (dla ostatniej kolumny podzielone na kategorie hello).</span><span class="sxs-lookup"><span data-stu-id="e145b-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="e145b-118">Poniżej przedstawiono fragment hello najpierw 20 kolumn dwóch uwag (wiersze) z tego zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="e145b-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="e145b-119">Istnieją brakujące wartości w kolumnach liczbowych i podzielone na kategorie hello w tym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="e145b-120">Przedstawione prostą metodę obsługi hello brakujące wartości.</span><span class="sxs-lookup"><span data-stu-id="e145b-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="e145b-121">Dodatkowe szczegóły danych hello są zbadane, gdy będziemy przechowywać w tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e145b-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="e145b-122">**Definicja:** *szybkość przeglądowego (kont.):* to hello odsetek kliknięć w hello danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="e145b-123">W tym zestawie danych Criteo hello Ewidencyjne to około 3.3% lub 0.033.</span><span class="sxs-lookup"><span data-stu-id="e145b-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="e145b-124"><a name="mltasks"></a>Przykłady prognozowania zadań</span><span class="sxs-lookup"><span data-stu-id="e145b-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="e145b-125">Dwa przykładowe prognozowania problemy zostały rozwiązane w tym przewodniku:</span><span class="sxs-lookup"><span data-stu-id="e145b-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="e145b-126">**Klasyfikacji binarnej**: wskazuje, czy użytkownik kliknął add:</span><span class="sxs-lookup"><span data-stu-id="e145b-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="e145b-127">Klasa 0: Nie kliknij</span><span class="sxs-lookup"><span data-stu-id="e145b-127">Class 0: No Click</span></span>
   * <span data-ttu-id="e145b-128">Klasa 1: kliknij przycisk</span><span class="sxs-lookup"><span data-stu-id="e145b-128">Class 1: Click</span></span>
2. <span data-ttu-id="e145b-129">**Regresja**: prognozuje prawdopodobieństwo powitania kliknij ad z funkcji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e145b-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="e145b-130"><a name="setup"></a>Ustaw się HDInsight klastra usługi Hadoop do analizy danych</span><span class="sxs-lookup"><span data-stu-id="e145b-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="e145b-131">**Uwaga:** jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="e145b-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="e145b-132">Konfigurowanie środowiska Azure nauki danych do tworzenia rozwiązań analizy predykcyjnej z klastrami usługi HDInsight w trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="e145b-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="e145b-133">[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md): to konto magazynu jest używana toostore danych w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e145b-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="e145b-134">dane Hello używane w klastrach HDInsight są przechowywane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e145b-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="e145b-135">[Dostosowywanie Hadoop w usłudze Azure Hdinsight do analizy danych](machine-learning-data-science-customize-hadoop-cluster.md): ten krok umożliwia utworzenie klastra usługi Azure HDInsight Hadoop z 64-bitowych Anaconda Python 2.7 zainstalowane we wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="e145b-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="e145b-136">Istnieją dwa toocomplete ważne czynności (opisanej w tym temacie), w przypadku dostosowywania hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e145b-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="e145b-137">Należy połączyć utworzony w kroku 1 z klastrem usługi HDInsight, po utworzeniu konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="e145b-138">To konto magazynu jest używane do uzyskiwania dostępu do danych, które mogą być przetwarzane w ramach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="e145b-139">Należy włączyć dostęp zdalny toohello węzła głównego klastra powitania po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="e145b-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="e145b-140">Pamiętaj poświadczenia dostępu zdalnego hello określone w tym miejscu (różne od tych określonych hello klastra podczas jego tworzenia): potrzebne toocomplete hello następujących procedur.</span><span class="sxs-lookup"><span data-stu-id="e145b-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="e145b-141">[Utwórz obszar roboczy usługi Azure ML](machine-learning-create-workspace.md): to Azure Machine Learning obszaru roboczego jest używany do tworzenia modeli uczenia maszyny po Eksploracja danych początkowych i w dół próbkowania w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="e145b-142"><a name="getdata"></a>Pobierz i wykorzystują dane ze źródła publiczny</span><span class="sxs-lookup"><span data-stu-id="e145b-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="e145b-143">Witaj [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) zestawu danych jest możliwy przez kliknięcie łącza hello, akceptując hello warunki użytkowania i podanie nazwy.</span><span class="sxs-lookup"><span data-stu-id="e145b-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="e145b-144">Migawki to wygląda jak jest następujący:</span><span class="sxs-lookup"><span data-stu-id="e145b-144">A snapshot of what this looks like is shown here:</span></span>

![Zaakceptuj postanowienia Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="e145b-146">Kliknij przycisk **tooDownload Kontynuuj** tooread więcej informacji na temat hello zestawu danych i ich dostępność.</span><span class="sxs-lookup"><span data-stu-id="e145b-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="e145b-147">Witaj danych znajduje się w publicznej [magazynu obiektów blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) lokalizacji: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="e145b-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="e145b-148">Witaj "wasb" odwołuje się tooAzure lokalizacji magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="e145b-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="e145b-149">Hello danych w tym magazynie obiektów blob publicznego składa się z trzech podfoldery rozpakowane danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="e145b-150">Witaj podfolder *raw/liczby/* zawiera hello pierwszych 21 dni dane — od dnia\_00 tooday\_20</span><span class="sxs-lookup"><span data-stu-id="e145b-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="e145b-151">Witaj podfolder *raw/train/* składa się z jednego dnia danych, dzień\_21</span><span class="sxs-lookup"><span data-stu-id="e145b-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="e145b-152">Witaj podfolder *pierwotnych i testowanie/* składa się z dwóch dni danych, dzień\_22 i dzień\_23</span><span class="sxs-lookup"><span data-stu-id="e145b-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="e145b-153">Dla tych, którzy mają toostart hello raw gzip danych, są one również dostępne w folderze głównym hello *raw /* jako day_NN.gz, gdzie NN przechodzi od 00 too23.</span><span class="sxs-lookup"><span data-stu-id="e145b-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="e145b-154">Tooaccess o innym podejściu Eksploruj i model te dane, które nie wymaga wszystkie lokalne pliki znajduje się w dalszej części tego przewodnika, gdy utworzymy tabele programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e145b-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="e145b-155"><a name="login"></a>Zaloguj się za toohello headnode klastra</span><span class="sxs-lookup"><span data-stu-id="e145b-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="e145b-156">toolog w headnode toohello hello klastra, użyj hello [portalu Azure](https://ms.portal.azure.com) toolocate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e145b-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="e145b-157">Kliknij ikonę Słoń HDInsight hello na powitania po lewej, a następnie kliknij dwukrotnie nazwę hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e145b-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="e145b-158">Przejdź toohello **konfiguracji** , kliknij dwukrotnie ikonę POŁĄCZ hello na powitania u dołu strony hello, a następnie wprowadź swoje poświadczenia dostępu zdalnego, po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="e145b-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="e145b-159">Trwa headnode toohello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e145b-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="e145b-160">Poniżej przedstawiono typowe pierwszego logowania toohello headnode klastra wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e145b-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Zaloguj się za toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="e145b-162">Po lewej stronie powitania widzimy hello "Hadoop wiersza polecenia", czyli naszych najważniejszą metodą roboczą dla hello Eksploracja danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="e145b-163">Przedstawiono również dwa przydatne adresy URL - "Hadoop Yarn stanu" i "Hadoop nazwa węzła".</span><span class="sxs-lookup"><span data-stu-id="e145b-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="e145b-164">adres URL stanu yarn Hello przedstawia postęp zadania i adres URL węzła nazwa hello zwraca szczegółowe informacje dotyczące konfiguracji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="e145b-165">Teraz możemy są skonfigurowane i gotowe toobegin pierwszej części przewodnika hello: Eksploracja danych przy użyciu Hive i przygotowanie danych do usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e145b-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="e145b-166"><a name="hive-db-tables"></a>Utwórz gałąź bazy danych i tabel</span><span class="sxs-lookup"><span data-stu-id="e145b-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="e145b-167">tabele toocreate gałęzi dla naszego zestawu danych Criteo hello Otwórz ***wiersza polecenia platformy Hadoop*** na hello pulpitu hello węzła głównego, a następnie wprowadź katalog Hive hello wprowadzając polecenie hello</span><span class="sxs-lookup"><span data-stu-id="e145b-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="e145b-168">Uruchom wszystkie polecenia gałęzi w tym przewodniku z hello Hive bin / directory wiersza.</span><span class="sxs-lookup"><span data-stu-id="e145b-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="e145b-169">Odpowiada on za wszelkie problemy ścieżki automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e145b-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="e145b-170">Używane hello pojęcia "Hive katalogu wiersza", "bin gałęzi / wiersza katalogu" i "wiersza polecenia usługi Hadoop" zamiennie.</span><span class="sxs-lookup"><span data-stu-id="e145b-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="e145b-171">tooexecute każde zapytanie Hive jedną zawsze używaj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e145b-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="e145b-172">Po hello Hive REPL pojawi się z "hive >" Zaloguj się, po prostu wyciąć i wkleić hello zapytania tooexecute go.</span><span class="sxs-lookup"><span data-stu-id="e145b-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="e145b-173">Hello następujący kod tworzy bazy danych "criteo", a następnie generuje 4 tabel:</span><span class="sxs-lookup"><span data-stu-id="e145b-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="e145b-174">*tabeli do wygenerowania liczby* oparty na dzień dni\_00 tooday\_20,</span><span class="sxs-lookup"><span data-stu-id="e145b-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="e145b-175">*tabeli do użycia jako hello train dataset* oparty na dzień\_21, i</span><span class="sxs-lookup"><span data-stu-id="e145b-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="e145b-176">dwa *tabel do użycia jako hello testowania zestawów danych* oparty na dzień\_22 i dzień\_23 odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e145b-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="e145b-177">Naszego zestawu danych testowych możemy podzielić na dwóch różnych tabel, ponieważ jeden z dni hello jest dniem wolnym od pracy i chcemy toodetermine modelu hello są wykrywane różnice między dni wolnych i nie święta od szybkości przeglądowego hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="e145b-178">Witaj skryptu [& #95 przykładowe; hive &#95; Utwórz &#95; criteo &#95; &#95; bazy danych i &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) są wyświetlane tutaj dla wygody:</span><span class="sxs-lookup"><span data-stu-id="e145b-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

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

<span data-ttu-id="e145b-179">Firma Microsoft należy zauważyć, że te tabele zewnętrzne jako możemy po prostu lokalizacji magazynu obiektów Blob (wasb) tooAzure punktu.</span><span class="sxs-lookup"><span data-stu-id="e145b-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="e145b-180">**Istnieją dwa sposoby tooexecute Hive dowolnego zapytania, które teraz wspomina.**</span><span class="sxs-lookup"><span data-stu-id="e145b-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="e145b-181">**Przy użyciu hello wiersza polecenia REPL Hive**: hello najpierw jest tooissue polecenia "hive" i skopiuj i Wklej zapytanie na powitania REPL Hive wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e145b-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="e145b-182">toodo tego, czy:</span><span class="sxs-lookup"><span data-stu-id="e145b-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="e145b-183">Teraz na powitania REPL wiersza polecenia, wycinanie i wklejanie zapytania hello go uruchomi.</span><span class="sxs-lookup"><span data-stu-id="e145b-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="e145b-184">**Zapisywanie zapytań tooa pliku i wykonywania polecenia hello**: hello jest drugi toosave hello zapytania tooa .hql pliku ([& #95 przykładowe; hive &#95; Utwórz &#95; criteo &#95; &#95; bazy danych i &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)), a następnie problem hello następujące polecenie tooexecute hello zapytania:</span><span class="sxs-lookup"><span data-stu-id="e145b-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="e145b-185">Potwierdź utworzenie bazy danych i tabeli</span><span class="sxs-lookup"><span data-stu-id="e145b-185">Confirm database and table creation</span></span>
<span data-ttu-id="e145b-186">Następnie potwierdzamy hello tworzenie hello bazy danych z hello następujące polecenie z hello Hive bin / directory wiersza:</span><span class="sxs-lookup"><span data-stu-id="e145b-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="e145b-187">Dzięki temu:</span><span class="sxs-lookup"><span data-stu-id="e145b-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="e145b-188">Tworzenie nowej bazy danych Witaj, "criteo" hello to potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="e145b-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="e145b-189">toosee tabele utworzyliśmy, możemy po prostu wysłać hello polecenie tutaj z hello Hive bin / directory wiersza:</span><span class="sxs-lookup"><span data-stu-id="e145b-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="e145b-190">Następnie widzimy hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e145b-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="e145b-191"><a name="exploration"></a>Eksploracja danych w gałęzi</span><span class="sxs-lookup"><span data-stu-id="e145b-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="e145b-192">Teraz możemy gotowe toodo eksploracji niektóre podstawowe dane w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="e145b-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="e145b-193">Możemy rozpocząć poprzez zliczanie hello wiele przykładów w pociągu hello i testowanie tabel danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="e145b-194">Liczba train przykłady</span><span class="sxs-lookup"><span data-stu-id="e145b-194">Number of train examples</span></span>
<span data-ttu-id="e145b-195">Witaj zawartość [& #95 przykładowe; hive &#95; liczba &#95; train &#95; tabeli &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) są wyświetlane tutaj:</span><span class="sxs-lookup"><span data-stu-id="e145b-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="e145b-196">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="e145b-197">Alternatywnie jedną mogą również wystawiać hello następujące polecenie z hello Hive bin / directory wiersza:</span><span class="sxs-lookup"><span data-stu-id="e145b-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="e145b-198">Wiele przykładów testu w hello dwóch testów w zestawach danych</span><span class="sxs-lookup"><span data-stu-id="e145b-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="e145b-199">Mamy teraz liczbę hello przykłady w zestawach danych Witaj dwie testu.</span><span class="sxs-lookup"><span data-stu-id="e145b-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="e145b-200">Witaj zawartość [& #95 przykładowe hive &#95; liczba &#95; criteo &#95; test &#95; dzień &#95; 22 &#95; tabeli &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) są tutaj:</span><span class="sxs-lookup"><span data-stu-id="e145b-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="e145b-201">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="e145b-202">W zwykły sposób, może również nazywamy hello skryptu z hello Hive bin / directory monitu wydając polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e145b-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="e145b-203">Na koniec omówione hello wiele przykładów testów w zestawie testów hello danych oparte na dniu\_23.</span><span class="sxs-lookup"><span data-stu-id="e145b-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="e145b-204">Witaj toodo polecenia jest podobne toohello, po prostu przedstawionego (odwoływać się za[& #95 przykładowe; hive &#95; liczba &#95; criteo &#95; test &#95; dzień &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="e145b-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="e145b-205">Dzięki temu:</span><span class="sxs-lookup"><span data-stu-id="e145b-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="e145b-206">Dystrybucji etykiety w zestawie danych train hello</span><span class="sxs-lookup"><span data-stu-id="e145b-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="e145b-207">Hello dystrybucji etykiety w zestawie danych train hello jest.</span><span class="sxs-lookup"><span data-stu-id="e145b-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="e145b-208">toosee, to zostanie przedstawiony zawartość [& #95 przykładowe; hive &#95; criteo &#95; & #95 etykiety; #95 & dystrybucji; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="e145b-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="e145b-209">Daje to hello etykiety dystrybucji:</span><span class="sxs-lookup"><span data-stu-id="e145b-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="e145b-210">Należy pamiętać, że odsetek hello dodatnią etykiety około 3.3% (zgodne z hello oryginalnego zestawu danych).</span><span class="sxs-lookup"><span data-stu-id="e145b-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="e145b-211">Dystrybucje Histogram niektóre liczbowe zmiennych w hello uczenia zestawu danych</span><span class="sxs-lookup"><span data-stu-id="e145b-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="e145b-212">Możemy użyć natywnego gałęzi "histogram\_liczbowa" funkcji toofind się, jakie dystrybucji hello zmiennych liczbowych hello wygląda następująco.</span><span class="sxs-lookup"><span data-stu-id="e145b-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="e145b-213">Poniżej przedstawiono zawartość hello [& #95 przykładowe; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="e145b-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="e145b-214">Daje to poniższe hello:</span><span class="sxs-lookup"><span data-stu-id="e145b-214">This yields hello following:</span></span>

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

<span data-ttu-id="e145b-215">Witaj PENETRACJA widok - rozłożenie kombinacja w gałęzi służy tooproduce wyjściowego przypominającego SQL, zamiast listy zwykle hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="e145b-216">Należy pamiętać, że w hello tej tabeli, pierwsza kolumna hello odpowiada toohello bin Centrum i hello drugi toohello bin częstotliwości.</span><span class="sxs-lookup"><span data-stu-id="e145b-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="e145b-217">Przybliżony percentylu niektóre liczbowe zmiennych w hello uczenia zestawu danych</span><span class="sxs-lookup"><span data-stu-id="e145b-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="e145b-218">Płynących ze zmiennymi liczbowych jest również hello obliczania przybliżonej percentylu.</span><span class="sxs-lookup"><span data-stu-id="e145b-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="e145b-219">Gałąź do natywnego "percentyl\_przybliżone" robi to firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e145b-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="e145b-220">Witaj zawartość [& #95 przykładowe; hive &#95; criteo &#95; przybliżonej &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) są:</span><span class="sxs-lookup"><span data-stu-id="e145b-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="e145b-221">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="e145b-222">Oznacz firma Microsoft hello dystrybucji percentylu zwykle jest blisko związane toohello histogram dystrybucji żadnych liczbowa zmiennej.</span><span class="sxs-lookup"><span data-stu-id="e145b-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="e145b-223">Znajdź liczbę unikatowych wartości dla niektórych podzielone na kategorie kolumn w zestawie danych train hello</span><span class="sxs-lookup"><span data-stu-id="e145b-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="e145b-224">Kontynuowanie hello Eksploracja danych, teraz znaleźliśmy, dla niektórych kolumn podzielone na kategorie hello liczbę unikatowych wartości, które podejmują.</span><span class="sxs-lookup"><span data-stu-id="e145b-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="e145b-225">toodo, to zostanie przedstawiony zawartość [& #95 przykładowe; hive &#95; criteo &#95; unikatowy &#95; wartości &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="e145b-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="e145b-226">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="e145b-227">Firma Microsoft Pamiętaj, że Col15 ma unikatowe wartości 19M!</span><span class="sxs-lookup"><span data-stu-id="e145b-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="e145b-228">Przy użyciu prostego technik, takich jak "hot jeden kodowanie" tooencode takich wymiarów wysokiej zmiennych podzielone na kategorie jest praktyce.</span><span class="sxs-lookup"><span data-stu-id="e145b-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="e145b-229">W szczególności firma Microsoft wyjaśnić i Wykaż metoda zaawansowanych, niezawodnych, zwana [uczenia z liczby](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) dla wydajne rozwiązania problemu ten problem.</span><span class="sxs-lookup"><span data-stu-id="e145b-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="e145b-230">Ta podsekcja możemy zakończyć analizując hello liczbę unikatowych wartości dla niektórych innych kategorii kolumn również.</span><span class="sxs-lookup"><span data-stu-id="e145b-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="e145b-231">Witaj zawartość [& #95 przykładowe; hive &#95; criteo &#95; unikatowy &#95; & #95 wartości wielu &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) są:</span><span class="sxs-lookup"><span data-stu-id="e145b-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="e145b-232">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="e145b-233">Ponownie widzimy, że z wyjątkiem Col20, wszystkie hello innych kolumn ma wiele unikatowych wartości.</span><span class="sxs-lookup"><span data-stu-id="e145b-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="e145b-234">Liczby wystąpień wspólnej par podzielone na kategorie zmiennych w zestawie danych train hello</span><span class="sxs-lookup"><span data-stu-id="e145b-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="e145b-235">liczby wystąpień wspólnej Hello par podzielone na kategorie zmiennych jest również przydatne.</span><span class="sxs-lookup"><span data-stu-id="e145b-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="e145b-236">To można ustalić przy użyciu kodu hello w [& #95 przykładowe; hive &#95; criteo &#95; sparowanego &#95; podzielone na kategorie &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="e145b-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="e145b-237">Firma Microsoft odwrócić liczby hello kolejności ich występowania i przyjrzyj się hello top 15 w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="e145b-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="e145b-238">Dzięki temu nam:</span><span class="sxs-lookup"><span data-stu-id="e145b-238">This gives us:</span></span>

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

## <span data-ttu-id="e145b-239"><a name="downsample"></a>Dół przykładowych zestawów danych powitania dla usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e145b-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="e145b-240">O eksplorowanych hello zestawów danych i sprawdzono, firma Microsoft może jak tego typu eksploracji dla zmiennych (takie jak kombinacje), możemy teraz dół hello próbek danych tak, aby firma Microsoft można tworzyć modele w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e145b-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="e145b-241">Odwołaj jest problem hello możemy skupić się na: podany zestaw atrybutów przykład (funkcja wartości z Col2 - Col40), możemy przewidzieć Jeśli Col1 jest 0 (nie kliknij) lub 1 (kliknij).</span><span class="sxs-lookup"><span data-stu-id="e145b-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="e145b-242">toodown przykładowe naszych pociągu i testowania zestawów danych too1% hello oryginalny rozmiar, możemy użyć funkcji macierzystej RAND() gałęzi.</span><span class="sxs-lookup"><span data-stu-id="e145b-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="e145b-243">Witaj dalej skryptu [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) robi to dla zestawu danych train hello:</span><span class="sxs-lookup"><span data-stu-id="e145b-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="e145b-244">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="e145b-245">Witaj skryptu [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; test &#95; dzień &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) zrobi to za dane testowe dzień\_22:</span><span class="sxs-lookup"><span data-stu-id="e145b-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="e145b-246">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="e145b-247">Na koniec hello skryptu [& #95 przykładowe; hive &#95; criteo &#95; próbkowanie &#95; test &#95; dzień &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) zrobi to za dane testowe dzień\_23:</span><span class="sxs-lookup"><span data-stu-id="e145b-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="e145b-248">Daje to:</span><span class="sxs-lookup"><span data-stu-id="e145b-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="e145b-249">O tym, możemy gotowe toouse próbkowany naszych dół nauczenia i przetestowania zestawów danych do tworzenia modeli w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e145b-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="e145b-250">Brak ważnych finalnych przed są dostarczane na tooAzure Machine Learning, czyli dotyczy hello liczba tabeli.</span><span class="sxs-lookup"><span data-stu-id="e145b-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="e145b-251">W następnej sekcji podrzędne hello omówiono to szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="e145b-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="e145b-252"><a name="count"></a>Krótkie omówienie hello liczba tabeli</span><span class="sxs-lookup"><span data-stu-id="e145b-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="e145b-253">Kilka kategorii zmienne widzieliśmy, mają bardzo duże wymiary.</span><span class="sxs-lookup"><span data-stu-id="e145b-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="e145b-254">W naszym przewodniku możemy przedstawić zaawansowane techniki, zwanej [uczenia z liczby](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode tych zmiennych w wydajny i niezawodny sposób.</span><span class="sxs-lookup"><span data-stu-id="e145b-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="e145b-255">Więcej informacji na temat tej metody jest hello łączem.</span><span class="sxs-lookup"><span data-stu-id="e145b-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="e145b-256">W tym przewodniku możemy skupić się na przy użyciu compact reprezentacje tooproduce liczba tabel wymiarów wysokiej funkcji podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="e145b-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="e145b-257">To nie jest hello tylko sposób tooencode podzielone na kategorie funkcje; Aby uzyskać więcej informacji na temat innych metod, można wyewidencjonować zainteresowanych użytkowników [co hot-encoding](http://en.wikipedia.org/wiki/One-hot) i [Tworzenie skrótu funkcji](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="e145b-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="e145b-258">toobuild liczba tabel w danych o liczbie hello, używamy danych hello hello folderu raw/liczba.</span><span class="sxs-lookup"><span data-stu-id="e145b-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="e145b-259">W hello modelowania sekcji zostanie przedstawiony użytkowników jak toobuild te liczby tabel podzielone na kategorie funkcji od podstaw lub toouse tabelę liczbę wstępnie skompilowanych dla ich eksploracji.</span><span class="sxs-lookup"><span data-stu-id="e145b-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="e145b-260">W jaki sposób, gdy firma Microsoft można znaleźć zbyt "wbudowana liczba tabel", możemy oznacza za pomocą hello liczba tabel, które firma Microsoft udostępnia.</span><span class="sxs-lookup"><span data-stu-id="e145b-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="e145b-261">Szczegółowe instrukcje dotyczące sposobu tooaccess te tabele znajdują się w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="e145b-262"><a name="aml"></a>Tworzenie modelu przy użyciu usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e145b-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="e145b-263">Nasz model budowania procesu w usłudze Azure Machine Learning obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e145b-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="e145b-264">Pobierz dane hello z tabele programu Hive w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e145b-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="e145b-265">Tworzenie eksperymentu hello: czyszczenie danych hello i featurize z liczby tabel</span><span class="sxs-lookup"><span data-stu-id="e145b-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="e145b-266">Kompilacja, pociągu i score hello model</span><span class="sxs-lookup"><span data-stu-id="e145b-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="e145b-267">Ocena hello modelu</span><span class="sxs-lookup"><span data-stu-id="e145b-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="e145b-268">Publikowanie hello model jako usługę sieci web</span><span class="sxs-lookup"><span data-stu-id="e145b-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="e145b-269">Teraz możemy modele gotowe toobuild w studio uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="e145b-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="e145b-270">Nasze dół próbki danych zostanie zapisany jako tabele programu Hive hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e145b-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="e145b-271">Używamy hello Azure Machine Learning **i zaimportuj dane** tooread modułu tych danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="e145b-272">Konto magazynu Hello poświadczenia tooaccess hello tego klastra znajdują się w jaki sposób.</span><span class="sxs-lookup"><span data-stu-id="e145b-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="e145b-273"><a name="step1"></a>Krok 1: Pobierz dane z tabel gałęzi do usługi Azure Machine Learning, za pomocą modułu i zaimportuj dane hello i wybrać go do eksperymentu uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="e145b-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="e145b-274">Najpierw wybrać **+ nowy** -> **EKSPERYMENTU** -> **pusty eksperyment**.</span><span class="sxs-lookup"><span data-stu-id="e145b-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="e145b-275">Następnie z hello **wyszukiwania** pole na górze hello w lewo, wyszukaj "Import Data".</span><span class="sxs-lookup"><span data-stu-id="e145b-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="e145b-276">Przeciąganie i upuszczanie hello **i zaimportuj dane** modułu w module hello toohello eksperymentu kanwy (hello środkowej części ekranu hello) toouse dla dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="e145b-277">Jest to jakie hello **i zaimportuj dane** wygląda jak podczas pobierania danych z tabeli Hive hello:</span><span class="sxs-lookup"><span data-stu-id="e145b-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Importuj dane pobiera dane](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="e145b-279">Dla hello **i zaimportuj dane** modułu, hello wartości parametrów hello, znajdujące się w hello grafiki są tylko przykładem hello sortowania wartości należy muszą tooprovide.</span><span class="sxs-lookup"><span data-stu-id="e145b-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="e145b-280">Poniżej przedstawiono pewne ogólne wskazówki na konfiguracji toofill hello parametr wyjściowy dla hello **i zaimportuj dane** modułu.</span><span class="sxs-lookup"><span data-stu-id="e145b-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="e145b-281">Wybierz "Zapytania Hive" **źródła danych**</span><span class="sxs-lookup"><span data-stu-id="e145b-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="e145b-282">W hello **zapytanie Hive bazy danych** polu Wybierz proste * FROM < Twojej\_bazy danych\_name.your\_tabeli\_nazwy >-jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="e145b-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="e145b-283">**Identyfikator URI serwera Hcatalog**: Jeśli klaster jest "abc", to po prostu: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="e145b-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="e145b-284">**Nazwa konta użytkownika Hadoop**: nazwa użytkownika hello wybrany w momencie hello oddanie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e145b-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="e145b-285">(Nie hello nazwa użytkownika dostępu zdalnego!)</span><span class="sxs-lookup"><span data-stu-id="e145b-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="e145b-286">**Hasło konta użytkownika Hadoop**: hello hasło dla nazwy użytkownika hello wybrany w momencie hello oddanie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e145b-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="e145b-287">(Nie hasła dostępu zdalnego Witaj!)</span><span class="sxs-lookup"><span data-stu-id="e145b-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="e145b-288">**Lokalizacja danych wyjściowych**: wybierz polecenie "Azure"</span><span class="sxs-lookup"><span data-stu-id="e145b-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="e145b-289">**Nazwa konta magazynu Azure**: hello konta magazynu skojarzone z klastrem hello</span><span class="sxs-lookup"><span data-stu-id="e145b-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="e145b-290">**Klucz konta magazynu Azure**: klucz hello hello konta magazynu skojarzone z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="e145b-291">**Nazwa kontenera Azure**: Jeśli nazwa klastra hello jest "abc", a następnie zazwyczaj jest to po prostu "abc",.</span><span class="sxs-lookup"><span data-stu-id="e145b-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="e145b-292">Raz hello **i zaimportuj dane** zakończeniu pobieranie danych (możesz zobaczyć hello zielony znacznik na powitania modułu), Zapisz te dane jako zestawu danych (o nazwie wybranych przez użytkownika).</span><span class="sxs-lookup"><span data-stu-id="e145b-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="e145b-293">Co to wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e145b-293">What this looks like:</span></span>

![Importuj dane zapisywanie danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="e145b-295">Kliknij prawym przyciskiem myszy hello output portu hello **i zaimportuj dane** modułu.</span><span class="sxs-lookup"><span data-stu-id="e145b-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="e145b-296">Takie działanie spowoduje wyświetlenie **Zapisz jako zestawu danych** opcji i **wizualizacja** opcji.</span><span class="sxs-lookup"><span data-stu-id="e145b-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="e145b-297">Witaj **wizualizacja** opcji, po kliknięciu wyświetla 100 wierszy danych hello, wraz ze prawym panelu, który jest przydatne w przypadku niektórych podsumowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="e145b-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="e145b-298">toosave danych, po prostu wybierz **Zapisz jako zestawu danych** i postępuj zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="e145b-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="e145b-299">tooselect dataset hello zapisywane do użycia w eksperymencie machine learning zlokalizować hello zestawów danych przy użyciu hello **wyszukiwania** pole pokazano powitania po rysunku.</span><span class="sxs-lookup"><span data-stu-id="e145b-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="e145b-300">Następnie po prostu typu out hello nazwa nadana hello dataset częściowo tooaccess go i przeciągnij hello zestawu danych na hello główny panel.</span><span class="sxs-lookup"><span data-stu-id="e145b-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="e145b-301">Upuszczenie go na panelu głównego hello zaznacza go do użycia w machine learning modelowania.</span><span class="sxs-lookup"><span data-stu-id="e145b-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Zestaw danych Drage na panelu głównego hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="e145b-303">W tym hello train i hello testu w zestawach danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="e145b-304">Należy również pamiętać nazwy bazy danych hello toouse i nazw tabel, których można użyć w tym celu.</span><span class="sxs-lookup"><span data-stu-id="e145b-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="e145b-305">wartości Hello używanych na rysunku hello są przeznaczone wyłącznie dla ilustracji purposes.* *</span><span class="sxs-lookup"><span data-stu-id="e145b-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="e145b-306"><a name="step2"></a>Krok 2: Tworzenie prostego eksperymentu w usłudze Azure Machine Learning toopredict kliknięć / nie kliknięcia</span><span class="sxs-lookup"><span data-stu-id="e145b-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="e145b-307">Nasze eksperymentu uczenia Maszynowego Azure wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e145b-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning eksperymentu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="e145b-309">Teraz omówione hello najważniejsze składniki z tego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="e145b-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="e145b-310">Dla przypomnienia potrzebujemy toodrag naszych zapisane nauczenia i przetestowania zestawy danych na kanwie eksperymentu tooour najpierw.</span><span class="sxs-lookup"><span data-stu-id="e145b-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="e145b-311">Brak danych</span><span class="sxs-lookup"><span data-stu-id="e145b-311">Clean Missing Data</span></span>
<span data-ttu-id="e145b-312">Witaj **Clean Missing Data** modułu jest sugeruje nazwa: go czyści brakujące dane w sposób, który może być określone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e145b-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="e145b-313">Trwa wyszukiwanie w tym module, widzimy to:</span><span class="sxs-lookup"><span data-stu-id="e145b-313">Looking into this module, we see this:</span></span>

![Wyczyść brakujące dane](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="e145b-315">W tym miejscu Wybraliśmy tooreplace wszystkie brakujące wartości od 0.</span><span class="sxs-lookup"><span data-stu-id="e145b-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="e145b-316">Istnieją inne opcje zostaną również, które są wyświetlane Analizując listę rozwijaną hello w hello module.</span><span class="sxs-lookup"><span data-stu-id="e145b-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="e145b-317">Inżynieria na powitania danych</span><span class="sxs-lookup"><span data-stu-id="e145b-317">Feature engineering on hello data</span></span>
<span data-ttu-id="e145b-318">Może istnieć miliony unikatowe wartości w przypadku niektórych funkcji podzielone na kategorie dużych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="e145b-319">Przy użyciu metod prosty przykład hot jeden kodowanie reprezentujący takich funkcji podzielone na kategorie wymiarów wysokiej jest całkowicie będzie niemożliwe.</span><span class="sxs-lookup"><span data-stu-id="e145b-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="e145b-320">W tym przewodniku zostaje przedstawiony sposób toouse liczba funkcji za pomocą wbudowanych toogenerate modułów uczenia maszynowego Azure compact reprezentacje tych wymiarów wysokiej zmiennych podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="e145b-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="e145b-321">Witaj wynik końcowy jest mniejszy rozmiar modelu, szkolenia szybsze i metryki wydajności, które są dość porównywalne toousing innych technik.</span><span class="sxs-lookup"><span data-stu-id="e145b-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="e145b-322">Kompilowanie zliczania transformacji</span><span class="sxs-lookup"><span data-stu-id="e145b-322">Building counting transforms</span></span>
<span data-ttu-id="e145b-323">Funkcje count toobuild, używamy hello **kompilacji zliczania przekształcenie** moduł, który jest dostępny w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e145b-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="e145b-324">Moduł Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e145b-324">hello module looks like this:</span></span>

<span data-ttu-id="e145b-325">![Utworzenie modułu zliczania przekształcenie](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![kompilacji zliczania przekształcenie modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="e145b-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e145b-326">W hello **liczba kolumn** , możemy wprowadź te kolumny Życzymy tooperform liczby.</span><span class="sxs-lookup"><span data-stu-id="e145b-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="e145b-327">Zazwyczaj są to (jak wspomniano) wymiarów wysokiej kolumny podzielone na kategorie.</span><span class="sxs-lookup"><span data-stu-id="e145b-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="e145b-328">Na początku hello wspomniano, tym hello Criteo dataset zawiera kolumny podzielone na kategorie 26: z Col15 tooCol40.</span><span class="sxs-lookup"><span data-stu-id="e145b-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="e145b-329">W tym miejscu możemy liczba na wszystkich z nich i zapewniają ich indeksów (z 15 too40 oddzielonych przecinkami, jak pokazano).</span><span class="sxs-lookup"><span data-stu-id="e145b-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="e145b-330">Moduł hello toouse w hello tryb MapReduce (odpowiedni dla dużych zestawów danych), możemy muszą uzyskać dostęp do klastra usługi HDInsight Hadoop tooan (powitalne używane jako eksploracji funkcji mogą być ponownie używane w tym celu również) i swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="e145b-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="e145b-331">Witaj poprzedniej ilustracjach jakie hello wypełniane wartości wygląda jak (Zastąp wartości hello ilustracyjną z tymi, które są istotne dla własnego przypadek użycia).</span><span class="sxs-lookup"><span data-stu-id="e145b-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Parametry modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="e145b-333">W powyższym rysunku hello, zostanie przedstawiony sposób tooenter hello danych wejściowych obiektu blob lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e145b-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="e145b-334">Ta lokalizacja zawiera dane hello zastrzeżone do tworzenia tabel liczba.</span><span class="sxs-lookup"><span data-stu-id="e145b-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="e145b-335">Po zakończeniu tego modułu hello transformacji dla można zapisać później prawym przyciskiem myszy modułu hello i wybierając hello **Zapisz jako transformacji** opcji:</span><span class="sxs-lookup"><span data-stu-id="e145b-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![Opcję "Zapisz jako transformacji"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="e145b-337">W Nasza architektura eksperymentu pokazanym powyżej hello zestawu danych "ytransform2" odpowiada dokładnie tooa zapisana liczba transformacji.</span><span class="sxs-lookup"><span data-stu-id="e145b-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="e145b-338">Hello pozostałej części tego eksperymentu, przyjęto założenie, że użyto czytnika hello **kompilacji zliczania przekształcenie** moduł na niektóre liczby toogenerate danych, a następnie może przy użyciu tych funkcji count toogenerate liczby na powitania pociągu i testowania zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="e145b-339">Wybieranie co tooinclude funkcje są liczone jako część pociągu hello i przetestować zbiory danych</span><span class="sxs-lookup"><span data-stu-id="e145b-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="e145b-340">Po mamy liczbą przekształcenie gotowe hello użytkownika można wybrać tooinclude jakie funkcje ich train i przetestować zestawów danych używających hello **zmodyfikować liczby parametrów tabeli** modułu.</span><span class="sxs-lookup"><span data-stu-id="e145b-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="e145b-341">Ten moduł zostanie przedstawiony tylko tutaj kompletności, ale w celu uproszczenia nie faktycznie jest używana w naszym doświadczeniu.</span><span class="sxs-lookup"><span data-stu-id="e145b-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modyfikowanie tabeli liczba parametrów](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="e145b-343">W takim przypadku jak widać, wybraliśmy toouse tylko hello dziennika prawdopodobieństwo i tooignore hello wycofania kolumny.</span><span class="sxs-lookup"><span data-stu-id="e145b-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="e145b-344">Parametry, takie jak hello odzyskiwanie bin progu, ile tooadd artykule poprzednich przykładach wygładzania, można również ustawić i czy toouse żadnych Laplacian hałasu lub nie.</span><span class="sxs-lookup"><span data-stu-id="e145b-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="e145b-345">Wszystkie te są zaawansowane funkcje i jest ona toobe zauważyć, że wartości domyślne hello są dobry punkt wyjścia dla użytkowników, którzy są nowy typ toothis generacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="e145b-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="e145b-346">Przekształcenia danych przed wygenerowaniem hello liczba funkcji</span><span class="sxs-lookup"><span data-stu-id="e145b-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="e145b-347">Teraz możemy skupić się na ważne punktu o Przekształcanie naszych train i przetestuj tooactually wcześniejszych danych generowania funkcji count.</span><span class="sxs-lookup"><span data-stu-id="e145b-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="e145b-348">Należy pamiętać, że istnieją dwa **wykonanie skryptu języka R** moduły używane przed stosujemy hello liczba transformacji tooour danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![Wykonanie skryptu języka R modułów](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="e145b-350">Poniżej przedstawiono skrypt języka R pierwszy hello:</span><span class="sxs-lookup"><span data-stu-id="e145b-350">Here is hello first R script:</span></span>

![Pierwszy skrypt języka R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="e145b-352">W ten skrypt języka R, możemy zmienić nazwę naszych toonames kolumny "Col1" za "Col40".</span><span class="sxs-lookup"><span data-stu-id="e145b-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="e145b-353">Jest to spowodowane przekształcenia liczba hello oczekuje nazwy w tym formacie.</span><span class="sxs-lookup"><span data-stu-id="e145b-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="e145b-354">W hello drugi skrypt języka R, możemy saldo hello dystrybucji między klasami dodatnie i ujemne (klasy 1 i 0 odpowiednio) przez klasę ujemna hello próbkowania.</span><span class="sxs-lookup"><span data-stu-id="e145b-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="e145b-355">Witaj R skrypt tutaj pokazuje, jak toodo to:</span><span class="sxs-lookup"><span data-stu-id="e145b-355">hello R script here shows how toodo this:</span></span>

![Drugi skrypt języka R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="e145b-357">W tym prostego skryptu języka R, używamy "pos\_minus\_współczynnik" hello tooset ilość równowagi między hello dodatnią i ujemną klasy hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="e145b-358">Jest to ważne, że toodo, ponieważ zwykle poprawy nierównowaga klasa ma zalety korzystania z klasyfikacji problemów w przypadku dystrybucji klasy hello niesymetryczna (odwołanie w tym przypadku mając klasy dodatnią 3.3% i 96.7% ujemna klasy).</span><span class="sxs-lookup"><span data-stu-id="e145b-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="e145b-359">Stosowania przekształcenia liczba hello na naszych danych</span><span class="sxs-lookup"><span data-stu-id="e145b-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="e145b-360">Ponadto można użyć hello **Zastosuj przekształcenie** tooapply modułu hello transformacje liczba na naszych pociągu i testowania zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="e145b-361">Ten moduł zostanie przekształcenia liczba hello zapisany co dane wejściowe i hello uczenia lub testowania zestawów danych, jak hello innych danych wejściowych i zwraca danych za pomocą funkcji count.</span><span class="sxs-lookup"><span data-stu-id="e145b-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="e145b-362">Przedstawiono tutaj:</span><span class="sxs-lookup"><span data-stu-id="e145b-362">It is shown here:</span></span>

![Zastosuj przekształcenie modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="e145b-364">Fragment wygląd hello liczba funkcji</span><span class="sxs-lookup"><span data-stu-id="e145b-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="e145b-365">Jest istotne toosee, jakie funkcje count hello wyglądać w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="e145b-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="e145b-366">W tym miejscu zostanie przedstawiony fragment to:</span><span class="sxs-lookup"><span data-stu-id="e145b-366">Here we show an excerpt of this:</span></span>

![Liczba funkcji](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="e145b-368">W tym fragmencie zostanie przedstawiony czy hello kolumn, które możemy zliczane na, możemy uzyskać liczby hello i dziennika prawdopodobieństwo w odpowiednich backoffs tooany dodanie.</span><span class="sxs-lookup"><span data-stu-id="e145b-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="e145b-369">Firma Microsoft są teraz gotowe toobuild modelu uczenia maszynowego Azure przy użyciu tych przekształcone zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="e145b-370">W następnej sekcji hello zostanie przedstawiony sposób można to zrobić.</span><span class="sxs-lookup"><span data-stu-id="e145b-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="e145b-371"><a name="step3"></a>Krok 3: Tworzenie, uczenie i score hello model</span><span class="sxs-lookup"><span data-stu-id="e145b-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="e145b-372">Wybór uczeń</span><span class="sxs-lookup"><span data-stu-id="e145b-372">Choice of learner</span></span>
<span data-ttu-id="e145b-373">Najpierw należy toochoose uczeń.</span><span class="sxs-lookup"><span data-stu-id="e145b-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="e145b-374">Możemy toouse przechodzenia drzewa decyzyjnego dwie klasy boosted jako naszych uczeń.</span><span class="sxs-lookup"><span data-stu-id="e145b-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="e145b-375">Poniżej przedstawiono hello domyślne opcje dla tego uczeń:</span><span class="sxs-lookup"><span data-stu-id="e145b-375">Here are hello default options for this learner:</span></span>

![Parametry Two-Class Boosted drzewa decyzyjnego](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="e145b-377">Nasze eksperymentu możemy będzie toochoose hello domyślne wartości.</span><span class="sxs-lookup"><span data-stu-id="e145b-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="e145b-378">Firma Microsoft należy pamiętać, że ten hello domyślne są zazwyczaj przydatne i podstaw szybkiego tooget dobry sposób na wydajność.</span><span class="sxs-lookup"><span data-stu-id="e145b-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="e145b-379">Na wydajność można poprawić przez profilach parametrów po wybraniu tooonce, do których masz linii bazowej.</span><span class="sxs-lookup"><span data-stu-id="e145b-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="e145b-380">Train hello model</span><span class="sxs-lookup"><span data-stu-id="e145b-380">Train hello model</span></span>
<span data-ttu-id="e145b-381">Szkolenia, możemy po prostu Wywołaj **Train Model** modułu.</span><span class="sxs-lookup"><span data-stu-id="e145b-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="e145b-382">Witaj dwie tooit dane wejściowe są uczeń Two-Class Boosted drzewa decyzyjnego hello i naszym zestawie danych pociągu.</span><span class="sxs-lookup"><span data-stu-id="e145b-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="e145b-383">To jest następujący:</span><span class="sxs-lookup"><span data-stu-id="e145b-383">This is shown here:</span></span>

![Train Model modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="e145b-385">Wynik hello modelu</span><span class="sxs-lookup"><span data-stu-id="e145b-385">Score hello model</span></span>
<span data-ttu-id="e145b-386">Gdy mamy uczonego modelu gotowe firma Microsoft tooscore na powitania testowania zestawu danych i tooevaluate jego wydajności.</span><span class="sxs-lookup"><span data-stu-id="e145b-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="e145b-387">Firma Microsoft to zrobić przy użyciu hello **Score Model** modułu pokazano powitania po rysunku, wraz z **Evaluate Model** modułu:</span><span class="sxs-lookup"><span data-stu-id="e145b-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Moduł Score Model (Generowanie wyników przez model)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="e145b-389"><a name="step4"></a>Krok 4: Ocena hello modelu</span><span class="sxs-lookup"><span data-stu-id="e145b-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="e145b-390">Wreszcie chcemy tooanalyze modelu wydajności.</span><span class="sxs-lookup"><span data-stu-id="e145b-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="e145b-391">W przypadku problemów klasyfikacji (binarnego) dwie klasy dobrej miary jest zazwyczaj, hello AUC.</span><span class="sxs-lookup"><span data-stu-id="e145b-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="e145b-392">toovisualize, możemy Podłączanie hello **Score Model** tooan modułu **Evaluate Model** modułu dla tego.</span><span class="sxs-lookup"><span data-stu-id="e145b-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="e145b-393">Kliknięcie przycisku **Visualize** na powitania **Evaluate Model** modułu daje grafiki, takie jak hello jednym następującego:</span><span class="sxs-lookup"><span data-stu-id="e145b-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Ocena modelu BDT modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="e145b-395">W danych binarnych (lub dwie klasy) klasyfikacji problemów, dobrym miara dokładności prognozy jest hello obszaru w krzywej (AUC).</span><span class="sxs-lookup"><span data-stu-id="e145b-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="e145b-396">W poniżej zostanie przedstawiony naszych wyników przy użyciu tego modelu w naszym zestawu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="e145b-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="e145b-397">tooget port wyjściowy powitania kliknij prawym przyciskiem myszy ten, hello **Evaluate Model** modułu, a następnie **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="e145b-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Wizualizuj modułu Evaluate Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="e145b-399"><a name="step5"></a>Krok 5: Opublikować hello model jako usługę sieci Web</span><span class="sxs-lookup"><span data-stu-id="e145b-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="e145b-400">toopublish możliwości Hello modelu uczenia maszynowego Azure jako usługi sieci web z co najmniej problemów jest przydatna funkcja dokonywania szeroko dostępne.</span><span class="sxs-lookup"><span data-stu-id="e145b-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="e145b-401">Po zakończeniu tej operacji, każdy użytkownik należy wywołania usługi sieci web toohello za dane wejściowe muszą prognoz dotyczących, czy usługa sieci web hello używa tooreturn modelu hello tych prognoz.</span><span class="sxs-lookup"><span data-stu-id="e145b-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="e145b-402">toodo, możemy najpierw zapisać uczonego modelu obiektu Trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="e145b-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="e145b-403">Jest to realizowane przez kliknięcie prawym przyciskiem myszy hello **Train Model** modułu i przy użyciu hello **Zapisz jako Uczonego modelu** opcji.</span><span class="sxs-lookup"><span data-stu-id="e145b-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="e145b-404">Następnie potrzebujemy toocreate dane wejściowe i wyjściowe portów dla naszej usługi sieci web:</span><span class="sxs-lookup"><span data-stu-id="e145b-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="e145b-405">port wejściowy przyjmującego hello sam formularz jako dane hello potrzebujemy prognoz dotyczących danych</span><span class="sxs-lookup"><span data-stu-id="e145b-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="e145b-406">port wyjściowy zwraca hello oceniane etykiety i hello skojarzone prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="e145b-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="e145b-407">Wybierz kilka wierszy danych dla portu wejściowego hello</span><span class="sxs-lookup"><span data-stu-id="e145b-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="e145b-408">Jest wygodną toouse **Zastosuj przekształcenie SQL** modułu tooselect tylko 10 wierszy tooserve jako hello portu dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="e145b-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="e145b-409">Wybierz tylko te wiersze danych dla naszych portu wejściowego przy użyciu zapytania SQL hello pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="e145b-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Port wejściowy danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="e145b-411">Usługa sieci Web</span><span class="sxs-lookup"><span data-stu-id="e145b-411">Web service</span></span>
<span data-ttu-id="e145b-412">Teraz możemy gotowe toorun małych eksperymentu, które mogą być używane toopublish naszej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="e145b-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="e145b-413">Generuj dane wejściowe dla usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e145b-413">Generate input data for webservice</span></span>
<span data-ttu-id="e145b-414">Krokiem zeroth ponieważ tabeli liczba hello jest duży, możemy wykonać kilka wierszy danych testowych i generowanie danych wyjściowych z jej z funkcji count.</span><span class="sxs-lookup"><span data-stu-id="e145b-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="e145b-415">Może to służyć jako formatu danych wejściowych hello naszej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e145b-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="e145b-416">To jest następujący:</span><span class="sxs-lookup"><span data-stu-id="e145b-416">This is shown here:</span></span>

![Utwórz BDT danych wejściowych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="e145b-418">Dla formatu danych wejściowych hello używamy teraz hello dane wyjściowe hello **Featurizer liczba** modułu.</span><span class="sxs-lookup"><span data-stu-id="e145b-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="e145b-419">Po zakończeniu uruchamiania to eksperymentu, Zapisz dane wyjściowe hello z hello **Featurizer liczba** modułu jako zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="e145b-420">Ten zestaw danych jest używany dla danych wejściowych hello w hello Usługa sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e145b-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="e145b-421">Ocenianie eksperymentu publikowania usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e145b-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="e145b-422">Najpierw zostanie przedstawiony to wygląda następująco.</span><span class="sxs-lookup"><span data-stu-id="e145b-422">First, we show what this looks like.</span></span> <span data-ttu-id="e145b-423">Struktura niezbędne Hello jest **Score Model** moduł, który akceptuje naszych obiekt uczonego modelu i kilka wierszy danych wejściowych, generowany w poprzednich krokach hello przy użyciu hello **Featurizer liczba** modułu.</span><span class="sxs-lookup"><span data-stu-id="e145b-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="e145b-424">Używamy tooproject "Wybieranie kolumn w zestawie danych" hello Scored etykiety i hello wynik prawdopodobieństwa.</span><span class="sxs-lookup"><span data-stu-id="e145b-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Wybieranie kolumn w zestawie danych](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="e145b-426">Zwróć uwagę, jak hello **Select Columns in Dataset** modułu może służyć do "filtrowanie" danych z zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e145b-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="e145b-427">Zostanie przedstawiony tutaj zawartość hello:</span><span class="sxs-lookup"><span data-stu-id="e145b-427">We show hello contents here:</span></span>

![Filtrowanie z hello Wybieranie kolumn w zestawie danych modułu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="e145b-429">tooget hello niebieski wejściowa i wyjściowa portów, należy po prostu kliknij **przygotowanie Usługa sieci Web** na powitania prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="e145b-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="e145b-430">Również uruchomienie tego eksperymentu pozwoli nam usługi sieci web hello toopublish: kliknij hello **OPUBLIKOWAĆ usługi sieci WEB** ikony w dolnej hello prawej, są wyświetlane tutaj:</span><span class="sxs-lookup"><span data-stu-id="e145b-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![Publikowanie usługi sieci Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="e145b-432">Po opublikowaniu usługi webservice hello uzyskujemy przekierowanego tooa strony, która wygląda w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="e145b-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Pulpit nawigacyjny usługi sieci Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="e145b-434">Po lewej stronie powitania przedstawia dwa łącza do usług sieci Web:</span><span class="sxs-lookup"><span data-stu-id="e145b-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="e145b-435">Witaj **żądanie/odpowiedź** usługi (lub rekordy zasobów) jest przeznaczony dla jednego prognoz i będziemy korzystać w tym workshop.</span><span class="sxs-lookup"><span data-stu-id="e145b-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="e145b-436">Witaj **BATCH EXECUTION** usługi (BES) służy do przewidywania partii i wymaga się, że prognoz toomake dane wejściowe, używane hello znajdują się w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e145b-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="e145b-437">Kliknięcie łącza hello **żądanie/odpowiedź** trwa tooa strona, która udostępnia wstępnie puszkach kodu w języku C#, python i R. Ten kod można łatwo dokonywania toohello wywołania usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e145b-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="e145b-438">Należy zauważyć, że ten klucz interfejsu API na tej stronie powitania musi toobe używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e145b-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="e145b-439">Jest wygodne toocopy tego python code za pośrednictwem tooa nowej komórki w notesie IPython hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="e145b-440">W tym miejscu zostanie przedstawiony segment kodu języka python z hello poprawny klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e145b-440">Here we show a segment of python code with hello correct API key.</span></span>

![Kod języka Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="e145b-442">Należy pamiętać, możemy zastąpić hello domyślny klucz interfejsu API z kluczem interfejsu API naszych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e145b-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="e145b-443">Kliknięcie przycisku **Uruchom** w tej komórce w IPython notesu daje powitania po odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="e145b-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![IPython odpowiedzi](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="e145b-445">Widzimy, że dla hello dwóch testowych przykłady, które firma Microsoft pytania (w ramach JSON hello hello skrypt w języku python), uzyskujemy wstecz odpowiedzi w postaci hello "Scored Labels Scored Probabilities".</span><span class="sxs-lookup"><span data-stu-id="e145b-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="e145b-446">Należy pamiętać, że w takim przypadku Wybraliśmy wartości domyślne hello kodu wstępnie zdefiniowanym hello zapewnia (0 dla wszystkich kolumn liczbowych i ciąg hello "value" dla wszystkich kolumn podzielone na kategorie).</span><span class="sxs-lookup"><span data-stu-id="e145b-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="e145b-447">Zakończenie nasze wskazówki end-to-end przedstawiający sposób na dużą skalę zestawu danych toohandle przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e145b-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="e145b-448">Firma Microsoft wprowadzenie terabajtów danych, utworzyć modelu prognozy i wdrożyć go jako usługę sieci web w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="e145b-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

