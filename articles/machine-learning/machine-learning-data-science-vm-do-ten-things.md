---
title: "aaaTen sposobów na hello maszyny wirtualnej nauki danych | Dokumentacja firmy Microsoft"
description: "Wykonaj różne Eksploracja danych i zadań modelowania na powitania nauki danych maszyny wirtualnej."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="60623-103">Dziesięć czynności, które można wykonywać na powitania nauki danych maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="60623-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="60623-104">Witaj Microsoft danych nauki maszyny wirtualnej (DSVM) jest środowisko projektowe nauki zaawansowanych danych, umożliwiający tooperform można poszczególne zadania eksploracji i modelowania danych.</span><span class="sxs-lookup"><span data-stu-id="60623-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="60623-105">Witaj środowisko zawiera już wbudowanych i powiązane z kilku popularnych danych narzędzia do analizy, dzięki któremu można łatwo tooget szybko rozpocząć z analizy dla lokalnych w chmurze czy hybrydowa wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="60623-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="60623-106">Witaj DSVM ściśle współpracuje z wielu usług Azure i jest w stanie tooread i przetwarzania danych, które są już przechowywane na platformie Azure, Magazyn danych SQL Azure, usługa Azure Data Lake, usługi Azure Storage lub w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60623-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="60623-107">Można też skorzystać innych narzędzi analizy, takich jak uczenie maszynowe Azure i fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="60623-108">W tym artykule firma Microsoft przeprowadzi użytkownika przez proces jak toouse Twojego tooperform DSVM różnych nauki danych zadań i interakcję z innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="60623-109">Poniżej podano niektóre czynności hello, które można wykonać na powitania DSVM:</span><span class="sxs-lookup"><span data-stu-id="60623-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="60623-110">Eksplorowanie danych i tworzenie modeli lokalnie na powitania DSVM przy użyciu programu Microsoft Server R, Python</span><span class="sxs-lookup"><span data-stu-id="60623-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="60623-111">Użyj tooexperiment notesu Jupyter z danymi w przeglądarce przy użyciu języka Python, 2, Python 3 Microsoft R wersji gotowe enterprise elementu R, skalowalności i wydajności</span><span class="sxs-lookup"><span data-stu-id="60623-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="60623-112">Operacjonalizuj modele utworzony przy użyciu języków R i Python w usłudze Azure Machine Learning, aby aplikacje klienckie mogą uzyskiwać dostęp do modeli przy użyciu prostego interfejsu sieci web usług</span><span class="sxs-lookup"><span data-stu-id="60623-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="60623-113">Administrowanie zasobami platformy Azure przy użyciu portalu Azure lub programu Powershell</span><span class="sxs-lookup"><span data-stu-id="60623-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="60623-114">Rozszerzanie miejsca do magazynowania i udostępniania dużych zestawów danych / kodu w całym zespołem przez tworzenie usługi Magazyn plików Azure jako dysk instalację na DSVM Twojego</span><span class="sxs-lookup"><span data-stu-id="60623-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="60623-115">Udostępnianie kodu z zespołem przy użyciu usługi GitHub i uzyskać dostępu do repozytorium, używając hello wstępnie zainstalowane Git klienci - Git Bash Git graficznego interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="60623-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="60623-116">Dostęp do różnych Azure danych i ich analiza usług przykład do magazynu obiektów blob platformy Azure, Azure Data Lake Azure HDInsight (Hadoop), bazy danych rozwiązania Cosmos platformy Azure, Magazyn danych SQL Azure & bazy danych</span><span class="sxs-lookup"><span data-stu-id="60623-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="60623-117">Twórz raporty i pulpit nawigacyjny za pomocą hello Power BI Desktop wstępnie zainstalowanych na powitania DSVM i wdrażanie ich w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="60623-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="60623-118">Dynamiczne skalowanie toomeet Twojego DSVM, potrzebne w projekcie</span><span class="sxs-lookup"><span data-stu-id="60623-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="60623-119">Instalowanie dodatkowych narzędzi na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="60623-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="60623-120">Użycie dodatkowe opłaty dla wielu hello dodatkowe dane magazynu i analiza usług wymienionych w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="60623-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="60623-121">Zobacz toohello [cennik usługi Azure](https://azure.microsoft.com/pricing/) strony, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="60623-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="60623-122">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="60623-122">**Prerequisites**</span></span>

* <span data-ttu-id="60623-123">Potrzebujesz subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-123">You need an Azure subscription.</span></span> <span data-ttu-id="60623-124">Można założyć bezpłatnej wersji próbnej [tutaj](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="60623-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="60623-125">Instrukcje dotyczące obsługi danych maszyny wirtualnej nauki na powitania portalu Azure są dostępne pod adresem [tworzenia maszyny wirtualnej](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="60623-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="60623-126">1. Eksplorowanie danych i tworzenie modeli przy użyciu programu Microsoft Server R lub Python</span><span class="sxs-lookup"><span data-stu-id="60623-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="60623-127">Można użyć w językach toodo R i Python z analizy danych bezpośrednio na powitania DSVM.</span><span class="sxs-lookup"><span data-stu-id="60623-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="60623-128">Dla języka R możesz użyć IDE o nazwie "Enterprise 8.0 obrotów R", który można znaleźć w hello start menu lub hello pulpitu.</span><span class="sxs-lookup"><span data-stu-id="60623-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="60623-129">Firma Microsoft udostępnia dodatkowe biblioteki u góry hello Otwórz tooenable sieci CRAN-źródła R skalowalne analizy i hello możliwości tooanalyze danych większy niż rozmiar pamięci hello dozwolone w sposób równoległy podzielony analizy.</span><span class="sxs-lookup"><span data-stu-id="60623-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="60623-130">Można także zainstalować IDE języka R z wyborem LIKE [programu RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="60623-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="60623-131">Dla języka Python możesz użyć IDE, takich jak Visual Studio Community Edition, mającej hello narzędzi Python Tools dla wstępnie zainstalowane rozszerzenia programu Visual Studio (PTVS).</span><span class="sxs-lookup"><span data-stu-id="60623-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="60623-132">Domyślnie tylko podstawowe środowisko Python 2.7 jest skonfigurowany na PTVS (bez żadnych biblioteki analizy, takich jak SciKit, Pandas).</span><span class="sxs-lookup"><span data-stu-id="60623-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="60623-133">W kolejności tooenable Anaconda Python 2.7 i 3.5 należy toodo hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="60623-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="60623-134">Tworzenie niestandardowego środowiska dla każdej wersji przechodząc zbyt**narzędzia** -> **narzędzi Python Tools** -> **środowiska Python** , a następnie klikając polecenie " **+ Niestandardowe**"w hello Visual Studio 2015 Community Edition</span><span class="sxs-lookup"><span data-stu-id="60623-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="60623-135">Wprowadź opis i ustawić hello środowiska ścieżki prefiks jako *c:\anaconda* Anaconda Python 2.7 lub *c:\anaconda\envs\py35* dla Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="60623-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="60623-136">Kliknij przycisk **Autowykrywanie** , a następnie **Zastosuj** toosave hello środowiska.</span><span class="sxs-lookup"><span data-stu-id="60623-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="60623-137">Oto ustawieniach niestandardowych środowiska hello wygląda jak w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60623-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![Instalator PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="60623-139">Zobacz hello [dokumentacji PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) dodatkowe informacje na temat toocreate środowiska Python.</span><span class="sxs-lookup"><span data-stu-id="60623-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="60623-140">Teraz możesz ustawiono toocreate nowy projekt języka Python.</span><span class="sxs-lookup"><span data-stu-id="60623-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="60623-141">Przejdź za**pliku** -> **nowy** -> **projektu** -> **Python** i wybierz typ hello Aplikacja języka Python, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="60623-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="60623-142">Można ustawić środowiska Python hello hello bieżącego projektu toohello wymaganej wersji (Anaconda 2.7 lub 3.5): kliknij prawym przyciskiem myszy hello **środowiska Python**, wybierz pozycję **środowiska Python Dodaj lub usuń**, i następnie wybierz hello żądana tooassociate środowisko z hello projektu.</span><span class="sxs-lookup"><span data-stu-id="60623-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="60623-143">Można znaleźć więcej informacji na temat pracy z narzędziami PTVS produktu hello [dokumentacji](https://github.com/Microsoft/PTVS/wiki) strony.</span><span class="sxs-lookup"><span data-stu-id="60623-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="60623-144">2. Używanie tooexplore notesu Jupyter i modelu danych z programem Python lub R</span><span class="sxs-lookup"><span data-stu-id="60623-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="60623-145">Witaj notesu Jupyter jest zaawansowane środowisko, które zapewnia przeglądarki "IDE" Eksploracja danych i modelowania.</span><span class="sxs-lookup"><span data-stu-id="60623-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="60623-146">Można użyć języka Python, 2, Python 3 lub R (Open Source i hello Microsoft R Server) w notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="60623-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="60623-147">Witaj toolaunch notesu Jupyter kliknij ikonę menu start hello / zatytułowany ikony pulpitu **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="60623-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="60623-148">Na powitania DSVM możesz również przejść za "https://localhost:9999 /" tooaccess hello Jupiter notesu.</span><span class="sxs-lookup"><span data-stu-id="60623-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="60623-149">Jeśli monituje o podanie hasła, użyj instrukcji podanych w hello ***jak toocreate silnego hasła na serwerze notesu Jupyter hello*** sekcji hello [hello udostępniania maszyny wirtualnej nauki danych Microsoft](machine-learning-data-science-provision-vm.md)toocreate tematu notesu Jupyter hello tooaccess silne hasło.</span><span class="sxs-lookup"><span data-stu-id="60623-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="60623-150">Po otwarciu notesu hello katalog, który zawiera kilka notesów przykładzie, które są wstępnie utworzonych pakietów do hello DSVM powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="60623-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="60623-151">Teraz możesz:</span><span class="sxs-lookup"><span data-stu-id="60623-151">Now you can:</span></span>

* <span data-ttu-id="60623-152">polecenie hello notesu toosee hello kodu.</span><span class="sxs-lookup"><span data-stu-id="60623-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="60623-153">Wykonanie każdej komórki naciskając **wprowadź SHIFT**.</span><span class="sxs-lookup"><span data-stu-id="60623-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="60623-154">Uruchom hello cały notes klikając **komórki** -> **Uruchom**</span><span class="sxs-lookup"><span data-stu-id="60623-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="60623-155">Tworzenie nowego notesu kliknięcie hello Jupyter ikona (w lewym górnym rogu), a następnie klikając polecenie **nowy** przycisk na powitania prawo, a następnie wybierając hello notesu języka (znanej także jako jądra).</span><span class="sxs-lookup"><span data-stu-id="60623-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="60623-156">Obecnie firma Microsoft obsługuje Python 2.7, Python 3.5 i R. jądra hello R obsługuje programowanie w zarówno typu Open source R, jak i hello enterprise skalowalne Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="60623-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="60623-157">Po przejściu w notesie hello można eksplorować dane, budowanie modelu hello, model hello przy użyciu bibliotek wybór testów.</span><span class="sxs-lookup"><span data-stu-id="60623-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="60623-158">3. Tworzenie modeli przy użyciu R lub Python i Operationalize je za pomocą usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60623-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="60623-159">Po wbudowane i sprawdzić poprawności modelu hello następnym krokiem jest zwykle toodeploy go w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="60623-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="60623-160">Dzięki temu klient aplikacji tooinvoke hello modelu prognozy w czasie rzeczywistym lub na podstawie trybu partii.</span><span class="sxs-lookup"><span data-stu-id="60623-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="60623-161">Usługa Azure Machine Learning zapewnia toooperationalize mechanizmu model wbudowane R lub Python.</span><span class="sxs-lookup"><span data-stu-id="60623-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="60623-162">Gdy użytkownik operacjonalizować model w usłudze Azure Machine Learning, usługi sieci web jest narażony, umożliwiającą klientom toomake wywołania REST, które należy przekazać w parametrach wejściowych i otrzymywać prognoz hello modelu jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="60623-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="60623-163">Jeśli użytkownik ma nie jeszcze zarejstrowano w usłudze Azure Machine Learning, odwiedzając hello można uzyskać wolnego obszaru roboczego lub standardowy obszaru roboczego [Azure Machine Learning Studio](https://studio.azureml.net/) strony głównej i kliknięcie na "wprowadzenie".</span><span class="sxs-lookup"><span data-stu-id="60623-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="60623-164">Kompilowanie i Python Operacjonalizuj modele</span><span class="sxs-lookup"><span data-stu-id="60623-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="60623-165">Oto fragment kodu w notesu Jupyter Python korzystająca z modelu prostego za pomocą biblioteki informacje SciKit hello.</span><span class="sxs-lookup"><span data-stu-id="60623-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="60623-166">Metoda Hello używane toodeploy Twojego python tooAzure modeli uczenia maszynowego zawija hello prognozowania modelu hello funkcji i decorates go z atrybutami podał hello wstępnie zainstalowane usługi Azure Machine Learning biblioteka języka python, które oznaczają komputerze Azure Identyfikator obszaru roboczego uczenia, klucz interfejsu API i hello danych wejściowych i zwracać parametrów.</span><span class="sxs-lookup"><span data-stu-id="60623-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="60623-167">Klient może teraz utworzyć usługi sieci web toohello wywołania.</span><span class="sxs-lookup"><span data-stu-id="60623-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="60623-168">Brak otoki wygody, które skonstruować hello żądania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="60623-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="60623-169">Oto przykładowy kod tooconsume hello sieci web usługi.</span><span class="sxs-lookup"><span data-stu-id="60623-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="60623-170">Biblioteka usługi Azure Machine Learning Hello jest obsługiwana tylko na Python 2.7 obecnie.</span><span class="sxs-lookup"><span data-stu-id="60623-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="60623-171">Modele kompilacji i Operacjonalizacji R</span><span class="sxs-lookup"><span data-stu-id="60623-171">Build and Operationalize R models</span></span>
<span data-ttu-id="60623-172">Można wdrożyć modeli R zbudowane na powitania maszyny wirtualnej nauki danych lub w innym miejscu na uczenie maszynowe Azure w taki sposób, który jest podobne toohow, które jest wykonywane dla języka Python.</span><span class="sxs-lookup"><span data-stu-id="60623-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="60623-173">Jej hello kroków:</span><span class="sxs-lookup"><span data-stu-id="60623-173">Her are hello steps:</span></span>

* <span data-ttu-id="60623-174">Utwórz tooprovide pliku settings.json, uwierzytelniania i identyfikator obszaru roboczego, na których token pokazane na powitania po przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="60623-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="60623-175">Funkcja prognozowania modelu hello zapisać otokę.</span><span class="sxs-lookup"><span data-stu-id="60623-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="60623-176">wywołanie ```publishWebService``` w hello toopass biblioteki usługi Azure Machine Learning w hello funkcja otoki.</span><span class="sxs-lookup"><span data-stu-id="60623-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="60623-177">Oto wstawki procedurą i kod hello, które można tooset używane górę, kompilacji, publikowania i zużywać model jako usługę sieci web w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="60623-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="60623-178">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="60623-178">Setup</span></span>
1. <span data-ttu-id="60623-179">Zainstaluj pakiet Machine Learning R hello wpisując ```install.packages("AzureML")``` w porównaniu R Enterprise 8.0 IDE lub środowiskiem IDE R.</span><span class="sxs-lookup"><span data-stu-id="60623-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="60623-180">Pobierz RTools z [tutaj](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="60623-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="60623-181">Należy toooperationalize narzędzie Ścieżka hello (i nazwane zip.exe) zip hello pakietu R do uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="60623-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="60623-182">Utwórz plik settings.json w obszarze katalog o nazwie ```.azureml``` w katalogu macierzystym i wprowadź parametry hello z obszaru roboczego uczenia maszynowego Azure:</span><span class="sxs-lookup"><span data-stu-id="60623-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="60623-183">Settings.JSON struktury plików:</span><span class="sxs-lookup"><span data-stu-id="60623-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="60623-184">Tworzenie modelu w R i opublikować ją w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60623-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="60623-185">Korzystanie z modelu hello wdrożony w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="60623-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="60623-186">model hello tooconsume od aplikacji klienckiej, używamy toolook biblioteki usługi Azure Machine Learning hello zapasowej hello opublikowane usługi sieci web wg nazwy przy użyciu hello `services` punkt końcowy hello toodetermine wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="60623-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="60623-187">Następnie po prostu Wywołaj hello `consume` funkcji i podaj toobe ramki danych hello przewidzieć.</span><span class="sxs-lookup"><span data-stu-id="60623-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="60623-188">Witaj następującego kodu to model hello tooconsume używane publikowane jako usługi sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="60623-189">Więcej informacji na temat hello Azure Machine Learning R biblioteki można znaleźć [tutaj](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="60623-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="60623-190">4. Administrowanie zasobami platformy Azure przy użyciu portalu Azure lub programu Powershell</span><span class="sxs-lookup"><span data-stu-id="60623-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="60623-191">Witaj DSVM nie zezwala tylko toobuild Twojego rozwiązania analizy lokalnie na hello maszyny wirtualnej, ale można też tooaccess usług w chmurze Azure firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="60623-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="60623-192">Platforma Azure udostępnia kilka obliczeń, magazynu, usługi analizy danych i innych usług, które mogą administrować i uzyskać dostęp z Twojej DSVM.</span><span class="sxs-lookup"><span data-stu-id="60623-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="60623-193">tooadminister zasobami subskrypcji i w chmurze Azure można użyć przeglądarki i toothe punktu [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60623-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="60623-194">Umożliwia także tooadminister programu Azure Powershell Twojej subskrypcji platformy Azure i zasobów za pomocą skryptu.</span><span class="sxs-lookup"><span data-stu-id="60623-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="60623-195">Można uruchomić programu Azure Powershell przy użyciu skrótu na pulpicie hello, lub z hello start menu zatytułowany "Microsoft Azure Powershell".</span><span class="sxs-lookup"><span data-stu-id="60623-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="60623-196">Zapoznaj się [dokumentacji programu Microsoft Azure Powershell](../powershell-azure-resource-manager.md) Aby uzyskać więcej informacji na temat sposobu do administrowania subskrypcji platformy Azure i zasobów za pomocą skryptów programu Windows Powershell.</span><span class="sxs-lookup"><span data-stu-id="60623-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="60623-197">5. Rozszerzanie miejsca do magazynowania w systemie plików udostępnionych</span><span class="sxs-lookup"><span data-stu-id="60623-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="60623-198">Analityków danych można udostępniać dużych zestawów danych, kodu lub innych zasobów w ramach hello zespołu.</span><span class="sxs-lookup"><span data-stu-id="60623-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="60623-199">Witaj DSVM sam ma około 70GB dostępnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="60623-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="60623-200">tooextend Twojego magazynu, można użyć hello Azure usługi plików i zainstalować go na powitania DSVM lub uzyskać do niego dostęp za pośrednictwem interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="60623-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="60623-201">Maksymalna ilość miejsca Hello hello Azure usługa plików udziału jest 5TB i limit rozmiaru poszczególnych plików wynosi 1TB.</span><span class="sxs-lookup"><span data-stu-id="60623-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="60623-202">Możesz użyć programu Azure Powershell toocreate udziału usługa plików Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="60623-203">Oto hello toorun skryptu w obszarze toocreate programu Azure PowerShell udział plików Azure usługi.</span><span class="sxs-lookup"><span data-stu-id="60623-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="60623-204">Teraz, po utworzeniu udziału plików na platformę Azure, możesz go zainstalować w żadnej maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="60623-205">Zaleca się, że hello maszyna wirtualna jest w tym samym centrum danych Azure jako hello magazynu konta tooavoid opóźnienia i danych opłat za transfer.</span><span class="sxs-lookup"><span data-stu-id="60623-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="60623-206">Poniżej przedstawiono hello polecenia toomount hello dysku na powitania DSVM, która może działać na programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="60623-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="60623-207">Teraz jak w przypadku dowolnego normalne dysku na powitania maszyny Wirtualnej można dostępu do dysku.</span><span class="sxs-lookup"><span data-stu-id="60623-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="60623-208">6. Udostępnianie kodu z zespołem przy użyciu usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="60623-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="60623-209">GitHub jest repozytorium kodu, gdzie można znaleźć wiele przykładowy kod i źródła dla różnych narzędzi z użyciem różnych technologii udostępnione przez społeczność deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="60623-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="60623-210">Jak hello technologii tootrack, a także przechowywać wersje plików kodu hello jest używany Git.</span><span class="sxs-lookup"><span data-stu-id="60623-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="60623-211">GitHub jest również platformy umożliwiającego utworzenie własnych repozytorium toostore Twojego zespołu udostępnionego kodu i dokumentacji zaimplementować kontroli wersji i również kontroli którzy tooview dostępu i współtworzenia kodu.</span><span class="sxs-lookup"><span data-stu-id="60623-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="60623-212">Odwiedź stronę hello [GitHub strony pomocy](https://help.github.com/) uzyskać więcej informacji na temat używania narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="60623-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="60623-213">Można użyć GitHub wśród toocollaborate sposoby hello z zespołem, użyj kodu opracowanych przez społeczność hello i współtworzenia społeczności wstecz toohello kodu.</span><span class="sxs-lookup"><span data-stu-id="60623-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="60623-214">Hello DSVM już zawiera załadowane z narzędziami klienckimi zarówno wiersza polecenia, jak dobrze tooaccess graficznego interfejsu użytkownika repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="60623-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="60623-215">Witaj toowork narzędzia wiersza polecenia Git i GitHub jest nazywany Git Bash.</span><span class="sxs-lookup"><span data-stu-id="60623-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="60623-216">Visual Studio zainstalowanych na powitania DSVM ma hello Git.</span><span class="sxs-lookup"><span data-stu-id="60623-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="60623-217">Ikony rozruchu można znaleźć dla tych narzędzi w hello start menu i hello pulpitu.</span><span class="sxs-lookup"><span data-stu-id="60623-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="60623-218">Kod toodownload z repozytorium GitHub używasz hello ```git clone``` polecenia.</span><span class="sxs-lookup"><span data-stu-id="60623-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="60623-219">Na przykład repozytorium nauki danych toodownload opublikowane przez firmę Microsoft do bieżącego katalogu hello można uruchomić hello następujące polecenia, po przejściu do ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="60623-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="60623-220">W programie Visual Studio, czy hello tej samej operacji klonowania.</span><span class="sxs-lookup"><span data-stu-id="60623-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="60623-221">powitania po zrzut ekranu pokazuje, jak tooaccess Git i GitHub narzędzia w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60623-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![Git w programie Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="60623-223">Można znaleźć więcej informacji dotyczących korzystania z repozytorium GitHub z kilku zasobów dostępnych w witrynie github.com Git toowork. Witaj [ściągawka](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) jest przydatne odwołanie.</span><span class="sxs-lookup"><span data-stu-id="60623-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="60623-224">7. Dostęp do różnych usług Azure danych i ich analiza</span><span class="sxs-lookup"><span data-stu-id="60623-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="60623-225">Obiekt bob Azure</span><span class="sxs-lookup"><span data-stu-id="60623-225">Azure Blob</span></span>
<span data-ttu-id="60623-226">Obiektów blob platformy Azure to niezawodne, ekonomiczny chmurze magazynu danych dużych i małych.</span><span class="sxs-lookup"><span data-stu-id="60623-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="60623-227">Daj nam przyjrzeć się, jak można przenosić tooAzure danych obiektów Blob i uzyskiwanie dostępu do danych przechowywanych w obiekcie Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="60623-228">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="60623-228">**Prerequisite**</span></span>

* <span data-ttu-id="60623-229">**Tworzenie konta magazynu obiektów Blob platformy Azure z [portalu Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="60623-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="60623-231">Upewnij się, że hello wstępnie zainstalowane narzędzie wiersza polecenia AzCopy znajduje się na ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="60623-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="60623-232">Podczas uruchamiania tego narzędzia można dodać hello zawierającego hello azcopy.exe tooyour ŚCIEŻKA środowiska zmiennej tooavoid pisania hello pełne polecenie ścieżki katalogu.</span><span class="sxs-lookup"><span data-stu-id="60623-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="60623-233">Aby uzyskać więcej informacji na temat narzędzia AzCopy można znaleźć zbyt[dokumentację programu AzCopy](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="60623-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="60623-234">Uruchom narzędzie Eksploratora usługi Storage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="60623-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="60623-235">Można go pobrać z [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="60623-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="60623-237">**Przenoszenia danych z maszyny Wirtualnej tooAzure obiektu Blob: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="60623-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="60623-238">toomove danych między lokalnych plików i magazynu obiektów blob, AzCopy można użyć w wierszu polecenia lub środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="60623-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="60623-239">Zastąp **C:\myfolder** przechowywania pliku, ścieżka toohello **mojekontomagazynu** tooyour nazwy konta magazynu obiektów blob, **mojkontener** nazwę kontenera toohello **klucz konta magazynu** klucz dostępu do magazynu obiektów blob tooyour.</span><span class="sxs-lookup"><span data-stu-id="60623-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="60623-240">Można znaleźć poświadczeń konta magazynu w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60623-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="60623-242">Uruchom polecenie AzCopy, programu PowerShell lub z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="60623-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="60623-243">Poniżej przedstawiono niektóre Przykładowe użycie polecenia programu AzCopy:</span><span class="sxs-lookup"><span data-stu-id="60623-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="60623-244">Po uruchomieniu programu AzCopy polecenia toocopy tooan obiektów blob platformy Azure, zobacz plik zostaną wyświetlone w Eksploratorze usługi Storage Azure wkrótce.</span><span class="sxs-lookup"><span data-stu-id="60623-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="60623-246">**Przenoszenia danych z maszyny Wirtualnej tooAzure obiektu Blob: Eksploratora usługi Storage platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="60623-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="60623-247">Możesz również przekazywać dane z pliku lokalnego hello w maszynie Wirtualnej za pomocą Eksploratora usługi Storage platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="60623-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="60623-248">kontener tooa danych tooupload, hello wybierz docelowy kontener i kliknij przycisk hello **przekazać** przycisku.![ Przekazywanie do Eksploratora usługi Storage](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="60623-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="60623-249">Polecenie hello **...**  toohello rogu hello **pliki** wybierz jednego lub wielu tooupload pliki z systemu plików hello a kliknij **przekazać** toobegin przekazywania plików hello.![ Przekazywanie plików tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="60623-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="60623-250">**Odczytywanie danych z obiektów Blob platformy Azure: moduł czytnika uczenia maszynowego**</span><span class="sxs-lookup"><span data-stu-id="60623-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="60623-251">W usłudze Azure Machine Learning Studio można użyć **modułu importu danych** tooread dane z Twojego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="60623-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="60623-253">**Odczytywanie danych z obiektów Blob platformy Azure: Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="60623-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="60623-254">Można użyć **BlobService** biblioteki tooread danych bezpośrednio z obiektu blob w programie notesu Jupyter lub Python.</span><span class="sxs-lookup"><span data-stu-id="60623-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="60623-255">Po pierwsze zaimportuj wymagane pakiety:</span><span class="sxs-lookup"><span data-stu-id="60623-255">First, import required packages:</span></span>

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

<span data-ttu-id="60623-256">Następnie podłącz poświadczeń konta obiektów Blob platformy Azure i odczytywanie danych z obiektu Blob:</span><span class="sxs-lookup"><span data-stu-id="60623-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="60623-257">dane Hello jest do odczytu jako ramki danych:</span><span class="sxs-lookup"><span data-stu-id="60623-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="60623-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="60623-259">Azure Data Lake</span></span>
<span data-ttu-id="60623-260">Azure Data Lake Storage to repozytorium hiperskali obciążeń analizy danych big data i zgodny z Hadoop Distributed pliku System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="60623-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="60623-261">Działa z ekosystemem Hadoop hello i hello Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="60623-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="60623-262">Zostanie przedstawiony sposób przenoszenia danych do hello Azure Data Lake Store i uruchom analytics przy użyciu usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="60623-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="60623-263">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="60623-263">**Prerequisite**</span></span>

* <span data-ttu-id="60623-264">Tworzenie z usługą Azure Data Lake Analytics w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60623-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="60623-266">Witaj **Azure Data Lake Tools** w **programu Visual Studio** znaleziono w tej [łącze](https://www.microsoft.com/download/details.aspx?id=49504) jest już zainstalowana na powitania Visual Studio Community Edition, który znajduje się na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="60623-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="60623-267">Po uruchomieniem programu Visual Studio i rejestrowanie w Twojej subskrypcji platformy Azure, powinna zostać wyświetlona Twoje konto usługi Azure Data Analytics i magazynu w lewym panelu hello programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60623-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="60623-269">**Przenoszenia danych z maszyny Wirtualnej tooData Lake: Azure Data Lake Explorer**</span><span class="sxs-lookup"><span data-stu-id="60623-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="60623-270">Można użyć **Azure Data Lake Explorer** tooupload danych z plików lokalne powitania w Twoim magazynie Lake tooData maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="60623-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="60623-272">Można również tworzyć tooproductionize potoku danych Twojej tooor przeniesienia danych z usługi Azure Data Lake za pomocą hello [Factory(ADF) danych Azure](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="60623-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="60623-273">Firma Microsoft możesz znaleźć toothis [artykułu](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide przez hello kroki toobuild hello danych potoków.</span><span class="sxs-lookup"><span data-stu-id="60623-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="60623-274">**Odczytywanie danych z usługi Azure Blob tooData Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="60623-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="60623-275">Jeśli dane znajdują się w magazynie obiektów Blob platformy Azure, mogą bezpośrednio odczytywać dane z obiektu blob magazynu Azure w zapytaniu U-SQL.</span><span class="sxs-lookup"><span data-stu-id="60623-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="60623-276">Przed tworzenia kwerendy U-SQL, upewnij się, że Twoje konto magazynu obiektów blob jest tooyour połączonej usługi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="60623-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="60623-277">Przejdź za**portalu Azure**, Znajdź pulpitu nawigacyjnego usługi Azure Data Lake Analytics, kliknij przycisk **Dodaj źródło danych**, wybierz typ magazynu zbyt**usługi Azure Storage** i dołączyć usługi magazynu Azure Nazwa konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="60623-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="60623-278">To może tooreference hello danych przechowywanych w hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="60623-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![Wprowadź konto magazynu i klucz](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="60623-280">W programie Visual Studio można odczytać danych z magazynu obiektów blob, niektóre manipulowania danymi, inżynieria funkcji i danych wyjściowych hello wynikowy danych tooeither usługi Azure Data Lake lub magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="60623-281">Podając odniesienie hello danych w magazynie obiektów blob, użyj **wasb: / /**; w przypadku odwołania hello danych w usłudze Azure Data Lake, użyj **swbhdfs: / /**</span><span class="sxs-lookup"><span data-stu-id="60623-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![Ramki danych](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="60623-283">Może używać powitania po zapytań U-SQL w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="60623-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="60623-284">Zapytanie po serwera toohello przesłane diagram przedstawiający hello stan zadania jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="60623-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![Diagram stanu zadania](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="60623-286">**Zapytania na danych w usłudze Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="60623-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="60623-287">Po hello dataset jest pozyskanych w usłudze Azure Data Lake, można użyć [języka U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery i eksplorować dane hello.</span><span class="sxs-lookup"><span data-stu-id="60623-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="60623-288">Języka U-SQL jest podobne tooT-SQL, ale łączy niektóre funkcje w języku C#, dzięki czemu użytkownicy mogą zapisywać niestandardowych modułów, funkcje zdefiniowane przez użytkownika i itp. Można użyć skryptów hello hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="60623-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="60623-289">Po tooserver przesłane, tripdata_summary hello zapytania. CSV znajdują się wkrótce w **Azure Data Lake Explorer**, można podejrzeć hello danych przez plik powitania kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="60623-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![Plik w Eksploratorze Lake danych Azure](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="60623-291">informacje o pliku hello toosee:</span><span class="sxs-lookup"><span data-stu-id="60623-291">toosee hello file information:</span></span>

![Podsumowanie pliku](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="60623-293">Klastrów HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="60623-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="60623-294">Usługa Azure HDInsight to zarządzana usługa Apache Hadoop, Spark, HBase i Storm w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="60623-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="60623-295">Można łatwo pracować z klastrami Azure HDInsight z maszyny wirtualnej nauki danych hello.</span><span class="sxs-lookup"><span data-stu-id="60623-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="60623-296">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="60623-296">**Prerequisite**</span></span>

* <span data-ttu-id="60623-297">Tworzenie konta magazynu obiektów Blob platformy Azure z [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60623-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="60623-298">To konto magazynu jest danych toostore używanej dla klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60623-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![Tworzenie konta magazynu obiektów Blob platformy Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="60623-300">Dostosowywanie Azure platforma Hadoop w usłudze Hdinsight z [portalu Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="60623-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="60623-301">Należy połączyć hello konta magazynu utworzone z klastrem usługi HDInsight podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="60623-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="60623-302">To konto magazynu jest używane do uzyskiwania dostępu do danych, które mogą być przetwarzane w ramach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="60623-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![Konto toostorage łącze utworzone z klastrem usługi HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="60623-304">Należy włączyć **dostępu zdalnego** toohello węzła głównego klastra powitania po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="60623-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="60623-305">Pamiętaj poświadczenia dostępu zdalnego hello określone w tym miejscu (różne od tych określonych hello klastra podczas jego tworzenia): potrzebne w następnej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="60623-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![Włączenie dostępu zdalnego](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="60623-307">Utwórz obszar roboczy usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="60623-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="60623-308">Z uczeniem maszynowym są przechowywane w tym obszaru roboczego uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="60623-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="60623-309">Wybierz opcje hello wyróżniane w portalu, jak pokazano w powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="60623-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![Tworzenie obszaru roboczego usługi Azure Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="60623-311">Następnie wprowadź parametry hello obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="60623-311">Then enter hello parameters for your workspace</span></span>

![Wprowadź parametry obszaru roboczego uczenia maszynowego](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="60623-313">Przekazywanie danych za pomocą notesu IPython.</span><span class="sxs-lookup"><span data-stu-id="60623-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="60623-314">Najpierw zaimportuj wymagane pakiety, podłącz poświadczeń, Utwórz bazę danych na koncie magazynu, a następnie załadować klastry tooHDI danych.</span><span class="sxs-lookup"><span data-stu-id="60623-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="60623-315">Alternatywnie można to wykonać [wskazówki](machine-learning-data-science-process-hive-walkthrough.md) tooupload taksówki NYC danych tooHDI klastra.</span><span class="sxs-lookup"><span data-stu-id="60623-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="60623-316">Główne kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="60623-316">Major steps include:</span></span>
  
  * <span data-ttu-id="60623-317">Narzędzie AzCopy: Pobierz zip CSV z folderu lokalnego tooyour publicznego obiektu blob</span><span class="sxs-lookup"><span data-stu-id="60623-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="60623-318">Narzędzie AzCopy: Przekaż rozpakowane udostępnionych woluminach Klastra z folderu lokalnego tooHDI klastra</span><span class="sxs-lookup"><span data-stu-id="60623-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="60623-319">Zaloguj się do hello węzła głównego klastra usługi Hadoop i Przygotuj się do analizy danych poznawcze</span><span class="sxs-lookup"><span data-stu-id="60623-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="60623-320">Po danych hello jest załadowany tooHDI klastra, można sprawdzić dane w Eksploratorze usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60623-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="60623-321">I masz nyctaxidb bazy danych, utworzonych w klastra HDI.</span><span class="sxs-lookup"><span data-stu-id="60623-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="60623-322">**Eksploracja danych: zapytań programu Hive w języku Python**</span><span class="sxs-lookup"><span data-stu-id="60623-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="60623-323">Ponieważ hello dane pochodzą z klastra usługi Hadoop, może użyć hello pyodbc pakietu tooconnect tooHadoop klastrów i kwerendy bazy danych przy użyciu Hive toodo eksploracji i inżynieria funkcji.</span><span class="sxs-lookup"><span data-stu-id="60623-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="60623-324">Witaj istniejące tabele, utworzone w kroku wymagań wstępnych hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="60623-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Wyświetlanie istniejących tabel](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="60623-326">Przyjrzyjmy się hello liczby rekordów w każdym miesiącu i hello częstotliwości Przechylony lub nie znajduje się w tabeli podróży hello:</span><span class="sxs-lookup"><span data-stu-id="60623-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Wykres liczby rekordów w każdym miesiącu](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Wykres programu końcówkę częstotliwości](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="60623-329">Możemy również obliczeniowe hello odległości między lokalizacją podnoszenia dropoff lokalizacji i porównania go po toohello rzeczy przed wyjazdem odległości.</span><span class="sxs-lookup"><span data-stu-id="60623-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Odbiór i dropoff tabeli](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Wykres odległość tootrip odległość podnoszenia/dropoff](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="60623-332">Teraz załóżmy przygotowanie próbkowany down (1%) zbiór danych do modelowania.</span><span class="sxs-lookup"><span data-stu-id="60623-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="60623-333">Możemy użyć tych danych w module czytnika uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="60623-333">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="60623-334">Po chwili można zauważyć, że dane hello został załadowany w klastrów platformy Hadoop:</span><span class="sxs-lookup"><span data-stu-id="60623-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabela danych](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="60623-336">**Odczytywanie danych z HDI za pomocą uczenia maszynowego: moduł czytnika**</span><span class="sxs-lookup"><span data-stu-id="60623-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="60623-337">Można także użyć hello **czytnika** modułu w bazie danych hello tooaccess Machine Learning Studio w klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="60623-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="60623-338">Podłącz hello poświadczeń klastrów HDI i konto magazynu Azure tooenable tworzenie modeli przy użyciu bazy danych w klastrach HDI uczenia maszynowego lasycznego, dokującego.</span><span class="sxs-lookup"><span data-stu-id="60623-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![Właściwości modułu Reader](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="60623-340">Witaj scored zestaw danych można następnie wyświetlić:</span><span class="sxs-lookup"><span data-stu-id="60623-340">hello scored dataset can then be viewed:</span></span>

![Widok oceniane zestawu danych](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="60623-342">& Baz danych Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="60623-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="60623-343">Usługa Azure SQL Data Warehouse jest magazyn danych elastycznej jako usługi za pomocą klasy korporacyjnej środowisko programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="60623-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="60623-344">Azure SQL Data Warehouse można udostępnić, wykonując następujące instrukcje hello podane w tym [artykułu](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="60623-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="60623-345">Po zainicjowanie obsługi usługi Azure SQL Data Warehouse, możesz użyć tej funkcji [wskazówki](machine-learning-data-science-process-sqldw-walkthrough.md) przekazywanie danych toodo, badanie i modelowania przy użyciu danych w ramach hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="60623-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="60623-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="60623-346">Azure Cosmos DB</span></span>
<span data-ttu-id="60623-347">Azure DB rozwiązania Cosmos jest bazą danych NoSQL w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="60623-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="60623-348">Pozwala toowork z dokumentami, takich jak JSON, a pozwala dokumentów hello toostore i zapytania.</span><span class="sxs-lookup"><span data-stu-id="60623-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="60623-349">Należy hello toodo po tooaccess kroki na wymagania bazy danych Azure rozwiązania Cosmos z hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="60623-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="60623-350">Zainstaluj zestaw SDK Python usługi DocumentDB (Uruchom ```pip install pydocumentdb``` z wiersza polecenia)</span><span class="sxs-lookup"><span data-stu-id="60623-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="60623-351">Tworzenie konta bazy danych Azure rozwiązania Cosmos i bazę danych z [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="60623-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="60623-352">Pobierz "Narzędzie migracji DB rozwiązania Cosmos Azure" z [tutaj](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) i wyodrębniać tooa katalogu</span><span class="sxs-lookup"><span data-stu-id="60623-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="60623-353">Importuj dane JSON (dane swe dzieła) przechowywanych w [publicznego obiektu blob](https://cahandson.blob.core.windows.net/samples/volcano.json) w bazie danych rozwiązania Cosmos przy użyciu narzędzia migracji toohello parametry polecenia następujące (dtui.exe z katalogu hello zainstalowaną hello rozwiązania Cosmos narzędzia do migracji bazy danych).</span><span class="sxs-lookup"><span data-stu-id="60623-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="60623-354">Wprowadź lokalizację źródłowa i docelowa hello z następującymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="60623-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="60623-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/; AccountKey = [[klucz]; Baza danych = /t.Collection:volcano1 swe dzieła</span><span class="sxs-lookup"><span data-stu-id="60623-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="60623-356">Po zaimportowaniu danych hello, możesz przejść tooJupyter i otwórz hello notesu zatytułowany *DocumentDBSample* zawierającą python code tooaccess usługi DocumentDB i czy niektóre podstawowe zapytań.</span><span class="sxs-lookup"><span data-stu-id="60623-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="60623-357">Możesz dodatkowe informacje na temat rozwiązania Cosmos DB, przechodząc na stronę usługi hello [stronę dokumentacji](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="60623-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="60623-358">8. Twórz raporty i pulpit nawigacyjny za pomocą hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="60623-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="60623-359">Daj nam wizualizacji pliku JSON swe dzieła hello, którą widzieliśmy w hello poprzedzających przykład DB rozwiązania Cosmos w usłudze Power BI toogain visual wgląd w dane hello.</span><span class="sxs-lookup"><span data-stu-id="60623-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="60623-360">Szczegółowy opis kroków są dostępne w hello [artykułu usługi Power BI](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="60623-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="60623-361">Poniżej przedstawiono ogólne kroki hello:</span><span class="sxs-lookup"><span data-stu-id="60623-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="60623-362">Otwórz Power BI Desktop i wykonaj "Pobierz dane".</span><span class="sxs-lookup"><span data-stu-id="60623-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="60623-363">Określ adres URL hello: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="60623-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="60623-364">Powinny pojawić zaimportowany jako listę rekordów JSON hello</span><span class="sxs-lookup"><span data-stu-id="60623-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="60623-365">Konwertuj Tabela tooa listy hello dzięki usłudze Power BI można pracować z hello takie same</span><span class="sxs-lookup"><span data-stu-id="60623-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="60623-366">Rozwiń kolumny hello, klikając hello Rozwiń ikonę (hello jedną ikoną "Strzałka w lewo i Strzałka w prawo" hello na powitania rogu hello kolumny)</span><span class="sxs-lookup"><span data-stu-id="60623-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="60623-367">Należy zauważyć, że lokalizacja znajduje się pole "Rekordu".</span><span class="sxs-lookup"><span data-stu-id="60623-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="60623-368">Rozwiń hello rekordu i wybierz tylko hello współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="60623-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="60623-369">Współrzędna jest kolumna listy</span><span class="sxs-lookup"><span data-stu-id="60623-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="60623-370">Dodaj nową kolumnę tooconvert hello listy współrzędnych kolumnę do przecinkami osobna kolumna LatLong łączenie hello dwa elementy w polu listy współrzędnych hello przy użyciu formuły hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="60623-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="60623-371">Na koniec przekonwertować hello ```Elevation``` tooDecimal kolumny i wybierz hello **Zamknij** i **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="60623-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="60623-372">Zamiast poprzednich krokach, możesz wkleić hello następującego kodu, który skrypty czynności hello używane w hello Zaawansowany edytor w usłudze Power BI umożliwia przekształcenia danych hello toowrite język kwerendy.</span><span class="sxs-lookup"><span data-stu-id="60623-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="60623-373">Masz teraz hello danych w modelu danych usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="60623-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="60623-374">Usługa Power BI pulpitu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="60623-374">Your Power BI desktop should appear as follows:</span></span>

![Program Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="60623-376">Można rozpocząć tworzenie raportów i wizualizacje przy użyciu hello modelu danych.</span><span class="sxs-lookup"><span data-stu-id="60623-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="60623-377">Możesz wykonać kroki hello na tym [artykułu usługi Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild raportu.</span><span class="sxs-lookup"><span data-stu-id="60623-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="60623-378">wynik końcowy Hello jest raport, który wygląda hello.</span><span class="sxs-lookup"><span data-stu-id="60623-378">hello end result is a report that looks like hello following.</span></span>

![Power BI Desktop widoku raportu - łącznika usługi Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="60623-380">9. Dynamiczne skalowanie toomeet Twojego DSVM, potrzebne w projekcie</span><span class="sxs-lookup"><span data-stu-id="60623-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="60623-381">Możesz skalować toomeet DSVM hello, który projekt w górę i w dół.</span><span class="sxs-lookup"><span data-stu-id="60623-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="60623-382">Jeśli nie potrzebujesz hello toouse maszyny Wirtualnej w hello wieczorem lub w weekendy, można po prostu zamknąć hello maszyny Wirtualnej z hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60623-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="60623-383">Ponosisz opłat za obliczenia, jeśli używasz tylko hello przycisku zamknięcia systemu operacyjnego na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="60623-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="60623-384">Jeśli konieczne toohandle analizy dużych i potrzebujesz większej pojemności procesora CPU, pamięć lub dysk można znaleźć wybór dużych rozmiarów maszyn wirtualnych w postaci liczby rdzeni Procesora, pamięci i typów dysków (w tym dysków półprzewodnikowych), które spełniają Twoich potrzeb dotyczących budżetowych i obliczeń.</span><span class="sxs-lookup"><span data-stu-id="60623-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="60623-385">Witaj Pełna lista maszyn wirtualnych wraz z ich ceny co godzinę obliczeń jest dostępna na powitania [cennik maszyn wirtualnych Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) strony.</span><span class="sxs-lookup"><span data-stu-id="60623-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="60623-386">Podobnie jeśli zmniejsza potrzeby wydajności przetwarzania maszyny Wirtualnej (na przykład: przenieść tooa najważniejszych obciążeń Hadoop lub w klastrze Spark), można skalować w dół hello klastra z hello [portalu Azure](https://portal.azure.com) i będą toohello ustawienia maszyny wirtualnej wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="60623-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="60623-387">Poniżej przedstawiono zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="60623-387">Here is a screenshot.</span></span>

![Ustawienia wystąpienie maszyny Wirtualnej](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="60623-389">10. Instalowanie dodatkowych narzędzi na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="60623-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="60623-390">Firma Microsoft ma spakowane kilka narzędzi, które mamy nadzieję, że są w stanie tooaddress wielu hello wspólne dane analizy potrzeb, a powinien zaoszczędzić czas, przez co pozwala uniknąć konieczności tooinstall i konfigurowanie środowiska jeden po drugim i oszczędność pieniędzy przez płatności tylko dla zasobów, które Użycie.</span><span class="sxs-lookup"><span data-stu-id="60623-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="60623-391">Można korzystać z innych danych Azure i usługi analizy profilowane w tym artykule tooenhance środowiska analytics.</span><span class="sxs-lookup"><span data-stu-id="60623-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="60623-392">Zdajemy w niektórych przypadkach potrzeb może wymagać dodatkowych narzędzi, w tym niektórych zastrzeżonych innych firm.</span><span class="sxs-lookup"><span data-stu-id="60623-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="60623-393">Masz pełny dostęp administracyjny na powitania maszyny wirtualnej tooinstall nowe narzędzia potrzebne.</span><span class="sxs-lookup"><span data-stu-id="60623-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="60623-394">Można także zainstalować dodatkowe pakiety Python i R, które nie są wstępnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="60623-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="60623-395">Dla języka Python możesz użyć dowolnej ```conda``` lub ```pip```.</span><span class="sxs-lookup"><span data-stu-id="60623-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="60623-396">R można użyć hello ```install.packages()``` w hello R konsoli lub za pomocą hello IDE i wybierz "**pakiety** -> **instalowanie pakietów** ".</span><span class="sxs-lookup"><span data-stu-id="60623-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="60623-397">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="60623-397">Summary</span></span>
<span data-ttu-id="60623-398">Są to tylko niektóre hello czynności, które można wykonać na powitania maszyny wirtualnej nauki danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="60623-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="60623-399">Istnieje wiele więcej sposobów toomake go środowisku analytics skuteczne.</span><span class="sxs-lookup"><span data-stu-id="60623-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

