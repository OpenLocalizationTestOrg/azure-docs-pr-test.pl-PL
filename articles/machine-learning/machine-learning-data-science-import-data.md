---
title: "aaaImport danych do usługi Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Jak tooimport dane do usługi Azure Machine Learning Studio z różnych źródeł danych. Dowiedz się, jakie typy danych i formatów danych są obsługiwane."
keywords: "Importowanie danych, formatu danych, typy danych, źródła danych, dane szkoleniowe"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="8c796-105">Importowanie danych szkoleniowych do usługi Azure Machine Learning Studio z różnych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="8c796-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="8c796-106">toouse własnych danych w usłudze Machine Learning Studio toodevelop i train rozwiązania analizy predykcyjnej można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8c796-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="8c796-107">przekazywanie danych z **pliku lokalnego** wyprzedzenia czasu z toocreate Twojego dysku twardego modułu zestawu danych, w obszarze roboczym</span><span class="sxs-lookup"><span data-stu-id="8c796-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="8c796-108">dostęp do danych z jednego z kilku **źródeł danych w trybie online** eksperymentu jest uruchomiona przy użyciu hello [i zaimportuj dane] [ import-data] modułu</span><span class="sxs-lookup"><span data-stu-id="8c796-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="8c796-109">Użyj danych z innej usługi Azure Machine learning **eksperymentu** zapisane jako zestawu danych</span><span class="sxs-lookup"><span data-stu-id="8c796-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="8c796-110">Użyj danych z lokalnego **bazy danych programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="8c796-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="8c796-111">Każdą z tych opcji jest opisany w tematach hello menu hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="8c796-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="8c796-112">Tych tematach opisano, jak tooimport danych na podstawie tych danych różnych źródeł toouse w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8c796-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="8c796-113">Wiele przykładowych zestawów danych są dostępne w usłudze Machine Learning Studio używanej dla danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="8c796-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="8c796-114">Aby uzyskać informacje o tych, zobacz [Użyj hello przykładowych zestawów danych w usłudze Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="8c796-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="8c796-115">W tym temacie wprowadzające również omówiono sposób tooget danych gotowe do użycia w usłudze Machine Learning Studio oraz opis, które formaty danych i typy danych są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="8c796-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="8c796-116">Przygotowanie danych do użycia w usłudze Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8c796-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="8c796-117">Usługa Machine Learning Studio jest zaprojektowana toowork prostokątne lub tabelarycznym danych, takich jak dane tekstowe, rozdzielany lub strukturę danych z bazy danych, chociaż w niektórych sytuacjach może być używany nieregularnych danych.</span><span class="sxs-lookup"><span data-stu-id="8c796-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="8c796-118">Najlepiej danych jest stosunkowo czysty.</span><span class="sxs-lookup"><span data-stu-id="8c796-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="8c796-119">Oznacza to, że należy tootake nad problemy, takie jak parametry bez cudzysłowów przed przekazaniem hello dane do eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="8c796-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="8c796-120">Jednak Brak modułów dostępnych w usłudze Machine Learning Studio umożliwiające niektórych manipulacji danymi w ramach eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="8c796-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="8c796-121">W zależności od algorytmów uczenia maszynowego hello należy używać, może być konieczne toodecide jak będzie obsługiwać danych strukturalnych problemy, takie jak brak wartości i rozrzedzone danych, a moduły, które mogą pomóc, z których.</span><span class="sxs-lookup"><span data-stu-id="8c796-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="8c796-122">Szukaj w hello **transformacji danych** części palety modułów hello modułów, które wykonują te funkcje.</span><span class="sxs-lookup"><span data-stu-id="8c796-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="8c796-123">W dowolnym momencie w eksperymencie można wyświetlać lub pobrania danych hello jest generowany przez moduł, klikając hello port wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="8c796-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="8c796-124">W zależności od modułu hello mogą być pobierania różne opcje dostępne lub możliwe toovisualize hello danych może być przeglądarki sieci web w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8c796-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="8c796-125">Dane formaty i typy danych obsługiwane</span><span class="sxs-lookup"><span data-stu-id="8c796-125">Data formats and data types supported</span></span>
<span data-ttu-id="8c796-126">Można je zaimportować do eksperymentu wiele typów danych, w zależności od tego, jaki mechanizm można używać danych tooimport i której pochodzi od:</span><span class="sxs-lookup"><span data-stu-id="8c796-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="8c796-127">Zwykły tekst (txt)</span><span class="sxs-lookup"><span data-stu-id="8c796-127">Plain text (.txt)</span></span>
* <span data-ttu-id="8c796-128">Wartości rozdzielanych przecinkami (CSV) z nagłówkiem (.csv) lub bez (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="8c796-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="8c796-129">Tabulatorem tabulatorami (TSV z nagłówkiem (.tsv) lub bez) (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="8c796-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="8c796-130">Plik programu Excel</span><span class="sxs-lookup"><span data-stu-id="8c796-130">Excel file</span></span>
* <span data-ttu-id="8c796-131">Tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8c796-131">Azure table</span></span>
* <span data-ttu-id="8c796-132">Tabelę programu hive</span><span class="sxs-lookup"><span data-stu-id="8c796-132">Hive table</span></span>
* <span data-ttu-id="8c796-133">Tabela bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="8c796-133">SQL database table</span></span>
* <span data-ttu-id="8c796-134">Wartości OData</span><span class="sxs-lookup"><span data-stu-id="8c796-134">OData values</span></span>
* <span data-ttu-id="8c796-135">Dane SVMLight (.svmlight) (zobacz hello [definicji SVMLight](http://svmlight.joachims.org/) dla informacji o formacie)</span><span class="sxs-lookup"><span data-stu-id="8c796-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="8c796-136">Atrybut danych relacji File Format (ARFF) (.arff) (zobacz hello [definicji ARFF](http://weka.wikispaces.com/ARFF) dla informacji o formacie)</span><span class="sxs-lookup"><span data-stu-id="8c796-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="8c796-137">Plik zip (.zip)</span><span class="sxs-lookup"><span data-stu-id="8c796-137">Zip file (.zip)</span></span>
* <span data-ttu-id="8c796-138">Plik obiektu lub obszar roboczy R (. RData)</span><span class="sxs-lookup"><span data-stu-id="8c796-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="8c796-139">W przypadku importowania danych w formacie, takich jak ARFF zawierający metadane, Machine Learning Studio korzysta z tej pozycji hello toodefine metadanych i typu danych każdej kolumny.</span><span class="sxs-lookup"><span data-stu-id="8c796-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="8c796-140">Po zaimportowaniu danych, takich jak format TSV lub CSV, który nie zawiera metadanych usługi Machine Learning Studio wnioskuje hello typ danych dla każdej kolumny przez hello dane próbkowania.</span><span class="sxs-lookup"><span data-stu-id="8c796-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="8c796-141">Jeśli dane hello również nie ma nagłówki kolumn, Machine Learning Studio udostępnia domyślne nazwy.</span><span class="sxs-lookup"><span data-stu-id="8c796-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="8c796-142">Można jawnie określ lub zmień hello nagłówki i typy danych kolumn za pomocą hello [edytowanie metadanych][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="8c796-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="8c796-143">następujące Hello **typy danych** są rozpoznawane przez Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="8c796-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="8c796-144">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8c796-144">String</span></span>
* <span data-ttu-id="8c796-145">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="8c796-145">Integer</span></span>
* <span data-ttu-id="8c796-146">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="8c796-146">Double</span></span>
* <span data-ttu-id="8c796-147">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="8c796-147">Boolean</span></span>
* <span data-ttu-id="8c796-148">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8c796-148">DateTime</span></span>
* <span data-ttu-id="8c796-149">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="8c796-149">TimeSpan</span></span>

<span data-ttu-id="8c796-150">Usługa Machine Learning Studio używa typu danych wewnętrznych o nazwie ***tabeli danych*** toopass danych między modułami.</span><span class="sxs-lookup"><span data-stu-id="8c796-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="8c796-151">Można jawnie przekonwertować danych w formacie tabeli danych przy użyciu hello [przekonwertować tooDataset] [ convert-to-dataset] modułu.</span><span class="sxs-lookup"><span data-stu-id="8c796-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="8c796-152">Każdy moduł akceptującego formatów innych niż tabela danych przekonwertuje hello danych tooData tabeli dyskretnie przed przekazaniem go toohello następnego modułu.</span><span class="sxs-lookup"><span data-stu-id="8c796-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="8c796-153">Jeśli to konieczne, możesz przekonwertować format tabeli danych do woluminu CSV, TSV, ARFF lub format SVMLight przy użyciu innych modułów konwersji.</span><span class="sxs-lookup"><span data-stu-id="8c796-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="8c796-154">Szukaj w hello **konwersje Format danych** części palety modułów hello modułów, które wykonują te funkcje.</span><span class="sxs-lookup"><span data-stu-id="8c796-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
