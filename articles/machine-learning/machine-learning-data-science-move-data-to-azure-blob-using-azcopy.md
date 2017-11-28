---
title: "aaaMove tooand danych z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy"
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
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="5ba10-103">Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="5ba10-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="5ba10-104">Narzędzie AzCopy to narzędzie wiersza polecenia przeznaczone dla przekazywanie, pobieranie i kopiowanie tooand danych z obiektu blob, plików i magazynowania tabeli Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba10-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="5ba10-105">Aby uzyskać instrukcje na temat instalowania programów AzCopy i dodatkowe informacje o użyciu hello platformy Azure, zobacz [wprowadzenie hello wiersza polecenia Azcopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5ba10-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="5ba10-106">Jeśli używasz maszyny Wirtualnej, który został skonfigurowany z dostarczonych przez skrypty hello [maszyn wirtualnych nauki danych na platformie Azure](machine-learning-data-science-virtual-machines.md), następnie AzCopy jest już zainstalowana na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ba10-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="5ba10-107">Magazyn obiektów blob tooAzure pełne wprowadzenie można znaleźć za[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i zbyt[usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ba10-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5ba10-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5ba10-108">Prerequisites</span></span>
<span data-ttu-id="5ba10-109">Ten dokument założono, że masz subskrypcji platformy Azure, konta magazynu i hello odpowiedniego klucza magazynu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="5ba10-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="5ba10-110">Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="5ba10-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="5ba10-111">tooset zapasową subskrypcji platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ba10-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5ba10-112">Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5ba10-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="5ba10-113">Uruchom polecenia AzCopy</span><span class="sxs-lookup"><span data-stu-id="5ba10-113">Run AzCopy commands</span></span>
<span data-ttu-id="5ba10-114">polecenia narzędzia AzCopy toorun, Otwórz okno polecenia i przejdź katalog instalacyjny AzCopy toohello na komputerze, w którym znajduje się plik wykonywalny AzCopy.exe hello.</span><span class="sxs-lookup"><span data-stu-id="5ba10-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="5ba10-115">Podstawowa składnia polecenia AzCopy Hello jest:</span><span class="sxs-lookup"><span data-stu-id="5ba10-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="5ba10-116">Możesz dodać ścieżki systemu tooyour lokalizacji instalacji hello AzCopy i następnie uruchom polecenia hello z dowolnego katalogu.</span><span class="sxs-lookup"><span data-stu-id="5ba10-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="5ba10-117">Domyślnie program AzCopy jest zainstalowany za*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* lub *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="5ba10-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="5ba10-118">Przekazywanie plików tooan obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5ba10-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="5ba10-119">tooupload pliku hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5ba10-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="5ba10-120">Pobierz pliki z obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5ba10-120">Download files from an Azure blob</span></span>
<span data-ttu-id="5ba10-121">toodownload pliku z obiektów blob platformy Azure, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5ba10-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="5ba10-122">Transferowania obiektów blob Azure kontenerów</span><span class="sxs-lookup"><span data-stu-id="5ba10-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="5ba10-123">obiekty BLOB tootransfer między Azure kontenery, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5ba10-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="5ba10-124">Porady dotyczące używania narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="5ba10-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="5ba10-125">Gdy **przekazywania** pliki, */S* przekazuje rekursywnie plików.</span><span class="sxs-lookup"><span data-stu-id="5ba10-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="5ba10-126">Bez tego parametru nie są przekazywane pliki w podkatalogach.</span><span class="sxs-lookup"><span data-stu-id="5ba10-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="5ba10-127">Gdy **pobierania** pliku, */S* wyszukiwania hello rekursywnie kontenera, dopóki wszystkie pliki w określonym katalogu hello i jego podkatalogach lub wszystkich plików spełniających hello określony wzorzec w hello podane pobierane są katalogu i jego podkatalogach.</span><span class="sxs-lookup"><span data-stu-id="5ba10-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="5ba10-128">Nie można określić **pliku konkretnego obiektu blob** toodownload przy użyciu hello */Source* parametru.</span><span class="sxs-lookup"><span data-stu-id="5ba10-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="5ba10-129">toodownload określonego pliku, określ za pomocą hello hello blob pliku nazwę toodownload */wzorca* parametru.</span><span class="sxs-lookup"><span data-stu-id="5ba10-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="5ba10-130">**/S** parametr może być używane toohave AzCopy poszukaj rekursywnie wzorzec nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="5ba10-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="5ba10-131">Bez parametru wzorzec hello AzCopy pobiera wszystkie pliki w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="5ba10-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

