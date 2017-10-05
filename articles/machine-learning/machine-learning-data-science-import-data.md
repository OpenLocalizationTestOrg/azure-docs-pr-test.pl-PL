---
title: "Importowanie danych do usługi Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Jak zaimportować dane do usługi Azure Machine Learning Studio z różnych źródeł danych. Dowiedz się, jakie typy danych i formatów danych są obsługiwane."
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
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="d1c4c-105">Importowanie danych szkoleniowych do usługi Azure Machine Learning Studio z różnych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="d1c4c-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="d1c4c-106">Aby użyć własnych danych w usłudze Machine Learning Studio do opracowywania i uczenia rozwiązania analizy predykcyjnej, można:</span><span class="sxs-lookup"><span data-stu-id="d1c4c-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="d1c4c-107">przekazywanie danych z **pliku lokalnego** wcześniejsze z dysku twardego do utworzenia modułu zestawu danych w obszarze roboczym</span><span class="sxs-lookup"><span data-stu-id="d1c4c-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="d1c4c-108">dostęp do danych z jednego z kilku **źródeł danych w trybie online** eksperymentu jest uruchomiona za pomocą [i zaimportuj dane] [ import-data] modułu</span><span class="sxs-lookup"><span data-stu-id="d1c4c-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="d1c4c-109">Użyj danych z innej usługi Azure Machine learning **eksperymentu** zapisane jako zestawu danych</span><span class="sxs-lookup"><span data-stu-id="d1c4c-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="d1c4c-110">Użyj danych z lokalnego **bazy danych programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="d1c4c-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="d1c4c-111">Każdej z tych opcji jest opisany w tematach menu poniżej.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="d1c4c-112">W tych tematach opisano, jak zaimportować dane z tych różnych źródeł danych do użycia w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="d1c4c-113">Wiele przykładowych zestawów danych są dostępne w usłudze Machine Learning Studio używanej dla danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="d1c4c-114">Aby uzyskać informacje o tych, zobacz [użyj przykładowych zestawów danych w usłudze Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="d1c4c-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="d1c4c-115">W tym temacie wprowadzające również omówiono sposób przygotowania danych do użycia w usłudze Machine Learning Studio oraz opis, które formaty danych i typy danych są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="d1c4c-116">Przygotowanie danych do użycia w usłudze Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="d1c4c-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="d1c4c-117">Usługa Machine Learning Studio jest przeznaczona do pracy z danymi prostokątne lub tabelarycznych, takich jak dane tekstowe, rozdzielany lub strukturę danych z bazy danych, chociaż w niektórych sytuacjach może być używany nieregularnych danych.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="d1c4c-118">Najlepiej danych jest stosunkowo czysty.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="d1c4c-119">Oznacza to, że należy zajmie się problemy, takie jak parametry bez cudzysłowów przed przekazać dane do eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="d1c4c-120">Jednak Brak modułów dostępnych w usłudze Machine Learning Studio umożliwiające niektórych manipulacji danymi w ramach eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="d1c4c-121">W zależności od algorytmów, którego będziesz używać uczenia maszynowego, konieczne może być zdecydować, w jaki sposób będzie obsługiwać danych strukturalnych problemy, takie jak brak wartości i rozrzedzone danych, a istnieją modułów, które mogą pomóc, z których.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="d1c4c-122">Szukaj w **transformacji danych** części palety modułów dla modułów, które wykonywanie tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="d1c4c-123">W dowolnym momencie w eksperymencie można wyświetlić lub pobrać dane, które jest generowany przez moduł, klikając port wyjściowy.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="d1c4c-124">W zależności od modułu mogą być pobierania różne opcje dostępne lub może być niemożliwe do wizualizacji danych w przeglądarce sieci web w usłudze Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="d1c4c-125">Dane formaty i typy danych obsługiwane</span><span class="sxs-lookup"><span data-stu-id="d1c4c-125">Data formats and data types supported</span></span>
<span data-ttu-id="d1c4c-126">Można je zaimportować do eksperymentu wiele typów danych, w zależności od tego, jaki mechanizm służy do importowania danych i której pochodzi od:</span><span class="sxs-lookup"><span data-stu-id="d1c4c-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="d1c4c-127">Zwykły tekst (txt)</span><span class="sxs-lookup"><span data-stu-id="d1c4c-127">Plain text (.txt)</span></span>
* <span data-ttu-id="d1c4c-128">Wartości rozdzielanych przecinkami (CSV) z nagłówkiem (.csv) lub bez (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="d1c4c-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="d1c4c-129">Tabulatorem tabulatorami (TSV z nagłówkiem (.tsv) lub bez) (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="d1c4c-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="d1c4c-130">Plik programu Excel</span><span class="sxs-lookup"><span data-stu-id="d1c4c-130">Excel file</span></span>
* <span data-ttu-id="d1c4c-131">Tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d1c4c-131">Azure table</span></span>
* <span data-ttu-id="d1c4c-132">Tabelę programu hive</span><span class="sxs-lookup"><span data-stu-id="d1c4c-132">Hive table</span></span>
* <span data-ttu-id="d1c4c-133">Tabela bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="d1c4c-133">SQL database table</span></span>
* <span data-ttu-id="d1c4c-134">Wartości OData</span><span class="sxs-lookup"><span data-stu-id="d1c4c-134">OData values</span></span>
* <span data-ttu-id="d1c4c-135">Dane SVMLight (.svmlight) (zobacz [definicji SVMLight](http://svmlight.joachims.org/) dla informacji o formacie)</span><span class="sxs-lookup"><span data-stu-id="d1c4c-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="d1c4c-136">Atrybut danych relacji File Format (ARFF) (.arff) (zobacz [definicji ARFF](http://weka.wikispaces.com/ARFF) dla informacji o formacie)</span><span class="sxs-lookup"><span data-stu-id="d1c4c-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="d1c4c-137">Plik zip (.zip)</span><span class="sxs-lookup"><span data-stu-id="d1c4c-137">Zip file (.zip)</span></span>
* <span data-ttu-id="d1c4c-138">Plik obiektu lub obszar roboczy R (. RData)</span><span class="sxs-lookup"><span data-stu-id="d1c4c-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="d1c4c-139">W przypadku importowania danych w formacie, takich jak ARFF zawierający metadane, Machine Learning Studio wykorzystuje te metadane do definiowania nagłówek i typ danych każdej kolumny.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="d1c4c-140">Po zaimportowaniu danych, takich jak format TSV lub CSV, który nie zawiera metadanych usługi Machine Learning Studio wnioskuje typ danych dla każdej kolumny poprzez próbkowanie danych.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="d1c4c-141">Jeśli dane również nie ma nagłówki kolumn, Machine Learning Studio udostępnia domyślne nazwy.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="d1c4c-142">Można jawnie określ lub zmień nagłówki i typy danych kolumn za pomocą [edytowanie metadanych][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="d1c4c-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="d1c4c-143">Następujące **typy danych** są rozpoznawane przez Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="d1c4c-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="d1c4c-144">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d1c4c-144">String</span></span>
* <span data-ttu-id="d1c4c-145">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="d1c4c-145">Integer</span></span>
* <span data-ttu-id="d1c4c-146">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="d1c4c-146">Double</span></span>
* <span data-ttu-id="d1c4c-147">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="d1c4c-147">Boolean</span></span>
* <span data-ttu-id="d1c4c-148">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="d1c4c-148">DateTime</span></span>
* <span data-ttu-id="d1c4c-149">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d1c4c-149">TimeSpan</span></span>

<span data-ttu-id="d1c4c-150">Usługa Machine Learning Studio używa typu danych wewnętrznych o nazwie ***tabeli danych*** do przekazywania danych między modułami.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="d1c4c-151">Dane można jawnie przekonwertować na format tabeli danych za pomocą [przekonwertować zestawu danych] [ convert-to-dataset] modułu.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="d1c4c-152">Każdy moduł akceptującego formatów innych niż tabela danych przekonwertuje dane do tabeli danych dyskretnie przed przekazaniem go do następnego modułu.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="d1c4c-153">Jeśli to konieczne, możesz przekonwertować format tabeli danych do woluminu CSV, TSV, ARFF lub format SVMLight przy użyciu innych modułów konwersji.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="d1c4c-154">Szukaj w **konwersje Format danych** części palety modułów dla modułów, które wykonywanie tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="d1c4c-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
