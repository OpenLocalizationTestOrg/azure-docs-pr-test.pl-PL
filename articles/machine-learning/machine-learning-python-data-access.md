---
title: "Dostęp do zestawów danych z biblioteki klienta usługi Machine Learning Python | Dokumentacja firmy Microsoft"
description: "Zainstaluj i Python biblioteki klienta umożliwiają dostęp do danych i zarządzać nimi usługi Azure Machine Learning bezpiecznie z lokalnego środowiska Python."
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="84764-103">Dostęp do zestawów danych z językiem Python za pomocą biblioteki klienta Python usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="84764-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="84764-104">Biblioteka klienta usługi Microsoft Azure Machine Learning Python w wersji zapoznawczej można włączyć bezpieczny dostęp do usługi Azure Machine Learning zestawów danych z lokalnego środowiska Python i umożliwia tworzenie i Zarządzanie zestawami danych w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="84764-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="84764-105">Ten temat zawiera instrukcje dotyczące sposobu:</span><span class="sxs-lookup"><span data-stu-id="84764-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="84764-106">Zainstaluj biblioteki klienckie Machine Learning Python</span><span class="sxs-lookup"><span data-stu-id="84764-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="84764-107">dostęp i przekazać zestawów danych, w tym instrukcje dotyczące sposobu uzyskania autoryzacji dostępu do usługi Azure Machine Learning zestawów danych z lokalnego środowiska Python</span><span class="sxs-lookup"><span data-stu-id="84764-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="84764-108">dostęp do pośredniego zestawów danych z eksperymentów</span><span class="sxs-lookup"><span data-stu-id="84764-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="84764-109">Użyj biblioteki klienckiej Python wyliczyć zestawów danych, dostępu do metadanych, wczytanie zawartości zestawu danych, Utwórz nowy zestaw danych i zaktualizować istniejący zestaw danych</span><span class="sxs-lookup"><span data-stu-id="84764-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="84764-110"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="84764-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="84764-111">Biblioteka klienta Python był testowany w następujących środowiskach:</span><span class="sxs-lookup"><span data-stu-id="84764-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="84764-112">Windows, Mac i Linux</span><span class="sxs-lookup"><span data-stu-id="84764-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="84764-113">Python 2.7 3.3 i 3.4</span><span class="sxs-lookup"><span data-stu-id="84764-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="84764-114">Ma ona zależność od następujących pakietów:</span><span class="sxs-lookup"><span data-stu-id="84764-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="84764-115">żądania</span><span class="sxs-lookup"><span data-stu-id="84764-115">requests</span></span>
* <span data-ttu-id="84764-116">dateutil języka Python</span><span class="sxs-lookup"><span data-stu-id="84764-116">python-dateutil</span></span>
* <span data-ttu-id="84764-117">pandas</span><span class="sxs-lookup"><span data-stu-id="84764-117">pandas</span></span>

<span data-ttu-id="84764-118">Firma Microsoft zaleca używanie dystrybucję oprogramowania Python, takie jak [Anaconda](http://continuum.io/downloads#all) lub [korony](https://store.enthought.com/downloads/), które pochodzą z języka Python, IPython i zainstalować trzy pakiety wymienione powyżej.</span><span class="sxs-lookup"><span data-stu-id="84764-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="84764-119">Chociaż IPython nie jest ścisłym wymogiem, jest doskonałe środowisko manipulowanie i wizualizacja danych interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="84764-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="84764-120"><a name="installation"></a>Jak zainstalować biblioteki klienta usługi Azure Machine Learning Python</span><span class="sxs-lookup"><span data-stu-id="84764-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="84764-121">Biblioteka klienta usługi Azure Machine Learning Python musi być zainstalowany także wykonać zadania opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="84764-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="84764-122">Jest ona dostępna z [indeksu pakietów języka Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="84764-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="84764-123">Aby zainstalować go w środowisku Python, uruchom następujące polecenie z lokalnego środowiska Python:</span><span class="sxs-lookup"><span data-stu-id="84764-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="84764-124">Alternatywnie można pobrać i zainstalować ze źródeł na [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="84764-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="84764-125">Jeśli masz zainstalowany na tym komputerze git umożliwia pip zainstalować bezpośrednio z repozytorium git:</span><span class="sxs-lookup"><span data-stu-id="84764-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="84764-126"><a name="datasetAccess"></a>Wstawki kodu Studio umożliwia dostęp do zestawów danych</span><span class="sxs-lookup"><span data-stu-id="84764-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="84764-127">Biblioteka klienta Python umożliwia programowy dostęp do istniejących zestawów danych z eksperymentów, które zostały uruchomione.</span><span class="sxs-lookup"><span data-stu-id="84764-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="84764-128">W interfejsie sieci web Studio mogą generować wstawki kodu, które obejmują wszystkie informacje niezbędne do pobrania i deserializacji zestawy danych jako obiekty Pandas DataFrame na komputerze lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="84764-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="84764-129"><a name="security"></a>Zabezpieczenia dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="84764-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="84764-130">Wstawki kodu podał Studio do użycia z biblioteki klienta Python zawiera identyfikator i autoryzacji tokenu.</span><span class="sxs-lookup"><span data-stu-id="84764-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="84764-131">Te umożliwianie pełnego dostępu do swojego obszaru roboczego i musi być chroniony, takie jak hasła.</span><span class="sxs-lookup"><span data-stu-id="84764-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="84764-132">Ze względów bezpieczeństwa funkcje wstawek kodu jest dostępna tylko dla użytkowników, którzy mają ich roli Ustaw jako **właściciela** dla obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="84764-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="84764-133">Rola użytkownika jest wyświetlany w usłudze Azure Machine Learning Studio na **użytkowników** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="84764-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![Bezpieczeństwo][security]

<span data-ttu-id="84764-135">Jeśli rola użytkownika nie jest ustawiony jako **właściciela**, możesz albo żądanie można reinvited jako właściciela lub poproś właściciela obszaru roboczego dostarczają fragmentu kodu.</span><span class="sxs-lookup"><span data-stu-id="84764-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="84764-136">Aby uzyskać token autoryzacji, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="84764-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="84764-137">Prosić o token właściciela.</span><span class="sxs-lookup"><span data-stu-id="84764-137">Ask for a token from an owner.</span></span> <span data-ttu-id="84764-138">Właściciele mogą uzyskiwać dostęp do swoich tokenów autoryzacji ze strony ustawień ich obszaru roboczego w Studio.</span><span class="sxs-lookup"><span data-stu-id="84764-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="84764-139">Wybierz **ustawienia** w okienku po lewej stronie, kliknij **TOKENY autoryzacji** wyświetlić tokeny podstawowego i pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="84764-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="84764-140">Chociaż podstawowej lub dodatkowej autoryzacji tokenów można używać we fragmencie kodu, zaleca się, że właścicieli udostępniać tylko tokeny dodatkowej autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="84764-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![Tokeny autoryzacji](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="84764-142">Poproś funkcjonować jako rolę właściciela.</span><span class="sxs-lookup"><span data-stu-id="84764-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="84764-143">Aby to zrobić, bieżącego właściciela obszaru roboczego musi najpierw należy usunąć z obszaru roboczego, a następnie ponownie zapraszać do niego jako właściciela.</span><span class="sxs-lookup"><span data-stu-id="84764-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="84764-144">Po uzyskaniu deweloperzy autoryzacji i identyfikator obszaru roboczego tokenu, są w stanie uzyskać dostępu do obszaru roboczego przy użyciu fragment kodu, niezależnie od ich roli.</span><span class="sxs-lookup"><span data-stu-id="84764-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="84764-145">Tokeny autoryzacji są zarządzane na **TOKENY autoryzacji** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="84764-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="84764-146">Ponowne ich wygenerowanie, ale w tej procedurze odwołuje dostęp do poprzednim tokenem.</span><span class="sxs-lookup"><span data-stu-id="84764-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="84764-147"><a name="accessingDatasets"></a>Zestawy dostępu do danych z aplikacji lokalnej Python</span><span class="sxs-lookup"><span data-stu-id="84764-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="84764-148">W usłudze Machine Learning Studio, kliknij przycisk **zestawów danych** na pasku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="84764-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="84764-149">Wybierz zestaw danych, które chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="84764-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="84764-150">Można wybrać dowolny z zestawów danych z **Moje zestawów danych** listy lub **przykłady** listy.</span><span class="sxs-lookup"><span data-stu-id="84764-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="84764-151">W dolnym pasku narzędzi, kliknij polecenie **Generuj kod dostępu do danych**.</span><span class="sxs-lookup"><span data-stu-id="84764-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="84764-152">Jeśli dane są w formacie niezgodne z biblioteki klienta języka Python, ten przycisk jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="84764-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![Zestawy danych][datasets]
4. <span data-ttu-id="84764-154">Wybierz fragment kodu z okna wyświetlana i skopiuj go do Schowka.</span><span class="sxs-lookup"><span data-stu-id="84764-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![Kod dostępu][dataset-access-code]
5. <span data-ttu-id="84764-156">Wklej kod do notesu lokalnych aplikacji Python.</span><span class="sxs-lookup"><span data-stu-id="84764-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![Notesu][ipython-dataset]

## <span data-ttu-id="84764-158"><a name="accessingIntermediateDatasets"></a>Dostęp do pośredniego zestawów danych z eksperymentów uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="84764-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="84764-159">Po uruchomieniu eksperymentu w usłudze Machine Learning Studio istnieje możliwość dostępu do pośredniego zestawów danych z węzłów wyjściowych modułów.</span><span class="sxs-lookup"><span data-stu-id="84764-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="84764-160">Pośredni zestawów danych są dane, które zostały utworzone i jest używany do pośredniego kroki po uruchomieniu narzędzia modelu.</span><span class="sxs-lookup"><span data-stu-id="84764-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="84764-161">Zestaw pośrednich danych jest możliwy tak długo, jak format danych jest zgodny z biblioteki klienta języka Python.</span><span class="sxs-lookup"><span data-stu-id="84764-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="84764-162">Obsługiwane są następujące formaty (stałe tych znajdują się w `azureml.DataTypeIds` klasy):</span><span class="sxs-lookup"><span data-stu-id="84764-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="84764-163">W postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="84764-163">PlainText</span></span>
* <span data-ttu-id="84764-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="84764-164">GenericCSV</span></span>
* <span data-ttu-id="84764-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="84764-165">GenericTSV</span></span>
* <span data-ttu-id="84764-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="84764-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="84764-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="84764-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="84764-168">Format można określić, ustawiając kursor nad węzłem danych wyjściowych modułu.</span><span class="sxs-lookup"><span data-stu-id="84764-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="84764-169">Jest on wyświetlany wraz z nazwa węzła w etykietce narzędzia.</span><span class="sxs-lookup"><span data-stu-id="84764-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="84764-170">Niektóre moduły, takich jak [podziału] [ split] modułu danych wyjściowych do formatu o nazwie `Dataset`, który nie jest obsługiwany przez bibliotekę klienta języka Python.</span><span class="sxs-lookup"><span data-stu-id="84764-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![Format zestawu danych][dataset-format]

<span data-ttu-id="84764-172">Należy użyć modułu konwersji, takich jak [Konwertuj do formatu CSV][convert-to-csv], aby uzyskać dane wyjściowe do obsługiwanego formatu.</span><span class="sxs-lookup"><span data-stu-id="84764-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![GenericCSV Format][csv-format]

<span data-ttu-id="84764-174">W poniższej procedurze pokazano przykład, w którym tworzy eksperyment, uruchamia go i uzyskuje dostęp do pośredniego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="84764-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="84764-175">Tworzenie nowego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="84764-175">Create a new experiment.</span></span>
2. <span data-ttu-id="84764-176">Wstaw **zestawu danych dla dorosłych klasyfikacji binarnej dochodu spisu** modułu.</span><span class="sxs-lookup"><span data-stu-id="84764-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="84764-177">Wstaw [podziału] [ split] modułu i połączenia jej danych wejściowych z danymi wyjściowymi modułu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="84764-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="84764-178">Wstaw [Konwertuj do formatu CSV] [ convert-to-csv] modułu i połączenia jej danych wejściowych do jednego z [podziału] [ split] danych wyjściowych modułu.</span><span class="sxs-lookup"><span data-stu-id="84764-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="84764-179">Zapisz eksperyment, uruchom go i zaczekaj na zakończenie działania.</span><span class="sxs-lookup"><span data-stu-id="84764-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="84764-180">Kliknij węzeł danych wyjściowych na [Konwertuj do formatu CSV] [ convert-to-csv] modułu.</span><span class="sxs-lookup"><span data-stu-id="84764-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="84764-181">Po wyświetleniu menu kontekstowego wybierz **Generuj kod dostępu do danych**.</span><span class="sxs-lookup"><span data-stu-id="84764-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menu kontekstowe][experiment]
8. <span data-ttu-id="84764-183">Wybierz fragment kodu i skopiuj go do Schowka z wyświetlonym oknie.</span><span class="sxs-lookup"><span data-stu-id="84764-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![Kod dostępu][intermediate-dataset-access-code]
9. <span data-ttu-id="84764-185">Wklej kod w Notatniku.</span><span class="sxs-lookup"><span data-stu-id="84764-185">Paste the code in your notebook.</span></span>
   
    ![Notesu][ipython-intermediate-dataset]
10. <span data-ttu-id="84764-187">Możesz wizualizować dane przy użyciu matplotlib.</span><span class="sxs-lookup"><span data-stu-id="84764-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="84764-188">Spowoduje to wyświetlenie w histogram kolumny wieku:</span><span class="sxs-lookup"><span data-stu-id="84764-188">This displays in a histogram for the age column:</span></span>
    
    ![Histogram][ipython-histogram]

## <span data-ttu-id="84764-190"><a name="clientApis"></a>Użyj biblioteki klienckiej Machine Learning Python dostępu, odczytu, tworzenie i zarządzanie nimi zbiory danych</span><span class="sxs-lookup"><span data-stu-id="84764-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="84764-191">Obszar roboczy</span><span class="sxs-lookup"><span data-stu-id="84764-191">Workspace</span></span>
<span data-ttu-id="84764-192">Obszar roboczy jest punkt wejścia dla biblioteki klienta języka Python.</span><span class="sxs-lookup"><span data-stu-id="84764-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="84764-193">Podaj `Workspace` token klasy identyfikator obszaru roboczego i autoryzacji do utworzenia wystąpienia:</span><span class="sxs-lookup"><span data-stu-id="84764-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="84764-194">Wyliczanie obiektów DataSet</span><span class="sxs-lookup"><span data-stu-id="84764-194">Enumerate datasets</span></span>
<span data-ttu-id="84764-195">Aby wyliczyć wszystkie zestawy danych danego obszaru roboczego:</span><span class="sxs-lookup"><span data-stu-id="84764-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="84764-196">Aby wyliczyć właśnie utworzone przez użytkownika zestawy danych:</span><span class="sxs-lookup"><span data-stu-id="84764-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="84764-197">Aby wyliczyć tylko zestawy danych przykład:</span><span class="sxs-lookup"><span data-stu-id="84764-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="84764-198">Aby dostęp do zestawu danych, według nazwy (która jest uwzględniana wielkość liter):</span><span class="sxs-lookup"><span data-stu-id="84764-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="84764-199">Lub zostanie do niego dostęp przez indeks:</span><span class="sxs-lookup"><span data-stu-id="84764-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="84764-200">Metadane</span><span class="sxs-lookup"><span data-stu-id="84764-200">Metadata</span></span>
<span data-ttu-id="84764-201">Zestaw danych ma metadanych, oprócz zawartości.</span><span class="sxs-lookup"><span data-stu-id="84764-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="84764-202">(Pośredniego zestawów danych są wyjątkiem od tej zasady i nie ma żadnych metadanych).</span><span class="sxs-lookup"><span data-stu-id="84764-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="84764-203">Niektóre wartości metadanych są przypisane przez użytkownika w czasie tworzenia:</span><span class="sxs-lookup"><span data-stu-id="84764-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="84764-204">Inne są wartości przypisane przez uczenie Maszynowe Azure:</span><span class="sxs-lookup"><span data-stu-id="84764-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="84764-205">Zobacz `SourceDataset` klasy, aby uzyskać więcej informacji na temat dostępnych metadanych.</span><span class="sxs-lookup"><span data-stu-id="84764-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="84764-206">Odczytaj zawartość</span><span class="sxs-lookup"><span data-stu-id="84764-206">Read contents</span></span>
<span data-ttu-id="84764-207">Wstawki kodu udostępniane przez usługi Machine Learning Studio automatycznie Pobierz i deserializacji do obiektu Pandas DataFrame zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="84764-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="84764-208">Jest to zrobić za pomocą `to_dataframe` metody:</span><span class="sxs-lookup"><span data-stu-id="84764-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="84764-209">Jeśli wolisz pobierania danych pierwotnych i samodzielnie przeprowadzić deserializacji, który jest opcją.</span><span class="sxs-lookup"><span data-stu-id="84764-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="84764-210">W tej chwili jest jedyną opcją dla formatach, takich jak "ARFF", którego nie można deserializować biblioteki klienckiej Python.</span><span class="sxs-lookup"><span data-stu-id="84764-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="84764-211">Można odczytać zawartości jako tekst:</span><span class="sxs-lookup"><span data-stu-id="84764-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="84764-212">Można odczytać zawartości jako dane binarne:</span><span class="sxs-lookup"><span data-stu-id="84764-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="84764-213">Możesz także po prostu otworzyć strumienia zawartości:</span><span class="sxs-lookup"><span data-stu-id="84764-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="84764-214">Utwórz nowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="84764-214">Create a new dataset</span></span>
<span data-ttu-id="84764-215">Biblioteka klienta Python umożliwia przekazywanie zestawów danych z programu Python.</span><span class="sxs-lookup"><span data-stu-id="84764-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="84764-216">Te zestawy danych będą dostępne do użycia w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="84764-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="84764-217">Jeśli dane znajdują się w Pandas DataFrame, należy użyć poniższego kodu:</span><span class="sxs-lookup"><span data-stu-id="84764-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="84764-218">Jeśli dane są już serializowane, możesz użyć:</span><span class="sxs-lookup"><span data-stu-id="84764-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="84764-219">Może serializować DataFrame Pandas, do następujących formatów jest biblioteka klienta języka Python (stałe tych znajdują się w `azureml.DataTypeIds` klasy):</span><span class="sxs-lookup"><span data-stu-id="84764-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="84764-220">W postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="84764-220">PlainText</span></span>
* <span data-ttu-id="84764-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="84764-221">GenericCSV</span></span>
* <span data-ttu-id="84764-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="84764-222">GenericTSV</span></span>
* <span data-ttu-id="84764-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="84764-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="84764-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="84764-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="84764-225">Aktualizuj istniejący zestaw danych</span><span class="sxs-lookup"><span data-stu-id="84764-225">Update an existing dataset</span></span>
<span data-ttu-id="84764-226">Jeśli użytkownik spróbuje przekazać nowy zestaw danych o nazwie, która odpowiada istniejący zestaw danych, należy pobrać błąd konfliktu.</span><span class="sxs-lookup"><span data-stu-id="84764-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="84764-227">Aby zaktualizować istniejący zestaw danych, należy najpierw pobrać odwołanie do istniejącego zestawu danych:</span><span class="sxs-lookup"><span data-stu-id="84764-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="84764-228">Następnie użyj `update_from_dataframe` do serializacji i Zastąp zawartość zestawu danych na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="84764-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="84764-229">Jeśli chcesz uszeregować danych w innym formacie, określ wartość opcjonalna `data_type_id` parametru.</span><span class="sxs-lookup"><span data-stu-id="84764-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="84764-230">Opcjonalnie możesz ustawić nowy opis, określając wartość `description` parametru.</span><span class="sxs-lookup"><span data-stu-id="84764-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="84764-231">Opcjonalnie możesz ustawić nową nazwę, określając wartość `name` parametru.</span><span class="sxs-lookup"><span data-stu-id="84764-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="84764-232">Od teraz będziesz pobrać przy użyciu nowej nazwy zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="84764-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="84764-233">Poniższy kod aktualizuje danych, nazwę i opis.</span><span class="sxs-lookup"><span data-stu-id="84764-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="84764-234">`data_type_id`, `name` i `description` parametry są opcjonalne i domyślnie ich poprzedniej wartości.</span><span class="sxs-lookup"><span data-stu-id="84764-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="84764-235">`dataframe` Parametr jest zawsze wymagane.</span><span class="sxs-lookup"><span data-stu-id="84764-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="84764-236">Jeśli dane są już serializowane, użyj `update_from_raw_data` zamiast `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="84764-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="84764-237">Jeśli po prostu Przekaż w `raw_data` zamiast `dataframe`, działa w podobny sposób.</span><span class="sxs-lookup"><span data-stu-id="84764-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

