---
title: "aaaSetting właściwości i metadanych za pomocą Import/Eksport Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dowiedz się toospecify toobe metadanych i właściwości konfiguracji na obiekty BLOB docelowego hello podczas uruchamiania hello Azure narzędzie importu/eksportu tooprepare dysków. Odnosi się toov1 hello narzędzie importu/eksportu."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="68a74-104">Ustawianie właściwości i metadanych podczas hello importowania</span><span class="sxs-lookup"><span data-stu-id="68a74-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="68a74-105">Po uruchomieniu tooprepare narzędzie importu/eksportu pakietu Microsoft Azure hello dysków, można określić właściwości i ustawić na obiekty BLOB docelowego hello toobe metadanych.</span><span class="sxs-lookup"><span data-stu-id="68a74-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="68a74-106">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="68a74-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="68a74-107">właściwości obiektu blob tooset, Utwórz plik tekstowy na komputerze lokalnym, który określa nazwy i wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="68a74-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="68a74-108">tooset metadane obiektu blob, Utwórz plik tekstowy na komputerze lokalnym, określający, metadane nazwy i wartości.</span><span class="sxs-lookup"><span data-stu-id="68a74-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="68a74-109">Przekaż hello tooone pełną ścieżkę lub oba te pliki toohello narzędzie importu/eksportu Azure jako część hello `PrepImport` operacji.</span><span class="sxs-lookup"><span data-stu-id="68a74-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="68a74-110">Po określeniu właściwości lub metadane pliku w ramach sesji kopiowania tych właściwości lub metadane są ustawione dla każdy obiekt blob importowanych w ramach tej sesji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="68a74-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="68a74-111">Jeśli chcesz toospecify inny zestaw właściwości lub metadane dla niektórych obiektów blob hello importowana należy toocreate oddzielnie skopiować sesji z różnych właściwości lub pliki metadanych.</span><span class="sxs-lookup"><span data-stu-id="68a74-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="68a74-112">Określ właściwości obiektu Blob w pliku tekstowym</span><span class="sxs-lookup"><span data-stu-id="68a74-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="68a74-113">właściwości obiektu blob toospecify, Utwórz lokalny plik tekstowy i zawierać kod XML, który określa właściwości nazwy elementów i wartości właściwości jako wartości.</span><span class="sxs-lookup"><span data-stu-id="68a74-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="68a74-114">Oto przykład, który określa niektórych wartości właściwości:</span><span class="sxs-lookup"><span data-stu-id="68a74-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="68a74-115">Zapisz lokalizacji lokalnej tooa pliku hello jak `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="68a74-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="68a74-116">Określ metadane obiektu Blob w pliku tekstowym</span><span class="sxs-lookup"><span data-stu-id="68a74-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="68a74-117">Podobnie toospecify metadane obiektu blob, Utwórz plik tekstowy lokalnego, który określa nazwy metadanych jako elementy, a wartości metadanych jako wartości.</span><span class="sxs-lookup"><span data-stu-id="68a74-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="68a74-118">Oto przykład, który określa niektórych wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="68a74-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="68a74-119">Zapisz lokalizacji lokalnej tooa pliku hello jak `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="68a74-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="68a74-120">Tworzenie kopii sesji w tym hello, właściwości lub pliki metadanych</span><span class="sxs-lookup"><span data-stu-id="68a74-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="68a74-121">Po uruchomieniu zadania importu hello hello Azure narzędzie importu/eksportu tooprepare, określ plik właściwości hello na powitania wiersza polecenia przy użyciu hello `PropertyFile` parametru.</span><span class="sxs-lookup"><span data-stu-id="68a74-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="68a74-122">Określ plik metadanych hello na powitania wiersza polecenia przy użyciu hello `/MetadataFile` parametru.</span><span class="sxs-lookup"><span data-stu-id="68a74-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="68a74-123">Oto przykład, który określa oba pliki:</span><span class="sxs-lookup"><span data-stu-id="68a74-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="68a74-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68a74-124">Next steps</span></span>

* [<span data-ttu-id="68a74-125">Format pliku właściwości i metadanych usługi Import/Export</span><span class="sxs-lookup"><span data-stu-id="68a74-125">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
