---
title: "aaaManage Azure Data Lake Analytics przy użyciu interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania konta usługi Data Lake Analytics toomanage, źródła danych i użytkowników przy użyciu wiersza polecenia platformy Azure"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="40ab7-103">Zarządzanie Azure Data Lake Analytics przy użyciu interfejsu wiersza polecenia platformy Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="40ab7-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="40ab7-104">Dowiedz się, jak toomanage kont usługi Azure Data Lake Analytics, źródeł danych użytkowników i zadań za pomocą hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab7-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="40ab7-105">Tematy dotyczące zarządzania toosee przy użyciu innych narzędzi, kliknij przycisk Wybierz kartę hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="40ab7-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="40ab7-106">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="40ab7-106">**Prerequisites**</span></span>

<span data-ttu-id="40ab7-107">Przed rozpoczęciem tego samouczka wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="40ab7-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="40ab7-108">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="40ab7-108">**An Azure subscription**.</span></span> <span data-ttu-id="40ab7-109">Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40ab7-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="40ab7-110">**Interfejs wiersza polecenia platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="40ab7-110">**Azure CLI**.</span></span> <span data-ttu-id="40ab7-111">Zobacz temat [Instalowanie i konfigurowanie interfejsu wiersza polecenia platformy Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="40ab7-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="40ab7-112">Pobierz i zainstaluj hello **wstępną** [narzędzia wiersza polecenia platformy Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) w celu toocomplete tego pokazu.</span><span class="sxs-lookup"><span data-stu-id="40ab7-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="40ab7-113">**Uwierzytelnianie**za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="40ab7-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="40ab7-114">Aby uzyskać więcej informacji na temat uwierzytelniania przy użyciu konta służbowego, zobacz [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="40ab7-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="40ab7-115">**Przełącz tryb usługi Azure Resource Manager toohello**za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="40ab7-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="40ab7-116">**polecenia usługi Data Lake Store i usługi Data Lake Analytics toolist hello:**</span><span class="sxs-lookup"><span data-stu-id="40ab7-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="40ab7-117">Zarządzanie kontami</span><span class="sxs-lookup"><span data-stu-id="40ab7-117">Manage accounts</span></span>
<span data-ttu-id="40ab7-118">Przed uruchomieniem zadania usługi Data Lake Analytics, musisz mieć konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="40ab7-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="40ab7-119">W przeciwieństwie do usługi Azure HDInsight nie płatności dla konta usługi Analytics zadania nie jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="40ab7-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="40ab7-120">Płacisz tylko za czas hello, gdy jest uruchomione zadanie.</span><span class="sxs-lookup"><span data-stu-id="40ab7-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="40ab7-121">Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40ab7-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="40ab7-122">Tworzenie kont</span><span class="sxs-lookup"><span data-stu-id="40ab7-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="40ab7-123">Aktualizowanie kont</span><span class="sxs-lookup"><span data-stu-id="40ab7-123">Update accounts</span></span>
<span data-ttu-id="40ab7-124">Witaj następujące polecenie aktualizuje hello właściwości istniejącego konta Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="40ab7-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="40ab7-125">Wyświetlanie listy kont</span><span class="sxs-lookup"><span data-stu-id="40ab7-125">List accounts</span></span>
<span data-ttu-id="40ab7-126">Lista Data Lake Analytics kont</span><span class="sxs-lookup"><span data-stu-id="40ab7-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="40ab7-127">Lista Data Lake Analytics kont w ramach określonej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="40ab7-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="40ab7-128">Uzyskiwanie szczegółowych informacji z określonego konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="40ab7-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="40ab7-129">Usuwanie konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="40ab7-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="40ab7-130">Zarządzaj źródłami danych konta</span><span class="sxs-lookup"><span data-stu-id="40ab7-130">Manage account data sources</span></span>
<span data-ttu-id="40ab7-131">Data Lake Analytics obsługuje obecnie hello następujące źródła danych:</span><span class="sxs-lookup"><span data-stu-id="40ab7-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="40ab7-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="40ab7-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="40ab7-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="40ab7-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="40ab7-134">Podczas tworzenia konta usługi Analytics należy wyznaczyć usługi Azure Data Lake Storage konta toobe hello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="40ab7-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="40ab7-135">Witaj domyślne konto magazynu ADL służy toostore zadania metadanych i zadania dziennika inspekcji.</span><span class="sxs-lookup"><span data-stu-id="40ab7-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="40ab7-136">Po utworzeniu konta usługi Analytics można dodać dodatkowe konta usługi Data Lake Storage i/lub konta usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab7-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="40ab7-137">Znajdź hello domyślne konto magazynu ADL</span><span class="sxs-lookup"><span data-stu-id="40ab7-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="40ab7-138">wartość Hello jest na liście właściwości: datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="40ab7-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="40ab7-139">Dodawanie dodatkowych kont magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="40ab7-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="40ab7-140">Są obsługiwane tylko obiektu Blob magazynu krótkiej nazwy.</span><span class="sxs-lookup"><span data-stu-id="40ab7-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="40ab7-141">Nie używaj nazwy FQDN, na przykład "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="40ab7-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="40ab7-142">Dodawanie dodatkowych kont usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="40ab7-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="40ab7-143">[-d] jest opcjonalnym przełącznikiem tooindicate czy hello Data Lake dodawane jest konto usługi Data Lake domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="40ab7-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="40ab7-144">Aktualizowanie istniejącego źródła danych</span><span class="sxs-lookup"><span data-stu-id="40ab7-144">Update existing data source</span></span>
<span data-ttu-id="40ab7-145">tooset istniejącej domyślnej hello toobe konta usługi Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="40ab7-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="40ab7-146">tooupdate istniejącego klucza konta magazynu obiektów Blob:</span><span class="sxs-lookup"><span data-stu-id="40ab7-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="40ab7-147">Lista źródeł danych:</span><span class="sxs-lookup"><span data-stu-id="40ab7-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics listy źródła danych](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="40ab7-149">Usuń źródła danych:</span><span class="sxs-lookup"><span data-stu-id="40ab7-149">Delete data sources:</span></span>
<span data-ttu-id="40ab7-150">Konto usługi Data Lake Store toodelete:</span><span class="sxs-lookup"><span data-stu-id="40ab7-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="40ab7-151">toodelete konta magazynu obiektów Blob:</span><span class="sxs-lookup"><span data-stu-id="40ab7-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="40ab7-152">Zarządzanie zadaniami</span><span class="sxs-lookup"><span data-stu-id="40ab7-152">Manage jobs</span></span>
<span data-ttu-id="40ab7-153">Aby można było utworzyć zadanie, musisz mieć konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="40ab7-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="40ab7-154">Aby uzyskać więcej informacji, zobacz [kont zarządzania usługi Data Lake Analytics](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="40ab7-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="40ab7-155">Lista zadań</span><span class="sxs-lookup"><span data-stu-id="40ab7-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics listy źródła danych](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="40ab7-157">Uzyskiwanie szczegółów zadania</span><span class="sxs-lookup"><span data-stu-id="40ab7-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="40ab7-158">Przesyłanie zadań</span><span class="sxs-lookup"><span data-stu-id="40ab7-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="40ab7-159">Hello domyślny priorytet zadania wynosi 1000, a hello domyślne stopień równoległości zadania jest 1.</span><span class="sxs-lookup"><span data-stu-id="40ab7-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="40ab7-160">Anulowanie zadań</span><span class="sxs-lookup"><span data-stu-id="40ab7-160">Cancel jobs</span></span>
<span data-ttu-id="40ab7-161">Użyj identyfikator zadania hello toofind hello listy poleceń, a następnie użyj anulowania toocancel hello zadania.</span><span class="sxs-lookup"><span data-stu-id="40ab7-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="40ab7-162">Zarządzanie katalogiem</span><span class="sxs-lookup"><span data-stu-id="40ab7-162">Manage catalog</span></span>
<span data-ttu-id="40ab7-163">wykaz Hello U-SQL jest toostructure używanych danych i kod, aby mogły być udostępniane przez skrypty U-SQL.</span><span class="sxs-lookup"><span data-stu-id="40ab7-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="40ab7-164">wykaz Hello umożliwia hello najwyższym możliwym poziomie wydajności z danymi w usłudze Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="40ab7-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="40ab7-165">Więcej informacji znajduje się w temacie [Używanie katalogu U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="40ab7-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="40ab7-166">Lista elementów katalogu</span><span class="sxs-lookup"><span data-stu-id="40ab7-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="40ab7-167">typy Hello zawierają bazy danych, schematów, zestawu, zewnętrzne źródło danych, tabeli, funkcji zwracającej tabelę lub statystyk tabeli.</span><span class="sxs-lookup"><span data-stu-id="40ab7-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="40ab7-168">Użyj grup ARM</span><span class="sxs-lookup"><span data-stu-id="40ab7-168">Use ARM groups</span></span>
<span data-ttu-id="40ab7-169">Aplikacje składają się zazwyczaj z wielu składników, na przykład aplikacji sieci Web, bazy danych, serwera bazy danych, magazynu i usług firm zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="40ab7-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="40ab7-170">Usługa Azure Resource Manager (ARM) umożliwia toowork z zasobami hello w aplikacji jako grupę, określonym tooas grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab7-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="40ab7-171">Można wdrożyć, zaktualizować, monitorować lub usunąć wszystkie zasoby hello aplikacji w jednej, skoordynowanej operacji.</span><span class="sxs-lookup"><span data-stu-id="40ab7-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="40ab7-172">Wdrażanie wykonuje się przy użyciu szablonu, którego można następnie używać w różnych środowiskach (testowanie, etap przejściowy i produkcja).</span><span class="sxs-lookup"><span data-stu-id="40ab7-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="40ab7-173">Można również uprościć rozliczenia w organizacji, wyświetlając hello zestawienia kosztów całej grupy hello.</span><span class="sxs-lookup"><span data-stu-id="40ab7-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="40ab7-174">Aby uzyskać więcej informacji, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40ab7-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="40ab7-175">Usługa Data Lake Analytics może zawierać hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="40ab7-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="40ab7-176">Usługa Azure Data Lake Analytics konta</span><span class="sxs-lookup"><span data-stu-id="40ab7-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="40ab7-177">Wymagane domyślne konto usługi Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="40ab7-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="40ab7-178">Dodatkowe usługi Azure Data Lake kont magazynu</span><span class="sxs-lookup"><span data-stu-id="40ab7-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="40ab7-179">Dodatkowe konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="40ab7-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="40ab7-180">Wszystkie te składniki w jednym toomake grupy ARM można tworzyć ich toomanage łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="40ab7-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Usługa Azure Data Lake Analytics konta i magazynu](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="40ab7-182">Konto usługi Data Lake Analytics i kont magazynu zależnego hello muszą być umieszczone w hello sam centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="40ab7-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="40ab7-183">jednak Hello ARM grupy może znajdować się w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="40ab7-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="40ab7-184">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="40ab7-184">See also</span></span>
* [<span data-ttu-id="40ab7-185">Omówienie usługi Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="40ab7-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="40ab7-186">Rozpoczynanie pracy z usługą Data Lake Analytics przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="40ab7-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="40ab7-187">Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="40ab7-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="40ab7-188">Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="40ab7-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

