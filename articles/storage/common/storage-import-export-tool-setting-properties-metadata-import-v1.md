---
title: "Ustawienie właściwości i metadanych za pomocą Import/Eksport Azure - v1 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak określić właściwości oraz metadanych ma być ustawiony na obiekty BLOB docelowego podczas uruchamiania narzędzia importu/eksportu Azure do przygotowania dysków. Odnosi się do v1 narzędzia importu/eksportu."
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
ms.openlocfilehash: 77bdaa5559de86cd1de9f30e70656e47fd5719e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="64d8a-104">Ustawianie właściwości i metadanych podczas procesu importowania</span><span class="sxs-lookup"><span data-stu-id="64d8a-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="64d8a-105">Po uruchomieniu narzędzia importu/eksportu w usłudze Microsoft Azure do przygotowania dysków, można określić właściwości i metadanych ma być ustawiony na docelowym obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="64d8a-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="64d8a-106">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="64d8a-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="64d8a-107">Aby ustawić właściwości obiektu blob, Utwórz plik tekstowy na komputerze lokalnym, który określa nazwy i wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="64d8a-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="64d8a-108">Aby ustawić metadane obiektu blob, Utwórz plik tekstowy na komputerze lokalnym, określający, metadane nazwy i wartości.</span><span class="sxs-lookup"><span data-stu-id="64d8a-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="64d8a-109">Przekaż pełną ścieżkę do jednej lub obu tych plików do narzędzia importu/eksportu Azure jako część `PrepImport` operacji.</span><span class="sxs-lookup"><span data-stu-id="64d8a-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="64d8a-110">Po określeniu właściwości lub metadane pliku w ramach sesji kopiowania tych właściwości lub metadane są ustawione dla każdy obiekt blob importowanych w ramach tej sesji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="64d8a-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="64d8a-111">Jeśli chcesz określić inny zestaw właściwości lub metadanych dla niektórych importowanych obiektów blob, należy utworzyć sesję oddzielna kopia z różnych właściwości lub pliki metadanych.</span><span class="sxs-lookup"><span data-stu-id="64d8a-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="64d8a-112">Określ właściwości obiektu Blob w pliku tekstowym</span><span class="sxs-lookup"><span data-stu-id="64d8a-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="64d8a-113">Aby określić właściwości obiektu blob, Utwórz plik tekstowy lokalnego i zawierać kod XML, który określa właściwości nazwy elementów i wartości właściwości jako wartości.</span><span class="sxs-lookup"><span data-stu-id="64d8a-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="64d8a-114">Oto przykład, który określa niektórych wartości właściwości:</span><span class="sxs-lookup"><span data-stu-id="64d8a-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="64d8a-115">Zapisz plik do lokalnej lokalizacji, takiej jak `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="64d8a-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="64d8a-116">Określ metadane obiektu Blob w pliku tekstowym</span><span class="sxs-lookup"><span data-stu-id="64d8a-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="64d8a-117">Podobnie Aby określić metadane obiektu blob, należy utworzyć plik tekstowy lokalnego, który określa nazwy metadanych jako elementy, a wartości metadanych jako wartości.</span><span class="sxs-lookup"><span data-stu-id="64d8a-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="64d8a-118">Oto przykład, który określa niektórych wartości metadanych:</span><span class="sxs-lookup"><span data-stu-id="64d8a-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="64d8a-119">Zapisz plik do lokalnej lokalizacji, takiej jak `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="64d8a-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="64d8a-120">Tworzenie sesji kopiowania, włącznie z właściwości lub pliki metadanych</span><span class="sxs-lookup"><span data-stu-id="64d8a-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="64d8a-121">W celu uruchomienia narzędzia importu/eksportu Azure, aby przygotować zadanie importu, określ plik właściwości przy użyciu wiersza polecenia `PropertyFile` parametru.</span><span class="sxs-lookup"><span data-stu-id="64d8a-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="64d8a-122">Określ plik metadanych przy użyciu wiersza polecenia `/MetadataFile` parametru.</span><span class="sxs-lookup"><span data-stu-id="64d8a-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="64d8a-123">Oto przykład, który określa oba pliki:</span><span class="sxs-lookup"><span data-stu-id="64d8a-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="64d8a-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64d8a-124">Next steps</span></span>

* [<span data-ttu-id="64d8a-125">Format pliku właściwości i metadanych usługi Import/Export</span><span class="sxs-lookup"><span data-stu-id="64d8a-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
