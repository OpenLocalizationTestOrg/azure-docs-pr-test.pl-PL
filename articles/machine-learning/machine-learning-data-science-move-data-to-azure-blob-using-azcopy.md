---
title: "Przenoszenie danych do i z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy | Dokumentacja firmy Microsoft"
description: "Przenoszenie danych do oraz z usługi Azure Blob Storage za pomocą usługi AzCopy"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: a41ccdd5739a5b10cef201910abd639ae3126c02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="b046c-103">Przenoszenie danych do i z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="b046c-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="b046c-104">Narzędzie AzCopy to narzędzie wiersza polecenia przeznaczone dla przekazywanie, pobieranie i kopiowanie danych do i z obiektów blob Microsoft Azure, plików i magazynowania tabeli.</span><span class="sxs-lookup"><span data-stu-id="b046c-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="b046c-105">Aby uzyskać instrukcje na temat instalowania programów AzCopy i dodatkowe informacje na temat używania go z platformą Azure, zobacz [wprowadzenie do korzystania z wiersza polecenia Azcopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b046c-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="b046c-106">Jeśli używasz maszyny Wirtualnej, który został skonfigurowany za pomocą skryptów dostarczonych przez [maszyn wirtualnych nauki danych na platformie Azure](machine-learning-data-science-virtual-machines.md), następnie AzCopy jest już zainstalowana na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b046c-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b046c-107">Pełne wprowadzenie do magazynu obiektów blob platformy Azure, można znaleźć w temacie [podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i [usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="b046c-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b046c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b046c-108">Prerequisites</span></span>
<span data-ttu-id="b046c-109">Tym dokumencie przyjęto założenie, że masz subskrypcję platformy Azure, konta magazynu i odpowiedniego klucza magazynu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="b046c-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="b046c-110">Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="b046c-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="b046c-111">Aby skonfigurować subskrypcję platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b046c-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b046c-112">Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b046c-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="b046c-113">Uruchom polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="b046c-113">Run AzCopy commands</span></span>
<span data-ttu-id="b046c-114">Aby uruchomić polecenia AzCopy, Otwórz okno polecenia i przejdź do katalog instalacyjny programu AzCopy na komputerze, w którym znajduje się AzCopy.exe pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="b046c-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="b046c-115">Podstawowa składnia polecenia AzCopy jest:</span><span class="sxs-lookup"><span data-stu-id="b046c-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="b046c-116">Możesz dodać lokalizacji instalacji programu AzCopy do ścieżki systemowej i Uruchom polecenia z dowolnego katalogu.</span><span class="sxs-lookup"><span data-stu-id="b046c-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="b046c-117">Domyślnie program AzCopy jest instalowana na *% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* lub *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="b046c-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="b046c-118">Przekazać pliki do obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b046c-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="b046c-119">Aby przekazać plik, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b046c-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="b046c-120">Pobierz pliki z obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b046c-120">Download files from an Azure blob</span></span>
<span data-ttu-id="b046c-121">Aby pobrać plik z obiektów blob platformy Azure, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b046c-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="b046c-122">Transferowania obiektów blob Azure kontenerów</span><span class="sxs-lookup"><span data-stu-id="b046c-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="b046c-123">Do przesyłania obiektów blob między Azure kontenery, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b046c-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="b046c-124">Porady dotyczące używania narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="b046c-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="b046c-125">Gdy **przekazywania** pliki, */S* przekazuje rekursywnie plików.</span><span class="sxs-lookup"><span data-stu-id="b046c-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="b046c-126">Bez tego parametru nie są przekazywane pliki w podkatalogach.</span><span class="sxs-lookup"><span data-stu-id="b046c-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="b046c-127">Gdy **pobieranie** pliku */S* wyszukuje rekursywnie kontenera do momentu usunięcia wszystkich plików w określonym katalogu i jego podkatalogach lub wszystkie pliki, które jest zgodny z określonym wzorcem w podanym katalogu i jego podkatalogach zostaną pobrane.</span><span class="sxs-lookup"><span data-stu-id="b046c-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="b046c-128">Nie można określić **pliku konkretnego obiektu blob** do pobrania przy użyciu */Source* parametru.</span><span class="sxs-lookup"><span data-stu-id="b046c-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="b046c-129">Aby pobrać określonego pliku, określ nazwę pliku obiektu blob można pobrać przy użyciu */wzorca* parametru.</span><span class="sxs-lookup"><span data-stu-id="b046c-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="b046c-130">**/S** parametru można mieć AzCopy Wyszukaj rekursywnie wzorzec nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="b046c-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="b046c-131">Bez parametru wzorzec AzCopy pobiera wszystkie pliki w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="b046c-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

