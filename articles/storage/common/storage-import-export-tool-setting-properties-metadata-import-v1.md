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
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Ustawianie właściwości i metadanych podczas hello importowania
Po uruchomieniu tooprepare narzędzie importu/eksportu pakietu Microsoft Azure hello dysków, można określić właściwości i ustawić na obiekty BLOB docelowego hello toobe metadanych. Wykonaj następujące kroki:  
  
1.  właściwości obiektu blob tooset, Utwórz plik tekstowy na komputerze lokalnym, który określa nazwy i wartości właściwości.  
  
2.  tooset metadane obiektu blob, Utwórz plik tekstowy na komputerze lokalnym, określający, metadane nazwy i wartości.  
  
3.  Przekaż hello tooone pełną ścieżkę lub oba te pliki toohello narzędzie importu/eksportu Azure jako część hello `PrepImport` operacji.  
  
> [!NOTE]
>  Po określeniu właściwości lub metadane pliku w ramach sesji kopiowania tych właściwości lub metadane są ustawione dla każdy obiekt blob importowanych w ramach tej sesji kopiowania. Jeśli chcesz toospecify inny zestaw właściwości lub metadane dla niektórych obiektów blob hello importowana należy toocreate oddzielnie skopiować sesji z różnych właściwości lub pliki metadanych.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>Określ właściwości obiektu Blob w pliku tekstowym  
właściwości obiektu blob toospecify, Utwórz lokalny plik tekstowy i zawierać kod XML, który określa właściwości nazwy elementów i wartości właściwości jako wartości. Oto przykład, który określa niektórych wartości właściwości:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Zapisz lokalizacji lokalnej tooa pliku hello jak `C:\WAImportExport\ImportProperties.txt`.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>Określ metadane obiektu Blob w pliku tekstowym  
Podobnie toospecify metadane obiektu blob, Utwórz plik tekstowy lokalnego, który określa nazwy metadanych jako elementy, a wartości metadanych jako wartości. Oto przykład, który określa niektórych wartości metadanych:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Zapisz lokalizacji lokalnej tooa pliku hello jak `C:\WAImportExport\ImportMetadata.txt`.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>Tworzenie kopii sesji w tym hello, właściwości lub pliki metadanych  
Po uruchomieniu zadania importu hello hello Azure narzędzie importu/eksportu tooprepare, określ plik właściwości hello na powitania wiersza polecenia przy użyciu hello `PropertyFile` parametru. Określ plik metadanych hello na powitania wiersza polecenia przy użyciu hello `/MetadataFile` parametru. Oto przykład, który określa oba pliki:  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>Następne kroki

* [Format pliku właściwości i metadanych usługi Import/Export](../storage-import-export-file-format-metadata-and-properties.md)
