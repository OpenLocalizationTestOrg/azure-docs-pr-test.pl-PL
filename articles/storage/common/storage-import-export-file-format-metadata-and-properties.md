---
title: "aaaAzure importu/eksportu metadanych i właściwości format pliku | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak metadanych toospecify i właściwości dla jednego lub więcej obiektów blob które są częścią importu lub eksportu zadania."
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
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="d92e7-103">Azure Import/Eksport usługi metadanych i właściwości format pliku</span><span class="sxs-lookup"><span data-stu-id="d92e7-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="d92e7-104">Można określić właściwości dla co najmniej jednego obiektu blob i metadanych jako część zadania importu lub eksportu.</span><span class="sxs-lookup"><span data-stu-id="d92e7-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="d92e7-105">metadane tooset lub właściwości dla obiektów blob jest tworzony jako część zadania importu, musisz podać metadanych lub właściwości pliku na dysku twardym powitania zawierający toobe danych hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="d92e7-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="d92e7-106">Dla zadania eksportu metadanych i właściwości zapisanych pliku metadanych lub właściwości tooa, który znajduje się na dysku twardym powitania zwrócił tooyou.</span><span class="sxs-lookup"><span data-stu-id="d92e7-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="d92e7-107">Format pliku metadanych</span><span class="sxs-lookup"><span data-stu-id="d92e7-107">Metadata file format</span></span>  
<span data-ttu-id="d92e7-108">format pliku metadanych Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d92e7-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="d92e7-109">XML Element</span><span class="sxs-lookup"><span data-stu-id="d92e7-109">XML Element</span></span>|<span data-ttu-id="d92e7-110">Typ</span><span class="sxs-lookup"><span data-stu-id="d92e7-110">Type</span></span>|<span data-ttu-id="d92e7-111">Opis</span><span class="sxs-lookup"><span data-stu-id="d92e7-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="d92e7-112">Element główny</span><span class="sxs-lookup"><span data-stu-id="d92e7-112">Root element</span></span>|<span data-ttu-id="d92e7-113">element główny Hello hello pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="d92e7-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="d92e7-114">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-114">String</span></span>|<span data-ttu-id="d92e7-115">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-115">Optional.</span></span> <span data-ttu-id="d92e7-116">Hello — element XML określa nazwę hello hello metadanych dla obiektu blob hello, a jego wartość określa wartość hello hello metadanych ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d92e7-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="d92e7-117">Format pliku właściwości</span><span class="sxs-lookup"><span data-stu-id="d92e7-117">Properties file format</span></span>  
<span data-ttu-id="d92e7-118">format pliku właściwości Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d92e7-118">hello format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="d92e7-119">XML Element</span><span class="sxs-lookup"><span data-stu-id="d92e7-119">XML Element</span></span>|<span data-ttu-id="d92e7-120">Typ</span><span class="sxs-lookup"><span data-stu-id="d92e7-120">Type</span></span>|<span data-ttu-id="d92e7-121">Opis</span><span class="sxs-lookup"><span data-stu-id="d92e7-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="d92e7-122">Element główny</span><span class="sxs-lookup"><span data-stu-id="d92e7-122">Root element</span></span>|<span data-ttu-id="d92e7-123">element główny Hello hello właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="d92e7-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="d92e7-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-124">String</span></span>|<span data-ttu-id="d92e7-125">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-125">Optional.</span></span> <span data-ttu-id="d92e7-126">Czas ostatniej modyfikacji Hello hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d92e7-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="d92e7-127">Tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="d92e7-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="d92e7-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-128">String</span></span>|<span data-ttu-id="d92e7-129">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-129">Optional.</span></span> <span data-ttu-id="d92e7-130">Witaj wartości ETag obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d92e7-130">hello blob's ETag value.</span></span> <span data-ttu-id="d92e7-131">Tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="d92e7-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="d92e7-132">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-132">String</span></span>|<span data-ttu-id="d92e7-133">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-133">Optional.</span></span> <span data-ttu-id="d92e7-134">Witaj rozmiar obiektu blob hello w bajtach.</span><span class="sxs-lookup"><span data-stu-id="d92e7-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="d92e7-135">Tylko zadania eksportu.</span><span class="sxs-lookup"><span data-stu-id="d92e7-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="d92e7-136">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-136">String</span></span>|<span data-ttu-id="d92e7-137">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-137">Optional.</span></span> <span data-ttu-id="d92e7-138">Typ zawartości Hello hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d92e7-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="d92e7-139">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-139">String</span></span>|<span data-ttu-id="d92e7-140">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-140">Optional.</span></span> <span data-ttu-id="d92e7-141">Witaj skrótu MD5 obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d92e7-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="d92e7-142">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-142">String</span></span>|<span data-ttu-id="d92e7-143">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-143">Optional.</span></span> <span data-ttu-id="d92e7-144">Witaj zawartości obiektu blob kodowania.</span><span class="sxs-lookup"><span data-stu-id="d92e7-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="d92e7-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-145">String</span></span>|<span data-ttu-id="d92e7-146">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-146">Optional.</span></span> <span data-ttu-id="d92e7-147">Witaj języka zawartości obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d92e7-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="d92e7-148">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d92e7-148">String</span></span>|<span data-ttu-id="d92e7-149">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d92e7-149">Optional.</span></span> <span data-ttu-id="d92e7-150">Hello pamięci podręcznej kontroli ciąg hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d92e7-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="d92e7-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d92e7-151">Next steps</span></span>

<span data-ttu-id="d92e7-152">Zobacz [zestaw właściwości obiektu blob](/rest/api/storageservices/set-blob-properties), [ustawić metadane obiektu Blob](/rest/api/storageservices/set-blob-metadata), i [ustawienie podczas pobierania właściwości i metadanych dla obiektu blob zasobów](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) szczegółowe zasady dotyczące ustawiania właściwości i metadane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d92e7-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
