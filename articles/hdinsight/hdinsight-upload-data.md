---
title: "aaaUpload danych dotyczących zadań Hadoop w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupload i dostępu do danych dotyczących zadań Hadoop w usłudze HDInsight przy użyciu hello Azure CLI, Eksploratora usługi Storage platformy Azure, programu Azure PowerShell, wiersza polecenia platformy Hadoop hello lub Sqoop."
keywords: "etl hadoop, pobieranie danych do platformy hadoop, hadoop ładowanie danych"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="0bea5-104">Przekazywanie danych dla zadań Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bea5-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="0bea5-105">Usługa Azure HDInsight udostępnia kompletne rozproszonego systemu plików usługi Hadoop (HDFS) w porównaniu z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0bea5-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="0bea5-106">Zaprojektowano go jako tooprovide rozszerzenia systemu plików HDFS bezproblemowej wystąpić toocustomers.</span><span class="sxs-lookup"><span data-stu-id="0bea5-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="0bea5-107">Umożliwia on hello pełny zestaw składników w toooperate ekosystemu Hadoop hello bezpośrednio na powitania danych, którymi zarządza.</span><span class="sxs-lookup"><span data-stu-id="0bea5-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="0bea5-108">Azure Blob storage i system plików HDFS są systemy różnych plików, które są zoptymalizowane pod kątem przechowywania danych i obliczenia na tych danych.</span><span class="sxs-lookup"><span data-stu-id="0bea5-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="0bea5-109">Aby uzyskać informacje dotyczące korzyści hello przy użyciu magazynu obiektów Blob platformy Azure, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="0bea5-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="0bea5-110">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="0bea5-110">**Prerequisites**</span></span>

<span data-ttu-id="0bea5-111">Należy uwzględnić następujące wymagania przed rozpoczęciem powitalne:</span><span class="sxs-lookup"><span data-stu-id="0bea5-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="0bea5-112">Klaster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bea5-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="0bea5-113">Aby uzyskać instrukcje, zobacz [Rozpoczynanie pracy z usługą Azure HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="0bea5-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="0bea5-114">Dlaczego magazynu obiektów blob?</span><span class="sxs-lookup"><span data-stu-id="0bea5-114">Why blob storage?</span></span>
<span data-ttu-id="0bea5-115">Usługa Azure HDInsight klastry są zwykle wdrażane toorun zadań MapReduce, a klastry hello są usuwane po zakończeniu tych zadań.</span><span class="sxs-lookup"><span data-stu-id="0bea5-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="0bea5-116">Utrzymywanie hello danych w klastrach systemu plików HDFS hello po zakończeniu obliczenia byłoby toostore sposób kosztowne tych danych.</span><span class="sxs-lookup"><span data-stu-id="0bea5-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="0bea5-117">Magazyn obiektów Blob Azure jest wysokiej dostępności, wysokiej skalowalności i wysokiej wydajności, opcja niskich kosztów i możliwe do udostępnienia magazynowania danych, które jest toobe przetworzona za pomocą usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bea5-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="0bea5-118">Zapisywanie danych w obiekcie blob umożliwia hello klastrów usługi HDInsight, które są używane do obliczeń toobe bezpiecznie wydana bez utraty danych.</span><span class="sxs-lookup"><span data-stu-id="0bea5-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="0bea5-119">Katalogi</span><span class="sxs-lookup"><span data-stu-id="0bea5-119">Directories</span></span>
<span data-ttu-id="0bea5-120">Kontenery magazynu obiektów Blob platformy Azure przechowują dane jako pary klucz wartość, a istnieje bez hierarchii katalogów.</span><span class="sxs-lookup"><span data-stu-id="0bea5-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="0bea5-121">Jednak Witaj "/" znak może być używana w toomake nazwa klucza hello wydaje się tak, jakby plik był przechowywany w ramach struktury katalogów.</span><span class="sxs-lookup"><span data-stu-id="0bea5-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="0bea5-122">HDInsight widzi je tak, jakby są rzeczywiste katalogów.</span><span class="sxs-lookup"><span data-stu-id="0bea5-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="0bea5-123">Na przykład klucz obiektu blob może mieć postać *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="0bea5-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="0bea5-124">Nie rzeczywiste katalogu "wejściowym" istnieje, ale powodu obecności toohello hello znak "/" w nazwie klucza hello, ma wygląd hello ścieżki do pliku.</span><span class="sxs-lookup"><span data-stu-id="0bea5-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="0bea5-125">W związku z tym Jeśli używasz narzędzia Azure Explorer mogą pojawić się niektóre pliki 0 bajtów.</span><span class="sxs-lookup"><span data-stu-id="0bea5-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="0bea5-126">Te pliki służą do dwóch celów:</span><span class="sxs-lookup"><span data-stu-id="0bea5-126">These files serve two purposes:</span></span>

* <span data-ttu-id="0bea5-127">Jeśli występują puste foldery, oznacz istnienia hello hello folderu.</span><span class="sxs-lookup"><span data-stu-id="0bea5-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="0bea5-128">Magazyn obiektów Blob Azure jest wystarczająco inteligentne tooknow, że jeśli obiektu blob o nazwie foo/pasek istnieje, jest folder o nazwie **foo**.</span><span class="sxs-lookup"><span data-stu-id="0bea5-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="0bea5-129">Ale hello tylko toosignify sposób pusty folder o nazwie **foo** jest posiadanie tego pliku specjalne 0 bajtów.</span><span class="sxs-lookup"><span data-stu-id="0bea5-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="0bea5-130">Blokady są specjalne metadane, które są wymagane przez hello Hadoop systemu plików, szczególnie hello uprawnienia i właścicieli hello folderów.</span><span class="sxs-lookup"><span data-stu-id="0bea5-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="0bea5-131">Narzędzia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0bea5-131">Command-line utilities</span></span>
<span data-ttu-id="0bea5-132">Firma Microsoft udostępnia hello następujące narzędzia toowork z magazynu obiektów Blob platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="0bea5-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="0bea5-133">Narzędzie</span><span class="sxs-lookup"><span data-stu-id="0bea5-133">Tool</span></span> | <span data-ttu-id="0bea5-134">Linux</span><span class="sxs-lookup"><span data-stu-id="0bea5-134">Linux</span></span> | <span data-ttu-id="0bea5-135">OS X</span><span class="sxs-lookup"><span data-stu-id="0bea5-135">OS X</span></span> | <span data-ttu-id="0bea5-136">Windows</span><span class="sxs-lookup"><span data-stu-id="0bea5-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="0bea5-137">[Interfejs wiersza polecenia platformy Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="0bea5-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="0bea5-138">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-138">✔</span></span> |<span data-ttu-id="0bea5-139">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-139">✔</span></span> |<span data-ttu-id="0bea5-140">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-140">✔</span></span> |
| <span data-ttu-id="0bea5-141">[Program Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="0bea5-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="0bea5-142">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-142">✔</span></span> |
| <span data-ttu-id="0bea5-143">[Narzędzie AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="0bea5-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="0bea5-144">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-144">✔</span></span> |
| [<span data-ttu-id="0bea5-145">Polecenie Hadoop</span><span class="sxs-lookup"><span data-stu-id="0bea5-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="0bea5-146">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-146">✔</span></span> |<span data-ttu-id="0bea5-147">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-147">✔</span></span> |<span data-ttu-id="0bea5-148">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="0bea5-149">Gdy hello wiersza polecenia platformy Azure, programu Azure PowerShell i narzędzia AzCopy można wszystkie można używać z zewnętrznej platformy Azure, hello Hadoop polecenia jest dostępna tylko na powitania klastra usługi HDInsight i zezwala na tylko podczas ładowania danych z hello lokalnego systemu plików do magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0bea5-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="0bea5-150"><a id="xplatcli"></a>Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0bea5-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="0bea5-151">Hello wiersza polecenia platformy Azure to narzędzie i platform, które pozwala toomanage Azure usługi.</span><span class="sxs-lookup"><span data-stu-id="0bea5-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="0bea5-152">Użyj powitania po magazynu obiektów Blob tooAzure danych tooupload kroki:</span><span class="sxs-lookup"><span data-stu-id="0bea5-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="0bea5-153">[Instalowanie i konfigurowanie hello Azure CLI for Mac, Linux i Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0bea5-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="0bea5-154">Otwórz wiersz polecenia, bash lub innego powłoki i użyj powitania po tooyour tooauthenticate subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0bea5-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="0bea5-155">Po wyświetleniu monitu wprowadź hello nazwę użytkownika i hasło dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0bea5-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="0bea5-156">Wprowadź hello następujących kont magazynu hello toolist polecenia dla Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="0bea5-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="0bea5-157">Wybierz konto magazynu hello zawierający hello obiektów blob, który ma toowork z, a następnie użyj powitania po klucz hello tooretrieve polecenia dla tego konta:</span><span class="sxs-lookup"><span data-stu-id="0bea5-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="0bea5-158">Powinny zostać zwrócone **głównej** i **dodatkowej** kluczy.</span><span class="sxs-lookup"><span data-stu-id="0bea5-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="0bea5-159">Kopiuj hello **głównej** wartość klucza, ponieważ będzie on używany w następnych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="0bea5-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="0bea5-160">Użyj następującego polecenia tooretrieve listę kontenerów obiektów blob w ramach konta magazynu hello hello:</span><span class="sxs-lookup"><span data-stu-id="0bea5-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="0bea5-161">Użyj następującego polecenia tooupload hello i pobierania plików toohello blob:</span><span class="sxs-lookup"><span data-stu-id="0bea5-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="0bea5-162">tooupload pliku:</span><span class="sxs-lookup"><span data-stu-id="0bea5-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="0bea5-163">toodownload pliku:</span><span class="sxs-lookup"><span data-stu-id="0bea5-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="0bea5-164">Jeśli będziesz zawsze pracować z hello same konta magazynu, możesz ustawić hello następujące zmienne środowiskowe zamiast określania hello konta i klucz dla każdego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0bea5-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="0bea5-165">**AZURE\_MAGAZYNU\_konta**: Nazwa konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="0bea5-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="0bea5-166">**AZURE\_MAGAZYNU\_dostępu\_klucza**: klucz konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="0bea5-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="0bea5-167"><a id="powershell"></a>Program Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bea5-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="0bea5-168">Program Azure PowerShell jest środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania obciążeń na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0bea5-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="0bea5-169">Aby uzyskać informacje o konfigurowaniu toorun Twojego stacji roboczej programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0bea5-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="0bea5-170">**tooupload tooAzure lokalnego pliku magazynu obiektów Blob**</span><span class="sxs-lookup"><span data-stu-id="0bea5-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="0bea5-171">Otwórz hello Azure PowerShell konsoli zgodnie z instrukcją w [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0bea5-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="0bea5-172">Ustaw wartości hello hello pierwsze pięć zmiennych w hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="0bea5-172">Set hello values of hello first five variables in hello following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="0bea5-173">Wklej hello do toorun konsoli programu Azure PowerShell hello go toocopy hello plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="0bea5-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="0bea5-174">Na przykład toowork utworzonych skryptów programu PowerShell z usługą HDInsight, zobacz [narzędzi HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="0bea5-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="0bea5-175"><a id="azcopy"></a>Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="0bea5-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="0bea5-176">Narzędzie AzCopy to narzędzie wiersza polecenia, które są zaprojektowane toosimplify hello zadanie transferu danych do i z konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0bea5-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="0bea5-177">Można używać jej jako autonomicznego narzędzia lub włączyć to narzędzie w istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bea5-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="0bea5-178">[Pobierz narzędzia AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="0bea5-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="0bea5-179">Składnia narzędzia AzCopy Hello jest:</span><span class="sxs-lookup"><span data-stu-id="0bea5-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="0bea5-180">Aby uzyskać więcej informacji, zobacz [AzCopy - przekazywania/pobieranie plików dla obiektów blob Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="0bea5-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="0bea5-181"><a id="commandline"></a>Wiersz polecenia usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="0bea5-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="0bea5-182">Wiersz polecenia Hadoop Hello jest przydatna do przechowywania danych do magazynu obiektów blob, gdy dane hello jest już obecny na powitania węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="0bea5-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="0bea5-183">W kolejności toouse hello polecenia Hadoop należy połączyć headnode toohello przy użyciu jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="0bea5-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="0bea5-184">**HDInsight opartych na systemie Windows**: [łączyć się przy użyciu pulpitu zdalnego](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="0bea5-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="0bea5-185">**HDInsight opartych na systemie Linux**: połączenie przy użyciu protokołu SSH ([hello polecenia SSH](hdinsight-hadoop-linux-use-ssh-unix.md) lub [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="0bea5-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="0bea5-186">Po nawiązaniu połączenia można użyć hello następującej składni tooupload toostorage pliku.</span><span class="sxs-lookup"><span data-stu-id="0bea5-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="0bea5-187">Na przykład: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="0bea5-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="0bea5-188">Ponieważ hello domyślnego systemu plików dla usługi HDInsight znajduje się w magazynie obiektów Blob Azure, /example/data.txt jest rzeczywiście w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0bea5-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="0bea5-189">Znajdują się w pliku toohello jako:</span><span class="sxs-lookup"><span data-stu-id="0bea5-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="0bea5-190">lub</span><span class="sxs-lookup"><span data-stu-id="0bea5-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="0bea5-191">Aby uzyskać listę innych Hadoop polecenia pracy z plikami, zobacz [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="0bea5-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="0bea5-192">W przypadku klastrów HBase hello domyślny rozmiar bloku używany podczas zapisywania danych 256KB.</span><span class="sxs-lookup"><span data-stu-id="0bea5-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="0bea5-193">Gdy nie ma problemów podczas korzystania z interfejsów API HBase lub interfejsów API REST, przy użyciu hello `hadoop` lub `hdfs dfs` większych niż ~ 12 GB danych toowrite polecenia powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="0bea5-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="0bea5-194">Zobacz hello [wyjątek magazynu do zapisu dla obiektu blob](#storageexception) sekcji poniżej, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="0bea5-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="0bea5-195">Klientach graficznego</span><span class="sxs-lookup"><span data-stu-id="0bea5-195">Graphical clients</span></span>
<span data-ttu-id="0bea5-196">Istnieje kilka aplikacji, które zapewniają interfejs graficzny służący do pracy z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0bea5-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="0bea5-197">Witaj poniżej znajduje się lista niektóre z tych aplikacji:</span><span class="sxs-lookup"><span data-stu-id="0bea5-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="0bea5-198">Klient</span><span class="sxs-lookup"><span data-stu-id="0bea5-198">Client</span></span> | <span data-ttu-id="0bea5-199">Linux</span><span class="sxs-lookup"><span data-stu-id="0bea5-199">Linux</span></span> | <span data-ttu-id="0bea5-200">OS X</span><span class="sxs-lookup"><span data-stu-id="0bea5-200">OS X</span></span> | <span data-ttu-id="0bea5-201">Windows</span><span class="sxs-lookup"><span data-stu-id="0bea5-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="0bea5-202">Microsoft Visual Studio Tools dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bea5-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="0bea5-203">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-203">✔</span></span> |<span data-ttu-id="0bea5-204">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-204">✔</span></span> |<span data-ttu-id="0bea5-205">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-205">✔</span></span> |
| [<span data-ttu-id="0bea5-206">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="0bea5-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="0bea5-207">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-207">✔</span></span> |<span data-ttu-id="0bea5-208">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-208">✔</span></span> |<span data-ttu-id="0bea5-209">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-209">✔</span></span> |
| [<span data-ttu-id="0bea5-210">Chmura magazynu Studio 2</span><span class="sxs-lookup"><span data-stu-id="0bea5-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="0bea5-211">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-211">✔</span></span> |
| [<span data-ttu-id="0bea5-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="0bea5-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="0bea5-213">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-213">✔</span></span> |
| [<span data-ttu-id="0bea5-214">Eksplorator systemu Azure</span><span class="sxs-lookup"><span data-stu-id="0bea5-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="0bea5-215">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-215">✔</span></span> |
| [<span data-ttu-id="0bea5-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="0bea5-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="0bea5-217">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-217">✔</span></span> |<span data-ttu-id="0bea5-218">✔</span><span class="sxs-lookup"><span data-stu-id="0bea5-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="0bea5-219">Visual Studio Tools dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="0bea5-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="0bea5-220">Aby uzyskać więcej informacji, zobacz [hello Nawigacja połączonych zasobów](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="0bea5-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="0bea5-221"><a id="storageexplorer"></a>Eksplorator usługi Storage platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0bea5-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="0bea5-222">*Eksplorator usługi Storage Azure* stanowi przydatne narzędzie sprawdzania i zmienianie hello danych w obiektach blob.</span><span class="sxs-lookup"><span data-stu-id="0bea5-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="0bea5-223">To narzędzie wolnego typu open source, który można pobrać z [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="0bea5-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="0bea5-224">Kod źródłowy Hello jest dostępna z tego łącza, a także.</span><span class="sxs-lookup"><span data-stu-id="0bea5-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="0bea5-225">Przed użyciem narzędzia hello, musisz znać Azure klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="0bea5-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="0bea5-226">Aby uzyskać instrukcje dotyczące pobierania tych informacji, zobacz hello "jak: widoku, kopiowania i regenerate magazynu klucze dostępu" sekcji [tworzenia, zarządzania i usuwania konta magazynu][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="0bea5-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="0bea5-227">Uruchom Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0bea5-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="0bea5-228">Jeśli po raz pierwszy hello uruchomieniu hello Eksploratora usługi Storage, zostanie wyświetlony monit dla hello **nazwa konta miej_sca VM** i **klucz konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="0bea5-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="0bea5-229">Po uruchomieniu go przed Użyj hello **Dodaj** przycisk tooadd nazwę nowego konta magazynu i klucza.</span><span class="sxs-lookup"><span data-stu-id="0bea5-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="0bea5-230">Wprowadź hello nazwy i klucza dla konta magazynu hello korzystali z klastrem usługi HDInsight, a następnie wybierz opcję **Otwórz z & APISZ**.</span><span class="sxs-lookup"><span data-stu-id="0bea5-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="0bea5-232">Na liście hello lewej toohello kontenery interfejsu hello kliknij nazwę hello hello kontenera, który jest skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0bea5-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="0bea5-233">Domyślnie to jest nazwa hello hello klastra usługi HDInsight, ale mogą być inne, jeśli podczas tworzenia klastra hello wprowadzone określonej nazwy.</span><span class="sxs-lookup"><span data-stu-id="0bea5-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="0bea5-234">Z paska narzędzi hello wybierz ikonę przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="0bea5-234">From hello tool bar, select hello upload icon.</span></span>

    ![Pasek narzędzi z ikoną przekazywania wyróżnione](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="0bea5-236">Określ tooupload pliku, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="0bea5-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="0bea5-237">Po wyświetleniu monitu wybierz **przekazać** tooupload hello pliku toohello głównym hello kontenera magazynu.</span><span class="sxs-lookup"><span data-stu-id="0bea5-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="0bea5-238">Jeśli chcesz tooupload hello pliku tooa określonej ścieżki, wprowadź ścieżkę hello w hello **docelowego** pola, a następnie wybierz **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="0bea5-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Okno dialogowe przekazywania pliku](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="0bea5-240">Po zakończeniu hello plików podczas przekazywania, można go z zadań w klastrze usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="0bea5-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="0bea5-241">Magazyn obiektów Blob Azure instalacji jako dysk lokalny</span><span class="sxs-lookup"><span data-stu-id="0bea5-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="0bea5-242">Zobacz [magazyn obiektów Blob Azure instalacji jako dysk lokalny](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bea5-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="0bea5-243">Usługi</span><span class="sxs-lookup"><span data-stu-id="0bea5-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="0bea5-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0bea5-244">Azure Data Factory</span></span>
<span data-ttu-id="0bea5-245">Hello usługi fabryka danych Azure jest w pełni zarządzaną usługę służącą do tworzenia magazynu, przetwarzanie danych i danych usługi przenoszenia danych usługi w potokach produkcji prostsze, skalowalne i niezawodne danych.</span><span class="sxs-lookup"><span data-stu-id="0bea5-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="0bea5-246">Fabryka danych Azure mogą być używane toomove dane do magazynu obiektów Blob platformy Azure lub toocreate potokach danych, które bezpośrednio takich jak używać funkcji usługi HDInsight Hive i wieprzowych.</span><span class="sxs-lookup"><span data-stu-id="0bea5-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="0bea5-247">Aby uzyskać więcej informacji, zobacz hello [dokumentacji fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="0bea5-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="0bea5-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="0bea5-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="0bea5-249">Sqoop to narzędzie przeznaczone tootransfer danych pomiędzy platformą Hadoop a relacyjnymi bazami danych.</span><span class="sxs-lookup"><span data-stu-id="0bea5-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="0bea5-250">Umożliwia tooimport danych z systemu zarządzania relacyjnymi bazami danych (RDBMS), takie jak SQL Server, MySQL lub Oracle w systemie plików usługi Hadoop distributed hello (HDFS), przekształcania danych hello w platformy Hadoop za pomocą MapReduce lub Hive, a następnie wyeksportować hello danych do RDBMS.</span><span class="sxs-lookup"><span data-stu-id="0bea5-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="0bea5-251">Aby uzyskać więcej informacji, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="0bea5-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="0bea5-252">Programowanie zestawów SDK</span><span class="sxs-lookup"><span data-stu-id="0bea5-252">Development SDKs</span></span>
<span data-ttu-id="0bea5-253">Magazyn obiektów Blob Azure można również uzyskać dostęp przy użyciu zestawu SDK platformy Azure z hello następujące języki programowania:</span><span class="sxs-lookup"><span data-stu-id="0bea5-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="0bea5-254">.NET</span><span class="sxs-lookup"><span data-stu-id="0bea5-254">.NET</span></span>
* <span data-ttu-id="0bea5-255">Java</span><span class="sxs-lookup"><span data-stu-id="0bea5-255">Java</span></span>
* <span data-ttu-id="0bea5-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="0bea5-256">Node.js</span></span>
* <span data-ttu-id="0bea5-257">PHP</span><span class="sxs-lookup"><span data-stu-id="0bea5-257">PHP</span></span>
* <span data-ttu-id="0bea5-258">Python</span><span class="sxs-lookup"><span data-stu-id="0bea5-258">Python</span></span>
* <span data-ttu-id="0bea5-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="0bea5-259">Ruby</span></span>

<span data-ttu-id="0bea5-260">Aby uzyskać więcej informacji na temat instalowania hello Azure SDK, zobacz [Azure pliki do pobrania.](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="0bea5-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0bea5-261">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="0bea5-261">Troubleshooting</span></span>
### <span data-ttu-id="0bea5-262"><a id="storageexception"></a>Wyjątek magazynu do zapisu dla obiektu blob</span><span class="sxs-lookup"><span data-stu-id="0bea5-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="0bea5-263">**Objawy**: przy użyciu hello `hadoop` lub `hdfs dfs` polecenia toowrite pliki, które są ~ 12 GB lub większy na klaster HBase, można napotkać hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="0bea5-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="0bea5-264">**Przyczyna**: bazy danych HBase w usłudze HDInsight clusters domyślny rozmiar bloku tooa 256 KB, podczas zapisywania tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="0bea5-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="0bea5-265">Gdy działa to w przypadku interfejsu API REST lub interfejsów API HBase, spowoduje błąd przy użyciu hello `hadoop` lub `hdfs dfs` narzędzi wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="0bea5-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="0bea5-266">**Rozdzielczość**: Użyj `fs.azure.write.request.size` toospecify większy rozmiar bloku.</span><span class="sxs-lookup"><span data-stu-id="0bea5-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="0bea5-267">Należy na podstawie użycia za pomocą hello `-D` parametru.</span><span class="sxs-lookup"><span data-stu-id="0bea5-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="0bea5-268">Witaj poniżej przedstawiono przykład użycia tego parametru z hello `hadoop` polecenia:</span><span class="sxs-lookup"><span data-stu-id="0bea5-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="0bea5-269">Można również zwiększyć wartość hello `fs.azure.write.request.size` globalnie, za pomocą narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="0bea5-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="0bea5-270">Witaj czynności do wykonania może być używana wartość hello toochange w hello Interfejsu sieci Web Ambari:</span><span class="sxs-lookup"><span data-stu-id="0bea5-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="0bea5-271">W przeglądarce Przejdź toohello Interfejsu sieci Web Ambari dla klastra.</span><span class="sxs-lookup"><span data-stu-id="0bea5-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="0bea5-272">Jest to https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest hello nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="0bea5-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="0bea5-273">Po wyświetleniu monitu wprowadź nazwę administratora hello i hasło dla hello klastra.</span><span class="sxs-lookup"><span data-stu-id="0bea5-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="0bea5-274">Hello po lewej stronie ekranu hello, zaznacz **HDFS**, a następnie wybierz hello **Configs** kartę.</span><span class="sxs-lookup"><span data-stu-id="0bea5-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="0bea5-275">W hello **filtru...**  wprowadź `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="0bea5-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="0bea5-276">Spowoduje to wyświetlenie hello pola i bieżąca wartość w środku hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="0bea5-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="0bea5-277">Zmień wartość hello z 262144 (256KB) toohello nową wartość.</span><span class="sxs-lookup"><span data-stu-id="0bea5-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="0bea5-278">Na przykład 4194304 (4MB).</span><span class="sxs-lookup"><span data-stu-id="0bea5-278">For example, 4194304 (4MB).</span></span>

![Obraz zmiany wartości hello za pośrednictwem interfejsu użytkownika sieci Web Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="0bea5-280">Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [Zarządzanie klastrów usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari hello](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="0bea5-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bea5-281">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0bea5-281">Next steps</span></span>
<span data-ttu-id="0bea5-282">Zapoznaniu się jak tooget danych do usługi HDInsight, przeczytaj hello następujące artykuły toolearn jak tooperform analizy:</span><span class="sxs-lookup"><span data-stu-id="0bea5-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="0bea5-283">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0bea5-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="0bea5-284">[Przesyłanie zadań Hadoop programowo][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="0bea5-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="0bea5-285">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="0bea5-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="0bea5-286">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="0bea5-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
