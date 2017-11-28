---
title: "aaaMove tooand danych z magazynu obiektów Blob platformy Azure przy użyciu języka Python | Dokumentacja firmy Microsoft"
description: "Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu języka Python"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="4accf-103">Przenieś tooand danych z magazynu obiektów Blob platformy Azure przy użyciu języka Python</span><span class="sxs-lookup"><span data-stu-id="4accf-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="4accf-104">W tym temacie opisano sposób toolist, przekazywanie i pobieranie obiektów blob przy użyciu hello interfejsu API języka Python.</span><span class="sxs-lookup"><span data-stu-id="4accf-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="4accf-105">Hello udostępniane w zestawie SDK usługi Azure API języka Python możesz:</span><span class="sxs-lookup"><span data-stu-id="4accf-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="4accf-106">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="4accf-106">Create a container</span></span>
* <span data-ttu-id="4accf-107">Przekazywanie obiektu blob do kontenera</span><span class="sxs-lookup"><span data-stu-id="4accf-107">Upload a blob into a container</span></span>
* <span data-ttu-id="4accf-108">Pobieranie obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4accf-108">Download blobs</span></span>
* <span data-ttu-id="4accf-109">Lista hello BLOB w kontenerze</span><span class="sxs-lookup"><span data-stu-id="4accf-109">List hello blobs in a container</span></span>
* <span data-ttu-id="4accf-110">Usuwanie obiektu blob</span><span class="sxs-lookup"><span data-stu-id="4accf-110">Delete a blob</span></span>

<span data-ttu-id="4accf-111">Aby uzyskać więcej informacji o używaniu hello interfejsu API języka Python, zobacz [jak tooUse hello usługi magazynu obiektów Blob w języku Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4accf-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="4accf-112">Jeśli używasz maszyny Wirtualnej, który został skonfigurowany z dostarczonych przez skrypty hello [maszyn wirtualnych nauki danych na platformie Azure](machine-learning-data-science-virtual-machines.md), następnie AzCopy jest już zainstalowana na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4accf-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="4accf-113">Magazyn obiektów blob tooAzure pełne wprowadzenie można znaleźć za[podstawy obiektów Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) i zbyt[usługi obiektów Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="4accf-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4accf-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4accf-114">Prerequisites</span></span>
<span data-ttu-id="4accf-115">Tym dokumencie przyjęto założenie, że masz subskrypcję platformy Azure, konta magazynu i hello odpowiedniego klucza magazynu dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="4accf-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="4accf-116">Przed przekazaniem/pobieranie danych, musisz znać Azure klucz konta magazynu nazwy i konta.</span><span class="sxs-lookup"><span data-stu-id="4accf-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="4accf-117">tooset zapasową subskrypcji platformy Azure, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4accf-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4accf-118">Aby uzyskać instrukcje dotyczące tworzenia konta magazynu oraz uzyskiwanie konta i informacje o kluczu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4accf-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="4accf-119">Przekazywanie danych tooBlob</span><span class="sxs-lookup"><span data-stu-id="4accf-119">Upload Data tooBlob</span></span>
<span data-ttu-id="4accf-120">Dodaj powitania po fragment górze hello dowolnego kodu języka Python, w którym chcesz tooprogrammatically dostępu do magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="4accf-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="4accf-121">Witaj **BlobService** obiektu umożliwia pracę z kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4accf-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="4accf-122">Hello następującego kodu tworzy obiekt BlobService przy użyciu hello magazynu konta nazwy i klucza konta.</span><span class="sxs-lookup"><span data-stu-id="4accf-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="4accf-123">Zamień na nazwę konta i klucz konta swój rzeczywistych konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="4accf-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="4accf-124">Użyj hello następujące metody tooupload danych tooa blob:</span><span class="sxs-lookup"><span data-stu-id="4accf-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="4accf-125">Umieść\_bloku\_obiektu blob\_z\_ścieżki (przekazuje hello zawartości pliku z określonej ścieżki hello)</span><span class="sxs-lookup"><span data-stu-id="4accf-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="4accf-126">Umieść\_block_blob\_z\_pliku (przekazuje hello zawartość z otwartego pliku/strumienia)</span><span class="sxs-lookup"><span data-stu-id="4accf-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="4accf-127">Umieść\_bloku\_obiektu blob\_z\_bajtów (przekazywanie jako tablicę bajtów)</span><span class="sxs-lookup"><span data-stu-id="4accf-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="4accf-128">Umieść\_bloku\_obiektu blob\_z\_tekst (przekazuje hello określona wartość tekstową przy użyciu hello określonego kodowania)</span><span class="sxs-lookup"><span data-stu-id="4accf-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="4accf-129">Witaj następującego przykładowego kodu przekazuje kontenera tooa pliku lokalnego:</span><span class="sxs-lookup"><span data-stu-id="4accf-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="4accf-130">Witaj następujący przykładowy kod przekazuje wszystkie pliki hello (z wyjątkiem katalogów) w magazynie tooblob katalogu lokalnego:</span><span class="sxs-lookup"><span data-stu-id="4accf-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="4accf-131">Pobierz dane z obiektu Blob</span><span class="sxs-lookup"><span data-stu-id="4accf-131">Download Data from Blob</span></span>
<span data-ttu-id="4accf-132">Użyj poniższych metod toodownload danych z obiektu blob hello:</span><span class="sxs-lookup"><span data-stu-id="4accf-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="4accf-133">Pobierz\_obiektu blob\_do\_ścieżki</span><span class="sxs-lookup"><span data-stu-id="4accf-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="4accf-134">Pobierz\_obiektu blob\_do\_pliku</span><span class="sxs-lookup"><span data-stu-id="4accf-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="4accf-135">Pobierz\_obiektu blob\_do\_bajtów</span><span class="sxs-lookup"><span data-stu-id="4accf-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="4accf-136">Pobierz\_obiektu blob\_do\_tekstu</span><span class="sxs-lookup"><span data-stu-id="4accf-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="4accf-137">Te metody, wykonujących hello niezbędne podziału gdy rozmiar hello hello danych przekracza 64 MB.</span><span class="sxs-lookup"><span data-stu-id="4accf-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="4accf-138">Witaj następujący przykładowy kod pobiera hello zawartość obiektu blob w pliku lokalnym tooa kontenera:</span><span class="sxs-lookup"><span data-stu-id="4accf-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="4accf-139">Witaj następujący przykładowy kod pobiera wszystkie obiekty BLOB z kontenera.</span><span class="sxs-lookup"><span data-stu-id="4accf-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="4accf-140">Używa listy\_obiektów blob tooget hello listę dostępnych obiektów blob w kontenerze hello i pobiera je tooa katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="4accf-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
