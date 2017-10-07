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
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Azure Import/Eksport usługi metadanych i właściwości format pliku
Można określić właściwości dla co najmniej jednego obiektu blob i metadanych jako część zadania importu lub eksportu. metadane tooset lub właściwości dla obiektów blob jest tworzony jako część zadania importu, musisz podać metadanych lub właściwości pliku na dysku twardym powitania zawierający toobe danych hello zaimportowane. Dla zadania eksportu metadanych i właściwości zapisanych pliku metadanych lub właściwości tooa, który znajduje się na dysku twardym powitania zwrócił tooyou.  
  
## <a name="metadata-file-format"></a>Format pliku metadanych  
format pliku metadanych Hello jest następujący:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|XML Element|Typ|Opis|  
|-----------------|----------|-----------------|  
|`Metadata`|Element główny|element główny Hello hello pliku metadanych.|  
|`metadata-name`|Ciąg|Opcjonalny. Hello — element XML określa nazwę hello hello metadanych dla obiektu blob hello, a jego wartość określa wartość hello hello metadanych ustawienia.|  
  
## <a name="properties-file-format"></a>Format pliku właściwości  
format pliku właściwości Hello jest następujący:  
  
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
  
|XML Element|Typ|Opis|  
|-----------------|----------|-----------------|  
|`Properties`|Element główny|element główny Hello hello właściwości pliku.|  
|`Last-Modified`|Ciąg|Opcjonalny. Czas ostatniej modyfikacji Hello hello obiektu blob. Tylko zadania eksportu.|  
|`Etag`|Ciąg|Opcjonalny. Witaj wartości ETag obiektu blob. Tylko zadania eksportu.|  
|`Content-Length`|Ciąg|Opcjonalny. Witaj rozmiar obiektu blob hello w bajtach. Tylko zadania eksportu.|  
|`Content-Type`|Ciąg|Opcjonalny. Typ zawartości Hello hello obiektu blob.|  
|`Content-MD5`|Ciąg|Opcjonalny. Witaj skrótu MD5 obiektu blob.|  
|`Content-Encoding`|Ciąg|Opcjonalny. Witaj zawartości obiektu blob kodowania.|  
|`Content-Language`|Ciąg|Opcjonalny. Witaj języka zawartości obiektu blob.|  
|`Cache-Control`|Ciąg|Opcjonalny. Hello pamięci podręcznej kontroli ciąg hello obiektu blob.|  

## <a name="next-steps"></a>Następne kroki

Zobacz [zestaw właściwości obiektu blob](/rest/api/storageservices/set-blob-properties), [ustawić metadane obiektu Blob](/rest/api/storageservices/set-blob-metadata), i [ustawienie podczas pobierania właściwości i metadanych dla obiektu blob zasobów](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) szczegółowe zasady dotyczące ustawiania właściwości i metadane obiektu blob.
