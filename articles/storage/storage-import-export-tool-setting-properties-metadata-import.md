---
title: "aaaSetting właściwości i metadanych za pomocą Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się toospecify toobe metadanych i właściwości konfiguracji na obiekty BLOB docelowego hello podczas uruchamiania hello Azure narzędzie importu/eksportu tooprepare dysków."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 05c2b13bead793c8ab5aac6ce25816be97fffb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="1e32f-103">Ustawianie właściwości i metadanych podczas hello importowania</span><span class="sxs-lookup"><span data-stu-id="1e32f-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="1e32f-104">Po uruchomieniu tooprepare narzędzie importu/eksportu pakietu Microsoft Azure hello dysków, można określić właściwości i ustawić na obiekty BLOB docelowego hello toobe metadanych.</span><span class="sxs-lookup"><span data-stu-id="1e32f-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="1e32f-105">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1e32f-105">Follow these steps:</span></span>

1.  <span data-ttu-id="1e32f-106">właściwości obiektu blob tooset, Utwórz plik tekstowy na komputerze lokalnym, który określa nazwy i wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="1e32f-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="1e32f-107">tooset metadane obiektu blob, Utwórz plik tekstowy na komputerze lokalnym, określający, metadane nazwy i wartości.</span><span class="sxs-lookup"><span data-stu-id="1e32f-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="1e32f-108">Przekaż hello tooone pełną ścieżkę lub oba te pliki toohello narzędzie importu/eksportu Azure jako część hello `PrepImport` operacji.</span><span class="sxs-lookup"><span data-stu-id="1e32f-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="1e32f-109">Po określeniu właściwości lub metadane pliku w ramach sesji kopiowania tych właściwości lub metadane są ustawione dla każdy obiekt blob importowanych w ramach tej sesji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="1e32f-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="1e32f-110">Jeśli chcesz toospecify inny zestaw właściwości lub metadane dla niektórych obiektów blob hello importowana należy toocreate oddzielnie skopiować sesji z różnych właściwości lub pliki metadanych.</span><span class="sxs-lookup"><span data-stu-id="1e32f-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="1e32f-111">Określ właściwości obiektu blob w pliku tekstowym</span><span class="sxs-lookup"><span data-stu-id="1e32f-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="1e32f-112">właściwości obiektu blob toospecify, Utwórz lokalny plik tekstowy i zawierać kod XML, który określa właściwości nazwy elementów i wartości właściwości jako wartości.</span><span class="sxs-lookup"><span data-stu-id="1e32f-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="1e32f-113">Oto przykład, który określa niektórych wartości właściwości:</span><span class="sxs-lookup"><span data-stu-id="1e32f-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="1e32f-114">Zapisz lokalizacji lokalnej tooa pliku hello jak `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="1e32f-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="1e32f-115">Określ metadane obiektu blob w pliku tekstowym</span><span class="sxs-lookup"><span data-stu-id="1e32f-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="1e32f-116">Podobnie toospecify metadane obiektu blob, Utwórz plik tekstowy lokalnego, który określa nazwy metadanych jako elementy, a wartości metadanych jako wartości.</span><span class="sxs-lookup"><span data-stu-id="1e32f-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="1e32f-117">Oto przykład, który określa niektórych wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="1e32f-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="1e32f-118">Zapisz lokalizacji lokalnej tooa pliku hello jak `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="1e32f-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="1e32f-119">Dodaj pliki metadanych i tooproperties ścieżka hello w dataset.csv</span><span class="sxs-lookup"><span data-stu-id="1e32f-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="1e32f-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e32f-120">Next steps</span></span>

* [<span data-ttu-id="1e32f-121">Format pliku właściwości i metadanych usługi Import/Export</span><span class="sxs-lookup"><span data-stu-id="1e32f-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
