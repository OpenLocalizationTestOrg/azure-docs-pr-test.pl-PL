---
title: "zestawy danych aaaAccess z biblioteki klienta usługi Machine Learning Python | Dokumentacja firmy Microsoft"
description: "Zainstalować i używać hello Python klienta biblioteki tooaccess danych i zarządzać nimi usługi Azure Machine Learning bezpiecznie z lokalnym środowiskiem Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="6980a-103">Zestawy danych dostęp za pomocą biblioteki klienta usługi Azure Machine Learning Python hello języka Python</span><span class="sxs-lookup"><span data-stu-id="6980a-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="6980a-104">Podgląd Hello biblioteki klienta usługi Microsoft Azure Machine Learning Python można włączyć bezpieczny dostęp tooyour zestawy danych usługi Azure Machine Learning z lokalnym środowiskiem Python i umożliwia tworzenie hello i Zarządzanie zestawami danych w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="6980a-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="6980a-105">Ten temat zawiera instrukcje dotyczące sposobu:</span><span class="sxs-lookup"><span data-stu-id="6980a-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="6980a-106">Zainstaluj biblioteki klienta usługi Machine Learning Python hello</span><span class="sxs-lookup"><span data-stu-id="6980a-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="6980a-107">dostęp i przekazać zestawów danych, w tym instrukcje dotyczące tooget autoryzacji tooaccess zestawy danych usługi Azure Machine Learning z lokalnego środowiska Python</span><span class="sxs-lookup"><span data-stu-id="6980a-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="6980a-108">dostęp do pośredniego zestawów danych z eksperymentów</span><span class="sxs-lookup"><span data-stu-id="6980a-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="6980a-109">używać zestawów danych hello Python klienta biblioteki tooenumerate, uzyskuje dostęp do metadanych, odczytu zawartości hello zestawu danych, Utwórz nowy zestaw danych i zaktualizować istniejący zestaw danych</span><span class="sxs-lookup"><span data-stu-id="6980a-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="6980a-110"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6980a-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="6980a-111">Biblioteka klienta Python Hello był testowany w obszarze hello następującego środowiska:</span><span class="sxs-lookup"><span data-stu-id="6980a-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="6980a-112">Windows, Mac i Linux</span><span class="sxs-lookup"><span data-stu-id="6980a-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="6980a-113">Python 2.7 3.3 i 3.4</span><span class="sxs-lookup"><span data-stu-id="6980a-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="6980a-114">Ma ona zależność na powitania następujące pakiety:</span><span class="sxs-lookup"><span data-stu-id="6980a-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="6980a-115">żądania</span><span class="sxs-lookup"><span data-stu-id="6980a-115">requests</span></span>
* <span data-ttu-id="6980a-116">dateutil języka Python</span><span class="sxs-lookup"><span data-stu-id="6980a-116">python-dateutil</span></span>
* <span data-ttu-id="6980a-117">pandas</span><span class="sxs-lookup"><span data-stu-id="6980a-117">pandas</span></span>

<span data-ttu-id="6980a-118">Firma Microsoft zaleca używanie dystrybucję oprogramowania Python, takie jak [Anaconda](http://continuum.io/downloads#all) lub [korony](https://store.enthought.com/downloads/), które pochodzą z języka Python, IPython i zainstalowane pakiety hello trzech z wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="6980a-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="6980a-119">Chociaż IPython nie jest ścisłym wymogiem, jest doskonałe środowisko manipulowanie i wizualizacja danych interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="6980a-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="6980a-120"><a name="installation"></a>Jak tooinstall hello biblioteki klienta usługi Azure Machine Learning Python</span><span class="sxs-lookup"><span data-stu-id="6980a-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="6980a-121">Biblioteka klienta usługi Azure Machine Learning Python Hello musi być zainstalowany toocomplete hello zadania opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="6980a-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="6980a-122">Jest ona dostępna z hello [indeksu pakietów języka Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="6980a-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="6980a-123">tooinstall uruchom go w środowisku Python hello następujące polecenie z lokalnego środowiska Python:</span><span class="sxs-lookup"><span data-stu-id="6980a-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="6980a-124">Alternatywnie można pobrać i zainstalować ze źródeł hello na [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="6980a-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="6980a-125">Jeśli masz git na komputerze jest zainstalowany program pip tooinstall bezpośrednio z repozytorium git hello:</span><span class="sxs-lookup"><span data-stu-id="6980a-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="6980a-126"><a name="datasetAccess"></a>Użyj zbiorów danych tooaccess wstawki kodu Studio</span><span class="sxs-lookup"><span data-stu-id="6980a-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="6980a-127">Biblioteka klienta Python Hello daje istniejący zestaw danych dostęp programistyczny tooyour z doświadczenia, które zostały uruchomione.</span><span class="sxs-lookup"><span data-stu-id="6980a-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="6980a-128">Z interfejsem sieci web Studio hello można wygenerować wstawki kodu, obejmujących wszystkie toodownload koniecznych hello oraz deserializacji zestawy danych jako obiekty Pandas DataFrame na komputerze lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6980a-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="6980a-129"><a name="security"></a>Zabezpieczenia dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="6980a-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="6980a-130">Witaj podał Studio do użycia z biblioteki klienta Python hello zawiera identyfikator i autoryzacji wstawki kodu tokenu.</span><span class="sxs-lookup"><span data-stu-id="6980a-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="6980a-131">Te zapewniają roboczym tooyour pełny dostęp i musi być chroniony, takie jak hasła.</span><span class="sxs-lookup"><span data-stu-id="6980a-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="6980a-132">Ze względów bezpieczeństwa funkcja fragment kodu hello jest tylko dostępne toousers, mające ich roli Ustaw jako **właściciela** hello obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6980a-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="6980a-133">Rola użytkownika jest wyświetlany w usłudze Azure Machine Learning Studio na powitania **użytkowników** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6980a-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Bezpieczeństwo][security]

<span data-ttu-id="6980a-135">Jeśli rola użytkownika nie jest ustawiony jako **właściciela**, możesz zażądać toobe reinvited jako właściciela, lub poproś właściciela hello hello tooprovide obszaru roboczego z hello fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="6980a-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="6980a-136">token autoryzacji hello tooobtain, możesz wybrać jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="6980a-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="6980a-137">Prosić o token właściciela.</span><span class="sxs-lookup"><span data-stu-id="6980a-137">Ask for a token from an owner.</span></span> <span data-ttu-id="6980a-138">Właściciele mogą uzyskiwać dostęp do swoich tokenów autoryzacji ze strony ustawień hello ich obszaru roboczego w Studio.</span><span class="sxs-lookup"><span data-stu-id="6980a-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="6980a-139">Wybierz **ustawienia** z hello lewego okienka i kliknij przycisk **TOKENY autoryzacji** toosee hello tokeny podstawowego i pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="6980a-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="6980a-140">Chociaż hello podstawowego lub tokeny dodatkowej autoryzacji hello można używać we fragmencie kodu hello, zaleca się, że właścicieli udostępniać tylko tokeny dodatkowej autoryzacji hello.</span><span class="sxs-lookup"><span data-stu-id="6980a-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Tokeny autoryzacji](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="6980a-142">Poproś toorole toobe awansowane właściciela.</span><span class="sxs-lookup"><span data-stu-id="6980a-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="6980a-143">toodo to bieżącego właściciela hello obszaru roboczego musi toofirst należy usunąć z obszaru roboczego hello, a następnie ponownie Cię zaprosił tooit jako właściciela.</span><span class="sxs-lookup"><span data-stu-id="6980a-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="6980a-144">Po uzyskaniu deweloperzy autoryzacji i identyfikator obszaru roboczego hello tokenu, są one możliwe tooaccess hello roboczym przy użyciu hello fragment kodu, niezależnie od ich roli.</span><span class="sxs-lookup"><span data-stu-id="6980a-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="6980a-145">Tokeny autoryzacji są zarządzane na powitania **TOKENY autoryzacji** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6980a-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="6980a-146">Ponowne ich wygenerowanie, ale w tej procedurze odwołuje dostęp toohello poprzednim tokenem.</span><span class="sxs-lookup"><span data-stu-id="6980a-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="6980a-147"><a name="accessingDatasets"></a>Zestawy dostępu do danych z aplikacji lokalnej Python</span><span class="sxs-lookup"><span data-stu-id="6980a-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="6980a-148">W usłudze Machine Learning Studio, kliknij przycisk **zestawów danych** hello pasku nawigacyjnym po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="6980a-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="6980a-149">Wybierz zestaw danych hello chcesz tooaccess.</span><span class="sxs-lookup"><span data-stu-id="6980a-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="6980a-150">Można wybrać dowolny hello zestawów danych z hello **Moje zestawów danych** listy lub hello **przykłady** listy.</span><span class="sxs-lookup"><span data-stu-id="6980a-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="6980a-151">Witaj dolnym pasku narzędzi kliknij **Generuj kod dostępu do danych**.</span><span class="sxs-lookup"><span data-stu-id="6980a-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="6980a-152">Jeśli dane hello jest w formacie niezgodne z biblioteki klienta hello Python, ten przycisk jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6980a-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![Zestawy danych][datasets]
4. <span data-ttu-id="6980a-154">Wybierz hello fragment kodu z wyświetlonym oknie hello i skopiuj go tooyour Schowka.</span><span class="sxs-lookup"><span data-stu-id="6980a-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Kod dostępu][dataset-access-code]
5. <span data-ttu-id="6980a-156">Wklej kod hello do notesu hello lokalnej aplikacji Python.</span><span class="sxs-lookup"><span data-stu-id="6980a-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Notesu][ipython-dataset]

## <span data-ttu-id="6980a-158"><a name="accessingIntermediateDatasets"></a>Dostęp do pośredniego zestawów danych z eksperymentów uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="6980a-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="6980a-159">Po uruchomieniu eksperymentu w usłudze Machine Learning Studio hello jest możliwe tooaccess hello pośredniego zestawy danych z węzłów wyjściowych hello modułów.</span><span class="sxs-lookup"><span data-stu-id="6980a-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="6980a-160">Pośredni zestawów danych są dane, które zostały utworzone i jest używany do pośredniego kroki po uruchomieniu narzędzia modelu.</span><span class="sxs-lookup"><span data-stu-id="6980a-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="6980a-161">Tak długo, jak hello format danych jest zgodny z biblioteki klienta Python hello pośredniego zestawów danych są dostępne.</span><span class="sxs-lookup"><span data-stu-id="6980a-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="6980a-162">Witaj obsługiwane są następujące formaty (stałe tych znajdują się w hello `azureml.DataTypeIds` klasy):</span><span class="sxs-lookup"><span data-stu-id="6980a-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="6980a-163">W postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="6980a-163">PlainText</span></span>
* <span data-ttu-id="6980a-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="6980a-164">GenericCSV</span></span>
* <span data-ttu-id="6980a-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="6980a-165">GenericTSV</span></span>
* <span data-ttu-id="6980a-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6980a-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="6980a-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6980a-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="6980a-168">Można określić formatu hello, ustawiając kursor nad węzłem danych wyjściowych modułu.</span><span class="sxs-lookup"><span data-stu-id="6980a-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="6980a-169">Jest on wyświetlany wraz z hello nazwa węzła, w etykietce narzędzia.</span><span class="sxs-lookup"><span data-stu-id="6980a-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="6980a-170">Niektóre moduły hello, na przykład hello [podziału] [ split] modułu, dane wyjściowe tooa formatu o nazwie `Dataset`, który nie jest obsługiwany przez bibliotekę klienta Python hello.</span><span class="sxs-lookup"><span data-stu-id="6980a-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Format zestawu danych][dataset-format]

<span data-ttu-id="6980a-172">Należy toouse moduł konwersji, takich jak [przekonwertować tooCSV][convert-to-csv], tooget dane wyjściowe do obsługiwanego formatu.</span><span class="sxs-lookup"><span data-stu-id="6980a-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![GenericCSV Format][csv-format]

<span data-ttu-id="6980a-174">Hello następujących krokach przedstawiono przykład, w którym tworzy eksperyment, uruchamia go i uzyskuje dostęp do hello pośredniego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="6980a-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="6980a-175">Tworzenie nowego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="6980a-175">Create a new experiment.</span></span>
2. <span data-ttu-id="6980a-176">Wstaw **zestawu danych dla dorosłych klasyfikacji binarnej dochodu spisu** modułu.</span><span class="sxs-lookup"><span data-stu-id="6980a-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="6980a-177">Wstaw [podziału] [ split] modułu i połącz dane wyjściowe toohello wejściowy zestaw danych modułu.</span><span class="sxs-lookup"><span data-stu-id="6980a-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="6980a-178">Wstaw [przekonwertować tooCSV] [ convert-to-csv] modułu i Połącz z jego wejściowych tooone hello [podziału] [ split] danych wyjściowych modułu.</span><span class="sxs-lookup"><span data-stu-id="6980a-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="6980a-179">Zapisz hello eksperymentu, uruchom go i poczekaj na jej toofinish uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6980a-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="6980a-180">Kliknij węzeł danych wyjściowych hello na powitania [przekonwertować tooCSV] [ convert-to-csv] modułu.</span><span class="sxs-lookup"><span data-stu-id="6980a-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="6980a-181">Po wyświetleniu menu kontekstowe hello zaznacz **Generuj kod dostępu do danych**.</span><span class="sxs-lookup"><span data-stu-id="6980a-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menu kontekstowe][experiment]
8. <span data-ttu-id="6980a-183">Wybierz hello fragment kodu i skopiuj go tooyour Schowka z wyświetlonym oknie hello.</span><span class="sxs-lookup"><span data-stu-id="6980a-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Kod dostępu][intermediate-dataset-access-code]
9. <span data-ttu-id="6980a-185">Wklej kod hello w Notatniku.</span><span class="sxs-lookup"><span data-stu-id="6980a-185">Paste hello code in your notebook.</span></span>
   
    ![Notesu][ipython-intermediate-dataset]
10. <span data-ttu-id="6980a-187">Można zwizualizować hello danych przy użyciu matplotlib.</span><span class="sxs-lookup"><span data-stu-id="6980a-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="6980a-188">Spowoduje to wyświetlenie w histogram hello wieku kolumny:</span><span class="sxs-lookup"><span data-stu-id="6980a-188">This displays in a histogram for hello age column:</span></span>
    
    ![Histogram][ipython-histogram]

## <span data-ttu-id="6980a-190"><a name="clientApis"></a>Użyj hello tooaccess biblioteki klienta Machine Learning Python, odczytu, tworzenie i zarządzanie nimi zbiory danych</span><span class="sxs-lookup"><span data-stu-id="6980a-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="6980a-191">Obszar roboczy</span><span class="sxs-lookup"><span data-stu-id="6980a-191">Workspace</span></span>
<span data-ttu-id="6980a-192">obszar roboczy Hello jest punkt wejścia hello hello Python klienta biblioteki.</span><span class="sxs-lookup"><span data-stu-id="6980a-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="6980a-193">Podaj hello `Workspace` klasy z z obszaru roboczego toocreate połączeń tokenu identyfikator i autoryzacji wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="6980a-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="6980a-194">Wyliczanie obiektów DataSet</span><span class="sxs-lookup"><span data-stu-id="6980a-194">Enumerate datasets</span></span>
<span data-ttu-id="6980a-195">tooenumerate wszystkie zestawy danych danego obszaru roboczego:</span><span class="sxs-lookup"><span data-stu-id="6980a-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="6980a-196">tooenumerate hello właśnie utworzone przez użytkownika zestawów danych:</span><span class="sxs-lookup"><span data-stu-id="6980a-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="6980a-197">przykład Witaj tylko tooenumerate zestawów danych:</span><span class="sxs-lookup"><span data-stu-id="6980a-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="6980a-198">Aby dostęp do zestawu danych, według nazwy (która jest uwzględniana wielkość liter):</span><span class="sxs-lookup"><span data-stu-id="6980a-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="6980a-199">Lub zostanie do niego dostęp przez indeks:</span><span class="sxs-lookup"><span data-stu-id="6980a-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="6980a-200">Metadane</span><span class="sxs-lookup"><span data-stu-id="6980a-200">Metadata</span></span>
<span data-ttu-id="6980a-201">Zestaw danych ma metadanych, w toocontent dodanie.</span><span class="sxs-lookup"><span data-stu-id="6980a-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="6980a-202">(Zestaw pośrednich danych są reguły toothis wyjątku i nie ma żadnych metadanych).</span><span class="sxs-lookup"><span data-stu-id="6980a-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="6980a-203">Niektóre wartości metadanych są przypisane przez użytkownika hello w czasie tworzenia:</span><span class="sxs-lookup"><span data-stu-id="6980a-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="6980a-204">Inne są wartości przypisane przez uczenie Maszynowe Azure:</span><span class="sxs-lookup"><span data-stu-id="6980a-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="6980a-205">Zobacz hello `SourceDataset` klasy więcej w metadanych dostępnych hello.</span><span class="sxs-lookup"><span data-stu-id="6980a-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="6980a-206">Odczytaj zawartość</span><span class="sxs-lookup"><span data-stu-id="6980a-206">Read contents</span></span>
<span data-ttu-id="6980a-207">wstawki kodu Hello udostępniane przez usługi Machine Learning Studio automatycznie Pobierz i deserializacji obiektu Pandas DataFrame tooa dataset hello.</span><span class="sxs-lookup"><span data-stu-id="6980a-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="6980a-208">Jest to zrobić za pomocą hello `to_dataframe` metody:</span><span class="sxs-lookup"><span data-stu-id="6980a-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="6980a-209">Jeśli preferowane toodownload hello nieprzetworzone dane i samodzielnie przeprowadzić deserializacji hello, który jest opcją.</span><span class="sxs-lookup"><span data-stu-id="6980a-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="6980a-210">W momencie hello jest tylko opcja hello formatów, takich jak "ARFF", które biblioteki klienta Python hello nie można wykonać deserializacji.</span><span class="sxs-lookup"><span data-stu-id="6980a-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="6980a-211">zawartość hello tooread jako tekst:</span><span class="sxs-lookup"><span data-stu-id="6980a-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="6980a-212">zawartość hello tooread jako wartość binarną:</span><span class="sxs-lookup"><span data-stu-id="6980a-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="6980a-213">Możesz także po prostu otworzyć zawartość toohello strumienia:</span><span class="sxs-lookup"><span data-stu-id="6980a-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="6980a-214">Utwórz nowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="6980a-214">Create a new dataset</span></span>
<span data-ttu-id="6980a-215">Biblioteka klienta Python Hello umożliwia zestawów tooupload danych z programu Python.</span><span class="sxs-lookup"><span data-stu-id="6980a-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="6980a-216">Te zestawy danych będą dostępne do użycia w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="6980a-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="6980a-217">Jeśli dane znajdują się w Pandas DataFrame, użyj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="6980a-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="6980a-218">Jeśli dane są już serializowane, możesz użyć:</span><span class="sxs-lookup"><span data-stu-id="6980a-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="6980a-219">Witaj Python jest biblioteka klienta stanie tooserialize następujące toohello Pandas DataFrame formatuje (stałe tych znajdują się w hello `azureml.DataTypeIds` klasy):</span><span class="sxs-lookup"><span data-stu-id="6980a-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="6980a-220">W postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="6980a-220">PlainText</span></span>
* <span data-ttu-id="6980a-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="6980a-221">GenericCSV</span></span>
* <span data-ttu-id="6980a-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="6980a-222">GenericTSV</span></span>
* <span data-ttu-id="6980a-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6980a-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="6980a-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="6980a-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="6980a-225">Aktualizuj istniejący zestaw danych</span><span class="sxs-lookup"><span data-stu-id="6980a-225">Update an existing dataset</span></span>
<span data-ttu-id="6980a-226">Jeśli spróbujesz tooupload nowy zestaw danych o nazwie, która odpowiada istniejący zestaw danych, należy pobrać błąd konfliktu.</span><span class="sxs-lookup"><span data-stu-id="6980a-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="6980a-227">tooupdate istniejący zestaw danych, należy najpierw tooget toohello istniejący zestaw danych odwołania:</span><span class="sxs-lookup"><span data-stu-id="6980a-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="6980a-228">Następnie użyj `update_from_dataframe` tooserialize i Zastąp zawartość hello dataset hello Azure:</span><span class="sxs-lookup"><span data-stu-id="6980a-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="6980a-229">Tooserialize hello danych tooa innym formacie należy określić wartość dla hello opcjonalne `data_type_id` parametru.</span><span class="sxs-lookup"><span data-stu-id="6980a-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="6980a-230">Opcjonalnie możesz ustawić nowy opis, określając wartość hello `description` parametru.</span><span class="sxs-lookup"><span data-stu-id="6980a-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="6980a-231">Opcjonalnie możesz ustawić nową nazwę, określając wartość hello `name` parametru.</span><span class="sxs-lookup"><span data-stu-id="6980a-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="6980a-232">Od teraz będziesz pobrać hello zestawu danych za pomocą hello tylko nową nazwę.</span><span class="sxs-lookup"><span data-stu-id="6980a-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="6980a-233">Witaj następującego kodu aktualizuje hello danych, nazwę i opis.</span><span class="sxs-lookup"><span data-stu-id="6980a-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="6980a-234">Witaj `data_type_id`, `name` i `description` parametry są opcjonalne i domyślne tootheir poprzedniej wartości.</span><span class="sxs-lookup"><span data-stu-id="6980a-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="6980a-235">Witaj `dataframe` parametru jest zawsze wymagane.</span><span class="sxs-lookup"><span data-stu-id="6980a-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="6980a-236">Jeśli dane są już serializowane, użyj `update_from_raw_data` zamiast `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="6980a-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="6980a-237">Jeśli po prostu Przekaż w `raw_data` zamiast `dataframe`, działa w podobny sposób.</span><span class="sxs-lookup"><span data-stu-id="6980a-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

