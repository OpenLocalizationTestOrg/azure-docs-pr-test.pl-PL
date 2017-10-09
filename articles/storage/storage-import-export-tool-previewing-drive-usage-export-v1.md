---
title: "aaaPreviewing użycia dysków dla zadania eksportu Import/Eksport Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopreview hello listę obiektów blob wybrany dla zadania eksportu w usłudze Import/Eksport Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 88495f921371458c0451da6878fd7cc9a45d20cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="bebdd-103">Wyświetlanie podglądu użycia dysków przez zadanie eksportu</span><span class="sxs-lookup"><span data-stu-id="bebdd-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="bebdd-104">Przed utworzeniem zadania eksportu należy toochoose wyeksportowane przez zestaw toobe obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="bebdd-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="bebdd-105">Hello usługi Import/Eksport Microsoft Azure umożliwia toouse listę obiektów blob ścieżki lub obiektu blob prefiksy toorepresent obiekty BLOB hello zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="bebdd-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="bebdd-106">Następnie należy toodetermine liczbę dysków należy toosend.</span><span class="sxs-lookup"><span data-stu-id="bebdd-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="bebdd-107">Witaj narzędzie importu/eksportu umożliwia hello `PreviewExport` użycia dysków toopreview polecenia dla obiektów blob hello wybrane, na podstawie rozmiaru hello dysków hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="bebdd-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="bebdd-108">Parametry wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bebdd-108">Command-line parameters</span></span>

<span data-ttu-id="bebdd-109">Można użyć hello następujące parametry, używając hello `PreviewExport` polecenie z hello narzędzie importu/eksportu.</span><span class="sxs-lookup"><span data-stu-id="bebdd-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="bebdd-110">Parametr wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bebdd-110">Command-line parameter</span></span>|<span data-ttu-id="bebdd-111">Opis</span><span class="sxs-lookup"><span data-stu-id="bebdd-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="bebdd-112">**/ logdir:**< LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="bebdd-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="bebdd-113">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bebdd-113">Optional.</span></span> <span data-ttu-id="bebdd-114">Katalog dziennika Hello.</span><span class="sxs-lookup"><span data-stu-id="bebdd-114">hello log directory.</span></span> <span data-ttu-id="bebdd-115">Pełne pliki dziennika zostaną zapisane toothis katalogu.</span><span class="sxs-lookup"><span data-stu-id="bebdd-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="bebdd-116">Jeśli katalog dziennika nie jest określony, bieżący katalog hello będzie używany jako katalog dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="bebdd-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="bebdd-117">**/SN:**< StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="bebdd-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="bebdd-118">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="bebdd-118">Required.</span></span> <span data-ttu-id="bebdd-119">zadanie eksportowania Hello nazwę konta magazynu hello hello.</span><span class="sxs-lookup"><span data-stu-id="bebdd-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="bebdd-120">**/SK:**< StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="bebdd-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="bebdd-121">Wymagany tylko wtedy, gdy nie określono kontenera sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="bebdd-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="bebdd-122">zadanie eksportowania Hello klucz konta usługi dla konta magazynu hello hello.</span><span class="sxs-lookup"><span data-stu-id="bebdd-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="bebdd-123">**/csas:**< ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="bebdd-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="bebdd-124">Wymagany tylko wtedy, gdy nie określono klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="bebdd-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="bebdd-125">kontener Hello sygnatury dostępu Współdzielonego dla listy hello obiekty BLOB toobe eksportowane w hello zadanie eksportu.</span><span class="sxs-lookup"><span data-stu-id="bebdd-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="bebdd-126">**/ ExportBlobListFile:**< ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="bebdd-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="bebdd-127">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="bebdd-127">Required.</span></span> <span data-ttu-id="bebdd-128">Ścieżka toohello XML pliku zawierającego listę obiektów blob ścieżek lub obiektu blob prefiksy ścieżki dla toobe obiekty BLOB hello wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="bebdd-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="bebdd-129">format pliku Hello używany w hello `BlobListBlobPath` element hello [zawiesić zadanie](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operacji hello interfejsu API REST usługi Import/Eksport.</span><span class="sxs-lookup"><span data-stu-id="bebdd-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="bebdd-130">**/ DriveSize:**< DriveSize\></span><span class="sxs-lookup"><span data-stu-id="bebdd-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="bebdd-131">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="bebdd-131">Required.</span></span> <span data-ttu-id="bebdd-132">Witaj rozmiar toouse dysków dla zadania eksportu *np.*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="bebdd-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="bebdd-133">Przykład wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="bebdd-133">Command-line example</span></span>

<span data-ttu-id="bebdd-134">Witaj poniższym przykładzie pokazano hello `PreviewExport` polecenia:</span><span class="sxs-lookup"><span data-stu-id="bebdd-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="bebdd-135">Hello eksportu obiektów blob listy plik może zawierać nazwy obiektów blob i obiektów blob prefiksy, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="bebdd-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="bebdd-136">Hello Azure narzędzie importu/eksportu zawiera listę wszystkich toobe obiekty BLOB wyeksportowany i oblicza jak toopack ich na dyski hello określony rozmiar, biorąc pod uwagę wszystkie niezbędne koszty następnie szacuje hello liczba dysków potrzebne obiekty BLOB hello toohold i użycie dysku informacje.</span><span class="sxs-lookup"><span data-stu-id="bebdd-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="bebdd-137">Oto przykład danych wyjściowych hello, z dziennikami informacyjną pominięte:</span><span class="sxs-lookup"><span data-stu-id="bebdd-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="bebdd-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bebdd-138">Next steps</span></span>

* [<span data-ttu-id="bebdd-139">Odwołanie do usługi Azure narzędzie importu/eksportu</span><span class="sxs-lookup"><span data-stu-id="bebdd-139">Azure Import/Export Tool reference</span></span>](storage-import-export-tool-how-to-v1.md)
