---
title: "wprowadzenie do usługi Azure Data Lake Analytics przy użyciu usługi Azure CLI 2.0 aaaGet | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć zadanie usługi Data Lake Analytics przy użyciu języka U-SQL toouse hello 2.0 interfejsu wiersza polecenia Azure toocreate konto usługi Data Lake Analytics i przesłać zadanie hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a><span data-ttu-id="2f330-103">Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2f330-103">Get started with Azure Data Lake Analytics using Azure CLI 2.0</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="2f330-104">W ramach tego samouczka utworzysz zadanie, które odczytuje zawartość pliku z wartościami rozdzielanymi tabulatorami (TSV) i konwertuje je do pliku z wartościami rozdzielanymi przecinkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="2f330-104">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma-separated values (CSV) file.</span></span> <span data-ttu-id="2f330-105">toogo za pośrednictwem hello obsługiwane tego samouczka przy użyciu innych narzędzi, użyj listy rozwijanej hello na powitania górnej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="2f330-105">toogo through hello same tutorial using other supported tools, use hello dropdown list on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f330-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f330-106">Prerequisites</span></span>
<span data-ttu-id="2f330-107">Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2f330-107">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="2f330-108">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="2f330-108">**An Azure subscription**.</span></span> <span data-ttu-id="2f330-109">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f330-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2f330-110">**Interfejs wiersza polecenia platformy Azure 2.0**.</span><span class="sxs-lookup"><span data-stu-id="2f330-110">**Azure CLI 2.0**.</span></span> <span data-ttu-id="2f330-111">Zobacz temat [Instalowanie i konfigurowanie interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f330-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="2f330-112">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="2f330-112">Log in tooAzure</span></span>

<span data-ttu-id="2f330-113">toolog w tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="2f330-113">toolog in tooyour Azure subscription:</span></span>

```
azurecli
az login
```

<span data-ttu-id="2f330-114">Są żądane toobrowse tooa URL, a następnie wprowadź kod uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2f330-114">You are requested toobrowse tooa URL, and enter an authentication code.</span></span>  <span data-ttu-id="2f330-115">A następnie wykonaj tooenter instrukcje hello swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="2f330-115">And then follow hello instructions tooenter your credentials.</span></span>

<span data-ttu-id="2f330-116">Po zalogowaniu, hello logowania polecenie wyświetla listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2f330-116">Once you have logged in, hello login command lists your subscriptions.</span></span>

<span data-ttu-id="2f330-117">toouse określonej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="2f330-117">toouse a specific subscription:</span></span>

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="2f330-118">Tworzenie konta usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2f330-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="2f330-119">Aby można było uruchomić jakiekolwiek zadanie, musisz mieć konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2f330-119">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="2f330-120">toocreate konto usługi Data Lake Analytics, należy określić hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2f330-120">toocreate a Data Lake Analytics account, you must specify hello following items:</span></span>

* <span data-ttu-id="2f330-121">**Grupa zasobów platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="2f330-121">**Azure Resource Group**.</span></span> <span data-ttu-id="2f330-122">W grupie zasobów platformy Azure należy utworzyć konto usługi Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2f330-122">A Data Lake Analytics account must be created within an Azure Resource group.</span></span> <span data-ttu-id="2f330-123">[Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) pozwala toowork z zasobami hello w aplikacji jako grupa.</span><span class="sxs-lookup"><span data-stu-id="2f330-123">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you toowork with hello resources in your application as a group.</span></span> <span data-ttu-id="2f330-124">Można wdrożyć, zaktualizować lub usunąć wszystkie zasoby hello aplikacji w jednej, skoordynowanej operacji.</span><span class="sxs-lookup"><span data-stu-id="2f330-124">You can deploy, update, or delete all of hello resources for your application in a single, coordinated operation.</span></span>  

<span data-ttu-id="2f330-125">toolist hello istniejącej grupy zasobów w ramach Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="2f330-125">toolist hello existing resource groups under your subscription:</span></span>

```
az group list
```

<span data-ttu-id="2f330-126">toocreate nową grupę zasobów:</span><span class="sxs-lookup"><span data-stu-id="2f330-126">toocreate a new resource group:</span></span>

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* <span data-ttu-id="2f330-127">**Nazwa konta usługi Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2f330-127">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="2f330-128">Każde konto usługi Data Lake Analytics ma nazwę.</span><span class="sxs-lookup"><span data-stu-id="2f330-128">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="2f330-129">**Lokalizacja**.</span><span class="sxs-lookup"><span data-stu-id="2f330-129">**Location**.</span></span> <span data-ttu-id="2f330-130">Użyj jednej z hello centrach danych platformy Azure, obsługiwanych przez usługę Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="2f330-130">Use one of hello Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="2f330-131">**Domyślne konto usługi Data Lake Store**: każde konto usługi Data Lake Analytics ma domyślne konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2f330-131">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>

<span data-ttu-id="2f330-132">toolist hello istniejącego konta Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="2f330-132">toolist hello existing Data Lake Store account:</span></span>

```
az dls account list
```

<span data-ttu-id="2f330-133">toocreate nowe konto usługi Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="2f330-133">toocreate a new Data Lake Store account:</span></span>

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

<span data-ttu-id="2f330-134">Użyj następującej składni toocreate konto usługi Data Lake Analytics hello:</span><span class="sxs-lookup"><span data-stu-id="2f330-134">Use hello following syntax toocreate a Data Lake Analytics account:</span></span>

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="2f330-135">Po utworzeniu konta można użyć hello następujące polecenia toolist hello kont i Pokaż szczegóły konta:</span><span class="sxs-lookup"><span data-stu-id="2f330-135">After creating an account, you can use hello following commands toolist hello accounts and show account details:</span></span>

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a><span data-ttu-id="2f330-136">Przekaż tooData data Lake — Magazyn</span><span class="sxs-lookup"><span data-stu-id="2f330-136">Upload data tooData Lake Store</span></span>
<span data-ttu-id="2f330-137">W ramach tego samouczka przetworzysz wybrane dzienniki wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2f330-137">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="2f330-138">Dziennik wyszukiwania Hello mogą być przechowywane w usłudze Data Lake store lub magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2f330-138">hello search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="2f330-139">Hello Azure portal udostępnia interfejs użytkownika do kopiowania niektórych przykładowych danych plików toohello domyślnego konta Data Lake Store, obejmujące plik dziennika wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2f330-139">hello Azure portal provides a user interface for copying some sample data files toohello default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="2f330-140">Zobacz [Przygotowanie danych źródłowych](data-lake-analytics-get-started-portal.md) konta Data Lake Store domyślne toohello tooupload hello danych.</span><span class="sxs-lookup"><span data-stu-id="2f330-140">See [Prepare source data](data-lake-analytics-get-started-portal.md) tooupload hello data toohello default Data Lake Store account.</span></span>

<span data-ttu-id="2f330-141">pliki tooupload przy użyciu interfejsu wiersza polecenia 2.0, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2f330-141">tooupload files using CLI 2.0, use hello following commands:</span></span>

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="2f330-142">Usługa Data Lake Analytics może także uzyskiwać dostęp do usługi Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2f330-142">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="2f330-143">Do przekazywania danych tooAzure obiektu Blob magazynu, zobacz [hello używanie interfejsu wiersza polecenia Azure z usługą Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2f330-143">For uploading data tooAzure Blob storage, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="2f330-144">Przesyłanie zadań usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2f330-144">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="2f330-145">zadania usługi Data Lake Analytics Hello są zapisywane w hello języka U-SQL.</span><span class="sxs-lookup"><span data-stu-id="2f330-145">hello Data Lake Analytics jobs are written in hello U-SQL language.</span></span> <span data-ttu-id="2f330-146">toolearn więcej informacji o języku U-SQL, zobacz [wprowadzenie do języka U-SQL](data-lake-analytics-u-sql-get-started.md) i [eence języka U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="2f330-146">toolearn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="2f330-147">**toocreate skrypt zadania usługi Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="2f330-147">**toocreate a Data Lake Analytics job script**</span></span>

<span data-ttu-id="2f330-148">Utwórz plik tekstowy z poniższy skrypt U-SQL, a następnie zapisz hello tekstu pliku tooyour w stacji roboczej:</span><span class="sxs-lookup"><span data-stu-id="2f330-148">Create a text file with following U-SQL script, and save hello text file tooyour workstation:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="2f330-149">Ten skrypt U-SQL odczytuje hello źródła danych pliku przy użyciu **Extractors.Tsv()**, a następnie tworzy plik csv przy użyciu **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="2f330-149">This U-SQL script reads hello source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

<span data-ttu-id="2f330-150">Nie należy modyfikować Witaj dwie ścieżki, chyba że skopiować plik źródłowy hello do innej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="2f330-150">Don't modify hello two paths unless you copy hello source file into a different location.</span></span>  <span data-ttu-id="2f330-151">Data Lake Analytics tworzy folder wyjściowy hello, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="2f330-151">Data Lake Analytics creates hello output folder if it doesn't exist.</span></span>

<span data-ttu-id="2f330-152">Jest prostsze ścieżek względnych toouse dla plików przechowywanych na domyślnych kont usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2f330-152">It is simpler toouse relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="2f330-153">Można także użyć ścieżek bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="2f330-153">You can also use absolute paths.</span></span>  <span data-ttu-id="2f330-154">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2f330-154">For example:</span></span>

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

<span data-ttu-id="2f330-155">Należy użyć ścieżek bezwzględnych tooaccess plików w połączonych kontach magazynu.</span><span class="sxs-lookup"><span data-stu-id="2f330-155">You must use absolute paths tooaccess files in linked Storage accounts.</span></span>  <span data-ttu-id="2f330-156">Składnia Hello plików przechowywanych w połączonego konta usługi Azure Storage jest następująca:</span><span class="sxs-lookup"><span data-stu-id="2f330-156">hello syntax for files stored in linked Azure Storage account is:</span></span>

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> <span data-ttu-id="2f330-157">Kontenery obiektów blob platformy Azure zawierające publiczne obiekty blob nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2f330-157">Azure Blob container with public blobs are not supported.</span></span>      
> <span data-ttu-id="2f330-158">Kontenery obiektów blob platformy Azure zawierające publiczne kontenery nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2f330-158">Azure Blob container with public containers are not supported.</span></span>      
>

<span data-ttu-id="2f330-159">**zadania toosubmit**</span><span class="sxs-lookup"><span data-stu-id="2f330-159">**toosubmit jobs**</span></span>

<span data-ttu-id="2f330-160">Użyj hello następującej składni toosubmit zadania.</span><span class="sxs-lookup"><span data-stu-id="2f330-160">Use hello following syntax toosubmit a job.</span></span>

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="2f330-161">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2f330-161">For example:</span></span>

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="2f330-162">**zadania toolist i Pokaż szczegóły zadania**</span><span class="sxs-lookup"><span data-stu-id="2f330-162">**toolist jobs and show job details**</span></span>

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="2f330-163">**zadania toocancel**</span><span class="sxs-lookup"><span data-stu-id="2f330-163">**toocancel jobs**</span></span>

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a><span data-ttu-id="2f330-164">Pobieranie wyników zadania</span><span class="sxs-lookup"><span data-stu-id="2f330-164">Retrieve job results</span></span>

<span data-ttu-id="2f330-165">Po zakończeniu zadania można użyć hello następujące pliki wyjściowe hello toolist polecenia i pobierania plików hello:</span><span class="sxs-lookup"><span data-stu-id="2f330-165">After a job is completed, you can use hello following commands toolist hello output files, and download hello files:</span></span>

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="2f330-166">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2f330-166">For example:</span></span>

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="2f330-167">Potoki i cykle</span><span class="sxs-lookup"><span data-stu-id="2f330-167">Pipelines and recurrences</span></span>

<span data-ttu-id="2f330-168">**Uzyskaj informacje na temat potoków i cykli**</span><span class="sxs-lookup"><span data-stu-id="2f330-168">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="2f330-169">Użyj hello `az dla job pipeline` polecenia toosee hello potoku informacji wcześniej zgłoszonych zadania.</span><span class="sxs-lookup"><span data-stu-id="2f330-169">Use hello `az dla job pipeline` commands toosee hello pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="2f330-170">Użyj hello `az dla job recurrence` polecenia toosee hello cyklu informacje dla poprzednio przesłany zadań.</span><span class="sxs-lookup"><span data-stu-id="2f330-170">Use hello `az dla job recurrence` commands toosee hello recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a><span data-ttu-id="2f330-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f330-171">Next steps</span></span>

* <span data-ttu-id="2f330-172">toosee hello dokumencie referencyjnym Data Lake Analytics CLI 2.0, zobacz [usługi Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="2f330-172">toosee hello Data Lake Analytics CLI 2.0 reference document, see [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="2f330-173">toosee hello dokumencie referencyjnym Data Lake magazynu CLI 2.0, zobacz [usługi Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="2f330-173">toosee hello Data Lake Store CLI 2.0 reference document, see [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="2f330-174">toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="2f330-174">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
