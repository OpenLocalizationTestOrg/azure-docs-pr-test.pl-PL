---
title: "Azure format importu/eksportu metadanych i właściwości pliku | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak określać metadanych i właściwości dla jednego lub więcej obiektów blob, które są częścią importu lub eksportu zadania."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="bcbfe-103">Azure Import/Eksport usługi metadanych i właściwości format pliku</span><span class="sxs-lookup"><span data-stu-id="bcbfe-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="bcbfe-104">Można określić właściwości dla co najmniej jednego obiektu blob i metadanych jako część zadania importu lub eksportu.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="bcbfe-105">Aby ustawić właściwości dla obiektów blob jest tworzony jako część zadania importu lub metadane, musisz podać metadanych lub właściwości pliku na dysku twardym, zawierający dane do zaimportowania.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="bcbfe-106">Dla zadania eksportu metadanych i właściwości są zapisywane w pliku metadanych lub właściwości, który znajduje się na dysku twardym zwracane.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="bcbfe-107">Format pliku metadanych</span><span class="sxs-lookup"><span data-stu-id="bcbfe-107">Metadata file format</span></span>  
<span data-ttu-id="bcbfe-108">Format pliku metadanych jest następująca:</span><span class="sxs-lookup"><span data-stu-id="bcbfe-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="bcbfe-109">XML Element</span><span class="sxs-lookup"><span data-stu-id="bcbfe-109">XML Element</span></span>|<span data-ttu-id="bcbfe-110">Typ</span><span class="sxs-lookup"><span data-stu-id="bcbfe-110">Type</span></span>|<span data-ttu-id="bcbfe-111">Opis</span><span class="sxs-lookup"><span data-stu-id="bcbfe-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="bcbfe-112">Element główny</span><span class="sxs-lookup"><span data-stu-id="bcbfe-112">Root element</span></span>|<span data-ttu-id="bcbfe-113">Element główny pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="bcbfe-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-114">String</span></span>|<span data-ttu-id="bcbfe-115">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-115">Optional.</span></span> <span data-ttu-id="bcbfe-116">XML element Określa nazwę metadane obiektu blob, a jego wartość określa wartość ustawienia metadanych.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="bcbfe-117">Format pliku właściwości</span><span class="sxs-lookup"><span data-stu-id="bcbfe-117">Properties file format</span></span>  
<span data-ttu-id="bcbfe-118">Format pliku właściwości jest następująca:</span><span class="sxs-lookup"><span data-stu-id="bcbfe-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="bcbfe-119">XML Element</span><span class="sxs-lookup"><span data-stu-id="bcbfe-119">XML Element</span></span>|<span data-ttu-id="bcbfe-120">Typ</span><span class="sxs-lookup"><span data-stu-id="bcbfe-120">Type</span></span>|<span data-ttu-id="bcbfe-121">Opis</span><span class="sxs-lookup"><span data-stu-id="bcbfe-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="bcbfe-122">Element główny</span><span class="sxs-lookup"><span data-stu-id="bcbfe-122">Root element</span></span>|<span data-ttu-id="bcbfe-123">Element główny pliku właściwości.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="bcbfe-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-124">String</span></span>|<span data-ttu-id="bcbfe-125">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-125">Optional.</span></span> <span data-ttu-id="bcbfe-126">Czas ostatniej modyfikacji obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-126">The last-modified time for the blob.</span></span> <span data-ttu-id="bcbfe-127">Tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="bcbfe-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-128">String</span></span>|<span data-ttu-id="bcbfe-129">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-129">Optional.</span></span> <span data-ttu-id="bcbfe-130">Wartość ETag obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-130">The blob's ETag value.</span></span> <span data-ttu-id="bcbfe-131">Tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="bcbfe-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-132">String</span></span>|<span data-ttu-id="bcbfe-133">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-133">Optional.</span></span> <span data-ttu-id="bcbfe-134">Rozmiar obiektu blob w bajtach.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-134">The size of the blob in bytes.</span></span> <span data-ttu-id="bcbfe-135">Tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="bcbfe-136">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-136">String</span></span>|<span data-ttu-id="bcbfe-137">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-137">Optional.</span></span> <span data-ttu-id="bcbfe-138">Typ zawartości obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="bcbfe-139">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-139">String</span></span>|<span data-ttu-id="bcbfe-140">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-140">Optional.</span></span> <span data-ttu-id="bcbfe-141">Skrót MD5 obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="bcbfe-142">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-142">String</span></span>|<span data-ttu-id="bcbfe-143">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-143">Optional.</span></span> <span data-ttu-id="bcbfe-144">Zawartość obiektu blob kodowania.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="bcbfe-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-145">String</span></span>|<span data-ttu-id="bcbfe-146">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-146">Optional.</span></span> <span data-ttu-id="bcbfe-147">Język zawartości obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="bcbfe-148">Ciąg</span><span class="sxs-lookup"><span data-stu-id="bcbfe-148">String</span></span>|<span data-ttu-id="bcbfe-149">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-149">Optional.</span></span> <span data-ttu-id="bcbfe-150">Ciąg kontroli pamięci podręcznej dla obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="bcbfe-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcbfe-151">Next steps</span></span>

<span data-ttu-id="bcbfe-152">Zobacz [zestaw właściwości obiektu blob](/rest/api/storageservices/set-blob-properties), [ustawić metadane obiektu Blob](/rest/api/storageservices/set-blob-metadata), i [ustawienie podczas pobierania właściwości i metadanych dla obiektu blob zasobów](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) szczegółowe zasady dotyczące ustawiania właściwości i metadane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bcbfe-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
