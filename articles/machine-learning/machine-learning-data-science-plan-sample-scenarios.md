---
title: "aaaIdentify zaawansowanych scenariuszy analizy dla usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Wybierz odpowiednie scenariusze hello robić, zaawansowane analizy predykcyjnej z hello proces nauki danych Team."
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
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="339cd-103">Scenariusze zaawansowanej analizy w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="339cd-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="339cd-104">W tym artykule omówiono hello różnych źródeł danych przykładowych i scenariusze docelowe, które są obsługiwane przez hello [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="339cd-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="339cd-105">Witaj TDSP zapewnia systematyczne podejście toocollaborate zespołów na tworzeniu aplikacji inteligentnego.</span><span class="sxs-lookup"><span data-stu-id="339cd-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="339cd-106">scenariusze Hello przedstawionych w tym miejscu przedstawiono opcje dostępne w hello przetwarzania danych w przepływie pracy, które są zależne od właściwości danych hello, lokalizacje źródłowe i repozytoriów docelowego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="339cd-107">Witaj **drzewa decyzyjnego** dla wybranie hello przykładowe scenariusze, które jest odpowiednie dla danych i cel są prezentowane w ostatniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="339cd-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="339cd-108">Przedstawia informacje o poszczególnych hello następujące sekcje przykładowy scenariusz.</span><span class="sxs-lookup"><span data-stu-id="339cd-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="339cd-109">Dla każdego scenariusza nauki danych lub zaawansowana analityka przepływu i obsługi zasobów platformy Azure są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="339cd-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="339cd-110">**Wszystkie następujące scenariusze hello musisz:**
> </span><span class="sxs-lookup"><span data-stu-id="339cd-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="339cd-111">[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="339cd-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="339cd-112">Utwórz obszar roboczy usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="339cd-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="339cd-113"><a name="smalllocal"></a>Scenariusz \#1: mały toomedium tabelarycznym zestawu danych w lokalnych plikach</span><span class="sxs-lookup"><span data-stu-id="339cd-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![Toomedium małych plików lokalnych][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="339cd-115">Dodatkowe zasoby platformy Azure: Brak</span><span class="sxs-lookup"><span data-stu-id="339cd-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="339cd-116">Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="339cd-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="339cd-117">Przekaż zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-117">Upload a dataset.</span></span>
3. <span data-ttu-id="339cd-118">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy przekazane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="339cd-119"><a name="smalllocalprocess"></a>Scenariusz \#2: małe toomedium zestawu danych lokalnych plików, które wymagają przetworzenia</span><span class="sxs-lookup"><span data-stu-id="339cd-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![Mała toomedium lokalnych plików z przetwarzaniem][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="339cd-121">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (notesu IPython server)</span><span class="sxs-lookup"><span data-stu-id="339cd-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="339cd-122">Utwórz maszynę wirtualną platformy Azure, systemem IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="339cd-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="339cd-123">Przekaż kontenera magazynu Azure tooan danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="339cd-124">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z kontenera magazynu systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="339cd-125">Przekształcanie danych, toocleaned w formie tabelarycznej.</span><span class="sxs-lookup"><span data-stu-id="339cd-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="339cd-126">Zapisz przekształcone dane w obiektach blob Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="339cd-127">Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="339cd-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="339cd-128">Odczytywanie danych hello z obiekty BLOB platformy Azure przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="339cd-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="339cd-129">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="339cd-130"><a name="largelocal"></a>Scenariusz \#3: dużego zestawu danych lokalnych plików przeznaczonych dla obiektów blob Azure</span><span class="sxs-lookup"><span data-stu-id="339cd-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Dużych plików lokalnych][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="339cd-132">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (notesu IPython server)</span><span class="sxs-lookup"><span data-stu-id="339cd-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="339cd-133">Utwórz maszynę wirtualną platformy Azure, systemem IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="339cd-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="339cd-134">Przekaż kontenera magazynu Azure tooan danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="339cd-135">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, dostęp do danych z obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="339cd-136">Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="339cd-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="339cd-137">Eksplorowanie danych i tworzenie funkcji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="339cd-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="339cd-138">Wyodrębnij przykładowych danych w małych i średnich.</span><span class="sxs-lookup"><span data-stu-id="339cd-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="339cd-139">Zapisz hello próbce danych w obiektach blob Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="339cd-140">Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="339cd-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="339cd-141">Odczytywanie danych hello z obiekty BLOB platformy Azure przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="339cd-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="339cd-142">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="339cd-143"><a name="smalllocaltodb"></a>Scenariusz \#4: mały toomedium zestawu danych lokalnych plików przeznaczonych dla programu SQL Server w maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="339cd-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Mała toomedium tooSQL lokalne pliki bazy danych na platformie Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="339cd-145">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="339cd-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="339cd-146">Utwórz maszynę wirtualną platformy Azure z programu SQL Server + IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="339cd-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="339cd-147">Przekaż kontenera magazynu Azure tooan danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="339cd-148">Wstępnie przetworzyć i czyszczenia danych w kontenerze magazynu platformy Azure przy użyciu IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="339cd-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="339cd-149">Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="339cd-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="339cd-150">Zapisywanie plików danych lokalnych tooVM (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków tooVM).</span><span class="sxs-lookup"><span data-stu-id="339cd-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="339cd-151">Dane tooSQL serwera bazy danych obciążenia uruchomione na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="339cd-152">Opcja \#1: użycie programu SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="339cd-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="339cd-153">TooSQL logowania maszyny Wirtualnej serwera</span><span class="sxs-lookup"><span data-stu-id="339cd-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="339cd-154">Uruchom program SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="339cd-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="339cd-155">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="339cd-155">Create database and target tables.</span></span>
   * <span data-ttu-id="339cd-156">Użyj jednej z zbiorczego hello importowanie metody tooload hello danych z plików lokalnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="339cd-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="339cd-157">Opcja \#2: przy użyciu IPython notesu — nie zaleca się dla średnich i większych zestawów danych</span><span class="sxs-lookup"><span data-stu-id="339cd-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="339cd-158">Używanie tooaccess ciąg połączenia ODBC programu SQL Server na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="339cd-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="339cd-159">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="339cd-159">Create database and target tables.</span></span>
   * <span data-ttu-id="339cd-160">Użyj jednej z zbiorczego hello importowanie metody tooload hello danych z plików lokalnej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="339cd-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="339cd-161">Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="339cd-161">Explore data, create features as needed.</span></span> <span data-ttu-id="339cd-162">Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="339cd-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="339cd-163">Tylko Pamiętaj toocreate niezbędne zapytania hello je.</span><span class="sxs-lookup"><span data-stu-id="339cd-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="339cd-164">Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.</span><span class="sxs-lookup"><span data-stu-id="339cd-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="339cd-165">Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="339cd-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="339cd-166">Witaj odczytu danych bezpośrednio z hello SQL Server przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="339cd-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="339cd-167">Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="339cd-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="339cd-168">Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="339cd-169"><a name="largelocaltodb"></a>Scenariusz \#5: dużego zestawu danych w lokalnych plikach, docelowa programu SQL Server w maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="339cd-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![TooSQL dużych plików lokalnej bazy danych na platformie Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="339cd-171">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="339cd-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="339cd-172">Utwórz maszynę wirtualną platformy Azure z programu SQL Server oraz serwer IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="339cd-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="339cd-173">Przekaż kontenera magazynu Azure tooan danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="339cd-174">(Opcjonalnie) Wstępnie przetworzyć i czyszczenia danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="339cd-175">a.</span><span class="sxs-lookup"><span data-stu-id="339cd-175">a.</span></span>  <span data-ttu-id="339cd-176">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="339cd-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="339cd-177">b.</span><span class="sxs-lookup"><span data-stu-id="339cd-177">b.</span></span>  <span data-ttu-id="339cd-178">Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="339cd-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="339cd-179">c.</span><span class="sxs-lookup"><span data-stu-id="339cd-179">c.</span></span>  <span data-ttu-id="339cd-180">Zapisywanie plików danych lokalnych tooVM (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków tooVM).</span><span class="sxs-lookup"><span data-stu-id="339cd-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="339cd-181">Dane tooSQL serwera bazy danych obciążenia uruchomione na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="339cd-182">a.</span><span class="sxs-lookup"><span data-stu-id="339cd-182">a.</span></span>  <span data-ttu-id="339cd-183">TooSQL logowania maszyny Wirtualnej serwera.</span><span class="sxs-lookup"><span data-stu-id="339cd-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="339cd-184">b.</span><span class="sxs-lookup"><span data-stu-id="339cd-184">b.</span></span>  <span data-ttu-id="339cd-185">Jeśli nie już zapisany na danych, pobieranie plików danych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="339cd-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="339cd-186">c.</span><span class="sxs-lookup"><span data-stu-id="339cd-186">c.</span></span>  <span data-ttu-id="339cd-187">Uruchom program SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="339cd-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="339cd-188">d.</span><span class="sxs-lookup"><span data-stu-id="339cd-188">d.</span></span>  <span data-ttu-id="339cd-189">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="339cd-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="339cd-190">e.</span><span class="sxs-lookup"><span data-stu-id="339cd-190">e.</span></span>  <span data-ttu-id="339cd-191">Użyj jednej z zbiorczego hello Importuj metody tooload hello dane.</span><span class="sxs-lookup"><span data-stu-id="339cd-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="339cd-192">f.</span><span class="sxs-lookup"><span data-stu-id="339cd-192">f.</span></span>  <span data-ttu-id="339cd-193">Jeśli sprzężeń tabel są wymagane, tworzyć sprzężenia tooexpedite indeksów.</span><span class="sxs-lookup"><span data-stu-id="339cd-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="339cd-194">Szybkość wczytywania rozmiary dużej ilości danych, zalecane jest utworzenie partycjonowane tabele i zbiorczego importowania danych hello równolegle.</span><span class="sxs-lookup"><span data-stu-id="339cd-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="339cd-195">Aby uzyskać więcej informacji, zobacz [tabel na partycje tooSQL równoległych importu danych](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="339cd-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="339cd-196">Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="339cd-196">Explore data, create features as needed.</span></span> <span data-ttu-id="339cd-197">Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="339cd-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="339cd-198">Tylko Pamiętaj toocreate niezbędne zapytania hello je.</span><span class="sxs-lookup"><span data-stu-id="339cd-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="339cd-199">Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.</span><span class="sxs-lookup"><span data-stu-id="339cd-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="339cd-200">Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="339cd-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="339cd-201">Witaj odczytu danych bezpośrednio z hello SQL Server przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="339cd-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="339cd-202">Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="339cd-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="339cd-203">Proste przepływu eksperymentu uczenia maszynowego Azure, począwszy od dataset przekazany</span><span class="sxs-lookup"><span data-stu-id="339cd-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="339cd-204"><a name="largedbtodb"></a>Scenariusz \#6: dużego zestawu danych w programie SQL Server bazy danych lokalnych, przeznaczonych dla programu SQL Server w maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="339cd-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Duże bazy danych SQL tooSQL lokalnej bazy danych na platformie Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="339cd-206">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="339cd-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="339cd-207">Utwórz maszynę wirtualną platformy Azure z programu SQL Server oraz serwer IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="339cd-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="339cd-208">Użyj jednej z danych hello wyeksportować metody tooexport hello danych z pliki toodump programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="339cd-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="339cd-209">Jeśli zdecydujesz toomove wszystkie dane z bazy danych z lokalnego hello, alternatywne (szybsze) metoda toomove hello pełnej bazy danych toothe wystąpienie programu SQL Server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="339cd-210">Pomiń hello kroki tooexport danych, Utwórz bazę danych i obciążenia/import danych toohello docelowej z bazy danych i wykonaj hello alternatywna metoda.</span><span class="sxs-lookup"><span data-stu-id="339cd-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="339cd-211">Przekaż kontenera magazynu tooAzure plików zrzutu.</span><span class="sxs-lookup"><span data-stu-id="339cd-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="339cd-212">Obciążenia hello danych tooa bazy danych SQL Server uruchomiony na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="339cd-213">a.</span><span class="sxs-lookup"><span data-stu-id="339cd-213">a.</span></span>  <span data-ttu-id="339cd-214">Toohello logowania maszyny Wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="339cd-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="339cd-215">b.</span><span class="sxs-lookup"><span data-stu-id="339cd-215">b.</span></span>  <span data-ttu-id="339cd-216">Pobieranie plików danych z folderu lokalnego wirtualna toohello kontenera magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="339cd-217">c.</span><span class="sxs-lookup"><span data-stu-id="339cd-217">c.</span></span>  <span data-ttu-id="339cd-218">Uruchom program SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="339cd-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="339cd-219">d.</span><span class="sxs-lookup"><span data-stu-id="339cd-219">d.</span></span>  <span data-ttu-id="339cd-220">Tworzenie tabel bazy danych i obiekt docelowy.</span><span class="sxs-lookup"><span data-stu-id="339cd-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="339cd-221">e.</span><span class="sxs-lookup"><span data-stu-id="339cd-221">e.</span></span>  <span data-ttu-id="339cd-222">Użyj jednej z zbiorczego hello Importuj metody tooload hello dane.</span><span class="sxs-lookup"><span data-stu-id="339cd-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="339cd-223">f.</span><span class="sxs-lookup"><span data-stu-id="339cd-223">f.</span></span>  <span data-ttu-id="339cd-224">Jeśli sprzężeń tabel są wymagane, tworzyć sprzężenia tooexpedite indeksów.</span><span class="sxs-lookup"><span data-stu-id="339cd-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="339cd-225">Szybkość wczytywania rozmiary dużej ilości danych, należy utworzyć toobulk importu hello danych i tabele partycjonowane równolegle.</span><span class="sxs-lookup"><span data-stu-id="339cd-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="339cd-226">Aby uzyskać więcej informacji, zobacz [tabel na partycje tooSQL równoległych importu danych](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="339cd-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="339cd-227">Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="339cd-227">Explore data, create features as needed.</span></span> <span data-ttu-id="339cd-228">Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="339cd-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="339cd-229">Tylko Pamiętaj toocreate niezbędne zapytania hello je.</span><span class="sxs-lookup"><span data-stu-id="339cd-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="339cd-230">Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.</span><span class="sxs-lookup"><span data-stu-id="339cd-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="339cd-231">Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="339cd-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="339cd-232">Witaj odczytu danych bezpośrednio z hello SQL Server przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="339cd-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="339cd-233">Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="339cd-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="339cd-234">Począwszy od dataset przekazany prosty przepływ eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="339cd-235">Alternatywna metoda toocopy pełnej bazy danych z lokalnego programu SQL Server tooAzure bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="339cd-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Odłączanie lokalnej bazy danych i Dołącz tooSQL bazy danych na platformie Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="339cd-237">Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)</span><span class="sxs-lookup"><span data-stu-id="339cd-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="339cd-238">tooreplicate hello całej bazy danych SQL Server w maszyną Wirtualną programu SQL Server, należy skopiować bazę danych z jednego serwera/lokalizacji tooanother, przy założeniu, że hello bazy danych można wykonać tymczasowo w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="339cd-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="339cd-239">Możesz to zrobić w hello Eksplorator obiektów SQL Server Management Studio lub za pomocą hello równoważnych poleceń języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="339cd-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="339cd-240">Odłączanie bazy danych hello w lokalizacji źródłowej hello.</span><span class="sxs-lookup"><span data-stu-id="339cd-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="339cd-241">Aby uzyskać więcej informacji, zobacz [odłączyć bazy danych](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="339cd-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="339cd-242">W oknie Eksploratora Windows lub wiersza polecenia systemu Windows hello kopiowania odłączyć plik bazy danych lub pliki i pliku dziennika lub lokalizacji docelowej toohello pliki na powitania maszyna wirtualna na platformie Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="339cd-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="339cd-243">Dołącz wystąpienia programu SQL Server hello kopiowane pliki toohello docelowej.</span><span class="sxs-lookup"><span data-stu-id="339cd-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="339cd-244">Aby uzyskać więcej informacji, zobacz [dołączyć bazę danych](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="339cd-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="339cd-245">[Przenoszenie bazy danych przy użyciu odłączyć i dołączyć (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="339cd-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="339cd-246"><a name="largedbtohive"></a>Scenariusz \#7: danych Big data w lokalnych plikach docelowa baza danych gałęzi w klastrach usługi Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="339cd-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Dane big data w celu lokalnego gałęzi][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="339cd-248">Dodatkowe zasoby platformy Azure: klastra usługi Hadoop w usłudze Azure HDInsight i maszyny wirtualnej platformy Azure (notesu IPython server)</span><span class="sxs-lookup"><span data-stu-id="339cd-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="339cd-249">Utwórz maszynę wirtualną platformy Azure, usługami IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="339cd-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="339cd-250">Tworzenie klastra usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="339cd-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="339cd-251">(Opcjonalnie) Wstępnie przetworzyć i czyszczenia danych.</span><span class="sxs-lookup"><span data-stu-id="339cd-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="339cd-252">a.</span><span class="sxs-lookup"><span data-stu-id="339cd-252">a.</span></span>  <span data-ttu-id="339cd-253">Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="339cd-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="339cd-254">b.</span><span class="sxs-lookup"><span data-stu-id="339cd-254">b.</span></span>  <span data-ttu-id="339cd-255">Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="339cd-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="339cd-256">c.</span><span class="sxs-lookup"><span data-stu-id="339cd-256">c.</span></span>  <span data-ttu-id="339cd-257">Zapisywanie plików danych lokalnych tooVM (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków tooVM).</span><span class="sxs-lookup"><span data-stu-id="339cd-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="339cd-258">Przekazywanie danych toohello domyślny kontener klastra Hadoop hello wybrany w hello krok 2.</span><span class="sxs-lookup"><span data-stu-id="339cd-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="339cd-259">Dane tooHive bazy danych obciążenia w klastrze usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="339cd-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="339cd-260">a.</span><span class="sxs-lookup"><span data-stu-id="339cd-260">a.</span></span>  <span data-ttu-id="339cd-261">Zaloguj się za toohello węzła głównego klastra usługi Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="339cd-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="339cd-262">b.</span><span class="sxs-lookup"><span data-stu-id="339cd-262">b.</span></span>  <span data-ttu-id="339cd-263">Otwórz hello wiersza polecenia usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="339cd-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="339cd-264">c.</span><span class="sxs-lookup"><span data-stu-id="339cd-264">c.</span></span>  <span data-ttu-id="339cd-265">Wprowadź katalog główny hello Hive za pomocą polecenia `cd %hive_home%\bin` w wierszu polecenia Hadoop.</span><span class="sxs-lookup"><span data-stu-id="339cd-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="339cd-266">d.</span><span class="sxs-lookup"><span data-stu-id="339cd-266">d.</span></span>  <span data-ttu-id="339cd-267">Uruchom hello Hive zapytania toocreate w bazie danych i tabele i ładowanie danych z tabel tooHive magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="339cd-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="339cd-268">Jeśli dane hello jest duży, użytkownicy mogą tworzyć hello tabelę programu Hive z partycjami.</span><span class="sxs-lookup"><span data-stu-id="339cd-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="339cd-269">Następnie użytkownicy mogą używać `for` pętli w hello wiersza polecenia usługi Hadoop na powitania węzła głównego tooload danych do tabeli Hive hello partycjonowanego partycji.</span><span class="sxs-lookup"><span data-stu-id="339cd-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="339cd-270">Eksplorowanie danych i tworzenie funkcji zgodnie z potrzebami w wierszu polecenia Hadoop.</span><span class="sxs-lookup"><span data-stu-id="339cd-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="339cd-271">Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="339cd-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="339cd-272">Tylko Pamiętaj toocreate niezbędne zapytania hello je.</span><span class="sxs-lookup"><span data-stu-id="339cd-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="339cd-273">a.</span><span class="sxs-lookup"><span data-stu-id="339cd-273">a.</span></span>  <span data-ttu-id="339cd-274">Zaloguj się za toohello węzła głównego klastra usługi Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="339cd-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="339cd-275">b.</span><span class="sxs-lookup"><span data-stu-id="339cd-275">b.</span></span>  <span data-ttu-id="339cd-276">Otwórz hello wiersza polecenia usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="339cd-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="339cd-277">c.</span><span class="sxs-lookup"><span data-stu-id="339cd-277">c.</span></span>  <span data-ttu-id="339cd-278">Wprowadź katalog główny hello Hive za pomocą polecenia `cd %hive_home%\bin` w wierszu polecenia Hadoop.</span><span class="sxs-lookup"><span data-stu-id="339cd-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="339cd-279">d.</span><span class="sxs-lookup"><span data-stu-id="339cd-279">d.</span></span>  <span data-ttu-id="339cd-280">Uruchamianie zapytań Hive hello w wierszu polecenia Hadoop na powitania węzła głównego hello Hadoop klastra tooexplore hello danych i tworzenie funkcji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="339cd-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="339cd-281">Jeśli wymagane lub pożądane, przykładowe hello toofit danych w usłudze Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="339cd-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="339cd-282">Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="339cd-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="339cd-283">Odczytywanie danych hello bezpośrednio z hello `Hive Queries` przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="339cd-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="339cd-284">Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.</span><span class="sxs-lookup"><span data-stu-id="339cd-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="339cd-285">Począwszy od dataset przekazany prosty przepływ eksperymentu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="339cd-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="339cd-286"><a name="decisiontree"></a>Drzewo decyzyjne dotyczące wyboru scenariusza</span><span class="sxs-lookup"><span data-stu-id="339cd-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="339cd-287">Hello poniższym diagramie przedstawiono opisanych powyżej scenariuszy hello i hello zaawansowane procesu analizy i technologii wyborów dokonanych przyjmujących tooeach hello wyszczególnione scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="339cd-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="339cd-288">Uwaga: przetwarzanie danych, eksploracji engineering funkcji i próbkowanie może być umieścić w jedną lub więcej metody/środowiska — w źródle hello, pośrednie, i/lub środowiska docelowego — i można kontynuować wielokrotnie powtarzane, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="339cd-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="339cd-289">Hello diagram tylko służy jako ilustrację niektóre możliwe przepływów i nie zapewnia kompleksowe wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="339cd-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Przykładowe DS procesu wskazówki scenariusze][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="339cd-291">Zaawansowane analizy w akcji przykłady</span><span class="sxs-lookup"><span data-stu-id="339cd-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="339cd-292">Aby uzyskać wskazówki dotyczące usługi Azure Machine Learning na trasie, które wykorzystują hello zaawansowane procesu analizy i technologii przy użyciu publicznego zestawów danych, zobacz:</span><span class="sxs-lookup"><span data-stu-id="339cd-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="339cd-293">[Zespół proces analizy danych w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="339cd-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="339cd-294">[Zespół proces analizy danych w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="339cd-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
