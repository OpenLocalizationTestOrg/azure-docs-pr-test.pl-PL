---
title: "Określenie scenariuszy zaawansowana analityka dla usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Wybierz odpowiednie scenariusze robić, zaawansowane analizy predykcyjnej z procesem nauki danych Team."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="9d491-103">Scenariusze zaawansowanej analizy w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9d491-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="9d491-104">W tym artykule przedstawiono różne źródła danych przykładowych i scenariusze docelowe, które są obsługiwane przez [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d491-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="9d491-105">TDSP dostarcza systematyczne rozwiązanie dla zespołów współpracować nad tworzenia aplikacji inteligentnego.</span><span class="sxs-lookup"><span data-stu-id="9d491-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="9d491-106">Scenariusze przedstawionych w tym miejscu przedstawiono opcje dostępne w przepływie pracy przetwarzania danych, które są zależne od właściwości danych, lokalizacji źródłowej i repozytoriów docelowego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="9d491-107">**Drzewa decyzyjnego** dla wybranie przykładowe scenariusze, które jest odpowiednie dla danych i cel są prezentowane w ostatniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9d491-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="9d491-108">Każdy z poniższych sekcji przedstawia przykładowy scenariusz.</span><span class="sxs-lookup"><span data-stu-id="9d491-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="9d491-109">Dla każdego scenariusza nauki danych lub zaawansowana analityka przepływu i obsługi zasobów platformy Azure są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="9d491-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="9d491-110">**Wszystkie z poniższych scenariuszy musisz:**
> </span><span class="sxs-lookup"><span data-stu-id="9d491-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="9d491-111">[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="9d491-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="9d491-112">Utwórz obszar roboczy usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9d491-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="9d491-113"><a name="smalllocal"></a>Scenariusz \#1: mały, aby średnia tabelarycznym zestawu danych w lokalnych plikach</span><span class="sxs-lookup"><span data-stu-id="9d491-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Małych i średnich plików lokalnych][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="9d491-115">Dodatkowe zasoby platformy Azure: Brak</span><span class="sxs-lookup"><span data-stu-id="9d491-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="9d491-116">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d491-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="9d491-117">Przekaż zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-117">Upload a dataset.</span></span>
3. <span data-ttu-id="9d491-118">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy przekazane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="9d491-119"><a name="smalllocalprocess"></a>Scenariusz \#2: małe średnia DataSet lokalnych plików, które wymagają przetworzenia</span><span class="sxs-lookup"><span data-stu-id="9d491-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Małych i średnich lokalnych plików z przetwarzaniem][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9d491-121">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (notesu IPython server)</span><span class="sxs-lookup"><span data-stu-id="9d491-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9d491-122">Utwórz maszynę wirtualną platformy Azure, systemem IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9d491-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="9d491-123">Przekazywanie danych do kontenera magazynu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9d491-124">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z kontenera magazynu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="9d491-125">Przekształć dane czyszczenia tabelarycznej.</span><span class="sxs-lookup"><span data-stu-id="9d491-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="9d491-126">Zapisz przekształcone dane w obiektach blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="9d491-127">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d491-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="9d491-128">Odczytywanie danych z obiekty BLOB platformy Azure przy użyciu [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="9d491-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="9d491-129">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9d491-130"><a name="largelocal"></a>Scenariusz \#3: dużego zestawu danych lokalnych plików przeznaczonych dla obiektów blob Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Dużych plików lokalnych][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9d491-132">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (notesu IPython server)</span><span class="sxs-lookup"><span data-stu-id="9d491-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9d491-133">Utwórz maszynę wirtualną platformy Azure, systemem IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9d491-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="9d491-134">Przekazywanie danych do kontenera magazynu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9d491-135">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, dostęp do danych z obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="9d491-136">Przekształcanie danych czyszczenia tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9d491-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="9d491-137">Eksplorowanie danych i tworzenie funkcji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9d491-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="9d491-138">Wyodrębnij przykładowych danych w małych i średnich.</span><span class="sxs-lookup"><span data-stu-id="9d491-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="9d491-139">Zapisz próbki danych w obiektach blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="9d491-140">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d491-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="9d491-141">Odczytywanie danych z obiekty BLOB platformy Azure przy użyciu [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="9d491-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="9d491-142">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9d491-143"><a name="smalllocaltodb"></a>Scenariusz \#4: mały, aby średnia zestawu danych lokalnych plików przeznaczonych dla programu SQL Server w maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Mały, aby średnia lokalnych plików do bazy danych SQL na platformie Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9d491-145">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="9d491-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9d491-146">Utwórz maszynę wirtualną platformy Azure z programu SQL Server + IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9d491-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="9d491-147">Przekazywanie danych do kontenera magazynu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9d491-148">Wstępnie przetworzyć i czyszczenia danych w kontenerze magazynu platformy Azure przy użyciu IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9d491-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="9d491-149">Przekształcanie danych czyszczenia tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9d491-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="9d491-150">Zapisywanie danych w plikach lokalnej maszyny Wirtualnej (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="9d491-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="9d491-151">Ładowanie danych do bazy danych programu SQL Server uruchomiony na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="9d491-152">Opcja \#1: użycie programu SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9d491-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="9d491-153">Logowanie do programu SQL Server maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9d491-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="9d491-154">Uruchom program SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9d491-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="9d491-155">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="9d491-155">Create database and target tables.</span></span>
   * <span data-ttu-id="9d491-156">Użyj jednej z zbiorczego zaimportować metod do ładowania danych z plików lokalnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d491-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="9d491-157">Opcja \#2: przy użyciu IPython notesu — nie zaleca się dla średnich i większych zestawów danych</span><span class="sxs-lookup"><span data-stu-id="9d491-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="9d491-158">Dostęp do serwera SQL na maszynie Wirtualnej, należy użyć ciągu połączenia ODBC.</span><span class="sxs-lookup"><span data-stu-id="9d491-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="9d491-159">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="9d491-159">Create database and target tables.</span></span>
   * <span data-ttu-id="9d491-160">Użyj jednej z zbiorczego zaimportować metod do ładowania danych z plików lokalnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d491-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="9d491-161">Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9d491-161">Explore data, create features as needed.</span></span> <span data-ttu-id="9d491-162">Należy pamiętać, że funkcje nie muszą być zmaterializowany w tabelach bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9d491-163">Pamiętaj, tylko niezbędne zapytanie, aby je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="9d491-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="9d491-164">Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.</span><span class="sxs-lookup"><span data-stu-id="9d491-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="9d491-165">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d491-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="9d491-166">Odczytywanie danych z bezpośrednio za pomocą programu SQL Server [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="9d491-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9d491-167">Wklej zapytanie niezbędne, który wyodrębnia pól i tworzy funkcje oraz przykłady danych, w razie potrzeby bezpośrednio w [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="9d491-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="9d491-168">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="9d491-169"><a name="largelocaltodb"></a>Scenariusz \#5: dużego zestawu danych w lokalnych plikach, docelowa programu SQL Server w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Dużych plików lokalnych do bazy danych SQL na platformie Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9d491-171">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="9d491-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9d491-172">Utwórz maszynę wirtualną platformy Azure z programu SQL Server oraz serwer IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9d491-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="9d491-173">Przekazywanie danych do kontenera magazynu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="9d491-174">(Opcjonalnie) Wstępnie przetworzyć i czyszczenia danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="9d491-175">a.</span><span class="sxs-lookup"><span data-stu-id="9d491-175">a.</span></span>  <span data-ttu-id="9d491-176">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="9d491-177">b.</span><span class="sxs-lookup"><span data-stu-id="9d491-177">b.</span></span>  <span data-ttu-id="9d491-178">Przekształcanie danych czyszczenia tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9d491-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="9d491-179">c.</span><span class="sxs-lookup"><span data-stu-id="9d491-179">c.</span></span>  <span data-ttu-id="9d491-180">Zapisywanie danych w plikach lokalnej maszyny Wirtualnej (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="9d491-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="9d491-181">Ładowanie danych do bazy danych programu SQL Server uruchomiony na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="9d491-182">a.</span><span class="sxs-lookup"><span data-stu-id="9d491-182">a.</span></span>  <span data-ttu-id="9d491-183">Zaloguj się do programu SQL Server maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d491-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="9d491-184">b.</span><span class="sxs-lookup"><span data-stu-id="9d491-184">b.</span></span>  <span data-ttu-id="9d491-185">Jeśli nie już zapisany na danych, pobieranie plików danych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="9d491-186">c.</span><span class="sxs-lookup"><span data-stu-id="9d491-186">c.</span></span>  <span data-ttu-id="9d491-187">Uruchom program SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9d491-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="9d491-188">d.</span><span class="sxs-lookup"><span data-stu-id="9d491-188">d.</span></span>  <span data-ttu-id="9d491-189">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="9d491-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="9d491-190">e.</span><span class="sxs-lookup"><span data-stu-id="9d491-190">e.</span></span>  <span data-ttu-id="9d491-191">Użyj jednej z zbiorczego zaimportować metod do ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="9d491-192">f.</span><span class="sxs-lookup"><span data-stu-id="9d491-192">f.</span></span>  <span data-ttu-id="9d491-193">Jeśli sprzężeń tabel są wymagane, należy utworzyć indeksy w celu przyspieszenia sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="9d491-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d491-194">Szybkość wczytywania rozmiary dużej ilości danych, zalecane jest tworzenie partycjonowane tabele i zbiorczego importowania danych równolegle.</span><span class="sxs-lookup"><span data-stu-id="9d491-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="9d491-195">Aby uzyskać więcej informacji, zobacz [równoległych importowanie danych do tabel na partycje SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9d491-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9d491-196">Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9d491-196">Explore data, create features as needed.</span></span> <span data-ttu-id="9d491-197">Należy pamiętać, że funkcje nie muszą być zmaterializowany w tabelach bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9d491-198">Pamiętaj, tylko niezbędne zapytanie, aby je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="9d491-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="9d491-199">Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.</span><span class="sxs-lookup"><span data-stu-id="9d491-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="9d491-200">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d491-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="9d491-201">Odczytywanie danych z bezpośrednio za pomocą programu SQL Server [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="9d491-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9d491-202">Wklej zapytanie niezbędne, który wyodrębnia pól i tworzy funkcje oraz przykłady danych, w razie potrzeby bezpośrednio w [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="9d491-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="9d491-203">Proste przepływu eksperymentu uczenia maszynowego Azure, począwszy od dataset przekazany</span><span class="sxs-lookup"><span data-stu-id="9d491-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="9d491-204"><a name="largedbtodb"></a>Scenariusz \#6: dużego zestawu danych w programie SQL Server bazy danych lokalnych, przeznaczonych dla programu SQL Server w maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Duże SQL bazy danych lokalnych do bazy danych SQL na platformie Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9d491-206">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="9d491-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="9d491-207">Utwórz maszynę wirtualną platformy Azure z programu SQL Server oraz serwer IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9d491-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="9d491-208">Użyj jednej z danych wyeksportować metod, aby wyeksportować dane z programu SQL Server do plików zrzutu.</span><span class="sxs-lookup"><span data-stu-id="9d491-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d491-209">Jeśli zdecydujesz się przeniesienie wszystkich danych z bazy danych lokalnych, to alternatywna metoda (szybsze), aby przenieść pełnej bazy danych do wystąpienia programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="9d491-210">Pomiń kroki, aby wyeksportować dane, Utwórz bazę danych i obciążenia/importowanie danych do docelowej bazy danych i wykonaj alternatywna metoda.</span><span class="sxs-lookup"><span data-stu-id="9d491-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="9d491-211">Przekazywanie plików zrzutu do kontenera magazynu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="9d491-212">Ładowanie danych do bazy danych programu SQL Server uruchomiony na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="9d491-213">a.</span><span class="sxs-lookup"><span data-stu-id="9d491-213">a.</span></span>  <span data-ttu-id="9d491-214">Zaloguj się do programu SQL Server maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d491-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="9d491-215">b.</span><span class="sxs-lookup"><span data-stu-id="9d491-215">b.</span></span>  <span data-ttu-id="9d491-216">Pobieranie plików danych z kontenera magazynu Azure do folderu lokalnego wirtualna.</span><span class="sxs-lookup"><span data-stu-id="9d491-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="9d491-217">c.</span><span class="sxs-lookup"><span data-stu-id="9d491-217">c.</span></span>  <span data-ttu-id="9d491-218">Uruchom program SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9d491-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="9d491-219">d.</span><span class="sxs-lookup"><span data-stu-id="9d491-219">d.</span></span>  <span data-ttu-id="9d491-220">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="9d491-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="9d491-221">e.</span><span class="sxs-lookup"><span data-stu-id="9d491-221">e.</span></span>  <span data-ttu-id="9d491-222">Użyj jednej z zbiorczego zaimportować metod do ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="9d491-223">f.</span><span class="sxs-lookup"><span data-stu-id="9d491-223">f.</span></span>  <span data-ttu-id="9d491-224">Jeśli sprzężeń tabel są wymagane, należy utworzyć indeksy w celu przyspieszenia sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="9d491-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d491-225">Szybsze ładowanie rozmiary dużej ilości danych, Utwórz partycjonowane tabele i do zbiorczego importowania danych równolegle.</span><span class="sxs-lookup"><span data-stu-id="9d491-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="9d491-226">Aby uzyskać więcej informacji, zobacz [równoległych importowanie danych do tabel na partycje SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9d491-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9d491-227">Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9d491-227">Explore data, create features as needed.</span></span> <span data-ttu-id="9d491-228">Należy pamiętać, że funkcje nie muszą być zmaterializowany w tabelach bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9d491-229">Pamiętaj, tylko niezbędne zapytanie, aby je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="9d491-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="9d491-230">Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.</span><span class="sxs-lookup"><span data-stu-id="9d491-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="9d491-231">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d491-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="9d491-232">Odczytywanie danych z bezpośrednio za pomocą programu SQL Server [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="9d491-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9d491-233">Wklej zapytanie niezbędne, który wyodrębnia pól i tworzy funkcje oraz przykłady danych, w razie potrzeby bezpośrednio w [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="9d491-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="9d491-234">Począwszy od dataset przekazany prosty przepływ eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="9d491-235">Alternatywna metoda kopiowania pełnej bazy danych z lokalnego serwera SQL do bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Odłączanie lokalnej bazy danych i Dołącz do bazy danych SQL na platformie Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="9d491-237">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="9d491-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="9d491-238">Aby replikować całą bazę danych programu SQL Server w maszyną Wirtualną programu SQL Server, należy skopiować bazę danych z jednej lokalizacji/serwera na inny, przy założeniu, że bazy danych może być podjęta tymczasowo w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="9d491-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="9d491-239">Możesz to zrobić w Eksploratorze obiektów SQL Server Management Studio lub za pomocą równoważnych poleceń języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="9d491-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="9d491-240">Odłącz bazę danych w lokalizacji źródłowej.</span><span class="sxs-lookup"><span data-stu-id="9d491-240">Detach the database at the source location.</span></span> <span data-ttu-id="9d491-241">Aby uzyskać więcej informacji, zobacz [odłączyć bazy danych](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="9d491-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="9d491-242">W oknie Eksploratora Windows lub wiersza polecenia systemu Windows skopiuj plik odłączono bazę danych lub pliki i pliku dziennika lub pliki do lokalizacji docelowej na maszynie Wirtualnej serwera SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="9d491-243">Dołącz skopiowanych plików w wystąpieniu programu SQL Server docelowym.</span><span class="sxs-lookup"><span data-stu-id="9d491-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="9d491-244">Aby uzyskać więcej informacji, zobacz [dołączyć bazę danych](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="9d491-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="9d491-245">[Przenoszenie bazy danych przy użyciu odłączyć i dołączyć (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="9d491-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="9d491-246"><a name="largedbtohive"></a>Scenariusz \#7: danych Big data w lokalnych plikach docelowa baza danych gałęzi w klastrach usługi Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="9d491-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Dane big data w celu lokalnego gałęzi][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="9d491-248">Dodatkowe zasoby platformy Azure: klastra usługi Hadoop w usłudze Azure HDInsight i maszyny wirtualnej platformy Azure (notesu IPython server)</span><span class="sxs-lookup"><span data-stu-id="9d491-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="9d491-249">Utwórz maszynę wirtualną platformy Azure, usługami IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9d491-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="9d491-250">Tworzenie klastra usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9d491-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="9d491-251">(Opcjonalnie) Wstępnie przetworzyć i czyszczenia danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="9d491-252">a.</span><span class="sxs-lookup"><span data-stu-id="9d491-252">a.</span></span>  <span data-ttu-id="9d491-253">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9d491-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="9d491-254">b.</span><span class="sxs-lookup"><span data-stu-id="9d491-254">b.</span></span>  <span data-ttu-id="9d491-255">Przekształcanie danych czyszczenia tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9d491-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="9d491-256">c.</span><span class="sxs-lookup"><span data-stu-id="9d491-256">c.</span></span>  <span data-ttu-id="9d491-257">Zapisywanie danych w plikach lokalnej maszyny Wirtualnej (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="9d491-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="9d491-258">Przekazywanie danych do domyślnego kontenera klastra usługi Hadoop wybranej w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="9d491-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="9d491-259">Ładowanie danych do bazy danych klastra usługi Azure HDInsight Hadoop Hive.</span><span class="sxs-lookup"><span data-stu-id="9d491-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="9d491-260">a.</span><span class="sxs-lookup"><span data-stu-id="9d491-260">a.</span></span>  <span data-ttu-id="9d491-261">Zaloguj się do węzła głównego klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="9d491-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="9d491-262">b.</span><span class="sxs-lookup"><span data-stu-id="9d491-262">b.</span></span>  <span data-ttu-id="9d491-263">Otwórz okno wiersza polecenia usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9d491-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9d491-264">c.</span><span class="sxs-lookup"><span data-stu-id="9d491-264">c.</span></span>  <span data-ttu-id="9d491-265">Wprowadź katalog główny Hive za pomocą polecenia `cd %hive_home%\bin` w wierszu polecenia Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9d491-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9d491-266">d.</span><span class="sxs-lookup"><span data-stu-id="9d491-266">d.</span></span>  <span data-ttu-id="9d491-267">Uruchamianie zapytań Hive, można utworzyć bazy danych i tabele i ładowanie danych z magazynu obiektów blob, tabel, w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="9d491-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d491-268">W przypadku dużych danych, użytkownicy mogą tworzyć tabeli Hive z partycjami.</span><span class="sxs-lookup"><span data-stu-id="9d491-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="9d491-269">Następnie użytkownicy mogą używać `for` pętli w Hadoop wiersza polecenia w węźle głównym ładowanie danych do tabeli Hive partycjonowanego partycji.</span><span class="sxs-lookup"><span data-stu-id="9d491-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="9d491-270">Eksplorowanie danych i tworzenie funkcji zgodnie z potrzebami w wierszu polecenia Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9d491-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="9d491-271">Należy pamiętać, że funkcje nie muszą być zmaterializowany w tabelach bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d491-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="9d491-272">Pamiętaj, tylko niezbędne zapytanie, aby je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="9d491-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="9d491-273">a.</span><span class="sxs-lookup"><span data-stu-id="9d491-273">a.</span></span>  <span data-ttu-id="9d491-274">Zaloguj się do węzła głównego klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="9d491-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="9d491-275">b.</span><span class="sxs-lookup"><span data-stu-id="9d491-275">b.</span></span>  <span data-ttu-id="9d491-276">Otwórz okno wiersza polecenia usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9d491-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9d491-277">c.</span><span class="sxs-lookup"><span data-stu-id="9d491-277">c.</span></span>  <span data-ttu-id="9d491-278">Wprowadź katalog główny Hive za pomocą polecenia `cd %hive_home%\bin` w wierszu polecenia Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9d491-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="9d491-279">d.</span><span class="sxs-lookup"><span data-stu-id="9d491-279">d.</span></span>  <span data-ttu-id="9d491-280">Uruchamianie zapytań Hive w wierszu polecenia Hadoop na węzła głównego klastra usługi Hadoop do danych i tworzenie funkcji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9d491-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="9d491-281">Jeśli wymagane lub pożądane, przykładowe dane, aby zmieścić ją w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="9d491-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="9d491-282">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9d491-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="9d491-283">Odczytywanie danych bezpośrednio z `Hive Queries` przy użyciu [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="9d491-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="9d491-284">Wklej zapytanie niezbędne, który wyodrębnia pól i tworzy funkcje oraz przykłady danych, w razie potrzeby bezpośrednio w [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="9d491-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="9d491-285">Począwszy od dataset przekazany prosty przepływ eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="9d491-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="9d491-286"><a name="decisiontree"></a>Drzewo decyzyjne dotyczące wyboru scenariusza</span><span class="sxs-lookup"><span data-stu-id="9d491-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="9d491-287">Poniższy diagram przedstawia opisanych powyżej scenariuszy i zaawansowane procesu analizy i technologii dokonanej prowadzące do każdego z wyszczególnione scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="9d491-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="9d491-288">Uwaga: przetwarzanie danych, eksploracji engineering funkcji i próbkowanie może być umieścić w metody na środowiskową — w źródle, pośrednie, lub środowiska docelowego — i można kontynuować wielokrotnie powtarzane, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9d491-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="9d491-289">Diagram tylko służy jako ilustrację niektóre możliwe przepływów i nie zapewnia kompleksowe wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="9d491-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Przykładowe DS procesu wskazówki scenariusze][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="9d491-291">Zaawansowane analizy w akcji przykłady</span><span class="sxs-lookup"><span data-stu-id="9d491-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="9d491-292">Przegląd usługi Azure Machine Learning end-to-end procesu zaawansowane analizy i technologii przy użyciu publicznego zestawów danych zobacz:</span><span class="sxs-lookup"><span data-stu-id="9d491-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="9d491-293">[Zespół proces analizy danych w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9d491-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="9d491-294">[Zespół proces analizy danych w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="9d491-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
