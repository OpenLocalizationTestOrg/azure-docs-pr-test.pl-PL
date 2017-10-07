---
title: "Skalowalna nauki danych z usługi Azure Data Lake: wskazówki end-to-end | Dokumentacja firmy Microsoft"
description: "Jak toouse usługi Azure Data Lake toodo binarnego i eksploracja klasyfikacji danych zadań w zestawie danych."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="e045b-103">Skalowalna nauki danych z usługi Azure Data Lake: wskazówki end-to-end</span><span class="sxs-lookup"><span data-stu-id="e045b-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="e045b-104">W tym przewodniku przedstawiono sposób toouse usługi Azure Data Lake toodo Eksplorowanie danych oraz zadania klasyfikacji binarnej na próbkę hello NYC taksówki podróży i taryfy toopredict zestawu danych czy Porada zostanie zwrócona w klasie.</span><span class="sxs-lookup"><span data-stu-id="e045b-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="e045b-105">Przeprowadza użytkownika przez kroki hello hello [proces nauki danych zespołu](http://aka.ms/datascienceprocess)end-to- end, z szkolenia toomodel pozyskiwania danych, a następnie toohello wdrożenia usługi sieci web, która publikuje hello modelu.</span><span class="sxs-lookup"><span data-stu-id="e045b-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="e045b-106">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e045b-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="e045b-107">Witaj [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) ma wszystkie toomake wymagane możliwości hello go łatwo toostore służące danych dowolnego rozmiar, kształt i szybkość i tooconduct przetwarzania danych, zaawansowane analizy i machine learning modelowania o wysokiej skalowalności w ekonomiczny sposób.</span><span class="sxs-lookup"><span data-stu-id="e045b-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="e045b-108">Opłaty są naliczane za poszczególne zadania wykonywane tylko wtedy, gdy dane są rzeczywiście przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="e045b-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="e045b-109">Azure Data Lake Analytics obejmuje U-SQL, języka, że mieszanka hello deklaratywne rodzaj SQL z wszechstronnymi możliwościami hello C# tooprovide skalowalne rozproszone możliwości zapytania.</span><span class="sxs-lookup"><span data-stu-id="e045b-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="e045b-110">Włącza tooprocess danych niestrukturalnych przy zastosowaniu schematu na odczyt, wstawianie niestandardowej logiki i zdefiniowanych przez użytkownika (UDF) działa i zawiera rozszerzalności tooenable przeprowadzać kontrolę nad jak tooexecute na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="e045b-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="e045b-111">toolearn więcej informacji na temat zasady projektowania klas hello za U-SQL, zobacz [programu Visual Studio w blogu](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="e045b-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="e045b-112">Usługa Data Lake Analytics to także kluczowa część pakietu Cortana Analytics współdziałająca z usługami Azure SQL Data Warehouse, Power BI i Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e045b-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="e045b-113">Zapewnia dane big data pełnej chmury i platformy zaawansowana analityka.</span><span class="sxs-lookup"><span data-stu-id="e045b-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="e045b-114">W tym przewodniku rozpoczyna się od opisu hello warunki wstępne i zasobów, które są potrzebne toocomplete hello zadania związane z usługi Data Lake Analytics tworzą hello w procesie nauki danych i w jaki sposób tooinstall je.</span><span class="sxs-lookup"><span data-stu-id="e045b-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="e045b-115">Następnie przedstawiono hello etapy przetwarzania danych przy użyciu języka U-SQL i stwierdza, pokazując jak toouse Python i Hive z toobuild Azure Machine Learning Studio i wdrażanie modeli predykcyjnych hello.</span><span class="sxs-lookup"><span data-stu-id="e045b-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="e045b-116">U-SQL i programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e045b-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="e045b-117">W tym przewodniku zaleca przy użyciu programu Visual Studio tooedit U-SQL skrypty tooprocess hello dataset.</span><span class="sxs-lookup"><span data-stu-id="e045b-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="e045b-118">skryptów U-SQL Hello są opisane w tym miejscu i dostępne w oddzielnym pliku.</span><span class="sxs-lookup"><span data-stu-id="e045b-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="e045b-119">proces Hello obejmuje wprowadzania, badać i hello dane próbkowania.</span><span class="sxs-lookup"><span data-stu-id="e045b-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="e045b-120">Pokazuje też, jak toorun U-SQL inicjowanych przez skrypty zadania z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="e045b-121">Tabele programu hive są tworzone dla danych hello w skojarzonych budynku hello toofacilitate klastra usługi HDInsight i wdrażania modelu klasyfikacji binarnej w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e045b-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="e045b-122">Python</span><span class="sxs-lookup"><span data-stu-id="e045b-122">Python</span></span>
<span data-ttu-id="e045b-123">Ten przewodnik zawiera również sekcja, która przedstawia sposób toobuild i wdrażanie modelu predykcyjnego przy użyciu języka Python w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e045b-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="e045b-124">Udostępniamy notesu Jupyter z hello skrypty języka Python dla tych kroków w tym procesie.</span><span class="sxs-lookup"><span data-stu-id="e045b-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="e045b-125">Witaj notesu zawiera kod niektóre procedury engineering dodatkowych funkcji i modeli konstrukcji, takie jak wieloklasowej klasyfikacji i regresji modelowania Ponadto model klasyfikacji binarnej toohello opisana w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="e045b-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="e045b-126">zadanie regresji Hello jest toopredict hello ilość Porada hello na podstawie innych funkcji poradę.</span><span class="sxs-lookup"><span data-stu-id="e045b-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="e045b-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e045b-127">Azure Machine Learning</span></span>
<span data-ttu-id="e045b-128">Azure Machine Learning Studio jest używane toobuild i wdrażanie modeli predykcyjnych hello.</span><span class="sxs-lookup"><span data-stu-id="e045b-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="e045b-129">Jest to realizowane przy użyciu dwóch metod: najpierw ze skryptami języka Python, a następnie tabele programu Hive w klastrze usługi HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="e045b-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="e045b-130">Skrypty</span><span class="sxs-lookup"><span data-stu-id="e045b-130">Scripts</span></span>
<span data-ttu-id="e045b-131">Tylko hello główne kroki zostały opisane w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="e045b-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="e045b-132">Możesz pobrać pełną hello **skrypt U-SQL** i **notesu Jupyter** z [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="e045b-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e045b-133">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e045b-133">Prerequisites</span></span>
<span data-ttu-id="e045b-134">Przed rozpoczęciem tych tematów, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e045b-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="e045b-135">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-135">An Azure subscription.</span></span> <span data-ttu-id="e045b-136">Jeśli nie masz już jeden, zobacz [Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e045b-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e045b-137">[Zalecane] Program Visual Studio 2013 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="e045b-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="e045b-138">Jeśli nie już masz jeden z tych wersji, możesz pobrać bezpłatną wersję społeczności z [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="e045b-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="e045b-139">Zamiast programu Visual Studio umożliwia także zapytań usługi Azure Data Lake toosubmit hello w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="e045b-140">Firma Microsoft udostępni instrukcje dotyczące sposobu toodo tak zarówno z programem Visual Studio, jak i w portalu hello w sekcji hello zatytułowany **przetwarzania danych w języku U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="e045b-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="e045b-141">Przygotowanie środowiska nauki danych dla usługi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e045b-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="e045b-142">środowisko nauki tooprepare hello danych w ramach tego przewodnika tworzenia hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="e045b-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="e045b-143">Azure Data Lake — magazyn (ADLS)</span><span class="sxs-lookup"><span data-stu-id="e045b-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="e045b-144">Usługi Azure Data Lake Analytics (ADLA)</span><span class="sxs-lookup"><span data-stu-id="e045b-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="e045b-145">Konto magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e045b-145">Azure Blob storage account</span></span>
* <span data-ttu-id="e045b-146">Konto usługi Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e045b-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="e045b-147">Usługi Azure Data Lake Tools dla programu Visual Studio (zalecane)</span><span class="sxs-lookup"><span data-stu-id="e045b-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="e045b-148">Ta sekcja zawiera instrukcje na temat toocreate tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="e045b-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="e045b-149">Jeśli wybierzesz toouse tabele programu Hive z usługi Azure Machine Learning, zamiast Python, toobuild modelu, konieczne będzie również tooprovision klastra usługi HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="e045b-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="e045b-150">Ta procedura alternatywne w opisanego w hello odpowiedniej sekcji poniżej.</span><span class="sxs-lookup"><span data-stu-id="e045b-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="e045b-151">Witaj **Azure Data Lake Store** można tworzyć zarówno oddzielnie lub po utworzeniu hello **Azure Data Lake Analytics** jako hello domyślny magazyn.</span><span class="sxs-lookup"><span data-stu-id="e045b-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="e045b-152">Instrukcje odwołuje się do tworzenia tych zasobów oddzielnie poniżej, ale hello konta magazynu usługi Data Lake muszą nie można utworzyć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="e045b-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="e045b-153">Tworzenie usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e045b-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="e045b-154">Tworzenie ADLS z hello [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e045b-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="e045b-155">Aby uzyskać więcej informacji, zobacz [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e045b-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="e045b-156">Należy się tooset się hello tożsamość usługi AAD klastra w hello **źródła danych** bloku hello **konfiguracji opcjonalnej** bloku opisane istnieje.</span><span class="sxs-lookup"><span data-stu-id="e045b-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="e045b-158">Tworzenie konta usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e045b-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="e045b-159">Tworzenie konta usługi ADLA z hello [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e045b-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="e045b-160">Aby uzyskać więcej informacji, zobacz [samouczek: wprowadzenie do usługi Azure Data Lake Analytics przy użyciu portalu Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e045b-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="e045b-162">Tworzenie konta magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e045b-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="e045b-163">Tworzenie konta magazynu obiektów Blob platformy Azure z hello [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e045b-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="e045b-164">Aby uzyskać więcej informacji, zobacz hello Utwórz konto magazynu w sekcji [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e045b-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="e045b-166">Konfigurowanie konta usługi Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e045b-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="e045b-167">Zaloguj się w górę/w usłudze Azure Machine Learning Studio z hello [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) strony.</span><span class="sxs-lookup"><span data-stu-id="e045b-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="e045b-168">Polecenie hello **Rozpocznij teraz** przycisk, a następnie wybierz pozycję "Wolnego obszaru roboczego" lub "Standardowe obszaru roboczego".</span><span class="sxs-lookup"><span data-stu-id="e045b-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="e045b-169">Dzięki temu będzie stanie toocreate eksperymentów w Studio uczenia Maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="e045b-170">Zainstaluj usługi Azure Data Lake Tools [zalecane]</span><span class="sxs-lookup"><span data-stu-id="e045b-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="e045b-171">Zainstaluj usługi Azure Data Lake Tools dla używanej wersji programu Visual Studio z [Azure Data Lake Tools dla programu Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="e045b-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="e045b-173">Po pomyślnym zainstalowaniu hello otwarcia programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e045b-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="e045b-174">Witaj usługi Data Lake kartę hello menu u góry hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="e045b-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="e045b-175">Zasobów platformy Azure powinny być wyświetlane w lewym panelu powitania po zalogowaniu do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="e045b-177">Witaj NYC taksówki rund w zestawie danych</span><span class="sxs-lookup"><span data-stu-id="e045b-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="e045b-178">Witaj zestaw danych użyliśmy tutaj jest publicznie dostępnych zestawu danych--hello [dataset rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="e045b-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="e045b-179">Hello podróży taksówki NYC danych składa się z około 20GB skompresowanego plików CSV (~ 48GB nieskompresowane), rejestrowanie ponad milion 173 poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży.</span><span class="sxs-lookup"><span data-stu-id="e045b-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="e045b-180">Każdy rekord podróży zawiera hello odbiór i przyjmowania lokalizacje i godziny anonimowe hack numer licencji (sterownik) i hello numer Medalionu (taksówki jego unikatowy identyfikator).</span><span class="sxs-lookup"><span data-stu-id="e045b-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="e045b-181">Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:</span><span class="sxs-lookup"><span data-stu-id="e045b-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="e045b-182">Witaj "trip_data" CSV zawiera szczegóły podróży, takie jak liczba pasażerów, pobranie i punkty dropoff czas trwania podróży i długość podróży.</span><span class="sxs-lookup"><span data-stu-id="e045b-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e045b-183">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="e045b-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="e045b-184">Witaj "trip_fare" CSV zawiera szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej.</span><span class="sxs-lookup"><span data-stu-id="e045b-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="e045b-185">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="e045b-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e045b-186">Hello unikatowy kluczy toojoin podróży\_danych i podróży\_taryfy składa się z następujących trzech pól hello: Medalionu, hack\_licencji i pobrania\_daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="e045b-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="e045b-187">pliki CSV raw Hello jest możliwy z obiektu blob magazynu Azure publicznego.</span><span class="sxs-lookup"><span data-stu-id="e045b-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="e045b-188">Witaj skryptu U-SQL dla tego sprzężenia jest hello [łączenia tabel podróży i taryfy](#join) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e045b-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="e045b-189">Przetwarzaj dane w języku U-SQL</span><span class="sxs-lookup"><span data-stu-id="e045b-189">Process data with U-SQL</span></span>
<span data-ttu-id="e045b-190">zadania przetwarzania danych Hello przedstawione w tej sekcji obejmują wprowadzania, sprawdzanie jakości eksploracji i hello dane próbkowania.</span><span class="sxs-lookup"><span data-stu-id="e045b-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="e045b-191">Również zostanie przedstawiony sposób toojoin podróży i taryfy tabel.</span><span class="sxs-lookup"><span data-stu-id="e045b-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="e045b-192">sekcja końcowego Hello zawiera wykonywania zadania przy użyciu skryptu U-SQL z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="e045b-193">Oto łącza podsekcji tooeach:</span><span class="sxs-lookup"><span data-stu-id="e045b-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="e045b-194">Wprowadzanie danych: odczytać danych z obiektu blob publiczny</span><span class="sxs-lookup"><span data-stu-id="e045b-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="e045b-195">Kontrola jakości danych</span><span class="sxs-lookup"><span data-stu-id="e045b-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="e045b-196">Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="e045b-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="e045b-197">Dołącz do tabel podróży i taryfy</span><span class="sxs-lookup"><span data-stu-id="e045b-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="e045b-198">Próbkowanie danych</span><span class="sxs-lookup"><span data-stu-id="e045b-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="e045b-199">Uruchamianie zadań U-SQL</span><span class="sxs-lookup"><span data-stu-id="e045b-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="e045b-200">skryptów U-SQL Hello są opisane w tym miejscu i dostępne w oddzielnym pliku.</span><span class="sxs-lookup"><span data-stu-id="e045b-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="e045b-201">Możesz pobrać pełną hello **skryptów U-SQL** z [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="e045b-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="e045b-202">tooexecute U-SQL, Otwórz program Visual Studio, kliknij przycisk **Plik--> Nowa--> Projekt**, wybierz **projektu U-SQL**, nazw i zapisz go w folderze tooa.</span><span class="sxs-lookup"><span data-stu-id="e045b-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="e045b-204">Jest możliwe toouse hello Azure Portal tooexecute U-SQL zamiast programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e045b-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="e045b-205">Można znaleźć toohello zasobów usługi Azure Data Lake Analytics w portalu hello i przesyłania zapytań bezpośrednio jako ilustrowane w powitania po rysunku.</span><span class="sxs-lookup"><span data-stu-id="e045b-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="e045b-207"><a name="ingest"></a>Wprowadzanie danych: Odczyt danych z obiektu blob publiczny</span><span class="sxs-lookup"><span data-stu-id="e045b-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="e045b-208">Witaj lokalizację danych hello w hello obiektów blob platformy Azure jest określany jako  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  i wyodrębniona przy użyciu **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="e045b-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="e045b-209">Podstawić własną nazwę kontenera i nazwy konta magazynu w następujących skryptów dla container_name@blob_storage_account_name hello wasb adresu.</span><span class="sxs-lookup"><span data-stu-id="e045b-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="e045b-210">Ponieważ nazwy plików hello znajdują się w tym samym formacie, możemy użyć **podróży\_data_ {\*\}CSV** tooread we wszystkich plikach 12 podróży.</span><span class="sxs-lookup"><span data-stu-id="e045b-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="e045b-211">Ponieważ w pierwszym wierszu hello nagłówki, możemy muszą tooremove hello nagłówków, a następnie zmień typy kolumn do nich odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="e045b-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="e045b-212">Możemy zapisać hello przetworzonych danych tooAzure usługi Data Lake Storage przy użyciu **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**przy użyciu konta magazynu obiektów Blob _ lub tooAzure  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="e045b-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="e045b-213">Firma Microsoft może odczytywać podobnie w zestawach danych taryfy hello.</span><span class="sxs-lookup"><span data-stu-id="e045b-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="e045b-214">Azure Data Lake Store kliknij prawym przyciskiem myszy, wybierz polecenie toolook danych w **Azure Portal--> Eksploratora danych** lub **Eksploratora plików** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e045b-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="e045b-217"><a name="quality"></a>Kontrola jakości danych</span><span class="sxs-lookup"><span data-stu-id="e045b-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="e045b-218">Po odczytano podróży i taryfy tabel w kontroli jakości danych może odbywać się w następujący sposób hello.</span><span class="sxs-lookup"><span data-stu-id="e045b-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="e045b-219">Hello co pliki CSV można magazynu obiektów Blob tooAzure danych wyjściowych lub usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e045b-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="e045b-220">Znajdź liczbę hello medallions i unikatowy numer medallions:</span><span class="sxs-lookup"><span data-stu-id="e045b-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e045b-221">Znajdź te medallions, w których zastosowano więcej niż 100 rund:</span><span class="sxs-lookup"><span data-stu-id="e045b-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e045b-222">Znajdź te nieprawidłowe rekordy pod względem pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="e045b-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e045b-223">Znajdź brakujące wartości dla niektórych zmiennych:</span><span class="sxs-lookup"><span data-stu-id="e045b-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="e045b-224"><a name="explore"></a>Eksploracja danych</span><span class="sxs-lookup"><span data-stu-id="e045b-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="e045b-225">Możemy niektórych tooget Eksploracja danych lepszego zrozumienia hello danych.</span><span class="sxs-lookup"><span data-stu-id="e045b-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="e045b-226">Znajdź hello dystrybucji rund Przechylony i Przechylony:</span><span class="sxs-lookup"><span data-stu-id="e045b-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e045b-227">Znajdź dystrybucji hello kwoty Porada wartościami odcięty: 0,5,10 i 20 kwoty.</span><span class="sxs-lookup"><span data-stu-id="e045b-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e045b-228">Znajdź podstawowe dane statystyczne odległości podróży:</span><span class="sxs-lookup"><span data-stu-id="e045b-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="e045b-229">Znajdź percentylu hello odległości podróży:</span><span class="sxs-lookup"><span data-stu-id="e045b-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="e045b-230"><a name="join"></a>Dołącz do tabel podróży i taryfy</span><span class="sxs-lookup"><span data-stu-id="e045b-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="e045b-231">Mogą zostać sprzężone tabele podróży i taryfy Medalionu, hack_license i pickup_time.</span><span class="sxs-lookup"><span data-stu-id="e045b-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="e045b-232">Dla każdego poziomu liczby pasażerów obliczyć hello liczbę rekordów, porada średnia kwota, odchylenie kwoty Porada stopień podróży Przechylony.</span><span class="sxs-lookup"><span data-stu-id="e045b-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="e045b-233"><a name="sample"></a>Próbkowanie danych</span><span class="sxs-lookup"><span data-stu-id="e045b-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="e045b-234">Najpierw możemy losowo wybierać 0,1% hello danych z tabeli sprzężonych hello:</span><span class="sxs-lookup"><span data-stu-id="e045b-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="e045b-235">Następnie przejdziemy stratyfikowana próbkowania przez binarny tip_class zmiennych:</span><span class="sxs-lookup"><span data-stu-id="e045b-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="e045b-236"><a name="run"></a>Uruchamianie zadań U-SQL</span><span class="sxs-lookup"><span data-stu-id="e045b-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="e045b-237">Po zakończeniu edycji skryptów U-SQL, możesz przesłać je toohello serwera przy użyciu konta usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e045b-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="e045b-238">Kliknij przycisk **usługi Data Lake**, **Prześlij zadanie**, wybierz użytkownika **konta usługi Analytics**, wybierz **równoległości**i kliknij przycisk **przesyłania**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="e045b-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="e045b-240">Gdy zadanie hello jest pomyślnie spełnione, hello stan zadania będą wyświetlane w programie Visual Studio do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="e045b-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="e045b-241">Po zakończeniu zadania hello może nawet powtarzania hello zadania wykonywania procesu i sprawdź hello bottleneck tooimprove kroki wydajność zadania.</span><span class="sxs-lookup"><span data-stu-id="e045b-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="e045b-242">Można także przejść tooAzure Portal toocheck hello stan zadań U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e045b-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="e045b-245">Teraz można sprawdzić pliki wyjściowe hello w magazynie obiektów Blob Azure lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="e045b-246">Dla naszych modelowania w następnym kroku hello użyjemy hello uporządkować przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="e045b-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="e045b-249">Tworzenie i wdrażanie modeli w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e045b-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="e045b-250">Przedstawiony dwie opcje dostępne dla Ciebie toopull danych do usługi Azure Machine Learning toobuild i</span><span class="sxs-lookup"><span data-stu-id="e045b-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="e045b-251">W pierwszej opcji hello, możesz użyć danych hello próbkowany została zapisana tooan obiektów Blob platformy Azure (w hello **danych próbkowania** kroku powyżej) i Python toobuild i wdrażanie modeli z usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e045b-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="e045b-252">W drugiej opcji hello zapytaniu hello dotyczącym danych w usłudze Azure Data Lake bezpośrednio za pomocą zapytań programu Hive.</span><span class="sxs-lookup"><span data-stu-id="e045b-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="e045b-253">Ta opcja wymaga utworzenia nowego klastra usługi HDInsight, lub użyj istniejącego klastra usługi HDInsight, gdzie hello gałąź Tabele toohello punktu taksówki NY danych w usłudze Azure Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="e045b-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="e045b-254">Omówiono obie te opcje poniżej.</span><span class="sxs-lookup"><span data-stu-id="e045b-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="e045b-255">Opcja 1: Użyj Python toobuild i wdrażanie modeli uczenia maszyny</span><span class="sxs-lookup"><span data-stu-id="e045b-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="e045b-256">toobuild i wdrażanie modeli uczenia komputera przy użyciu języka Python, tworzenie notesu Jupyter na komputerze lokalnym lub w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e045b-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="e045b-257">Witaj notesu Jupyter podanego w [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) zawiera hello tooexplore pełny kod, wizualizację danych, funkcja zespołu inżynieryjnego, modelowania i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e045b-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="e045b-258">W tym artykule zostanie przedstawiony tylko modelowania hello i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e045b-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="e045b-259">Importuj biblioteki języka Python</span><span class="sxs-lookup"><span data-stu-id="e045b-259">Import Python libraries</span></span>
<span data-ttu-id="e045b-260">W kolejności toorun hello przykładowe notesu Jupyter lub hello pliku skryptu języka Python, hello następujące pakiety Python niezbędne.</span><span class="sxs-lookup"><span data-stu-id="e045b-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="e045b-261">Jeśli używasz usługi uczenie maszynowe Azure notesu hello te pakiety zostały wstępnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="e045b-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="e045b-262">Przeczytaj hello danych z obiektu blob</span><span class="sxs-lookup"><span data-stu-id="e045b-262">Read in hello data from blob</span></span>
* <span data-ttu-id="e045b-263">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="e045b-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="e045b-264">Odczytu w postaci tekstu</span><span class="sxs-lookup"><span data-stu-id="e045b-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="e045b-266">Dodaj nazwy kolumn i oddziel kolumn</span><span class="sxs-lookup"><span data-stu-id="e045b-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="e045b-267">Zmień toonumeric niektóre kolumny</span><span class="sxs-lookup"><span data-stu-id="e045b-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="e045b-268">Tworzenie modeli uczenia maszyny</span><span class="sxs-lookup"><span data-stu-id="e045b-268">Build machine learning models</span></span>
<span data-ttu-id="e045b-269">W tym miejscu budujemy toopredict model klasyfikacji binarnej czy podróży jest Przechylony lub nie.</span><span class="sxs-lookup"><span data-stu-id="e045b-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="e045b-270">W hello notesu Jupyter można znaleźć inne dwa modele: wieloklasowej klasyfikacji i regresji modeli.</span><span class="sxs-lookup"><span data-stu-id="e045b-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="e045b-271">Najpierw musimy toocreate fikcyjny zmiennych, które mogą być używane w scikit — Dowiedz się modeli</span><span class="sxs-lookup"><span data-stu-id="e045b-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="e045b-272">Utwórz ramkę danych dla hello modelowania</span><span class="sxs-lookup"><span data-stu-id="e045b-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="e045b-273">Uczenie i testowanie 60 40 podziału</span><span class="sxs-lookup"><span data-stu-id="e045b-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="e045b-274">Regresja logistyczna w zestawie szkolenia</span><span class="sxs-lookup"><span data-stu-id="e045b-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="e045b-275">Wynik testowania zestawu danych</span><span class="sxs-lookup"><span data-stu-id="e045b-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="e045b-276">Oblicz metryki oceny</span><span class="sxs-lookup"><span data-stu-id="e045b-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="e045b-277">Tworzenie interfejsu API usługi sieci Web i używać go w języku Python</span><span class="sxs-lookup"><span data-stu-id="e045b-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="e045b-278">Chcemy maszyny hello toooperationalize uczenie modelu po został skompilowany.</span><span class="sxs-lookup"><span data-stu-id="e045b-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="e045b-279">W tym miejscu używamy modelu binarnego logistyczna hello jako przykład.</span><span class="sxs-lookup"><span data-stu-id="e045b-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="e045b-280">Upewnij się, że scikit hello — Dowiedz się więcej wersji w komputerze lokalnym jest 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="e045b-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="e045b-281">Jeśli używasz usługi Azure ML studio usługi nie masz tooworry na ten temat.</span><span class="sxs-lookup"><span data-stu-id="e045b-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="e045b-282">Znajdź poświadczenia obszar roboczy z usługi Azure ML studio ustawień.</span><span class="sxs-lookup"><span data-stu-id="e045b-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="e045b-283">W usłudze Azure Machine Learning Studio, kliknij przycisk **ustawienia** --> **nazwa** --> **tokeny autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="e045b-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![C3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="e045b-285">Tworzenie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e045b-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="e045b-286">Pobieranie poświadczeń usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="e045b-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="e045b-287">Wywołanie interfejsu API usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e045b-287">Call Web service API.</span></span> <span data-ttu-id="e045b-288">Masz toowait 5 – 10 sekund po hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="e045b-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="e045b-289">Opcja 2: Tworzenie i wdrażanie modeli bezpośrednio w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e045b-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="e045b-290">Azure Machine Learning Studio można odczytać dane bezpośrednio z usługi Azure Data Lake Store można toocreate używane i wdrażanie modeli.</span><span class="sxs-lookup"><span data-stu-id="e045b-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="e045b-291">Ta metoda używa tabeli programu Hive, który wskazuje na hello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e045b-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="e045b-292">Wymaga to udostępniane oddzielny klaster Azure HDInsight, na które hello Hive tabela została utworzona.</span><span class="sxs-lookup"><span data-stu-id="e045b-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="e045b-293">Witaj, jak następujące sekcje Pokaż toodo to.</span><span class="sxs-lookup"><span data-stu-id="e045b-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="e045b-294">Tworzenie klastra usługi HDInsight w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e045b-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="e045b-295">Tworzenie klastra usługi HDInsight (Linux) z hello [Azure Portal](http://portal.azure.com). Aby uzyskać więcej informacji, zobacz hello **tworzenia klastra usługi HDInsight z tooAzure dostępu do usługi Data Lake Store** sekcji [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e045b-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="e045b-297">Tworzenie tabeli Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e045b-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="e045b-298">Teraz utworzymy używana w usłudze Azure Machine Learning Studio w hello klastra usługi HDInsight przy użyciu hello danych przechowywanych w usłudze Azure Data Lake Store w poprzednim kroku hello toobe tabel Hive.</span><span class="sxs-lookup"><span data-stu-id="e045b-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="e045b-299">Przejdź toohello właśnie utworzony klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e045b-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="e045b-300">Kliknij przycisk **ustawienia** --> **właściwości** --> **klastra tożsamości w usłudze AAD** --> **dostępem ADLS**, Upewnij się, że konto usługi Azure Data Lake Store zostanie dodane na liście hello z odczytu, zapisu i wykonywania praw.</span><span class="sxs-lookup"><span data-stu-id="e045b-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="e045b-302">Następnie kliknij przycisk **pulpitu nawigacyjnego** dalej toohello **ustawienia** przycisk i okno zostanie wyskakujące.</span><span class="sxs-lookup"><span data-stu-id="e045b-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="e045b-303">Kliknij przycisk **Hive View** w hello prawym górnym rogu strony hello i zostanie wyświetlony hello **edytora zapytań**.</span><span class="sxs-lookup"><span data-stu-id="e045b-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="e045b-306">Wklej powitania po toocreate skrypty Hive tabeli.</span><span class="sxs-lookup"><span data-stu-id="e045b-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="e045b-307">Witaj lokalizację źródła danych jest w dokumentacji usługi Azure Data Lake Store w ten sposób: **adl://data_lake_store_name.azuredatalakestore.net:443/nazwa_folderu/nazwa_pliku**.</span><span class="sxs-lookup"><span data-stu-id="e045b-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="e045b-308">Po zakończeniu zapytania hello zobaczysz wyniki hello następująco:</span><span class="sxs-lookup"><span data-stu-id="e045b-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="e045b-310">Tworzenie i wdrażanie modeli w usłudze Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e045b-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="e045b-311">Firma Microsoft są teraz gotowe toobuild i wdrażanie modelu, który wskazuje, czy etykietki otrzymuje przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e045b-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="e045b-312">Witaj stratyfikowana przykładowych danych jest gotowy toobe używane w tym klasyfikacji binarnej (Porada lub nie) problem.</span><span class="sxs-lookup"><span data-stu-id="e045b-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="e045b-313">Witaj modeli predykcyjnych, przy użyciu wieloklasowej klasyfikacji (tip_class) i regresji (tip_amount) również może być skompilowany i wdrożony w usłudze Azure Machine Learning Studio, ale w tym miejscu możemy Pokaż tylko sposób toohandle hello wielkość użyciu hello model klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="e045b-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="e045b-314">Pobierz dane hello do uczenia Maszynowego Azure przy użyciu hello **importowanie danych** modułu dostępne w hello **danych wejściowych i wyjściowych** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e045b-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="e045b-315">Aby uzyskać więcej informacji, zobacz hello [modułu importu danych](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) strony odwołania.</span><span class="sxs-lookup"><span data-stu-id="e045b-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="e045b-316">Wybierz **zapytanie Hive** jako hello **źródła danych** w hello **właściwości** panelu.</span><span class="sxs-lookup"><span data-stu-id="e045b-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="e045b-317">Wklej hello następującego skryptu Hive w hello **zapytanie Hive bazy danych** edytora</span><span class="sxs-lookup"><span data-stu-id="e045b-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="e045b-318">Wprowadź hello URI HDInsight klastra (znajdują się w portalu Azure), poświadczenia usługi Hadoop, lokalizacja danych wyjściowych i nazwę kontenera nazwa/kluczy konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e045b-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="e045b-320">Przykład eksperymentu klasyfikacji binarnej odczytywanie danych z tabeli Hive przedstawiono hello rysunku poniżej.</span><span class="sxs-lookup"><span data-stu-id="e045b-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="e045b-322">Po utworzeniu hello eksperyment, kliknij przycisk **ustawić usługę sieci Web** --> **predykcyjnej usługi sieci Web**</span><span class="sxs-lookup"><span data-stu-id="e045b-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="e045b-324">Oceniania eksperymentu, po zakończeniu kliknij przycisk Uruchom hello tworzone automatycznie **wdrażanie usługi sieci Web**</span><span class="sxs-lookup"><span data-stu-id="e045b-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="e045b-326">wkrótce zostanie wyświetlony pulpit nawigacyjny usługi sieci web Hello:</span><span class="sxs-lookup"><span data-stu-id="e045b-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="e045b-328">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e045b-328">Summary</span></span>
<span data-ttu-id="e045b-329">Kończenie pracy tego przewodnika utworzono środowisku nauki danych do tworzenia skalowalnych rozwiązań end-to-end w usłudze Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e045b-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="e045b-330">To środowisko zostało tooanalyze używane duże publicznego zestawu danych, zabierz hello canonical kroki hello proces analizy danych, z pozyskiwania danych za pomocą uczenia modelu i następnie toohello wdrożenie hello model jako usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="e045b-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="e045b-331">U-SQL została tooprocess używane i Eksploruj przykładowe dane hello.</span><span class="sxs-lookup"><span data-stu-id="e045b-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="e045b-332">Python i Hive były używane z toobuild Azure Machine Learning Studio i wdrażanie modeli predykcyjnych.</span><span class="sxs-lookup"><span data-stu-id="e045b-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="e045b-333">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="e045b-333">What's next?</span></span>
<span data-ttu-id="e045b-334">Hello uczenia ścieżkę [zespołu danych nauki procesu (TDSP)](http://aka.ms/datascienceprocess) zapewnia tootopics łącza temat każdego kroku w hello zaawansowane analizy procesu.</span><span class="sxs-lookup"><span data-stu-id="e045b-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="e045b-335">Istnieje szereg wskazówki wyszczególnione na powitania [wskazówki dotyczące procesu nauki danych zespołu](data-science-process-walkthroughs.md) jak strony tego pokazy toouse zasobów i usług w różnych scenariuszach analizy predykcyjnej:</span><span class="sxs-lookup"><span data-stu-id="e045b-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="e045b-336">Hello proces nauki danych zespołu w działaniu: przy użyciu magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="e045b-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="e045b-337">Hello proces nauki danych zespołu w działaniu: z użyciem klastrów usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="e045b-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="e045b-338">Hello proces nauki danych zespołu: przy użyciu programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="e045b-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="e045b-339">Omówienie hello proces analizy danych za pomocą Spark w usłudze Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e045b-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

