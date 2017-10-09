---
title: "tooAzure aaaIntroduction magazynu obiektów Blob | Dokumentacja firmy Microsoft"
description: "Wprowadzenie tooAzure magazynu obiektów Blob"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="1e374-103">Wprowadzenie tooBlob magazynu</span><span class="sxs-lookup"><span data-stu-id="1e374-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="1e374-104">Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych obiektów niestrukturalnych, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1e374-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="1e374-105">Możesz użyć danych tooexpose magazynu obiektów Blob publicznie toohello world lub toostore danych aplikacji prywatnie.</span><span class="sxs-lookup"><span data-stu-id="1e374-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="1e374-106">Najczęstsze zastosowania usługi Blob Storage obejmują:</span><span class="sxs-lookup"><span data-stu-id="1e374-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="1e374-107">Obrazy lub dokumentów bezpośrednio tooa przeglądarki</span><span class="sxs-lookup"><span data-stu-id="1e374-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="1e374-108">Przechowywanie plików do dostępu rozproszonego</span><span class="sxs-lookup"><span data-stu-id="1e374-108">Storing files for distributed access</span></span>
* <span data-ttu-id="1e374-109">Przesyłanie strumieniowe audio i wideo</span><span class="sxs-lookup"><span data-stu-id="1e374-109">Streaming video and audio</span></span>
* <span data-ttu-id="1e374-110">Zapisywanie danych w celu tworzenia kopii zapasowych, przywracania, odzyskiwania po awarii i archiwizowania</span><span class="sxs-lookup"><span data-stu-id="1e374-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="1e374-111">Przechowywanie danych w celu analizy w usłudze lokalnej lub hostowanej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1e374-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="1e374-112">Pojęcia dotyczące usługi Blob</span><span class="sxs-lookup"><span data-stu-id="1e374-112">Blob service concepts</span></span>

<span data-ttu-id="1e374-113">Usługa Blob Hello zawiera hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="1e374-113">hello Blob service contains hello following components:</span></span>

![Architektura obiektów blob](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="1e374-115">**Konto magazynu:** wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1e374-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="1e374-116">Konto magazynu może być **konta magazynu ogólnego przeznaczenia** lub **kontem magazynu obiektów Blob** które jest przeznaczone do przechowywania obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="1e374-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="1e374-117">Aby uzyskać więcej informacji, zobacz [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) (Informacje o kontach usługi Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="1e374-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="1e374-118">**Kontener:** kontener zawiera grupowanie zestawu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="1e374-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="1e374-119">Wszystkie obiekty blob muszą być w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="1e374-119">All blobs must be in a container.</span></span> <span data-ttu-id="1e374-120">Konto może zawierać nieograniczoną liczbę kontenerów.</span><span class="sxs-lookup"><span data-stu-id="1e374-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="1e374-121">Kontener może przechowywać nieograniczoną liczbę obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="1e374-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="1e374-122">Należy pamiętać, że czy nazwa kontenera hello muszą być małymi literami.</span><span class="sxs-lookup"><span data-stu-id="1e374-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="1e374-123">**Obiekt blob:** plik dowolnego typu o dowolnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="1e374-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="1e374-124">Usługa Azure Storage udostępnia trzy typy obiektów blob: blokowe, stronicowe i uzupełnialne.</span><span class="sxs-lookup"><span data-stu-id="1e374-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="1e374-125">*Blokowe obiekty blob* idealnie nadają się do przechowywania tekstu lub plików binarnych, takich dokumenty czy pliki multimedialne.</span><span class="sxs-lookup"><span data-stu-id="1e374-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="1e374-126">*Uzupełnialne* są podobne tooblock obiekty BLOB w tym składają się z bloków, ale zoptymalizowane do operacji uzupełnialnych, więc są przydatne w scenariuszach logowania.</span><span class="sxs-lookup"><span data-stu-id="1e374-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="1e374-127">Pojedynczy blokowy obiekt blob może zawierać zapasowej too50, 000 bloków too100 MB, rozmiar całkowity może nieco przekraczać 4,75 TB (100 MB X 50 000).</span><span class="sxs-lookup"><span data-stu-id="1e374-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="1e374-128">Dołącz pojedynczego obiektu blob może zawierać zapasowej too50, 000 bloków too4 MB, całkowita rozmiaru nieco przekraczać 195 GB (4 MB X 50 000).</span><span class="sxs-lookup"><span data-stu-id="1e374-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="1e374-129">*Stronicowe obiekty BLOB* może być zapasowej too1 TB, rozmiar i są bardziej efektywne w przypadku operacji częstego odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="1e374-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="1e374-130">Maszyny wirtualne platformy Azure używa stronicowych obiektów blob jako systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="1e374-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="1e374-131">Aby uzyskać szczegółowe informacje o nazewnictwie kontenerów i obiektów blob, zobacz temat [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) (Nazewnictwo i odwoływanie się do kontenerów, obiektów blob i metadanych).</span><span class="sxs-lookup"><span data-stu-id="1e374-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e374-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e374-132">Next steps</span></span>

* [<span data-ttu-id="1e374-133">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="1e374-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="1e374-134">Wprowadzenie do magazynu obiektów Blob przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1e374-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)