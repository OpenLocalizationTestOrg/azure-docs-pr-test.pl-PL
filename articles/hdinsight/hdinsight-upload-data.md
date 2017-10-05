---
title: "Przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przekazywanie i uzyskać dostęp do danych dotyczących zadań Hadoop w usłudze HDInsight przy użyciu wiersza polecenia platformy Azure, Eksploratora usługi Storage platformy Azure, programu Azure PowerShell, wiersz polecenia Hadoop lub Sqoop."
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
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="742c5-104">Przekazywanie danych dla zadań Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="742c5-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="742c5-105">Usługa Azure HDInsight udostępnia kompletne rozproszonego systemu plików usługi Hadoop (HDFS) w porównaniu z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="742c5-106">Zaprojektowano go jako rozszerzenie systemu plików HDFS aby zapewnić bezproblemową obsługę klientów.</span><span class="sxs-lookup"><span data-stu-id="742c5-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="742c5-107">Umożliwia on pełny zestaw składników w ekosystemie Hadoop do działania bezpośrednio na danych, którymi zarządza.</span><span class="sxs-lookup"><span data-stu-id="742c5-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="742c5-108">Azure Blob storage i system plików HDFS są systemy różnych plików, które są zoptymalizowane pod kątem przechowywania danych i obliczenia na tych danych.</span><span class="sxs-lookup"><span data-stu-id="742c5-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="742c5-109">Aby uzyskać informacje o zaletach przy użyciu magazynu obiektów Blob platformy Azure, zobacz [magazynu obiektów Blob Azure użycia z usługą HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="742c5-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="742c5-110">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="742c5-110">**Prerequisites**</span></span>

<span data-ttu-id="742c5-111">Przed rozpoczęciem należy uwzględnić następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="742c5-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="742c5-112">Klaster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="742c5-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="742c5-113">Aby uzyskać instrukcje, zobacz [Rozpoczynanie pracy z usługą Azure HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="742c5-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="742c5-114">Dlaczego magazynu obiektów blob?</span><span class="sxs-lookup"><span data-stu-id="742c5-114">Why blob storage?</span></span>
<span data-ttu-id="742c5-115">Klastry HDInsight Azure zwykle są wdrażane do uruchomienia zadań MapReduce, a klastry są usuwane po zakończeniu tych zadań.</span><span class="sxs-lookup"><span data-stu-id="742c5-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="742c5-116">Przechowywanie danych w systemie plików HDFS klastrów po zakończeniu obliczenia będzie kosztowna sposób przechowywania tych danych.</span><span class="sxs-lookup"><span data-stu-id="742c5-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="742c5-117">Magazyn obiektów Blob Azure jest wysokiej dostępności, wysokiej skalowalności i wysokiej wydajności, opcja niskich kosztów i możliwe do udostępnienia magazynowania danych, które mają być przetwarzane przy użyciu usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="742c5-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="742c5-118">Zapisywanie danych w obiekcie blob umożliwia klastrów usługi HDInsight, które są używane do obliczeń bezpiecznie wydana bez utraty danych.</span><span class="sxs-lookup"><span data-stu-id="742c5-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="742c5-119">Katalogi</span><span class="sxs-lookup"><span data-stu-id="742c5-119">Directories</span></span>
<span data-ttu-id="742c5-120">Kontenery magazynu obiektów Blob platformy Azure przechowują dane jako pary klucz wartość, a istnieje bez hierarchii katalogów.</span><span class="sxs-lookup"><span data-stu-id="742c5-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="742c5-121">Jednak znak "/" umożliwia wewnątrz nazwy klucza wydawać tak, jakby plik był przechowywany w ramach struktury katalogów.</span><span class="sxs-lookup"><span data-stu-id="742c5-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="742c5-122">HDInsight widzi je tak, jakby są rzeczywiste katalogów.</span><span class="sxs-lookup"><span data-stu-id="742c5-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="742c5-123">Na przykład klucz obiektu blob może mieć postać *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="742c5-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="742c5-124">Nie rzeczywiste katalogu "wejściowym" istnieje, ale z powodu obecności znaku "/" w nazwie klucza ma wygląd ścieżki do pliku.</span><span class="sxs-lookup"><span data-stu-id="742c5-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="742c5-125">W związku z tym Jeśli używasz narzędzia Azure Explorer mogą pojawić się niektóre pliki 0 bajtów.</span><span class="sxs-lookup"><span data-stu-id="742c5-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="742c5-126">Te pliki służą do dwóch celów:</span><span class="sxs-lookup"><span data-stu-id="742c5-126">These files serve two purposes:</span></span>

* <span data-ttu-id="742c5-127">Jeśli występują puste foldery, oznacz istnienia folderu.</span><span class="sxs-lookup"><span data-stu-id="742c5-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="742c5-128">Magazyn obiektów Blob Azure jest inteligentne dowiedzieć się, że istnienie obiektu blob o nazwie foo/pasek istnieje folder o nazwie **foo**.</span><span class="sxs-lookup"><span data-stu-id="742c5-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="742c5-129">Jedynym sposobem oznaczającego pusty folder o nazwie, ale **foo** jest posiadanie tego pliku specjalne 0 bajtów.</span><span class="sxs-lookup"><span data-stu-id="742c5-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="742c5-130">Posiadają specjalne metadanych, które są wymagane przez system plików Hadoop, szczególnie uprawnienia i właścicieli dla folderów.</span><span class="sxs-lookup"><span data-stu-id="742c5-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="742c5-131">Narzędzia wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="742c5-131">Command-line utilities</span></span>
<span data-ttu-id="742c5-132">Firma Microsoft udostępnia następujące narzędzia do pracy z magazynem obiektów Blob Azure:</span><span class="sxs-lookup"><span data-stu-id="742c5-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="742c5-133">Narzędzie</span><span class="sxs-lookup"><span data-stu-id="742c5-133">Tool</span></span> | <span data-ttu-id="742c5-134">Linux</span><span class="sxs-lookup"><span data-stu-id="742c5-134">Linux</span></span> | <span data-ttu-id="742c5-135">OS X</span><span class="sxs-lookup"><span data-stu-id="742c5-135">OS X</span></span> | <span data-ttu-id="742c5-136">Windows</span><span class="sxs-lookup"><span data-stu-id="742c5-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="742c5-137">[Interfejs wiersza polecenia platformy Azure][azurecli]</span><span class="sxs-lookup"><span data-stu-id="742c5-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="742c5-138">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-138">✔</span></span> |<span data-ttu-id="742c5-139">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-139">✔</span></span> |<span data-ttu-id="742c5-140">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-140">✔</span></span> |
| <span data-ttu-id="742c5-141">[Program Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="742c5-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="742c5-142">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-142">✔</span></span> |
| <span data-ttu-id="742c5-143">[Narzędzie AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="742c5-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="742c5-144">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-144">✔</span></span> |
| [<span data-ttu-id="742c5-145">Polecenie Hadoop</span><span class="sxs-lookup"><span data-stu-id="742c5-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="742c5-146">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-146">✔</span></span> |<span data-ttu-id="742c5-147">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-147">✔</span></span> |<span data-ttu-id="742c5-148">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="742c5-149">Gdy wiersza polecenia platformy Azure, programu Azure PowerShell i narzędzia AzCopy można wszystkie można używać z zewnętrznej platformy Azure, Hadoop polecenia jest dostępna tylko w klastrze usługi HDInsight i zezwala na tylko podczas ładowania danych z lokalnego systemu plików do magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="742c5-150"><a id="xplatcli"></a>Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="742c5-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="742c5-151">Interfejsu wiersza polecenia Azure to narzędzie i platform, które umożliwia zarządzanie usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="742c5-152">Aby przekazać dane do magazynu obiektów Blob platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="742c5-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="742c5-153">[Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure dla komputerów Mac, Linux i Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="742c5-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="742c5-154">Otwórz wiersz polecenia, bash lub innego powłoki i służą do uwierzytelniania do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="742c5-155">Po wyświetleniu monitu wprowadź nazwę użytkownika i hasło dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="742c5-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="742c5-156">Wprowadź następujące polecenie, aby wyświetlić listę kont magazynu dla Twojej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="742c5-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="742c5-157">Wybierz konto magazynu, które zawiera blob, które mają być używane, a następnie użyj następującego polecenia, aby pobrać klucz dla tego konta:</span><span class="sxs-lookup"><span data-stu-id="742c5-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="742c5-158">Powinny zostać zwrócone **głównej** i **dodatkowej** kluczy.</span><span class="sxs-lookup"><span data-stu-id="742c5-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="742c5-159">Kopiuj **głównej** wartość klucza, ponieważ będzie on używany w następnych krokach.</span><span class="sxs-lookup"><span data-stu-id="742c5-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="742c5-160">Aby pobrać listę kontenerów obiektów blob w ramach konta magazynu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="742c5-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="742c5-161">Przekazywania i pobierania plików do obiektu blob, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="742c5-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="742c5-162">Aby przekazać plik:</span><span class="sxs-lookup"><span data-stu-id="742c5-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="742c5-163">Aby pobrać plik:</span><span class="sxs-lookup"><span data-stu-id="742c5-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="742c5-164">Jeśli będziesz zawsze pracować z tego samego konta magazynu, można ustawić następujące zmienne środowiskowe zamiast określania konta i klucz dla każdego polecenia:</span><span class="sxs-lookup"><span data-stu-id="742c5-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="742c5-165">**AZURE\_MAGAZYNU\_konta**: Nazwa konta magazynu</span><span class="sxs-lookup"><span data-stu-id="742c5-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="742c5-166">**AZURE\_MAGAZYNU\_dostępu\_klucza**: klucz konta magazynu</span><span class="sxs-lookup"><span data-stu-id="742c5-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="742c5-167"><a id="powershell"></a>Program Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="742c5-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="742c5-168">Program Azure PowerShell jest środowiskiem skryptów, które umożliwia kontrolowanie i automatyzowania wdrażania i zarządzania obciążeń na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="742c5-169">Aby uzyskać informacji na temat konfigurowania stacji roboczej do uruchomienia programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="742c5-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="742c5-170">**Aby przekazać plik lokalny do magazynu obiektów Blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="742c5-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="742c5-171">Otwórz konsolę programu Azure PowerShell, zgodnie z instrukcją w [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="742c5-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="742c5-172">Ustaw wartości zmiennych pierwsze pięć w poniższym skrypcie:</span><span class="sxs-lookup"><span data-stu-id="742c5-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="742c5-173">Wklej skryptu w konsoli programu Azure PowerShell, aby uruchomić ją można skopiować pliku.</span><span class="sxs-lookup"><span data-stu-id="742c5-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="742c5-174">Na przykład skrypty programu PowerShell utworzone do pracy z usługą HDInsight, zobacz [narzędzi HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="742c5-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="742c5-175"><a id="azcopy"></a>Narzędzie AzCopy</span><span class="sxs-lookup"><span data-stu-id="742c5-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="742c5-176">Narzędzie AzCopy to narzędzie wiersza polecenia, które jest przeznaczona do upraszcza zadanie transferu danych do i z konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="742c5-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="742c5-177">Można używać jej jako autonomicznego narzędzia lub włączyć to narzędzie w istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="742c5-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="742c5-178">[Pobierz narzędzia AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="742c5-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="742c5-179">Składnia narzędzia AzCopy jest następująca:</span><span class="sxs-lookup"><span data-stu-id="742c5-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="742c5-180">Aby uzyskać więcej informacji, zobacz [AzCopy - przekazywania/pobieranie plików dla obiektów blob Azure][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="742c5-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="742c5-181"><a id="commandline"></a>Wiersz polecenia usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="742c5-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="742c5-182">W wierszu polecenia Hadoop tylko przydaje się do przechowywania danych do magazynu obiektów blob, gdy danych jest już obecny na węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="742c5-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="742c5-183">Aby można było użyć polecenia Hadoop, musisz najpierw połączyć się headnode przy użyciu jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="742c5-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="742c5-184">**HDInsight opartych na systemie Windows**: [łączyć się przy użyciu pulpitu zdalnego](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="742c5-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="742c5-185">**HDInsight opartych na systemie Linux**: połączenie przy użyciu protokołu SSH ([polecenia SSH](hdinsight-hadoop-linux-use-ssh-unix.md) lub [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="742c5-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="742c5-186">Po nawiązaniu połączenia można użyć następującej składni do przekazania pliku do magazynu.</span><span class="sxs-lookup"><span data-stu-id="742c5-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="742c5-187">Na przykład: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="742c5-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="742c5-188">Ponieważ jest domyślny system plików dla usługi HDInsight w magazynie obiektów Blob platformy Azure, /example/data.txt jest rzeczywiście w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="742c5-189">Możesz także zapoznać się plik jako:</span><span class="sxs-lookup"><span data-stu-id="742c5-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="742c5-190">lub</span><span class="sxs-lookup"><span data-stu-id="742c5-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="742c5-191">Aby uzyskać listę innych Hadoop polecenia pracy z plikami, zobacz [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="742c5-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="742c5-192">Na klastrów HBase domyślnie bloku rozmiar używany podczas zapisywania danych to 256KB.</span><span class="sxs-lookup"><span data-stu-id="742c5-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="742c5-193">Gdy nie ma problemów podczas korzystania z interfejsów API HBase lub interfejsów API REST, za pomocą `hadoop` lub `hdfs dfs` polecenia do zapisania danych większych niż ~ 12 GB powoduje wystąpienie błędu.</span><span class="sxs-lookup"><span data-stu-id="742c5-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="742c5-194">Zobacz [wyjątek magazynu do zapisu dla obiektu blob](#storageexception) sekcji poniżej, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="742c5-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="742c5-195">Klientach graficznego</span><span class="sxs-lookup"><span data-stu-id="742c5-195">Graphical clients</span></span>
<span data-ttu-id="742c5-196">Istnieje kilka aplikacji, które zapewniają interfejs graficzny służący do pracy z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="742c5-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="742c5-197">Poniżej przedstawiono listę niektóre z tych aplikacji:</span><span class="sxs-lookup"><span data-stu-id="742c5-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="742c5-198">Klient</span><span class="sxs-lookup"><span data-stu-id="742c5-198">Client</span></span> | <span data-ttu-id="742c5-199">Linux</span><span class="sxs-lookup"><span data-stu-id="742c5-199">Linux</span></span> | <span data-ttu-id="742c5-200">OS X</span><span class="sxs-lookup"><span data-stu-id="742c5-200">OS X</span></span> | <span data-ttu-id="742c5-201">Windows</span><span class="sxs-lookup"><span data-stu-id="742c5-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="742c5-202">Microsoft Visual Studio Tools dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="742c5-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="742c5-203">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-203">✔</span></span> |<span data-ttu-id="742c5-204">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-204">✔</span></span> |<span data-ttu-id="742c5-205">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-205">✔</span></span> |
| [<span data-ttu-id="742c5-206">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="742c5-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="742c5-207">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-207">✔</span></span> |<span data-ttu-id="742c5-208">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-208">✔</span></span> |<span data-ttu-id="742c5-209">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-209">✔</span></span> |
| [<span data-ttu-id="742c5-210">Chmura magazynu Studio 2</span><span class="sxs-lookup"><span data-stu-id="742c5-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="742c5-211">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-211">✔</span></span> |
| [<span data-ttu-id="742c5-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="742c5-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="742c5-213">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-213">✔</span></span> |
| [<span data-ttu-id="742c5-214">Eksplorator systemu Azure</span><span class="sxs-lookup"><span data-stu-id="742c5-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="742c5-215">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-215">✔</span></span> |
| [<span data-ttu-id="742c5-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="742c5-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="742c5-217">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-217">✔</span></span> |<span data-ttu-id="742c5-218">✔</span><span class="sxs-lookup"><span data-stu-id="742c5-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="742c5-219">Visual Studio Tools dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="742c5-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="742c5-220">Aby uzyskać więcej informacji, zobacz [Przejdź połączonych zasobów](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="742c5-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="742c5-221"><a id="storageexplorer"></a>Eksplorator usługi Storage platformy Azure</span><span class="sxs-lookup"><span data-stu-id="742c5-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="742c5-222">*Eksplorator usługi Storage Azure* stanowi przydatne narzędzie do sprawdzania i zmiany danych w obiektach blob.</span><span class="sxs-lookup"><span data-stu-id="742c5-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="742c5-223">To narzędzie wolnego typu open source, który można pobrać z [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="742c5-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="742c5-224">Kod źródłowy jest dostępny z tego łącza, a także.</span><span class="sxs-lookup"><span data-stu-id="742c5-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="742c5-225">Przed użyciem tego narzędzia, musisz znać Azure klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="742c5-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="742c5-226">Aby uzyskać instrukcje dotyczące pobierania tych informacji, zobacz "jak: widoku, kopiowania i regenerate magazynu klucze dostępu" sekcji [tworzenia, zarządzania i usuwania konta magazynu][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="742c5-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="742c5-227">Uruchom Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="742c5-228">Jeśli przy pierwszym uruchomieniu Eksploratora magazynu, zostanie wyświetlony monit dla **nazwa konta miej_sca VM** i **klucz konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="742c5-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="742c5-229">Po uruchomieniu go przed użyj **Dodaj** przycisk, aby dodać nową nazwę konta magazynu i klucza.</span><span class="sxs-lookup"><span data-stu-id="742c5-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="742c5-230">Wprowadź nazwę i klucza konta magazynu używane przez klaster usługi HDInsight, a następnie wybierz **Otwórz z & APISZ**.</span><span class="sxs-lookup"><span data-stu-id="742c5-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="742c5-232">Na liście kontenerów do lewej strony interfejsu kliknij nazwę kontenera, w którym jest skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="742c5-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="742c5-233">Domyślnie to jest nazwą klastra usługi HDInsight, ale mogą być inne, jeśli określona nazwa wprowadzona podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="742c5-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="742c5-234">Na pasku narzędzi wybierz ikonę przekazywania.</span><span class="sxs-lookup"><span data-stu-id="742c5-234">From the tool bar, select the upload icon.</span></span>

    ![Pasek narzędzi z ikoną przekazywania wyróżnione](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="742c5-236">Określ plik do przekazania, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="742c5-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="742c5-237">Po wyświetleniu monitu wybierz **przekazać** można przekazać pliku do katalogu głównego kontenera magazynu.</span><span class="sxs-lookup"><span data-stu-id="742c5-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="742c5-238">Jeśli chcesz przekazać pliku do określonej ścieżki, wprowadź ścieżkę w **docelowego** a następnie wybierz opcję **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="742c5-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![Okno dialogowe przekazywania pliku](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="742c5-240">Po zakończeniu przekazywania, można go użyć z zadań w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="742c5-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="742c5-241">Magazyn obiektów Blob Azure instalacji jako dysk lokalny</span><span class="sxs-lookup"><span data-stu-id="742c5-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="742c5-242">Zobacz [magazyn obiektów Blob Azure instalacji jako dysk lokalny](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="742c5-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="742c5-243">Usługi</span><span class="sxs-lookup"><span data-stu-id="742c5-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="742c5-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="742c5-244">Azure Data Factory</span></span>
<span data-ttu-id="742c5-245">Usługi fabryka danych Azure jest w pełni zarządzaną usługę służącą do tworzenia magazynu, przetwarzanie danych i danych usługi przenoszenia danych usługi w potokach produkcji prostsze, skalowalne i niezawodne danych.</span><span class="sxs-lookup"><span data-stu-id="742c5-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="742c5-246">Fabryka danych Azure może służyć do przenoszenia danych do magazynu obiektów Blob platformy Azure lub utworzyć potoki danych, które bezpośrednio przy użyciu funkcji usługi HDInsight, takich jak Hive i Pig.</span><span class="sxs-lookup"><span data-stu-id="742c5-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="742c5-247">Aby uzyskać więcej informacji, zobacz [dokumentacji fabryki danych Azure](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="742c5-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="742c5-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="742c5-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="742c5-249">Sqoop to narzędzie przeznaczone do transferu danych między Hadoop a relacyjnymi bazami danych.</span><span class="sxs-lookup"><span data-stu-id="742c5-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="742c5-250">Można go użyć do importowania danych z systemu zarządzania relacyjnymi bazami danych (RDBMS), takie jak SQL Server, MySQL lub Oracle w systemie plików usługi Hadoop distributed (HDFS), Przekształć dane w platformy Hadoop za pomocą MapReduce lub Hive, a następnie wyeksportować dane do RDBMS.</span><span class="sxs-lookup"><span data-stu-id="742c5-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="742c5-251">Aby uzyskać więcej informacji, zobacz [Sqoop użycia z usługą HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="742c5-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="742c5-252">Programowanie zestawów SDK</span><span class="sxs-lookup"><span data-stu-id="742c5-252">Development SDKs</span></span>
<span data-ttu-id="742c5-253">Magazyn obiektów Blob Azure można również uzyskać dostęp za pomocą zestawu Azure SDK w następujących językach programowania:</span><span class="sxs-lookup"><span data-stu-id="742c5-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="742c5-254">.NET</span><span class="sxs-lookup"><span data-stu-id="742c5-254">.NET</span></span>
* <span data-ttu-id="742c5-255">Java</span><span class="sxs-lookup"><span data-stu-id="742c5-255">Java</span></span>
* <span data-ttu-id="742c5-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="742c5-256">Node.js</span></span>
* <span data-ttu-id="742c5-257">PHP</span><span class="sxs-lookup"><span data-stu-id="742c5-257">PHP</span></span>
* <span data-ttu-id="742c5-258">Python</span><span class="sxs-lookup"><span data-stu-id="742c5-258">Python</span></span>
* <span data-ttu-id="742c5-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="742c5-259">Ruby</span></span>

<span data-ttu-id="742c5-260">Aby uzyskać więcej informacji na temat instalowania zestawów SDK usługi Azure, zobacz [Azure pliki do pobrania.](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="742c5-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="742c5-261">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="742c5-261">Troubleshooting</span></span>
### <span data-ttu-id="742c5-262"><a id="storageexception"></a>Wyjątek magazynu do zapisu dla obiektu blob</span><span class="sxs-lookup"><span data-stu-id="742c5-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="742c5-263">**Objawy**: przy użyciu `hadoop` lub `hdfs dfs` poleceń, aby zapisywać pliki, które są ~ 12 GB lub większej na klaster HBase, może wystąpić następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="742c5-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="742c5-264">**Przyczyna**: HBase w usłudze HDInsight clusters domyślne do blok o rozmiarze 256 KB podczas zapisywania do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="742c5-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="742c5-265">Gdy działa to w przypadku interfejsu API REST lub interfejsów API HBase, spowoduje błąd przy użyciu `hadoop` lub `hdfs dfs` narzędzi wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="742c5-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="742c5-266">**Rozdzielczość**: Użyj `fs.azure.write.request.size` do określ większy rozmiar bloku.</span><span class="sxs-lookup"><span data-stu-id="742c5-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="742c5-267">Należy na podstawie użycia za pomocą `-D` parametru.</span><span class="sxs-lookup"><span data-stu-id="742c5-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="742c5-268">Poniżej przedstawiono przykład użycia tego parametru z `hadoop` polecenia:</span><span class="sxs-lookup"><span data-stu-id="742c5-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="742c5-269">Można również zwiększyć wartość `fs.azure.write.request.size` globalnie, za pomocą narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="742c5-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="742c5-270">Poniższe kroki można zmienić wartość w interfejsie użytkownika sieci Web Ambari:</span><span class="sxs-lookup"><span data-stu-id="742c5-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="742c5-271">W przeglądarce przejdź do Interfejsu sieci Web Ambari dla klastra.</span><span class="sxs-lookup"><span data-stu-id="742c5-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="742c5-272">Jest to https://CLUSTERNAME.azurehdinsight.net, gdzie **CLUSTERNAME** jest nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="742c5-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="742c5-273">Po wyświetleniu monitu wprowadź nazwę administratora i hasła dla klastra.</span><span class="sxs-lookup"><span data-stu-id="742c5-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="742c5-274">Po lewej stronie ekranu, wybierz **HDFS**, a następnie wybierz **Configs** kartę.</span><span class="sxs-lookup"><span data-stu-id="742c5-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="742c5-275">W **filtru...**  wprowadź `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="742c5-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="742c5-276">Spowoduje to wyświetlenie pola i bieżąca wartość w środku strony.</span><span class="sxs-lookup"><span data-stu-id="742c5-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="742c5-277">Zmień wartość z 262144 (256KB) do nowej wartości.</span><span class="sxs-lookup"><span data-stu-id="742c5-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="742c5-278">Na przykład 4194304 (4MB).</span><span class="sxs-lookup"><span data-stu-id="742c5-278">For example, 4194304 (4MB).</span></span>

![Obraz zmiany wartości za pośrednictwem interfejsu użytkownika sieci Web Ambari](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="742c5-280">Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu użytkownika sieci Web Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="742c5-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="742c5-281">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="742c5-281">Next steps</span></span>
<span data-ttu-id="742c5-282">Teraz, gdy wiesz, jak można pobrać danych do usługi HDInsight, przeczytaj następujące artykuły, aby dowiedzieć się, jak wykonywać analizy:</span><span class="sxs-lookup"><span data-stu-id="742c5-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="742c5-283">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="742c5-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="742c5-284">[Przesyłanie zadań Hadoop programowo][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="742c5-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="742c5-285">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="742c5-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="742c5-286">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="742c5-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
